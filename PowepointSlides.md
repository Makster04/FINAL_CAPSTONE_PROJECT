# ARMIS: Automated Regime Modeling via Interpretable Signals

---

## Slide 1: Economic Regime Forecasting with ARMIS
**Subtitle**: Classifying the Future of the Economy — One Quarter at a Time

---

## Slide 2: Why This Model Matters
- Forecasts **macro regime shifts** with clear, interpretable labels
- Turns abstract risk into **discrete planning categories**
- Helps stakeholders act on insights, not just probabilities
- Adds transparency via **SHAP explainability**

---

## Slide 3: The Key Conceptual Shift
| From                                 | To                                           |
|--------------------------------------|----------------------------------------------|
| Continuous risk score (0-1)          | Discrete economic regimes                   |
| "How risky is next quarter?"         | "Boom, Stability, Slowdown, or Recession?"  |
| Regression models                    | Multi-class classifiers                      |
| SHAP over single risk score          | SHAP over regime class distribution          |
| Risk bands (Low, Medium, High)       | Economic regimes (B/S/S/R)                   |

---

## Slide 4: The Core Question
> "Based on the last 4 quarters of macro indicators, what regime will the U.S. enter next?"

**Goal**: Predict one of four states:
- **Boom**
- **Stability**
- **Slowdown**
- **Recession**

---

## Slide 5: Why It’s Marketable
- ✅ **Human-readable output**: Not just probabilities
- 🔍 **SHAP interpretability**: Global and local transparency
- ⏳ **Time-aware inputs**: 4 lagged quarters only
- 🧩 **Scenario ready**: Simulate shocks (e.g., rising unemployment)

---

## Slide 6: Who Benefits from ARMIS?
- **Asset Managers**: Portfolio positioning by regime
- **Economists / CFOs**: Macro planning & budgeting
- **Policymakers**: Timing monetary or fiscal interventions
- **Fintechs / Dashboards**: Real-time macro regime layers

---

## Slide 7: Macro Indicators Used
| Theme               | Indicators (examples)               | Timing     |
|---------------------|-------------------------------------|------------|
| Confidence          | BCI, CCI                            | Leading    |
| Labor Market        | Jobs, Unemployment, Claims         | Lagging–Coincident |
| Inflation           | CPI, PPI, Crude Oil                | Leading    |
| Rates               | Fed Funds, Baa-Aaa Spread          | Lagging/Mixed |
| Real Economy        | Durable Goods, Housing Starts      | Leading    |
| Volatility          | VIX                                | Leading    |
| Liquidity           | Real M2                            | Lagging    |
| Credit              | Deficit %GDP, Credit Conditions    | Lagging    |

---

## Slide 8: Derived Features
| Feature                | Formula                          |
|------------------------|----------------------------------|
| Fiscal Stress Index    | Deficit × Fed Rate               |
| Jobs Momentum          | ΔJobs / ΔUnemployment         |
| Inflation Gap          | PPI - CPI                        |
| Yield Spread           | 10Y Treasury - 2Y Treasury       |
| Volatility Shock       | ΔVIX QoQ                       |
| Inventory Ratio        | Inventories / Retail Sales       |

---

## Slide 9: Regime Definitions
| Regime      | Characteristics                                      |
|-------------|-------------------------------------------------------|
| Boom        | High growth, strong jobs, rising capacity            |
| Stability   | Steady growth, balanced macro signals                |
| Slowdown    | Cooling growth, softening jobs                       |
| Recession   | Falling GDP, rising unemployment                     |

✅ Labels assigned from GDP, unemployment, and CU — not NBER timing

---

## Slide 10: Modeling Strategy
- **Input**: Lagged features (1-4 quarters)
- **Target**: 1 regime class for the **next quarter**
- **Data split**: Chronological (e.g., train: 1970–2010, test: 2011–2024)
- **Models**: Logistic Regression, XGBoost, Random Forest, LSTM (optional)

---

## Slide 11: Forecasting Output
| Quarter   | Predicted Regime | Probabilities                        |
|-----------|------------------|--------------------------------------|
| Q1 2024   | Stability         | Boom: 5%, Stability: 64%, Slowdown: 24%, Recession: 7% |
| Q2 2024   | Slowdown          | Boom: 2%, Stability: 35%, Slowdown: 45%, Recession: 18% |
| Q3 2024   | Recession         | Boom: 0%, Stability: 10%, Slowdown: 28%, **Recession: 62%** |

---

## Slide 12: Evaluation Metrics
- Accuracy / Precision / Recall per class
- F1-score (especially for Recession)
- **Transition sensitivity**: Catching regime shifts
- Confusion matrix + time-aware validation

---

## Slide 13: SHAP-Based Explainability
- **Global SHAP**: Which indicators push toward Recession?
- **Local SHAP**: Why Q3 2024 = Recession?
- Visuals: summary bar plot, force plot, SHAP timeline

---

## Slide 14: Historical Validation
- Compare model regimes to:
  - 2001 recession
  - 2008 GFC
  - 2020 COVID shock

✅ Validates labeling logic & model consistency

---

## Slide 15: Use Cases & Deployment
- Real-time ARMIS API
- Embedded in dashboards or investor decks
- SMS/email alerts for regime transitions
- Scenario analysis: "What if inflation spikes?"

---

## Slide 16: Unique Selling Points
- 🧠 **Discrete regimes** over fuzzy scores
- 🔎 **Interpretable via SHAP**
- ⏱️ **Time-aware forecasting logic**
- 🔁 **Modular & extensible** pipeline

---

## Slide 17: Final Deliverables
- 🧠 Multi-class regime classification model
- 🧪 SHAP explainability for transparency
- 📈 Evaluated across historical shocks
- 📊 Exportable to dashboard, alerts, reports
- 🌍 Expandable to sectors or global economies

