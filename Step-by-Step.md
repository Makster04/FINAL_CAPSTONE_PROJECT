
# 📊 Project Roadmap: Macroeconomic Regime Forecasting via Hybrid Time Series Modeling

## 🔍 Project Overview
**Objective**: Build a hybrid time series pipeline that forecasts key macroeconomic indicators and predicts the upcoming economic regime (Boom, Stability, Slowdown, Recession) using the datasets: lags.csv, Regime_Lables.csv, and Prediction_Indicators.csv.

---

## ✅ Step 1: Data Collection & Preparation
**Datasets Used**: lags.csv, Prediction_Indicators.csv, Regime_Lables.csv

**Goals**:
- Load macroeconomic data and regime labels
- Merge datasets on observation_date
- Drop duplicate and fully empty columns
- Fill missing values with column-wise mean

**Visuals**:
- Data availability timeline
- Heatmap of missingness before/after filling

---

## 🏗️ Step 2: Feature Engineering
**Datasets Used**: lags.csv, Prediction_Indicators.csv

**Goals**:
- Create lagged features (1 to 4 quarters)
- Add 4-quarter rolling mean, std, and percent change
- Engineer derived features:
  - Fiscal Stress = (Deficit % GDP) × (Interest Rate)
  - Inflation Gap = PPI - CPI
  - Jobs Momentum = Jobs / Unemployment Change
  - Inventory Ratio = Inventories / Retail Sales
  - Macro Stress Flags = binary indicators

**Visuals**:
- Correlation heatmap (original vs derived)
- Rolling stats around regime switches

---

## 🧠 Step 3: Regime Labeling
**Dataset Used**: Prediction_Indicators.csv

**Goals**:
- Use rule-based function to classify quarters
- Labels: Boom, Stability, Slowdown, Recession
- Based on thresholds of GDP, Unemployment, Jobs, Capacity, Production

**Visuals**:
- Bar plot of regime distribution
- GDP vs Unemployment colored by regime

---

## 🔍 Step 4: Historical Pattern Analysis
**Datasets Used**: Prediction_Indicators.csv, regime-labeled output

**Goals**:
- Analyze patterns near regime transitions
- Focus on downturns: 1974–75, 1980, 2008, 2020

**Visuals**:
- Time series overlay for GDP, Unemployment, Production
- Highlighted zones by regime

---

## 📈 Step 5: Forecasting Indicators (Step 8.1)
**Datasets Used**: lags.csv, derived features from Step 2

**Goals**:
- Identify which macro indicators require forecasting
- Choose model by indicator type:
  - **VAR**: Use for jointly forecasting GDP + Unemployment due to co-dependence
  - **Prophet**: Use for seasonal, trend-sensitive indicators like Jobs, Retail Sales
  - **XGBoostRegressor**: Use for all others with nonlinear trends
- Run sliding window forecast for next 4 quarters
- Save predictions as future_forecasts_df

**Visuals**:
- Line plot: Actual vs Forecasted indicator values
- Prophet output: Trend, seasonality, holidays
- Residual/error bands for top indicators forecasted

---

## 🧩 Step 6: Regime Classification on Forecasted Indicators (Step 8.2)
**Input**: future_forecasts_df

**Goals**:
- Use trained regime classifier to predict regimes from forecasted indicators
- Output regime class and probabilities per quarter
- Save to regime_predictions.csv

**Visuals**:
- Stacked bar chart of predicted probabilities
- Forecasted regime timeline (2024–2026)

---

## 🤖 Step 7: Retrospective Regime Classifier
**Datasets Used**: lags.csv, Regime_Lables.csv

**Goals**:
- Train classifier on historical lagged indicators
- Use SMOTE for class balancing
- XGBoostClassifier with sliding window validation

**Visuals**:
- Confusion matrix
- Classification report table
- SHAP feature importance

---

## 📅 Step 8: Forecasting Logic
**Input**: Forecasted macro indicators from Step 5

**Goals**:
- Forecast future quarters iteratively:
  - Step 1: Predict indicators (VAR, Prophet, XGB)
  - Step 2: Feed indicators into classifier
  - Step 3: Predict regime + class probabilities
- Save to master_forecast_table

**Visuals**:
- Regime probability timeline
- Lead Time curve
- Drift chart of top features

---

## 📌 Deliverables
- forecast_pipeline.py: End-to-end pipeline
- forecasted_indicators.csv: All forecasted macro values
- regime_predictions.csv: Regime classification results
- evaluation_metrics.txt: Accuracy & metrics
- SHAP plots and visual explainer assets

---

## 📊 Visualizations Summary
- Regime timeline chart (past + forecasted)
- Macro indicator forecast lines
- SHAP bar + waterfall plots
- Prophet decompositions
- Confusion matrix & classification summary