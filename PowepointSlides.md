

---

### 📈 Slide 1: Title Slide  
## *Forecasting the Next Economic Regime — One Quarter at a Time*  
**Mak Trnka – Data Scientist**  
**Capstone Project | April 2025**

> “The economy doesn’t just grow or shrink — it shifts.”

---

### 📊 Slide 2: Key Takeaways (Overview Up Front ✅)

🔍 **What We Did:**  
- Forecast macro indicators like GDP, jobs, and inflation  
- Predicted upcoming **economic regime** (e.g. Recession, Boom)  
- Explained what drove those shifts

✅ **Why It Matters:**  
- CFOs & hedge funds can plan before markets react  
- SHAP plots explain the *why* behind regime predictions  
- 82% accuracy predicting past regime changes, 1–2 quarters early

---

### 💡 Slide 3: What is an “Economic Regime”? (Clear & Non-Technical ✅)

> A “regime” is the *state of the economy*. We forecast which one’s next.

| Regime       | What It Means                        | Strategic Implication         |
|--------------|---------------------------------------|-------------------------------|
| 💥 Boom       | Strong growth, low unemployment       | Expand, hire, invest          |
| 📊 Stability  | Steady indicators, mild growth        | Stay the course               |
| ⚠️ Slowdown   | Job & growth signals weakening        | Reduce risk, hedge            |
| 📉 Recession  | Broad contraction, falling demand     | Conserve, reallocate          |

---

### 🧠 Slide 4: The Problem This Solves

Financial leaders like CFOs, hedge fund managers, and central banks need clear, forward-looking signals to guide budgeting, hiring, monentary decisions, and investment.

Traditional economic forecasts are vague and binary — offering little detail on what’s coming next, and too late to act on.

Our goal is to build a hybrid time series model that forecasts key macroeconomic indicators and classifies upcoming quarters into clear, interpretable economic regimes — helping leaders make decisions before the shift.


🎯 **We predict not just what changes — but when, how, and why**

---

### ⚙️ Slide 5: How We Did It — In 3 Steps

**Forecast → Predict → Explain**

1. Forecast key indicators 1 quarter ahead  
2. Predict regime using **XGBoost Classifier**  
3. Use **SHAP** to explain drivers of regime

📦 Data: 30+ macro indicators from FRED, BLS (1970–2024)  
🧪 Training: 200+ quarters of historical regime patterns  

---

### 🔮 Slide 6: Results — What’s Coming Next

📅 **Predicted Regimes: 2025 Outlook**

| Quarter  | Regime       | Top Drivers                  |
|----------|--------------|------------------------------|
| Q2 2025  | ⚠️ Slowdown   | Job softness, credit tightening  
| Q3 2025  | ⚠️ Slowdown   | Retail pullback, higher inventories  
| Q4 2025  | 📉 Recession  | GDP drop, rising unemployment  

🧠 *Visual: Add SHAP summary + forecast line charts here*

---

### 🧪 Slide 7: Model Choice — Why We Used XGBoost

✅ Best performing model on classification task
✅ Handles mixed, nonlinear macro signals
✅ Pairs with SHAP for full transparency
✅ Tested with sliding windows for time-aware validation

| Metric          | Value    |
|-----------------|----------|
| Accuracy        | ~82%     |
| F1 (Recession)  | ~0.72    |
| Validation      | Sliding-window CV |

📊 *Visual: Add Confusion Matrix & Transition Matrix*

---

### 🛠️ Slide 8: How We Built the Model (Condensed)

**Features:**  
- Lagged indicators (1–4 quarters)  
- Rolling means, std devs, % change  
- Custom features: Fiscal Stress, Inflation Gap  

**Modeling Steps:**  
- Cleaned & aligned 30+ indicators  
- Balanced classes with SMOTE  
- Forecasted inputs via VAR/XGBoost/Prophet
- Trained classifier on lagged patterns

---

### 📈 Slide 9: Evaluation Highlights

| Method           | Insight                            |
|------------------|-------------------------------------|
| SHAP Timeline    | Top feature shifts over time        |
| Confusion Matrix | Which regimes got misclassified     |
| Transition Matrix| Accuracy around regime changes      |
| Lead Time Curve  | How early we spot downturns         |

📌 *Caught early signals before 2008 & 2020 downturns*

---

### 📌 Slide 10: Key Recommendations

💼 **For CFOs**: Adjust budgets and hiring based on forecast regime  
📈 **For Hedge Funds**: Rebalance portfolios *before* regime switch  
🏛 **For Central Banks**: Use early signals to guide monetary response  

📊 *Show how SHAP + probability scores offer transparent guidance*

---

### 🚀 Slide 11: What’s Next

| Phase      | Action                                             |
|------------|----------------------------------------------------|
| Now        | Finalize outputs and GitHub documentation          |
| Near-Term  | Deploy dashboard / API for internal testing        |
| Long-Term  | Add LSTM + ensemble models for multi-quarter views |

---

### ❓ Slide 12: Q&A / Closing

> “The economy evolves in patterns — not surprises.  
We forecast its **next move**, explain the **why**, and help you act with **clarity.**”

---



NOTES:

Absolutely — here's a **detailed Notes section for each slide** to guide your live presentation. Each note is written for a non-technical audience, helping you stay conversational, clear, and focused on value.

---

### 📈 Slide 1: Title Slide  
**Speaker Notes:**  
> “Hi everyone, my name is Mak Trnka. Today, I’m presenting a model I built to help leaders get ahead of the economy — not behind it.  
Instead of just predicting if the economy goes up or down, this model forecasts what *phase* we’re entering — and more importantly, *why*.”

---

### 📊 Slide 2: Key Takeaways  
**Speaker Notes:**  
> “Let me give you the bottom line up front.  
We forecasted macroeconomic indicators like GDP and unemployment one quarter ahead, then predicted what *state* the economy was entering — like a Recession or Boom.  
We also used a tool called SHAP to explain *why* those forecasts happened — in plain English.  
This gives leaders time to prepare before markets or headlines catch up.”

---

### 💡 Slide 3: What is an “Economic Regime”?  
**Speaker Notes:**  
> “You’ll hear me use the word *regime* — all that means is the state or phase of the economy.  
Are we in a boom? Are we stable? Are we slowing down? Or headed into recession?  
Each regime has a different strategy. So knowing what’s coming helps CFOs and investors act early — not react late.”

---

### 🧠 Slide 4: The Problem This Solves  
**Speaker Notes:**  
> “Here’s the real challenge: Most forecasts are too generic. They just say ‘GDP might fall’ or ‘inflation is cooling.’  
But leaders need clarity — they want to know *what’s next* and *how to prepare*.  
This model doesn’t just forecast numbers — it translates them into economic phases, so teams can align strategy and timing.”

---

### ⚙️ Slide 5: How We Did It — In 3 Steps  
**Speaker Notes:**  
> “We broke it down into three steps:  
1) First, we forecast the key signals — like jobs and output — a quarter ahead.  
2) Then we use a machine learning model, XGBoost, to classify what regime is coming.  
3) And finally, we use a method called SHAP to explain which indicators pushed the model toward that result — so we’re not left with a black box.”

---

### 🔮 Slide 6: Results — What’s Coming Next  
**Speaker Notes:**  
> “Here’s what we found. In Q2 and Q3 of 2025, the economy is likely to slow down — based on signs like weaker job growth and tighter credit.  
By Q4, we’re likely entering a Recession.  
This matches historical patterns — and the model highlights exactly which signals triggered the shift.”

---

### 🧪 Slide 7: Model Choice — Why We Used XGBoost  
**Speaker Notes:**  
> “I tried multiple models, but XGBoost performed best — especially in complex conditions where signals don’t behave in linear ways.  
It was accurate and, importantly, it works well with SHAP — which gives us transparency into what’s driving the prediction.  
This is how we make the model not just *accurate*, but *trustworthy*.”

---

### 🛠️ Slide 8: How We Built the Model  
**Speaker Notes:**  
> “We used 30+ indicators — like GDP, jobs, credit, and inflation — and created lag features to learn how changes unfold over time.  
We also built custom features to capture stress, like the gap between inflation measures or fiscal pressure.  
We forecasted inputs using time series models like VAR, and then trained the classifier on those lagged patterns.”

---

### 📈 Slide 9: Evaluation Highlights  
**Speaker Notes:**  
> “We didn’t just check if the model got the final label right.  
We also checked:  
- How early did it catch regime shifts?  
- Which regimes got confused?  
- Which signals shifted before a downturn?  
This kind of evaluation tells us if the model gives *useful lead time*, not just rear-view accuracy.”

---

### 📌 Slide 10: Key Recommendations  
**Speaker Notes:**  
> “This model isn’t just academic — it’s actionable.  
If you’re a CFO, you can adjust hiring or spending early.  
Hedge funds can hedge risk *before* volatility hits.  
Central banks and fintech firms can use these shifts to make smarter alerts, dashboards, or decisions.  
The key is that the predictions are interpretable — we don’t just say ‘Recession is coming’ — we show what’s causing it.”

---

### 🚀 Slide 11: What’s Next  
**Speaker Notes:**  
> “Going forward, I plan to finalize the codebase and results, then build this into a usable dashboard.  
In the future, we can expand to deep learning models — like LSTMs — to look further out across multiple quarters.  
And ideally, this becomes a real-world forecasting tool with alert systems and updates.”

---

### ❓ Slide 12: Q&A / Closing  
**Speaker Notes:**  
> “So to wrap up:  
The economy doesn’t shift overnight — it evolves.  
This model helps us see what direction we’re heading in, explain why, and prepare ahead.  
Thanks so much — I’m happy to take any questions.”

---

Let me know if you’d like this as a printable speaker handout or in PowerPoint export format — I can also generate visuals (like SHAP or flow diagrams) to drop into the slides.