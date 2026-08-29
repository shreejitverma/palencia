# Growth Operations & Analytics Standard Operating Procedures (SOP)

> The definitive step-by-step operational runbook for growth engineers, media buyers, and marketing analysts at Palencia Diamonds — governing daily bid pacing, weekly creative testing, catalog feed maintenance, and monthly econometric attribution.

| | |
|---|---|
| **Owner** | Growth Marketing & Analytics Operations |
| **Last reviewed** | 2026-08-29 |
| **Review cadence** | Quarterly |
| **Status** | Active |

---

## 1. The Growth Operating Rhythm Overview

```
┌─────────────────┬───────────────────────────────────┬───────────────────────────────────────┐
│ Cadence         │ Core Tasks & Deliverables         │ Primary Operating Systems & Tools     │
├─────────────────┼───────────────────────────────────┼───────────────────────────────────────┤
│ **Daily (08:30) │ Pacing verification, CAC/ROAS     │ Meta Ads Manager, Google Ads,         │
│                 │ anomaly checks, budget caps       │ Shopify Real-Time Dashboard           │
├─────────────────┼───────────────────────────────────┼───────────────────────────────────────┤
│ **Weekly        │ Creative testing graduation,      │ Triple Whale / Northbeam, Meta Ads    │
│ (Mon 10:00)**   │ fatiguing ad pauses, DCT launch   │ Creative Sandbox, Asana Sprint Board  │
├─────────────────┼───────────────────────────────────┼───────────────────────────────────────┤
│ **Bi-Weekly**   │ Product feed validation, Merchant │ Google Merchant Center, Meta Commerce │
│                 │ Center disapproval triage         │ Manager, DataFeedWatch                │
├─────────────────┼───────────────────────────────────┼───────────────────────────────────────┤
│ **Monthly**     │ Econometric MMM re-calibration,   │ Python MMM Engine, BigQuery Analytics,│
│                 │ cross-channel budget allocation   │ Geo-Lift Incrementality Reports       │
├─────────────────┼───────────────────────────────────┼───────────────────────────────────────┤
│ **Quarterly**   │ Strategic media mix audit,        │ Executive Leadership Dashboard,       │
│                 │ agency & partner performance      │ Finance P&L Reconciliation            │
└─────────────────┴───────────────────────────────────┴───────────────────────────────────────┘
```

---

## 2. SOP 1: Daily Morning Performance & Pacing Audit (15-Minute Protocol)

Every morning at **08:30 AM**, the media buying team executes this 5-step checklist:

1. **Verify Yesterday’s Blended CAC & MER (Marketing Efficiency Ratio)**:
   - Calculate $\text{MER} = \frac{\text{Total Shopify Net Revenue}}{\text{Total Ad Spend Across All Platforms}}$.
   - *Target Benchmark*: $\text{MER} \ge 4.5\times$ for blended e-commerce operations.
2. **Inspect Campaign Spend Pacing**:
   - Check if any Meta Advantage+ or Google PMax campaign spent $> 120\%$ of its target daily budget before 2:00 PM (indicates potential runaway bid pacing).
3. **Inspect Conversion API (CAPI) Signal Health**:
   - Navigate to Meta Events Manager $\to$ Diagnostics. Confirm **Event Match Quality (EMQ)** score is $\ge 8.0/10.0$ and zero HTTP 500 error alerts exist.
4. **Identify Runaway Ad Creatives**:
   - If any individual ad spent $> 2\times\text{ Target CPA}$ with zero purchases in the last 48 hours, pause immediately.
5. **Log Status in Growth Slack Channel**:
   - Format: `[DATE] Spend: $X,XXX | Revenue: $XX,XXX | Blended MER: X.XX | Actions Taken: [Notes]`.

---

## 3. SOP 2: Weekly Creative Testing & Graduation Protocol

Every **Monday morning**, execute the 3:2:2 Dynamic Creative Testing (DCT) lifecycle:

```
                            THE 4-STAGE GRADUATION LIFECYCLE
                            
  STAGE 1: EVALUATE           STAGE 2: GRADUATE             STAGE 3: RE-TEST
 ┌─────────────────────────┐ ┌─────────────────────────┐ ┌─────────────────────────┐
 │ Review Sandbox Ad Sets  │ │ Extract winning Post ID │ │ If concept was a near-  │
 │ Criteria for Winner:    │ │ (`fb_ad_id`) preserving │ │ winner, iterate hook:   │
 │ • ≥ 10 Purchases        │ │ social likes & comments.│ │ • Keep winning body/CTA │
 │ • CPA ≤ Target CPA      │ │ Add to Primary ASC      │ │ • Film 3 new visual cuts│
 │ • Hook Rate ≥ 30%       │ │ Scaling Campaign.       │ │ • Re-launch in Sandbox  │
 └─────────────────────────┘ └─────────────────────────┘ └─────────────────────────┘
```

---

## 4. SOP 3: Product Feed Hygiene & Catalog Sync (Google & Meta)

Fine jewelry catalogs require accurate diamond grading specs, real-time metal stock status, and dynamic pricing updates:

```
┌──────────────────────────────────────┬────────────────────────────────────────────────────────┐
│ Feed Attribute Requirement           │ Standard & Format Specification                        │
├──────────────────────────────────────┼────────────────────────────────────────────────────────┤
│ **Title Optimization**               │ `[Brand] + [Carat] + [Shape] + [Metal] + [Style]`       │
│                                      │ Example: *Palencia 2.00ct Oval Platinum Solitaire Ring*│
├──────────────────────────────────────┼────────────────────────────────────────────────────────┤
│ **Certification Tagging**            │ Add custom label: `custom_label_0 = "GIA_Certified"`   │
│                                      │ or `"IGI_Certified"` for granular PMax asset grouping. │
├──────────────────────────────────────┼────────────────────────────────────────────────────────┤
│ **Real-Time Price Sync**             │ Daily automated Google Content API & Meta Catalog sync │
│                                      │ preventing pricing discrepancy disapprovals.          │
├──────────────────────────────────────┼────────────────────────────────────────────────────────┤
│ **High-Resolution White Background** │ Primary image on pure white (`#FFFFFF`) with zero      │
│                                      │ watermarks per Google Merchant Center guidelines.      │
└──────────────────────────────────────┴────────────────────────────────────────────────────────┘
```

---

## 5. SOP 4: Monthly MMM Calibration & Incrementality Re-Allocation

At the end of each month, the analytics lead executes the Python Marketing Mix Model to generate next month's optimal budget distribution:

```bash
# Step 1: Export weekly spend and revenue dataset from BigQuery
bq query --use_legacy_sql=false \
  'SELECT week_start_date, meta_spend, google_spend, tiktok_spend, total_revenue 
   FROM `palencia-data.analytics.weekly_marketing_metrics` 
   ORDER BY week_start_date ASC' > mmm_dataset.csv

# Step 2: Execute Bayesian MMM Optimizer
python3 -m analytics.production_mmm --input mmm_dataset.csv --next_month_budget 150000
```

---

## Related documents

- [Ad Tech & Paid Media Pipeline](ad-tech-and-paid-media-pipeline.md)
- [Creative Strategy & Briefing](creative-strategy-and-briefing.md)
- [Landing Page & CRO Playbook](landing-page-and-cro-playbook.md)
- [Marketing Strategy](marketing-strategy.md)
- [Channels & Social](channels-and-social.md)
- [Documentation Home](../../README.md)
