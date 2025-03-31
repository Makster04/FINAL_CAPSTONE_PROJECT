
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

## 📍 Here’s your updated Capstone Roadmap with the **time-series evaluation metrics fully integrated** into Section 8. Everything is blended naturally into your existing structure:

---

## 📍 8. Model Evaluation

### 📊 Classification Metrics:
- Accuracy, Precision, Recall, F1 per class  
- ROC-AUC (macro + per-class)  
- Confusion Matrix  

### 🕒 Time-Series Evaluation Metrics:

Because this is a **sequential prediction task**, we go beyond traditional classification metrics to capture *when* a prediction is made — not just *what* is predicted.

#### ⏱️ Lead Time Detection
> **Goal**: Measure how early (or late) the model predicts an upcoming regime shift.

- For each true regime transition (e.g., Stability → Recession), calculate:
  - How many quarters ahead (or behind) the model made the correct switch.
- Track **average lead time per regime** (positive = early detection).
- Useful for evaluating early warning capability of the model.

#### 🔄 Regime Transition vs Stability Accuracy
> **Goal**: Check if the model performs better during transitions or in stable periods.

- Define **transition periods** (±1 quarter from regime change).
- Compute:
  - `F1_Transition`: F1 Score during regime shifts
  - `F1_Stable`: F1 Score during non-transition periods
- Helps stakeholders understand reliability at turning points.

#### 📈 Rolling F1 Over Time
> **Goal**: Visualize how model performance evolves quarter-by-quarter.

- Calculate a rolling F1 score over a window (e.g., 8 quarters).
- Reveals drop-offs during recessions or shocks.
- Add this curve to `evaluation.ipynb` and the dashboard.

```python
rolling_f1 = []
window = 8
for i in range(window, len(y_true)):
    score = f1_score(y_true[i-window:i], y_pred[i-window:i], average='macro')
    rolling_f1.append(score)
```

#### 📉 Prediction Volatility (Regime Stability Index)
> **Goal**: Penalize models that switch regimes too frequently.

- Count the number of predicted regime changes per year.
- Compare to the ground truth frequency.
- High volatility may indicate poor generalization or overreaction.

```python
def count_switches(seq):
    return sum(1 for i in range(1, len(seq)) if seq[i] != seq[i-1])
```

#### 📊 Brier Score (Optional)
> Evaluate probabilistic confidence in predictions (e.g., from Softmax or XGBoost).

- Lower Brier score = better calibrated probabilities
- Especially useful for stakeholder confidence in Recession probabilities

```python
from sklearn.metrics import brier_score_loss
brier_score_loss(y_true == 'Recession', model.predict_proba(X)[:, index])
```

---

### 📈 Visuals:
- Timeline: predicted vs true regimes (with overlay)
- SHAP attribution per quarter (feature importance evolution)
- **Lead-time plots** per regime  
- **Rolling F1 curve** (8-quarter window)  
- **Transition vs Stability accuracy table**  
- Prediction volatility comparison (true vs model switches per year)


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