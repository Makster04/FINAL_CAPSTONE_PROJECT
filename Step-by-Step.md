
# ✅ Capstone Roadmap: ARMIS  
**Automated Regime Modeling via Interpretable Signals**  
*Forecasting the next quarter’s macroeconomic regime using time-lagged indicators*

---

## 📍 1. Problem Statement & Objective  

### 🎯 Goal  
Predict the **upcoming quarter’s economic regime** — one of {**Boom, Stability, Slowdown, Recession**} — based on the prior 4 quarters of macroeconomic signals.

### 🔑 Motivation  
Binary recession forecasting is often too coarse. ARMIS produces **discrete, interpretable regime labels** that reflect the nuanced stages of the economic cycle, offering stakeholders a clearer decision framework.

---

## 📍 2. Data Collection  

### 📦 Core Indicator Themes & Timing  

| Theme               | Indicator                                      | Timing     |
|---------------------|------------------------------------------------|------------|
| **Confidence**       | Consumer Confidence                            | Leading    |
|                     | Business Confidence                            | Leading    |
| **Labor Market**     | Total Jobs                                     | Coincident |
|                     | Unemployment Rate                              | Lagging    |
|                     | Labor Force Participation                      | Coincident |
| **Inflation**        | Consumer Price Index (CPI)                     | Lagging    |
|                     | Producer Price Index (PPI)                     | Leading    |
|                     | Crude Oil Prices                                | Leading    |
| **Interest Rates**   | Fed Funds Rate                                 | Lagging    |
|                     | Baa-Aaa Treasury Constant Maturity Rate        | Mixed      |
| **Real Economy**     | Housing Starts                                 | Leading    |
|                     | Durable Goods Orders                           | Leading    |
|                     | Capacity Utilization                           | Coincident |
| **Production**       | Industrial Production                          | Coincident |
| **Fiscal & Credit**  | Deficit as % of GDP                            | Lagging    |
|                     | Baa-Aaa Corporate Bond Yield                   | Lagging    |
|                     | Credit Conditions Subindex                      | Lagging    |
| **Liquidity**        | Real M2 Stocks                                 | Lagging    |
| **Sales/Inventory**  | Business Inventories                           | Lagging    |
|                     | Retail Sales                                   | Coincident |
| **Volatility**       | VIX (Volatility Index)                         | Leading    |


📌 *Timing tags help structure lags and validate regime transitions.*

---

## 📍 3. Regime Definition & Labeling  

ARMIS uses a **rule-based labeling scheme** to classify historical quarters into one of four regimes:

| Regime     | Characteristics |
|------------|-----------------|
| **Boom**     | High GDP (>3%), low/falling unemployment, strong production |
| **Stability**| Steady GDP (1–3%), stable labor & inflation |
| **Slowdown** | Sub-1% GDP, weakening labor, soft demand |
| **Recession**| Negative GDP (2+ quarters), high/falling capacity, job losses |

📌 Labels are assigned using thresholds on GDP, unemployment, and capacity utilization — not just NBER retrospectives.

---

## 📍 4. Historical Pattern Analysis (Retro Lens) 🔍  

- Build **pre-regime-transition snapshots** (1974-75, 1980, 1981-82, 1991, 2001, 2008, 2020)  
- Identify which indicators **change earliest** before downturns or recoveries  
- Use pattern recognition to validate labeling and feature design

✅ Ensures model is grounded in historical economic transitions.

---

## 📍 5. Data Preparation & EDA  

- Convert all indicators to **quarterly format**  
- Apply **z-score normalization**  
- Analyze regime-specific trends over time  
- Run **PCA or TSNE** to explore regime separability  
- Visualize regime boundaries via scatter plots or clusters

---

## 📍 6. Feature Engineering  

### 🔁 Temporal Features  
- Create 1–4 quarter lags per indicator  
- Add rolling stats (mean, % change, std dev)

### ⚙️ Derived Metrics  

| Feature | Formula |
|--------|---------|
| **Fiscal Stress Index** | Deficit % GDP × Interest Rate |
| **Inflation Gap** | PPI – CPI |
| **Jobs Momentum** | ΔJobs / ΔUnemployment |
| **Inventory Ratio** | Inventories ÷ Retail Sales |
| **Volatility Shock** | QoQ % Change in VIX |
| **Liquidity Shock** | ΔReal M2 QoQ |

📌 Each feature’s behavior is validated across regime transitions.

---

## 📍 7. Modeling Approaches  

### 🧰 Classification Models  

| Model | Strength |
|-------|----------|
| **XGBoostClassifier / LightGBM** | Accuracy + SHAP explainability |
| **Random Forest** | Robust baseline |
| **Logistic Regression (Softmax)** | Interpretable benchmark |
| **LSTM / TCN (Optional)** | Sequence-aware (for experimentation) |

📌 Focus on models with **`predict_proba`** and **SHAP support**.

---

## 📍 8. Forecasting Logic  

- Input = 4-quarter lagged macro indicators  
- Output = 1 of 4 regime classes for the next quarter  
- Use **sliding windows** for training (time-aware structure)  
- Predict one quarter ahead, optionally evaluate 2Q/3Q ahead

---

## 📍 9. Train-Test Strategy & Validation  

### ⏱️ Chronological Split  
- Example: Train on 1970–2010, Test on 2011–2024  
- Avoids data leakage and respects time sequence

### 📐 Evaluation Metrics  

| Metric | Use |
|--------|-----|
| **Accuracy** | Overall match rate |
| **F1 (per class)** | Balanced regime detection |
| **Precision/Recall** | Especially for Recession class |
| **Confusion Matrix** | Understand misclassification behavior |

📌 Use **Transition-F1** to evaluate detection of regime changes.

---

## 📍 10. Output Interpretation  

| Quarter | Predicted Regime | Class Probabilities |
|---------|------------------|---------------------|
| Q1 2024 | Stability         | [Boom: 5%, Stability: 64%, Slowdown: 24%, Recession: 7%] |
| Q2 2024 | Slowdown          | [Boom: 2%, Stability: 35%, Slowdown: 45%, Recession: 18%] |
| Q3 2024 | Recession         | [Boom: 0%, Stability: 10%, Slowdown: 28%, **Recession: 62%**] |

📌 Smooth class probability distributions help justify model confidence.

---

## 📍 11. SHAP-Based Explainability  

- Use **Global SHAP** to rank top features for each regime  
- Use **Local SHAP** to explain why it ended up STABLE  predicttion in Q3 2024  
- Visualize feature attribution over time (SHAP timelines)

---

## 📍 12. Evaluation Strategy  

| Method | Insight |
|--------|--------|
| Lead Time Curve | How early regime transitions are predicted |
| SHAP Timeline | Show which features drove changes across time |
| Transition Matrix | Accuracy around switches (e.g. Slowdown → Recession) |
| Confusion Matrix | Identify which regimes get misclassified |

📌 Include **transition-focused visualizations** to highlight early warning success.

---

---

## 📊 Optional Dashboard Add-ons  

- Regime Forecast Gauge  
- Regime Probability Chart  
- SHAP Feature Attribution View  
- “What if?” mode (e.g. simulate shock to jobs or rates)

---

## ✅ Final Deliverables  

- 🔍 Time-aware economic regime classification system  
- 📈 Validated on decades of macro data  
- 🧠 Interpretable and explainable via SHAP  
- 📊 Dashboard- and API-ready for real-time integration  
- 🧩 Expandable to global or sectoral forecasts

---

Let me know if you'd like this turned into a PDF, slide deck, or project notebook structure — happy to generate the next format for you!