## 📈 Slide 1: ARMIS  
### *Automated Regime Modeling via Interpretable Signals*  
> **Forecasting the Next Economic Regime — One Quarter at a Time**  
**Author**: Mak Trnka  
**Date**: April 2025

---

## 📊 Slide 2: Overview

**ARMIS Presentation Roadmap**  
2. Business Problem  
3. Who Benefits from the Model  
4. Data Preparation & Preprocessing  
5. Modeling Approaches (Pre-Forecast)  
6. Forecasting + Deployment Architecture  
7. SHAP Interpretability  
8. Sample Output from the Model  
9. Evaluation & Validation  
10. Business Recommendations  
11. Next Steps  
12. Q&A

---


## 🧠 Slide 3: Business Problem

> “What economic regime is the U.S. heading into — and why?”

- Binary recession/no-recession models lack nuance.  
- Probabilistic outputs (e.g., "72% chance of recession") often confuse more than clarify.  
- ARMIS classifies the economy into **four actionable regimes**.  
- It **explains** what variables are driving these shifts.

---

## 👥 Slide 4: Who Benefits from This Model?

| Stakeholder         | Use Case                                  |
|---------------------|--------------------------------------------|
| 💼 Executives       | Strategic planning & cost allocation       |
| 📈 Fund Managers    | Adjusting portfolios based on regime       |
| 🧠 Economists       | Scenario modeling & explanation            |
| 📱 Fintech Teams     | Regime-based overlays in user apps         |
| 🧮 Data Engineers    | Embedding regime logic into pipelines      |
| 📰 Media/Think Tanks | Data-supported narratives                  |

---

## 🧹 Slide 5: Data Preparation & Preprocessing

| Step        | Description                                                              |
|-------------|--------------------------------------------------------------------------|
| Sources     | OECD, FRED, IMF, St. Louis Fed                                           |
| Indicators  | 30+ macro signals: CPI, VIX, Jobs, Durable Goods, Fed Funds, M2, etc.   |
| Enrichment  | Lags (1-4Q), **rolling mean/std**, % change, engineered signals         |
| Final Set   | ~250 features per quarter (1970–2025), categorized by indicator timing  |

📌 Features are organized by **leading, lagging, and coincident** categories.  
📌 Applied rolling statistics (mean, std) over 4-quarter windows to smooth volatility and capture trend dynamics.

---

## 🧰 Slide 6: Modeling Approaches (Pre-Forecast)

| Model               | Strengths                     |
|---------------------|-------------------------------|
| XGBoost/LightGBM    | Accuracy + SHAP compatibility |
| Random Forest       | Strong baseline               |
| Logistic Regression | Interpretable benchmark       |
| LSTM / TCN (optional)| Sequence-aware experimentation|

- Format: **4Q lagged data → predict next quarter’s regime**.  
- Labels based on rules for GDP, unemployment, capacity utilization.  
- Metrics include accuracy, F1, **Transition-F1**, and confusion matrix.  
- Used a **sliding window framework**:  
  - Train model using lagged inputs from quarters *t-4 to t-1*  
  - Predict regime for quarter *t*  
  - Slide window forward one step for next training instance

```plaintext
[Q1, Q2, Q3, Q4] → Predict Q5
[Q2, Q3, Q4, Q5] → Predict Q6
```

---

## 🔮 Slide 7: Forecasting + Deployment Architecture

> Forecasting macro indicators enables **real-time regime prediction**

```plaintext
[Historical Macros]
      ↓
   [ARIMA Forecast]
      ↓
[Enriched Indicators]
      ↓
[Trained Classifier]
      ↓
[SHAP Explanations]
```

- ARIMA projects next-quarter macro inputs.  
- Classifier assigns a regime based on those inputs.  
- SHAP interprets the model’s decision.

---

## 🔍 Slide 8: SHAP Interpretability

| Type         | What It Explains                            |
|--------------|----------------------------------------------|
| Global SHAP  | Key features for each regime type            |
| Local SHAP   | Feature importance for one prediction (e.g., Q4 2025) |

📌 SHAP values are calculated post-classification using predicted or actual inputs.

**Suggested Visuals:**  
- Global SHAP bar chart  
- Local SHAP force plot

---

## 📤 Slide 9: Sample Output from the Model

| Quarter   | Regime       | Top Drivers (Local SHAP)       |
|-----------|--------------|---------------------------------|
| 2025 Q2   | Stability     | GDP Growth, Credit Conditions  |
| 2025 Q3   | Slowdown      | Jobless Claims, Oil Prices     |
| 2025 Q4   | Recession     | Durable Goods ↓, M2 ↓          |
| 2026 Q1   | Recession     | CPI ↑, Jobless Claims ↑        |

✅ Forecasts use **ARIMA-projected inputs**  
✅ Explanations use **Local SHAP analysis**

---

## 🧪 Slide 10: Evaluation & Validation

| Metric             | Insight                                |
|--------------------|----------------------------------------|
| Accuracy / F1      | Regime classification performance      |
| Confusion Matrix   | Type-specific errors                   |
| Transition Matrix  | Predicting regime shifts               |
| SHAP Timeline      | Drivers behind transitions             |
| Lead Time Curve    | Early detection of upcoming changes    |

✅ Successfully aligns with past recessions: 2001, 2008, 2020

---

## 💼 Slide 11: Business Recommendations

1. Embed ARMIS into executive dashboards.  
2. Use predicted regimes to trigger **scenario planning**.  
3. Establish alerts for rising recession probabilities.  
4. Present SHAP-based drivers in internal strategy decks.  
5. Run "what-if" simulations with hypothetical macro shocks.

> Forecasts the **next economic state** — and explains **why**.

---

## 🚀 Slide 12: Next Steps

| Stage     | Action                                                |
|-----------|--------------------------------------------------------|
| Now       | Use ARIMA for real-time macro forecasting             |
| Next      | Evaluate Seq2Seq, Prophet, Transformer alternatives   |
| Later     | Extend ARMIS to domains: labor, housing, sectors      |
| Ongoing   | Develop dashboard/API for live regime updates         |

> Expand to **multi-step horizons** and broader economic modeling.

---

## ❓ Slide 13: Q&A

> “The future isn’t binary — it’s a regime.
ARMIS helps forecast it, explain it, and prepare for it.”

📍 [Suggested final image: compass, radar, or economic dashboard metaphor]

