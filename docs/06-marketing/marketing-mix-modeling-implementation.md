# Marketing Mix Modeling (MMM) & Advanced Attribution Implementation

This document provides a comprehensive, step-by-step technical guide for implementing a production-grade Bayesian Marketing Mix Model (MMM) for Palencia Diamonds. As a high-AOV business with long consideration cycles (30-90 days), traditional last-click attribution (GA4) or platform-reported attribution (Meta/Google Ads) is fundamentally broken and leads to fatal misallocation of capital.

We rely on **Bayesian Marketing Mix Modeling** combined with **Incrementality Testing (Geo-Holdouts)** to determine true ROAS (Return on Ad Spend) and Marginal CPA.

---

## 1. The Attribution Problem at Palencia

When a customer buys a $15,000 engagement ring, the multi-touch journey often looks like this:
1. **Day 1 (Discovery):** Sees a Meta Video Ad (Hook: "Why lab diamonds?"). Clicks. Browses.
2. **Day 5 (Research):** Searches "Palencia vs VRAI" on Google. Clicks a Brand Search Ad.
3. **Day 14 (Retargeting):** Sees a Meta DPA (Dynamic Product Ad) with the exact ring. Doesn't click.
4. **Day 30 (Nurture):** Receives email #4 from our welcome series. 
5. **Day 45 (Purchase):** Types "Palencia.com" directly into the browser and buys.

**The Multi-Attribution Chaos:**
*   **Meta Ads Manager:** Claims 100% credit (7-day click / 1-day view).
*   **Google Ads:** Claims 100% credit (data-driven attribution).
*   **Google Analytics (GA4):** Claims 100% credit for "Direct / None" (last non-direct click).
*   **Klaviyo:** Claims 100% credit (last email opened).

If you sum up the platform-reported revenue, you will double or triple-count sales. 

**The Solution:** Triangulation via MMM. We use top-down statistical modeling (MMM) to analyze aggregated spend vs. aggregated revenue, grounded by bottom-up incrementality testing.

---

## 2. The Tech Stack

We utilize Google's **LightweightMMM** library, which is built on JAX and NumPyro for fast Bayesian inference via Markov Chain Monte Carlo (MCMC).

*   **Data Warehouse:** Google BigQuery
*   **Orchestration:** Apache Airflow (Cloud Composer)
*   **Modeling Framework:** Python 3.10+, JAX, NumPyro, LightweightMMM
*   **Visualization:** Streamlit / Looker

---

## 3. Step-by-Step Technical Implementation

### Phase 1: Data Ingestion & Cleansing (The Foundation)

A model is only as good as its inputs. We require daily aggregated data spanning at least 18-24 months to capture seasonality and sufficient variance in ad spend.

**1. Define Media Variables (The "Inputs"):**
Break channels down by *tactic*, not just platform. Lumping Brand Search with PMax ruins the model.
*   `meta_prospecting_spend`, `meta_prospecting_impressions`
*   `meta_retargeting_spend`, `meta_retargeting_impressions`
*   `google_pmax_spend`
*   `google_search_nonbrand_spend`
*   `google_search_brand_spend` (Highly collinear with organic demand; must be isolated)

**2. Define Control Variables (The "Base Sales" drivers):**
*   `organic_search_sessions` (Proxy for baseline brand awareness)
*   `email_sends` (Volume of CRM activity)
*   `is_holiday_bfcm` (Binary flag for Black Friday week)
*   `is_holiday_vday` (Binary flag for Valentine's Day week)
*   `macro_gold_price` (Gold commodity pricing index - crucial for fine jewelry)

**3. Define the Response Variable (The "Output"):**
*   `daily_net_revenue` (Excluding wholesale, B2B, or non-marketing-driven sales. Must account for returns/cancellations).

**BigQuery Materialized View (Airflow DAG executes this daily):**

```sql
CREATE OR REPLACE MATERIALIZED VIEW `palencia-data.marketing.mmm_daily_features` AS
SELECT 
    d.date,
    SUM(r.net_revenue) as revenue,
    COALESCE(SUM(m.meta_prospecting_spend), 0) as meta_prospecting_spend,
    COALESCE(SUM(m.meta_retargeting_spend), 0) as meta_retargeting_spend,
    COALESCE(SUM(g.google_pmax_spend), 0) as google_pmax_spend,
    COALESCE(SUM(g.google_search_brand_spend), 0) as google_search_brand_spend,
    COALESCE(SUM(ga.organic_sessions), 0) as organic_sessions,
    COALESCE(SUM(k.email_sends), 0) as email_sends,
    IF(EXTRACT(MONTH FROM d.date) = 11 AND EXTRACT(DAY FROM d.date) >= 20, 1, 0) as is_holiday_bfcm,
    IF(EXTRACT(MONTH FROM d.date) = 2 AND EXTRACT(DAY FROM d.date) <= 14, 1, 0) as is_holiday_vday
FROM 
    `palencia-data.core.dim_dates` d
LEFT JOIN `palencia-data.sales.fct_orders` r ON d.date = r.order_date
LEFT JOIN `palencia-data.marketing.fct_meta_spend` m ON d.date = m.date
LEFT JOIN `palencia-data.marketing.fct_google_spend` g ON d.date = g.date
LEFT JOIN `palencia-data.traffic.fct_ga4_sessions` ga ON d.date = ga.date
LEFT JOIN `palencia-data.crm.fct_klaviyo_sends` k ON d.date = k.date
GROUP BY 1, 9, 10
ORDER BY d.date ASC;
```

### Phase 2: Dealing with Luxury E-commerce Outliers

In high-AOV jewelry, a single customer buying a $150,000 bespoke necklace on a random Tuesday can skew the entire model, making the algorithm think Meta Ads suddenly had a 100x ROAS spike.

**Data Smoothing Protocol:**
Before feeding `revenue` to the model, we cap extreme outliers. Any daily revenue exceeding the 99th percentile + 3 Standard Deviations is capped to the 99th percentile limit.

---

### Phase 3: Model Architecture & Hyperparameters

We use Bayesian modeling to account for two critical marketing realities:
1.  **Adstock (Carryover Effect):** Marketing has a half-life. A video seen today influences a purchase 3 weeks from now. (Modeled via Weibull or Geometric decay).
2.  **Diminishing Returns (Saturation):** Spending $10k/day might yield a 3.0 ROAS, but scaling to $50k/day saturates the audience and drops ROAS to 1.5. (Modeled via Hill functions).

**Python Implementation (Airflow Task):**

```python
import jax.numpy as jnp
from lightweight_mmm import lightweight_mmm
from lightweight_mmm import optimize_media
from lightweight_mmm import preprocessing
from lightweight_mmm import utils

# 1. Fetch & Split Data
# Assume `df` is loaded from BigQuery `mmm_daily_features`
split_point = len(df) - 28 # Hold out last 28 days for out-of-sample testing
media_data = df[['meta_prospecting_spend', 'meta_retargeting_spend', 'google_pmax_spend', 'google_search_brand_spend']].values
target_data = df['revenue'].values
extra_features = df[['organic_sessions', 'email_sends', 'is_holiday_bfcm', 'is_holiday_vday']].values

# 2. Preprocess & Scale
# Scaling to mean=0, variance=1 is required for stable MCMC sampling in NumPyro
media_scaler = preprocessing.CustomScaler(divide_operation=jnp.mean)
target_scaler = preprocessing.CustomScaler(divide_operation=jnp.mean)
extra_features_scaler = preprocessing.CustomScaler(divide_operation=jnp.mean)

media_data_train = media_scaler.fit_transform(media_data[:split_point])
target_train = target_scaler.fit_transform(target_data[:split_point])
extra_features_train = extra_features_scaler.fit_transform(extra_features[:split_point])

# 3. Initialize Model
# We use 'hill_adstock' to model both diminishing returns (Hill) and decay (Adstock)
mmm = lightweight_mmm.LightweightMMM(model_name="hill_adstock")

# 4. Define Priors (Crucial for Bayesian Models)
# We set tight priors on Brand Search (we know it's highly correlative, low incremental)
# and looser priors on Prospecting.
custom_priors = {
    "coef_media": jnp.array([0.5, 0.3, 0.4, 0.05]) # Lower prior for the 4th column (Brand Search)
}

# 5. Fit Model (MCMC Sampling)
# Runs on GPU/TPU if available via JAX
mmm.fit(
    media=media_data_train,
    media_prior=media_data_train.sum(axis=0), # Default prior proportional to spend
    target=target_train,
    extra_features=extra_features_train,
    number_warmup=1000,
    number_samples=2000,
    number_chains=4,
    custom_priors=custom_priors,
    seed=42
)

# 6. Check Model Fit (R-hat and MAPE)
# R-hat should be < 1.1 for all parameters indicating chains converged.
```

---

### Phase 4: Grounding the Model (Geo-Holdout Testing)

An uncalibrated MMM is just a glorified correlation engine. It will mistakenly attribute organic sales to Brand Search because they move together perfectly. It *must* be grounded in physical reality through incrementality testing.

**The Geo-Holdout Protocol:**
1.  **The Test:** Using a tool like Google's CausalImpact, we select a test region (e.g., California + Texas) and a control region (rest of US). We pause Meta Prospecting Ads entirely in the test region for 30 days.
2.  **The Measurement:** The model predicts what CA+TX revenue *should* have been if ads were running. We compare this to the actual revenue. 
3.  **The Result:** If synthetic baseline was $500k, and actual was $400k, the true incremental value of Meta Ads in that period was $100k. 
4.  **The Calibration:** We calculate the true ROAS from this test and inject it directly into the MMM's Bayesian Priors.

```python
# Pseudo-code for calibrating the MMM with Geo-Test results
# We tell the model: "Do not guess the ROI for Meta Prospecting; we know it is exactly 1.8x based on our Texas holdout."

calibration_data = {
    "media_names": ["meta_prospecting_spend"],
    "roi_mean": jnp.array([1.8]),
    "roi_std": jnp.array([0.15]) # Confidence interval from the CausalImpact test
}

mmm.fit(
    # ... standard parameters ...
    media_prior=calibration_data["roi_mean"],
    degrees_of_freedom=calibration_data["roi_std"]
)
```

---

## 4. Operationalizing the Output (The "So What?")

A beautiful model sitting in a Jupyter Notebook is useless. It must drive daily media buying decisions.

### 1. True ROAS Multiplier Matrix
We generate a Multiplier Matrix updated on the 1st of every month. Media buyers use this to translate the fake "Platform ROAS" into our True ROAS.

| Channel | Platform Reported ROAS | MMM True ROAS | **Multiplier** | Action |
| :--- | :--- | :--- | :--- | :--- |
| **Meta Prospecting** | 1.5x | 2.2x | **1.46x** | Under-reporting. Scale spend UP. |
| **Meta Retargeting** | 6.0x | 2.0x | **0.33x** | Over-reporting. Maintain baseline. |
| **Google PMax** | 3.5x | 3.1x | **0.88x** | Fairly accurate. Optimize normally. |
| **Google Brand Search** | 15.0x | 1.2x | **0.08x** | Highly cannibalistic. Defense minimums only. |

**Daily Workflow:** In our Looker dashboard, a calculated field multiplies the live Meta API ROAS by the 1.46x multiplier. Media buyers optimize campaigns based on the *True ROAS* column.

### 2. Marginal ROAS (mROAS) & The Saturation Curve
Average ROAS tells us how we did yesterday. **Marginal ROAS** tells us what the *next* dollar will yield tomorrow.

The MMM outputs the exact saturation curve (Hill function) for each channel. 

*   *Scenario:* Meta Prospecting is currently yielding a 2.2x Average ROAS at $5,000/day. However, the model's saturation curve shows that scaling from $5,000 to $6,000 will only yield a Marginal ROAS of 0.8x. 
*   *Rule:* **Media Buyers are strictly forbidden from scaling a channel past its MMM saturation inflection point**, regardless of how good the in-platform Average ROAS looks. 

### 3. Automated Budget Optimization
When the CFO releases the monthly budget (e.g., $250,000), we run the LightweightMMM optimizer to calculate the mathematically perfect distribution of that cash across channels to maximize total revenue.

```python
# Find the optimal distribution of $250k across our 4 media channels for the next 30 days
optimal_allocation, optimal_revenue = optimize_media.find_optimal_budgets(
    n_time_periods=30,
    media_mix_model=mmm,
    budget=250000,
    prices=jnp.ones(4) # Assuming spend is already in dollar units
)

print("Optimal Spend Allocation:", optimal_allocation)
print("Predicted Incremental Revenue:", optimal_revenue)
```

---

## 5. Maintenance & Retraining SOP

1.  **Daily:** Airflow DAG appends yesterday's data to the BigQuery `mmm_daily_features` view.
2.  **Weekly:** Looker dashboard updates rolling 30-day True ROAS trends for executive review.
3.  **Monthly (1st of Month):** Data Science team triggers the `mmm.fit()` pipeline on the latest 24 months of data. New Multiplier Matrices and Saturation limits are published to the Media Buying team via Slack.
4.  **Quarterly:** Growth Ops executes one new Geo-Holdout test (e.g., pausing YouTube Ads in Florida) to recalibrate a specific channel's priors.

By graduating from Last-Click to Bayesian MMM, Palencia transitions from "buying clicks" to "allocating capital." We stop optimizing for algorithms and start optimizing for true incremental business growth.
