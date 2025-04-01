Absolutely — here’s your **updated roadmap** with concise and powerful additions to incorporate **pre-recession historical analysis** where it fits naturally. This will boost your project's credibility, interpretability, and marketability — without adding bloat.

---

# ✅ Capstone Roadmap: Recession Risk Forecasting (Unsupervised / Continuous)  
*Forecast the next quarter’s recession probability-like risk score using macroeconomic signals*

---

## 📍 1. Define the Problem & Scope  

### 🎯 Goal  
> Forecast a **continuous score** representing **economic fragility** or **recession risk** in the **next quarter**, using past 4 quarters of macro indicators.

### 🔍 Key Insight  
Instead of hard classification into discrete regimes, we learn a **smooth risk signal** that rises/falls as economic fundamentals deteriorate or strengthen — using regression, distance models, or latent representations.

---

## 📍 2. Data Collection  

### 📦 Categorized Economic Indicators with Timing Classification

| Theme                  | Indicators                                             | Type       |
|------------------------|--------------------------------------------------------|------------|
| **Confidence & Sentiment** | Consumer Confidence, Business Confidence               | **Leading**   |
| **Labor Market**       | Jobs Added, Unemployment Rate, Labor Force Participation | Jobs Added: **Leading**<br>Unemployment: **Lagging**<br>Labor Force Participation: **Lagging** |
| **Inflation**          | CPI, PPI                                               | CPI: **Lagging**<br>PPI: **Leading** |
| **Rates & Policy**     | Fed Funds Rate, Yield Curve Spread                     | Fed Funds Rate: **Lagging** (Policy-Reactive)<br>Yield Curve Spread: **Leading** |
| **Real Economy**       | Housing Starts, Durable Goods Orders, Capacity Utilization | Housing Starts: **Leading**<br>Durable Goods Orders: **Leading**<br>Capacity Utilization: **Coincident** |
| **Production**         | Industrial Production                                  | **Coincident** |
| **Fiscal Stress**      | Deficit % GDP, Corporate Bond Spreads                  | Both: **Lagging** |
| **Liquidity**          | Real M2 Stocks                                         | **Lagging** |
| **Sales/Inventory**    | Business Inventories, Retail Sales                     | Inventories: **Lagging**<br>Retail Sales: **Coincident** |
| **Volatility**         | Volatility Index (VIX)                                 | **Leading** (sentiment proxy) |

---

📌 Tip: These datasets can also be used for **retrospective validation** — analyzing how indicators behaved 4 quarters before past recessions (e.g., 2001, 2008, 2020).

---

## 📍 3. Data Understanding & EDA  

- Convert all indicators to **quarterly frequency**  
- Plot historical **economic shocks** and overlay indicators  
- Create **z-scored time series** for comparison  
- Calculate **lag correlations** with NBER recessions or GDP drops  
- Explore feature clusters using PCA or TSNE  

📌 Optional: Build **"pre-recession snapshots"** to see how macro indicators behaved in the 4–5 quarters prior to known recessions — useful for building trust in your model’s logic.

---

## 📍 4. Construct Recession Risk Proxy (Optional)  

If you want to **train a regression model**, construct a soft "target" using interpretable macro rules:

```python
proxy_recession_risk = (
    0.25 * zscore(1 - capacity_utilization) +
    0.25 * zscore(unemployment_rate) +
    0.20 * zscore(deficit_percent_gdp * interest_rate) +
    0.15 * zscore(inventory_to_sales_ratio) +
    0.15 * zscore(vix)
)
```

This becomes your **target risk score** (between 0–1 or scaled appropriately).  
📌 Validate this score by comparing it against real-world pre-recession periods.

---

## 📍 5. Feature Engineering  

### 🧠 Lags & Temporal Dynamics  
- Lag features by 1–4 quarters  
- Use rolling % changes, volatility, z-score normalization  

### ⚙️ Derived Features  

| Feature | Formula |
|--------|---------|
| **Fiscal Stress Index** | Deficit % GDP × Interest Rate |
| **Inflation Gap** | PPI – CPI |
| **Liquidity Shock** | ΔM2 QoQ |
| **Jobs Momentum** | ∆Jobs / ∆Unemployment |
| **Inventory-to-Sales Ratio** | Inventories / Retail Sales |
| **Volatility Shock** | QoQ % Change in VIX |
| **Yield Curve Inversion** | 10Y – 2Y spread (negative = inverted)

📌 Use retrospective analysis to confirm which of these **consistently shift** before past downturns.

---

## 📍 6. Modeling Options  

### 🧰 If Using Regression  
| Model | Notes |
|-------|-------|
| **XGBoostRegressor / LightGBM** | Strong performance, easy SHAP |
| **Random Forest Regressor** | Ensemble baseline |
| **LSTM / Temporal CNN Regressor** | Capture sequence patterns |
| **Bayesian Ridge / BSTS** | Include uncertainty bands |
| **VAR** | For economic system dynamics |
| **SHAP / LIME** | Add interpretability  

### 🧰 If Using Unsupervised / Distance-Based  
| Model | Purpose |
|-------|---------|
| **Autoencoder / PCA** | Learn typical “healthy” quarters, score deviations |
| **KMeans / DBSCAN** | Cluster pre-recession patterns, compute distance |
| **Mahalanobis Distance** | Distance from historical “stable” center |

---

## 📍 7. Forecasting Logic  

- Use **sliding window**: Past 4 quarters → Predict next quarter’s recession risk score  
- Optionally forecast 2–3 quarters ahead using autoregressive structure  
- Add ensemble averaging across time horizons (1Q, 2Q, 3Q risk)  

📌 Compare current predictions to **historical risk levels** during 2001, 2008, and 2020 recessions to understand similarity patterns.

Here’s your **updated roadmap** with a clean and concise section added on **Train-Test Splitting and Model Validation**, placed right after **Section 7: Forecasting Logic**, where it naturally fits in the pipeline. This new **Section 7.1** includes train/test strategy, regression metrics, and optional binary evaluation for stakeholder alignment.

---

## 📍 7. Forecasting Logic  

- Use **sliding window**: Past 4 quarters → Predict next quarter’s recession risk score  
- Optionally forecast 2–3 quarters ahead using autoregressive structure  
- Add ensemble averaging across time horizons (1Q, 2Q, 3Q risk)  

📌 Compare current predictions to **historical risk levels** during 2001, 2008, and 2020 recessions to understand similarity patterns.

---

## 📍 7.1 Train-Test Strategy & Validation Metrics ✅  

To ensure real-world usability and avoid leakage, use a **chronological train/test split**:

- Example: Train = 1970–2010, Test = 2011–2024  
- Use **sliding windows** to simulate forecasting:  
  `X = past 4 quarters → y = risk next quarter`

### ✅ Core Metrics (Regression)

| Metric | Use |
|--------|-----|
| **MAE / RMSE** | Accuracy of predicted vs proxy scores |
| **R² Score** | How well model explains variance in risk |
| **MAPE** | If your risk score is scaled 0–100% |

```python
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
mae = mean_absolute_error(y_true, y_pred)
rmse = mean_squared_error(y_true, y_pred, squared=False)
r2 = r2_score(y_true, y_pred)
```

### ⚠️ Optional: Binary Evaluation (if comparing to real recessions)

If you want to measure how well your score **flags true recessions**, convert it to binary:

```python
y_pred_binary = (y_pred > 0.6).astype(int)
```

Then calculate:
- **Precision / Recall / F1**
- **ROC AUC**
- Compare lead time to real NBER-defined downturns

📌 This step helps justify the model to non-technical stakeholders.

---

## 📍 8. Evaluation Strategy  

### 📉 If You Use a Proxy Risk Target  

| Metric | Use |
|--------|-----|
| **RMSE, MAE** | How close the model’s predicted score is to the proxy |
| **MAPE** | % error in predicting risk level |
| **R²** | Explanatory power |

### ⏳ Time-Sensitive Evaluation  

| Method | Insight |
|--------|--------|
| **Lead Time Curve** | Plot how early model detects rising risk before true recession |
| **Recession Overlay** | Align NBER dates and predicted risk curve |
| **SHAP by Time** | Show which indicators raise risk over time |
| **Prediction Volatility** | Smooth transitions preferred over jumpy forecasts |

📌 Bonus: Create a **Lead Time Comparison Table** for past recessions, showing how early your model flagged elevated risk levels.

---

## 📍 9. Output & Interpretation  

| Quarter | Forecasted Recession Risk |
|---------|----------------------------|
| 2023 Q3 | 12.4% |
| 2023 Q4 | 29.1% |
| 2024 Q1 | **58.7%** |
| 2024 Q2 | 61.3% |

Use threshold bands:  
- 0–25% = Low Risk  
- 25–50% = Moderate  
- 50–75% = High Risk  
- 75–100% = Imminent Danger  

📌 When presenting outputs, overlay prior recession periods and compare historical vs predicted risk scores.

---

## 📍 10. Final Deliverables Structure  

```bash
project/
├── data/
│   ├── *.csv (all indicators)
├── notebooks/
│   ├── eda.ipynb
│   ├── proxy_score_engineering.ipynb
│   ├── feature_engineering.ipynb
│   ├── regression_modeling.ipynb
│   ├── unsupervised_detection.ipynb
│   ├── evaluation.ipynb
│   └── retro_recession_analysis.ipynb  # ← NEW 📌
├── scripts/
│   ├── pipeline.py
│   ├── proxy_builder.py
│   ├── forecasting_window.py
│   └── shap_utils.py
├── presentation/
│   └── Recession_Risk_Dashboard_Deck.pdf
```

---

## 📊 Optional Dashboard Features (Streamlit)

- 📈 Line chart: Predicted risk score over time  
- 🎯 Risk Gauge: Current quarter’s recession risk  
- 🔍 SHAP Summary: Top risk-driving signals this quarter  
- ⏱️ Lead time tracker  
- 🕰️ Retro mode: “What the model would’ve said in 2007, 2020…”

---

## ✅ Outcome  

- Forecasts **recession risk as a probability-like signal**  
- Uses **macro patterns** without hard labels  
- Explains **why** risk is rising (via SHAP)  
- Incorporates **historical context** for trust and pattern-matching  
- Ready for dashboards, APIs, and macro alert systems  

---
