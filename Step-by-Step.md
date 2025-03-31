
---

# ✅ Capstone Roadmap: Economic Turn Prediction Model  
*Predict next quarter’s macroeconomic regime: Boom, Stability, Slowdown, or Recession*

---

## 📍 1. Define the Problem & Scope
### 🎯 Goal  
> Predict the next quarter's economic regime using lagged macroeconomic indicators.

### 🔍 Key Idea:
Use **leading** indicators (e.g. sentiment, yield curve) as predictors and **rule-based logic** on lagging indicators (e.g. GDP, unemployment, CU) to define economic regimes — no NBER dependency.

---

## 📍 2. Data Collection
### 🧾 Included Datasets:
| File Name | Type | Use |
|-----------|------|-----|
| `Consumer_Confidence_Index.csv` | Leading | Feature |
| `Business_Confidence_Index.csv` | Leading | Feature |
| `Initial_Claims.csv` | Leading | Feature |
| `Jobs_Added.csv` | Leading | Feature |
| `Housing_Starts.csv` | Leading | Feature |
| `Yield_Curve.csv` | Leading | Feature |
| `Federal_Funds_Rate.csv` | Leading (policy-reactive) | Feature |
| `Global_Supply_Chain_Pressure_Index.xls` | Leading | Feature |
| `Crude_Oil_Prices.csv` | Contextual | Feature |

| `Capacity_Utilization_Index.csv` | Coincident / Leading | Feature + Label Logic |
| `Industrial_Production_Index.csv` | Coincident | Feature |
| `Real_Broad_Dollar_Index.csv` | Coincident | Feature |

| `PPI_Inflation_Rate.csv` | Lagging | Feature |
| `CPI_Inflation_Rate.csv` | Lagging | Feature |
| `Unemployment_Rate.csv` | Lagging | Feature |
| `Labor_Force_Participation.csv` | Lagging | Feature |
| `Real_Gross_Domestic_Product.csv` | Lagging | **Label source** |
| `Deficit_Percent_GDP.csv` | Lagging | Feature (used in derived fiscal stress index) |

---

## 📍 3. Data Understanding & EDA
- Align all indicators to a **quarterly frequency**
- Visualize indicator trends and shock periods (2001, 2008, 2020)
- Group indicators by type (leading, lagging, coincident)
- Analyze **lead-lag behavior** visually: which indicators show early shifts?

**Deliverables:**
- Line charts: indicators over time with **color-coded regime overlays**
- ACF/PACF on momentum indicators
- Breakpoint detection (e.g., major recession pivots)

---

## 📍 4. Label Engineering (Rule-Based Only)
You’ll use a rule-based approach to assign quarterly regime labels.

| Regime | GDP | Unemployment | Capacity Utilization |
|--------|-----|--------------|------------------------|
| **Boom** | >3% | Low & falling | >80% |
| **Stability** | 1–3% | Stable | ~75–80% |
| **Slowdown** | 0–1% | Rising | Falling |
| **Recession** | <0% for 2+ quarters | High | <75% |

📌 **No NBER recession flags used.**  
📌 Optional: Use clustering (e.g. KMeans, HMM) to validate label quality.

---

## 📍 5. Feature Engineering
- Create **1–4 quarter lags** for all inputs  
- Engineer rolling statistics:  
  - Rolling averages, % changes, volatility  
- Build derived features:
  - `Yield Spread` = 10Y – 2Y  
  - `Fiscal Stress Index` = (Deficit % GDP) × (Interest Rate)  
  - `Inflation Gap` = PPI – CPI  
  - `Jobs Momentum` = ∆Jobs_Added / ∆Unemployment  

**Normalize** via z-score scaling for all numeric features

---

## 📍 6. Train-Test Split
- Use a **chronological split** (e.g., Train: 1970–2010 | Test: 2011–2023)
- Simulate forecasting via **sliding windows**:  
  - e.g., past 4 quarters → predict next quarter’s regime
- Prevent leakage from future signals

---

## 📍 7. Modeling
### Model Types:
- **Logistic Regression (Softmax)** — baseline  
- **Random Forest / XGBoost / LightGBM** — high-performance with SHAP  
- **LSTM / Temporal CNN** — optional deep sequence modeling  
- **Prophet/ARIMA** — optional input forecasting

📌 Compare model performance:
- With vs without leading indicators  
- With vs without fiscal/monetary stress proxies  
- Using only interpretable vs sequential architectures

---

## 📍 8. Model Evaluation
### Metrics:
- Accuracy, Precision, Recall, F1 per class  
- ROC-AUC (macro + per-class)  
- Confusion Matrix  
- Time-aware metrics:
  - F1 over time  
  - Timeliness of regime switches (e.g. detect recession early?)

### Visuals:
- Timeline: predicted vs true regimes  
- SHAP attribution per quarter  
- Lead-time plots: how early does model see Slowdowns or Recessions?

---

## 📍 9. Business Impact
### Stakeholder Use Cases:
- **Investors**: Allocate risk based on regime probability  
- **CFOs**: Adjust hiring, CAPEX with macro guidance  
- **Policymakers**: Use early warnings from CU, Confidence, and Jobs  

### Limitations:
- Data latency (some indicators delayed)  
- Regime boundaries can be fuzzy  
- Shocks (e.g. pandemics) may disrupt historic relationships

---

## 📍 10. Final Deliverables Structure
```bash
project-root/
├── README.md ✅
├── .gitignore
├── data/
│   ├── *.csv, *.xls (macroeconomic indicators) ✅
├── notebooks/
│   ├── eda.ipynb
│   ├── labeling.ipynb
│   ├── feature_engineering.ipynb
│   ├── modeling.ipynb ✅
│   ├── evaluation.ipynb ✅
│   └── final_notebook.ipynb ✅
├── scripts/
│   ├── data_pull.py
│   ├── labeling_logic.py ✅
│   └── features.py
├── presentation/
│   └── Economic_Turn_Classification_Presentation.pdf ✅
```

---

## 📍 11. Non-Technical Presentation
Slides include:
- Visual of how model sees turning points before they’re obvious  
- SHAP or bar charts for top regime predictors  
- Timeline: prediction vs actual regime  
- Stakeholder action matrix by regime

---

## 📍 12. Optional Streamlit Dashboard
### Features:
- Select time range & lag window  
- Toggle indicators (Confidence, Jobs, Yield Curve, etc.)  
- Display:
  - Predicted regime + probabilities  
  - SHAP breakdown  
  - Lead-time plot for Recession probability

---

## ✅ Final Outcome:
- 20+ curated indicators as features  
- Rule-based regime labeling  
- Full time-aware ML pipeline  
- Interpretation-ready for business decisions  
- Expandable to global, sectoral, or city-level use

---

Want a sample `labeling_logic.py` to generate regime labels based on your thresholds? Or a SHAP template for visualizing Boom vs Recession drivers?