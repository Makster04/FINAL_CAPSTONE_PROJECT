# Macroeconomic Regime Forecasting via Hybrid Time Series Modeling

## Business & Data Understanding

### Business Problem
Financial leaders—such as CFOs, hedge fund managers, and central banks—need clear, forward-looking insights into the economy to guide decisions. Traditional economic forecasts are vague, delayed, and difficult to interpret. Our goal was to create a forecasting pipeline that not only predicts the next economic phase but also explains why it’s happening.

### Primary Stakeholders
- **CFOs & Executives**: Adjust budgets, hiring, and capital planning based on regime predictions
- **Hedge Fund Managers**: Adjust portfolio risk and sector allocations before markets react
- **Central Banks & Policymakers**: Use regime indicators for monetary and fiscal planning
- **Fintech Teams**: Integrate regime tagging into dashboards and alerting systems
- **Economists & Think Tanks**: Use interpretable trends to tell stronger macroeconomic stories

### Objective
Build an interpretable, time-aware model to:
- Forecast key macro indicators like GDP, Jobs, and Inflation one quarter ahead
- Classify the upcoming economic regime: Boom, Stability, Slowdown, Recession
- Use SHAP to provide transparency on what drives each prediction

---

## Data Understanding

### Data Sources
- Federal Reserve Economic Data (FRED)
- Bureau of Labor Statistics (BLS)
- Constructed Datasets:
  - `lags.csv` (lagged indicators)
  - `Prediction_Indicators.csv` (main inputs)
  - `Regime_Labels.csv` (target labels)

### Data Preparation Highlights
- Merged datasets on `observation_date`
- Dropped duplicates and fully null columns
- Filled missing values with column means
- 30+ macro indicators from 1970–2024
- Engineered 25+ features per quarter (lags, rolling stats, stress indicators)
- Tools: `pandas`, `sqlite3`, `sklearn`, `Prophet`, `XGBoost`, `matplotlib`, `shap`

---

## Modeling Pipeline

### Forecasting Models (Step 1)
Used three models depending on indicator type:
- **VAR**: For interconnected variables (e.g. GDP & Unemployment)
- **Prophet**: For seasonal indicators (e.g. Retail Sales, Jobs)
- **XGBoostRegressor**: For volatile or nonlinear indicators (e.g. Credit spreads)

Used **sliding window** forecasting to project 4 quarters ahead.

### Regime Classifier (Step 2)
- Model: `XGBoostClassifier`
- Features: Lagged indicators (1–4 quarters), rolling stats, engineered flags
- SMOTE used for class balance
- Validated using **sliding window cross-validation**

### Interpretability (Step 3)
- Used **SHAP** to understand feature influence for each regime prediction
- Delivered both local (quarter-level) and global (over-time) explanations

---

## Evaluation

### Key Metrics
| Metric             | Value      |
|--------------------|------------|
| Accuracy           | ~82%       |
| F1 Score (Recession)| ~0.72     |
| Lead Time Detected | ~3 Quarters|

### Evaluation Visuals
- **Confusion Matrix**: Stable & Boom well-predicted, some confusion between Recession vs Slowdown
- **Transition Matrix**: Strong performance in predicting correct regime shifts
- **SHAP Timeline**: Showed driver evolution leading into 2008 & 2020 downturns
- **Lead Time Curve**: Detected downturns 2–3 quarters before actual switch

---

## Key Recommendations

| Role         | Recommendation                                    |
|--------------|----------------------------------------------------|
| CFOs         | Adjust budgets and hiring plans early              |
| Hedge Funds  | Rebalance portfolios before regime shifts          |
| Central Banks| Use forecasts to inform monetary policy timelines  |
| Fintech Teams| Build alert systems using forecasted regimes       |
| Economists   | Use SHAP insights for storytelling and reports     |

---

## 🔮 Next Steps

| Phase      | Action                                             |
|------------|----------------------------------------------------|
| **Now**        | Finalize outputs and GitHub documentation          |
| **Near-Term**  | Deploy dashboard / API for internal testing        |
| **Long-Term**  | Add LSTM + ensemble models for multi-quarter views |

Additional Future Ideas:
- Add **counterfactual simulations** to explore "What if" scenarios
- Extend model to simulate policy changes or sector-specific impacts
- Incorporate **real-time data pipelines** for live regime alerts

---

## Project Assets
- `forecast_pipeline.py`: Main logic for forecasting + classification
- `regime_predictions.csv`: Output regime results with probabilities
- `future_forecasts_df.csv`: Forecasted indicators for future quarters
- `shap_outputs/`: Global & local SHAP explanations
- `evaluation_metrics.txt`: Accuracy, F1, confusion, and lead time summaries

---

## Conclusion
This model bridges the gap between economic forecasting and real-world strategy. It empowers decision-makers to take action before downturns arrive — and provides clear reasoning behind every prediction. With strong lead time, interpretability, and extensibility, this pipeline can serve as the foundation for smarter fiscal, monetary, and investment decisions.