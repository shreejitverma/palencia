# Ad Tech & Paid Media Pipeline: End-to-End Architecture & Operational Playbook

> The canonical engineering and media buying guide for digital advertising systems — covering algorithmic ranking, real-time auctions, server-side data ingestion, privacy-preserving attribution, and scalable campaign operations across Meta, Google, TikTok, X, and the Programmatic Open Web.

| | |
|---|---|
| **Owner** | Marketing & Growth Engineering |
| **Last reviewed** | 2026-08-29 |
| **Review cadence** | Quarterly |
| **Status** | Active |

---

## 1. Executive Overview & The Global Advertising Topology

Digital advertising operates at the intersection of **distributed systems engineering** (evaluating tens of millions of candidate ads and executing multi-party auctions in under 40 milliseconds) and **growth strategy** (creative testing, bid pacing, data enrichment, and econometric measurement).

Modern platforms operate either as **Walled Gardens** (controlling user interface, ad inventory, and ad server simultaneously) or within the **Programmatic Open Web** (federated exchanges using the OpenRTB protocol).

```
                  ┌────────────────────────────────────────────────────────┐
                  │                 ADVERTISER ECOSYSTEM                   │
                  │   Palencia Diamonds Growth & Performance Marketing     │
                  └──────────────────────────┬─────────────────────────────┘
                                             │ Campaigns, Budgets, Creatives
                                             ▼
                 ┌─────────────────────────────────────────────────────────┐
                 │                DEMAND-SIDE INTERFACES                   │
                 │   Meta Ads Manager │ Google Ads │ X Ads │ TikTok Ads    │
                 │   DSP (The Trade Desk, DV360, Amazon DSP for Open Web)  │
                 └──────────────────────────┬─────────────────────────────┘
                                            │
   ┌────────────────────────────────────────┴──────────────────────────────────────┐
   │                           THE AD TECH INGESTION ENGINE                        │
   │  • Event Tracking: Pixel, SDKs, Server-Side APIs (Meta CAPI, Google Enhanced)  │
   │  • First-Party Data: Customer Lists, Offline Conversions, CRM Ingestion       │
   │  • Identity Graph: Probabilistic & Deterministic ID Matching                  │
   └────────────────────────────────────────┬──────────────────────────────────────┘
                                            │ Real-time Events & Signal Enrichment
                                            ▼
   ┌───────────────────────────────────────────────────────────────────────────────┐
   │                     REAL-TIME AD ENGINE PIPELINE (< 40ms)                     │
   │                                                                               │
   │  [1. Request Context]  ──► [2. Candidate Retrieval] ──► [3. Heavy ML Ranking] │
   │   Device, Session,          Multi-Tower ANN / Vector    pCTR, pCVR, Long-Term  │
   │   Context, User State       Filtering (Millions ➔ 500)   Value (DCN, MMoE)     │
   │                                                               │               │
   │                                                               ▼               │
   │  [6. Serving & Render] ◄── [5. Dynamic Assembly]   ◄── [4. The Auction Engine]│
   │   CDN Delivery, Edge        Dynamic Creative (DCO),     eCPM Value Formula,   │
   │   Tracking Pixels           Copy, CTA Personalization   VCG/GSP, Pacing/PID   │
   └────────────────────────────────────────┬──────────────────────────────────────┘
                                            │
                                            ▼
   ┌───────────────────────────────────────────────────────────────────────────────┐
   │                     ATTRIBUTION & FEEDBACK INTELLIGENCE                       │
   │  • Conversion Deduplication & Attribution Windows (1d/7d click, 1d view)      │
   │  • Privacy Layer: SKAdNetwork 4.0 / AdAttributionKit, Privacy Sandbox         │
   │  • Measurement Triangulation: MTA + Geo-Lift Testing + MMM (Bayesian)         │
   │  • Real-Time Model Retraining & Parameter Server Updates                      │
   └───────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. The 8-Stage Real-Time Pipeline (< 40ms SLA)

Every ad impression served across social feeds or search results flows through this 8-stage sequence within a 40-millisecond execution budget:

```
 [ Total Budget: 40 ms ]
 ├── 0ms  ──► Edge Ingress & Authentication (gRPC / Envoy): ~3 ms
 ├── 3ms  ──► Feature Store Lookup (User Embedding from Dragonfly/RocksDB): ~5 ms
 ├── 8ms  ──► Candidate Retrieval (ANN Vector Index via ScaNN/HNSW): ~4 ms
 ├── 12ms ──► Heavy ML Ranking (GPU Inference via Triton / TensorRT): ~15 ms
 ├── 27ms ──► Auction Engine, Pacing & Frequency Capping (Redis Cluster): ~4 ms
 ├── 31ms ──► Dynamic Creative Assembly & CDN URL Signing: ~3 ms
 ├── 34ms ──► Response Serialization & Egress: ~2 ms
 └── 36ms ──► [COMPLETE - 4ms SLA Buffer Remaining]
```

### Stage 1: Campaign Hierarchy & Budget Pacing
- **Hierarchy**: Campaign (Objective, centralized Advantage Budget) $\to$ Ad Set (Targeting, Placements, Bidding) $\to$ Ad (Creative, Copy, URL).
- **PID Budget Controllers**: Pacing engines dynamically throttle or boost bids throughout a 24-hour cycle to avoid budget exhaustion during non-peak hours.

### Stage 2: Signal Ingestion & Identity Matching
- Ingests client-side browser events and server-side webhooks (Meta CAPI, Google Enhanced Conversions).
- Hashed PII (SHA-256) matches anonymous web events back to deterministic user profiles.

### Stage 3: Real-Time Context Trigger
- Mobile app/web client requests a feed refresh or search query. Payload includes user token, device hardware, network speed, battery state, and the last 10 in-session interactions.

### Stage 4: Candidate Retrieval (Filtering Millions to 500)
- **Two-Tower Neural Networks** perform vector cosine matching over an Approximate Nearest Neighbor (ANN) index (HNSW/ScaNN) in $< 5\text{ ms}$.

### Stage 5: Heavy Machine Learning Ranking
- **Deep & Cross Networks (DCN-v2)** and **Multi-Gate Mixture-of-Experts (MMoE)** compute discrete probabilities: $p(\text{Click})$, $p(\text{Conversion} \mid \text{Click})$, and $p(\text{Negative Feedback})$.

### Stage 6: The Auction Engine & eCPM Bid Calculation
- Every ad's diverse bid structure (CPC, CPA, ROAS, CPM) is normalized into an **Effective Cost Per Mille (eCPM)**.
- Executes Vickrey-Clarke-Groves (VCG) or Generalized Second-Price (GSP) clearing rules.

### Stage 7: Dynamic Creative Assembly & Edge CDN Delivery
- Selects the winning visual hook, primary copy, and CTA button customized to user preferences, served from edge CDN caches.

### Stage 8: Attribution, Measurement & Retraining Loop
- Conversion beacons and server-side purchases update the central Feature Store to recalibrate conversion priors in real time.

---

## 3. Mathematical & Machine Learning Foundations

```
       USER & CONTEXT TOWER                              AD CREATIVE TOWER
 ┌───────────────────────────────┐               ┌───────────────────────────────┐
 │ Dense Features (Age, Geo, LTV)│               │ Ad ID, Advertiser ID, Category│
 │ Sparse Sequences (Recent Feed)│               │ Multimodal Embeddings (Vision)│
 │ Real-time Context (App State) │               │ Historical CTR / CVR priors   │
 └──────────────┬────────────────┘               └──────────────┬────────────────┘
                │                                               │
                ▼ [Embedding + Dense Layers]                    ▼ [Embedding + Dense Layers]
 ┌───────────────────────────────┐               ┌───────────────────────────────┐
 │ User Latent Vector u ∈ R^d    │               │ Ad Latent Vector v ∈ R^d      │
 └──────────────┬────────────────┘               └──────────────┬────────────────┘
                │                                               │
                └───────────────────────┬───────────────────────┘
                                        │
                                        ▼ Dot Product / Cosine Similarity
                           s(u, v) = <u, v> / (||u|| ||v||)
                                        │
                                        ▼ Top-K Search
                      Hierarchical Navigable Small World (HNSW)
```

### 3.1 Two-Tower Vector Retrieval (InfoNCE Loss)
To retrieve relevant ads from a pool of 10,000,000+ candidates in under 5ms, platforms train two parallel neural towers using **In-Batch Negative Softmax Loss (InfoNCE)**:

$$\mathcal{L} = -\sum_{i=1}^{B} \log \frac{\exp\left(\frac{\mathbf{u}_i^\top \mathbf{v}_i}{\tau}\right)}{\exp\left(\frac{\mathbf{u}_i^\top \mathbf{v}_i}{\tau}\right) + \sum_{j \neq i}^{B} \exp\left(\frac{\mathbf{u}_i^\top \mathbf{v}_j}{\tau}\right)}$$

Where:
- $\mathbf{u}_i \in \mathbb{R}^d$ is the User & Context embedding vector.
- $\mathbf{v}_i \in \mathbb{R}^d$ is the Positive Ad Creative embedding vector.
- $\mathbf{v}_j$ ($j \neq i$) acts as in-batch negative samples.
- $\tau$ is the temperature hyperparameter controlling distribution sharpness.

### 3.2 Deep & Cross Network (DCN-v2) Feature Crossing
To model non-linear combinatorial relationships (e.g., `Device == iOS` $\times$ `Category == Solitaire` $\times$ `Time == Evening`) without manual feature engineering:

$$\mathbf{x}_{l+1} = \mathbf{x}_0 \mathbf{x}_l^\top \mathbf{w}_l + \mathbf{b}_l + \mathbf{x}_l$$

### 3.3 Delayed Feedback & Hazard Survival Modeling
High-consideration fine jewelry purchases experience conversion lag (a click on Monday converting on Friday). Platforms model this through **Survival Hazard Analysis**:

$$\lambda(t \mid \mathbf{x}) = \lim_{\Delta t \to 0} \frac{P(t \le T < t + \Delta t \mid T \ge t, \mathbf{x})}{\Delta t}$$

$$P(\text{Conversion} \mid \text{Click}, \mathbf{x}) = p(\mathbf{x}) \cdot \exp\left( -\int_0^t \lambda(s \mid \mathbf{x}) ds \right)$$

### 3.4 Auction Mechanics: GSP vs VCG Derivations

#### 1. Generalized Second Price (GSP) — Google Search
Advertisers are sorted by $\text{Ad Rank} = \text{Bid}_i \times \text{Quality Score}_i$. The winner pays:

$$\text{PPC}_i = \frac{\text{Bid}_{i+1} \times \text{Quality Score}_{i+1}}{\text{Quality Score}_i} + \$0.01$$

#### 2. Vickrey-Clarke-Groves (VCG) — Meta Ads
Winners pay the **social opportunity cost** inflicted on other auction participants:

$$\text{Price}_i = \sum_{j \neq i} V_j(S_{-i}^*) - \sum_{j \neq i} V_j(S^*)$$

Where $V_j(S_{-i}^*)$ is the total market value when bidder $i$ is excluded, and $V_j(S^*)$ is the actual market value when bidder $i$ participates. VCG mathematically guarantees **Dominant-Strategy Incentive Compatibility (DSIC)**: truth-telling bids are always optimal.

#### 3. Standardized eCPM Value Function
$$\text{Total Value}_i = \left( \text{Bid}_i \times p(\text{CTR})_i \times p(\text{CVR})_i \times 1000 \right) + \text{Quality Score}_i - \text{User Penalty}_i$$

---

## 4. Platform-by-Platform Architectural Breakdown

```
┌─────────────────┬───────────────────┬───────────────────┬───────────────────┬───────────────────┐
│ Dimension       │ Meta (FB & IG)    │ Google Ecosystem  │ TikTok            │ X (Twitter)       │
├─────────────────┼───────────────────┼───────────────────┼───────────────────┼───────────────────┤
│ **Core Graph**  │ Social Graph +    │ Intent Graph +    │ Content Interest  │ Real-time Stream  │
│                 │ Behavioral Habits │ Search Queries    │ Graph (For You)   │ & Follower Graph  │
├─────────────────┼───────────────────┼───────────────────┼───────────────────┼───────────────────┤
│ **Core Engine** │ Meta Lattice /    │ DeepRank / MUM /  │ Monolith Sparse   │ Earlybird Lucene  │
│                 │ Andromeda ML      │ Smart Bidding     │ Parameter Server  │ + Heavy Ranker    │
├─────────────────┼───────────────────┼───────────────────┼───────────────────┼───────────────────┤
│ **Auction**     │ VCG (Value to     │ GSP (Ad Rank &    │ eCPM Value        │ Second-Price /    │
│                 │ User & Market)    │ Quality Score)    │ Optimization      │ GSP Auction       │
├─────────────────┼───────────────────┼───────────────────┼───────────────────┼───────────────────┤
│ **Autonomous**  │ Advantage+ (ASC)  │ Performance Max   │ Smart Performance │ Smart Budget      │
│                 │ Shopping / Leads  │ (PMax) Campaigns  │ Campaign (SPC)    │ Optimizer         │
└─────────────────┴───────────────────┴───────────────────┴───────────────────┴───────────────────┘
```

---

## 5. Server-Side Data Engineering & CAPI Architecture

With client-side tracking losing up to 30% of signals post-iOS 14.5, enterprise marketing requires a direct **Server-to-Server CAPI Pipeline** with robust deduplication.

```
 Client-Side (Browser/App)                Server-Side (Advertiser Backend)
 ┌──────────────────────┐                 ┌─────────────────────────────┐
 │ Meta Pixel / Web SDK │                 │ E-commerce Server (Shopify) │
 └──────────┬───────────┘                 └──────────────┬──────────────┘
            │ Event: Purchase ($150)                     │ CAPI Payload (Hashed PII)
            │ (fbp, fbc, IP, UA)                         │ (SHA256 Email, Phone, Value)
            └───────────────────────┬────────────────────┘
                                    │
                                    ▼
                     ┌──────────────────────────────┐
                     │ Server-Side Deduplication    │
                     │ (Matches unique `event_id`)  │
                     └──────────────┬───────────────┘
                                    │
                                    ▼
                     ┌──────────────────────────────┐
                     │ Platform Identity Graph      │
                     │ (Deterministic Graph Mapping)│
                     └──────────────┬───────────────┘
                                    │
                                    ▼
                     ┌──────────────────────────────┐
                     │ Feature Store & ML Retraining│
                     └──────────────────────────────┘
```

### Production Meta CAPI Payload Generator (TypeScript)

```typescript
import { createHash } from 'crypto';

export interface CapiPurchaseEvent {
  eventId: string;           // Must match the client-side pixel event_id
  timestamp: number;
  email: string;
  phone: string;
  firstName: string;
  lastName: string;
  city: string;
  state: string;
  zip: string;
  country: string;
  fbpCookie?: string;        // _fbp browser cookie
  fbcCookie?: string;        // _fbc click ID cookie
  clientIp: string;
  userAgent: string;
  currency: string;
  value: number;
  orderId: string;
  productIds: string[];
}

export function buildMetaCapiPayload(event: CapiPurchaseEvent) {
  // Normalize and SHA-256 hash customer PII
  const sha256 = (str: string) =>
    createHash('sha256').update(str.trim().toLowerCase()).digest('hex');

  return {
    data: [
      {
        event_name: 'Purchase',
        event_time: Math.floor(event.timestamp / 1000),
        event_id: event.eventId,
        action_source: 'website',
        user_data: {
          em: [sha256(event.email)],
          ph: [sha256(event.phone.replace(/[^0-9]/g, ''))],
          fn: [sha256(event.firstName)],
          ln: [sha256(event.lastName)],
          ct: [sha256(event.city)],
          st: [sha256(event.state)],
          zp: [sha256(event.zip)],
          country: [sha256(event.country)],
          client_ip_address: event.clientIp,
          client_user_agent: event.userAgent,
          fbp: event.fbpCookie,
          fbc: event.fbcCookie,
        },
        custom_data: {
          currency: event.currency,
          value: event.value,
          order_id: event.orderId,
          content_type: 'product',
          content_ids: event.productIds,
        },
      },
    ],
  };
}
```

---

## 6. Creative Engineering & Dynamic Video Synthesis

In modern algorithmic advertising, **creative is the targeting**. Algorithms analyze frame pixels, audio frequencies, and on-screen text to route ads to matching audience clusters.

```
                     MULTIMODAL CREATIVE EXTRACTION PIPELINE
                     
 ┌────────────────────────────────────────────────────────────────────────────┐
 │ RAW VIDEO AD CREATIVE (MP4 / 4K / 60fps)                                   │
 └─────────────────────────────────────┬──────────────────────────────────────┘
                                       │
         ┌─────────────────────────────┼─────────────────────────────┐
         ▼                             ▼                             ▼
┌──────────────────┐          ┌──────────────────┐          ┌──────────────────┐
│ Computer Vision  │          │ Audio & Speech   │          │ OCR & Semantic   │
│ (CLIP / ViT)     │          │ (Whisper / ASR)  │          │ Text Analysis    │
├──────────────────┤          ├──────────────────┤          ├──────────────────┤
│ Frame embeddings,│          │ Transcription of │          │ On-screen badge  │
│ object detection,│          │ spoken dialogue, │          │ text, pricing,   │
│ pacing & cuts.   │          │ voice tone & BGM.│          │ CTA typography.  │
└────────┬─────────┘          └────────┬─────────┘          └────────┬─────────┘
         │                             │                             │
         └─────────────────────────────┼─────────────────────────────┘
                                       │
                                       ▼ Concatenate & Project
                      ┌─────────────────────────────────┐
                      │ Multimodal Ad Vector: v ∈ R^512 │
                      └────────────────┬────────────────┘
                                       │
                                       ▼ Cosine Similarity
                      [ Matches User Interest Graph ]
```

### 6.1 The 3:2:2 Dynamic Creative Testing (DCT) Matrix
- **3 Video / Visual Hooks**: Test 3 distinct opening 0-3 second cuts (e.g., Macro diamond sparkle vs Customer proposal vs Jeweler bench crafting).
- **2 Body Angles**: Angle A (Emotional romance & forever value) vs Angle B (GIA/IGI certification specs & direct pricing).
- **2 Headlines**: Headline 1 (Trust & Guarantee) vs Headline 2 (Social Proof & Reviews).

### 6.2 Automated FFmpeg Video Assembly Pipeline (Node.js)

```typescript
import { spawn } from 'child_process';

export interface DynamicVideoConfig {
  hookPath: string;
  bodyPath: string;
  ctaPath: string;
  headlineText: string;
  outputPath: string;
}

export async function renderDynamicAd(config: DynamicVideoConfig): Promise<void> {
  const filterGraph = [
    `[0:v][0:a][1:v][1:a][2:v][2:a]concat=n=3:v=1:a=1[v_concat][a_concat]`,
    `[v_concat]drawtext=text='${config.headlineText}':fontcolor=white:fontsize=48:box=1:boxcolor=black@0.6:x=(w-text_w)/2:y=h-350:enable='between(t,0,3)'[v_out]`
  ].join(';');

  const args = [
    '-i', config.hookPath,
    '-i', config.bodyPath,
    '-i', config.ctaPath,
    '-filter_complex', filterGraph,
    '-map', '[v_out]',
    '-map', '[a_concat]',
    '-c:v', 'libx264',
    '-preset', 'fast',
    '-crf', '22',
    '-c:a', 'aac',
    config.outputPath
  ];

  return new Promise((resolve, reject) => {
    const proc = spawn('ffmpeg', args);
    proc.on('close', (code) => (code === 0 ? resolve() : reject(new Error(`FFmpeg error code ${code}`))));
  });
}
```

---

## 7. Privacy-Preserving Attribution: SKAN 4.0 & Differential Privacy

Under Apple's App Tracking Transparency (ATT), ad platforms rely on **cryptographic privacy protocols**.

```
                           SKAN 4.0 THREE-WINDOW LIFECYCLE
                           
  Day 0                         Day 2            Day 7                     Day 35
 ───┼─────────────────────────────┼────────────────┼─────────────────────────┼───► Time
    │◄───── WINDOW 1 (0-2d) ─────►│◄── WIN 2 (3-7d)►│◄──── WINDOW 3 (8-35d) ──►│
    │  • Fine Value (0-63) OR     │  • Coarse Value│  • Coarse Value         │
    │    Coarse (low/med/high)    │    (low/med/hi)│    (low/med/high)       │
    │  • Randomized 24-48h delay  │  • Random delay│  • Random delay         │
    ▼                             ▼                ▼                         ▼
 [ Postback 1 Sent ]             [ Postback 2 Sent] [ Postback 3 Sent ]
```

### Crowd Anonymity Tiers in SKAdNetwork 4.0
- **Tier 0**: Low volume $\to$ Source ID: 2 digits (Campaign 0-99), Conversion Value: Null.
- **Tier 1**: Moderate volume $\to$ Source ID: 2 digits, Conversion Value: Coarse (`low`, `medium`, `high`).
- **Tier 2**: High volume $\to$ Source ID: 3 digits, Conversion Value: Fine (6-bit integer 0–63).
- **Tier 3**: Maximum volume $\to$ Source ID: 4 digits (Campaign + Location + Creative), Fine Value: 0–63.

---

## 8. Econometric Marketing Mix Modeling (MMM) in Python

Below is the complete, runnable Python implementation of a Bayesian-style econometric MMM applying **Geometric Adstock (Decay)** and **Hill Saturation (Diminishing Marginal Returns)** with budget optimization:

```python
import numpy as np
import pandas as pd
from scipy.optimize import minimize
from sklearn.metrics import r2_score

def geometric_adstock(spend: np.ndarray, decay_rate: float) -> np.ndarray:
    """Computes carryover memory decay: x_adstocked[t] = spend[t] + decay * x_adstocked[t-1]"""
    adstocked = np.zeros_like(spend, dtype=float)
    adstocked[0] = spend[0]
    for t in range(1, len(spend)):
        adstocked[t] = spend[t] + decay_rate * adstocked[t - 1]
    return adstocked

def hill_saturation(adstocked_spend: np.ndarray, K: float, S: float) -> np.ndarray:
    """Computes S-curve diminishing returns: y = x^S / (K^S + x^S)"""
    x_s = np.power(np.maximum(adstocked_spend, 0), S)
    k_s = np.power(K, S)
    return x_s / (k_s + x_s + 1e-9)

class ProductionMMM:
    def __init__(self):
        self.params = None
        self.channel_names = []

    def _forward_pass(self, params_vec: np.ndarray, spend_matrix: np.ndarray) -> np.ndarray:
        n_channels = spend_matrix.shape[1]
        n_weeks = spend_matrix.shape[0]
        pred_rev = np.zeros(n_weeks)
        
        for c in range(n_channels):
            decay = params_vec[c * 4 + 0]
            K = params_vec[c * 4 + 1]
            S = params_vec[c * 4 + 2]
            beta = params_vec[c * 4 + 3]
            
            raw_spend = spend_matrix[:, c]
            adstocked = geometric_adstock(raw_spend, decay)
            sat = hill_saturation(adstocked, K, S)
            pred_rev += beta * sat
            
        intercept = params_vec[-1]
        pred_rev += intercept
        return pred_rev

    def fit(self, X_spend: pd.DataFrame, y_revenue: pd.Series):
        self.channel_names = list(X_spend.columns)
        n_channels = len(self.channel_names)
        spend_mat = X_spend.values
        y_true = y_revenue.values

        bounds = []
        initial_guess = []
        for c in range(n_channels):
            max_spend = np.max(spend_mat[:, c])
            bounds.extend([(0.01, 0.90), (max_spend * 0.1, max_spend * 3.0), (0.5, 2.5), (0.0, None)])
            initial_guess.extend([0.3, max_spend * 0.5, 1.0, np.mean(y_true) / (n_channels + 1)])
            
        bounds.append((0.0, np.mean(y_true)))
        initial_guess.append(np.mean(y_true) * 0.2)

        def loss(params_vec):
            y_pred = self._forward_pass(params_vec, spend_mat)
            return np.sqrt(np.mean((y_true - y_pred) ** 2))

        res = minimize(loss, initial_guess, bounds=bounds, method='L-BFGS-B')
        self.params = res.x
        return self

    def optimize_budget(self, total_budget: float) -> dict:
        """Solves optimal channel budget allocation using SLSQP."""
        n_channels = len(self.channel_names)
        def objective(spend_vec):
            rev = 0.0
            for c in range(n_channels):
                decay = self.params[c * 4 + 0]
                K = self.params[c * 4 + 1]
                S = self.params[c * 4 + 2]
                beta = self.params[c * 4 + 3]
                steady_adstock = spend_vec[c] / (1.0 - decay)
                sat = hill_saturation(np.array([steady_adstock]), K, S)[0]
                rev += beta * sat
            return -rev

        constraints = {'type': 'eq', 'fun': lambda b: np.sum(b) - total_budget}
        bounds = [(0.0, total_budget) for _ in range(n_channels)]
        init = [total_budget / n_channels] * n_channels

        res = minimize(objective, init, method='SLSQP', bounds=bounds, constraints=constraints)
        return {self.channel_names[i]: round(res.x[i], 2) for i in range(n_channels)}
```

---

## 9. Real-Time Feature Stores & Streaming Flink Aggregations

To supply live click velocities to ranking models, Apache Flink computes **15-minute sliding window aggregations** over high-throughput Kafka streams:

```sql
CREATE VIEW ad_realtime_velocity_15m AS
SELECT
    ad_id,
    COUNT(CASE WHEN event_type = 'impression' THEN 1 END) AS impressions_15m,
    COUNT(CASE WHEN event_type = 'click' THEN 1 END) AS clicks_15m,
    COUNT(CASE WHEN event_type = 'conversion' THEN 1 END) AS conversions_15m,
    CAST(COUNT(CASE WHEN event_type = 'click' THEN 1 END) AS DOUBLE) / 
        NULLIF(COUNT(CASE WHEN event_type = 'impression' THEN 1 END), 0) AS realtime_ctr_15m,
    HOP_END(event_time, INTERVAL '10' SECOND, INTERVAL '15' MINUTE) AS window_end_time
FROM ad_click_stream
GROUP BY
    HOP(event_time, INTERVAL '10' SECOND, INTERVAL '15' MINUTE),
    ad_id;
```

---

## 10. Connected TV (CTV) & SSAI Manifest Insertion

Connected TV integrates digital targeting into television inventory through **Server-Side Ad Insertion (SSAI)** using standardized **VAST 4.2 XML manifests**:

```xml
<VAST version="4.2">
  <Ad id="palencia_diamond_30s">
    <InLine>
      <AdSystem>PalenciaSSAIServer</AdSystem>
      <AdTitle>Handcrafted Diamonds - The Art of Trust</AdTitle>
      <Impression><![CDATA[https://telemetry.adtech.com/impression?ad=palencia_30s]]></Impression>
      <Creatives>
        <Creative>
          <Linear>
            <Duration>00:00:30</Duration>
            <TrackingEvents>
              <Tracking event="firstQuartile"><![CDATA[https://telemetry.adtech.com/q1]]></Tracking>
              <Tracking event="complete"><![CDATA[https://telemetry.adtech.com/complete]]></Tracking>
            </TrackingEvents>
            <MediaFiles>
              <MediaFile delivery="progressive" type="video/mp4" width="1920" height="1080">
                <![CDATA[https://cdn.palenciadiamonds.com/video/ctv_1080p.mp4]]>
              </MediaFile>
            </MediaFiles>
          </Linear>
        </Creative>
      </Creatives>
    </InLine>
  </Ad>
</VAST>
```

---

## 11. Conversion Rate Optimization (CRO) & Edge Personalization

```typescript
// Cloudflare Worker: Sub-10ms Landing Page Personalization based on Ad Context
export default {
  async fetch(request: Request): Promise<Response> {
    const url = new URL(request.url);
    const response = await fetch(request);
    const utmTerm = url.searchParams.get('utm_term') || '';

    const rewriter = new HTMLRewriter()
      .on('#hero-headline', {
        element(el) {
          if (utmTerm.includes('lab_grown')) {
            el.setInnerContent('Certified Lab-Grown Diamonds. Exacting Standards. Honest Prices.');
          } else if (utmTerm.includes('solitaire')) {
            el.setInnerContent('Handcrafted Platinum Solitaire Engagement Rings.');
          }
        },
      });

    return rewriter.transform(response);
  },
};
```

---

## 12. Operational Media Buying & Incident Response Runbook

### 12.1 Performance Diagnostics Matrix

```
┌───────────────────────────────┬───────────────────────────┬───────────────────────────────┐
│ Metric Diagnostic             │ Root Cause Identification │ Remediation Action            │
├───────────────────────────────┼───────────────────────────┼───────────────────────────────┤
│ High Frequency (> 3.5) +      │ Creative Fatigue / Burnout│ Deploy fresh visual hooks;    │
│ Falling CTR + Rising CPA      │ (Audience exhausted ad)   │ rotate concepts immediately.  │
├───────────────────────────────┼───────────────────────────┼───────────────────────────────┤
│ Low Hook Rate (< 20%) +       │ Weak Opening 3-Second Cut │ Test new high-contrast video  │
│ High Hold Rate (> 50%)        │ (Core value proposition is│ openers and text overlays.    │
│                               │ strong, but hook fails)   │                               │
├───────────────────────────────┼───────────────────────────┼───────────────────────────────┤
│ High Hook Rate (> 40%) +      │ Landing Page / Offer Mismatch│ Align landing page hero text  │
│ Low Checkout Rate             │ or slow page load (> 2.5s)│ with ad copy; optimize LCP.   │
└───────────────────────────────┴───────────────────────────┴───────────────────────────────┘
```

### 12.2 24-Hour Incident Response Triage Tree

```
                        AD TECH INCIDENT RESPONSE TREE
                        
           [ SYMPTOM: CPA Spikes 2x or Spend Flatlines ]
                                │
                                ▼
 ┌─────────────────────────────────────────────────────────────┐
 │ STEP 1: VERIFY TRACKING HEALTH & CAPI INGESTION             │
 │ • Check Meta Events Manager / Google Ads Diagnostics.       │
 │ • Is Event Match Quality (EMQ) < 6.0?                       │
 │ • Are server-side webhook payloads throwing HTTP 400/500s?  │
 └──────────────────────────────┬──────────────────────────────┘
                                │ (If Tracking is Healthy)
                                ▼
 ┌─────────────────────────────────────────────────────────────┐
 │ STEP 2: INSPECT AD AUCTION CLEARING DYNAMICS                │
 │ • Check First-Time Impression Ratio (FTIR). If < 30%,       │
 │   creative fatigue is capping market volume.                │
 │ • Check Auction Overlap Rate. If > 20%, multiple internal   │
 │   ad sets are bidding against each other.                   │
 └──────────────────────────────┬──────────────────────────────┘
                                │ (If Auction is Normal)
                                ▼
 ┌─────────────────────────────────────────────────────────────┐
 │ STEP 3: INSPECT LANDING PAGE & CHECKOUT GATEWAY             │
 │ • Verify Edge Worker latency (< 50ms).                      │
 │ • Test Shopify / Stripe checkout webhooks & payment APIs.   │
 │ • Check Core Web Vitals (LCP < 2.0s).                       │
 └─────────────────────────────────────────────────────────────┘
```

---

## Related documents

- [Marketing Strategy](marketing-strategy.md)
- [Channels & Social](channels-and-social.md)
- [Content & SEO](content-and-seo.md)
- [Data Privacy & Security](../05-compliance-ethics/data-privacy-and-security.md)
- [CRM & Clienteling](../04-sales-cx/crm-and-clienteling.md)
- [Documentation Home](../../README.md)
