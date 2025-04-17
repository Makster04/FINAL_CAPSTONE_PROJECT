Here’s a simplified, non-technical version of your slides that keeps your core message while making the language more audience-friendly — especially for business folks like CFOs, hedge fund managers, and central bank staff:

---

### 📈 Slide 1: Title Slide  
## *Forecasting the Next Economic Regime — One Quarter at a Time*  
**Mak Trnka – Data Scientist**  
**Capstone Project | April 2025**  

> “The economy doesn’t just grow or shrink — it shifts.”

---

### 📊 Slide 2: Key Takeaways (Simple Overview)

🔍 **What This Project Did:**  
- Looked ahead at things like GDP, jobs, and inflation  
- Predicted where the economy is headed next — boom or bust?  
- Explained *why* those changes are coming

✅ **Why It Matters:**  
- Helps business and finance leaders prepare early  
- Clear reasons behind each prediction  
- 82% accurate in spotting past changes — before they happened

---

### 💡 Slide 3: What Is an “Economic Regime”?

> Think of it like the *mood* of the economy. We predict what mood comes next.

| Regime       | What’s Happening                | What Leaders Might Do         |
|--------------|----------------------------------|-------------------------------|
| 💥 Boom       | Strong growth, lots of jobs      | Hire, expand, invest          |
| 📊 Stability  | Calm growth, steady signals      | Stay the course               |
| ⚠️ Slowdown   | Economy starting to weaken       | Be cautious, manage risk      |
| 📉 Recession  | Economy shrinking, demand falling| Cut costs, hold back          |

---

### 🧠 Slide 4: Why This Matters

People in charge — CFOs, investors, central banks — need early signs of change to make smart choices.

But most forecasts today are unclear or come too late.

We built a smart system that watches economic signals, spots patterns, and tells you which *type* of economy is coming — and *why* — so you can prepare.

🎯 **Not just “what” changes — but “when,” “how,” and “why.”**

---

### ⚙️ Slide 5: The Big Idea — In 3 Steps

We kept it simple:

1. **Look ahead** at key signals like GDP and unemployment  
2. **Predict** what economic mood is next  
3. **Explain** what caused the shift

📦 We used trusted data from FRED and BLS (1970–2024)  
🧪 Trained on over 50 years of history

---

### 🔮 Slide 6: What We See Coming

📅 **2025 Predictions**

| Quarter  | Regime       | Why It Might Happen             |
|----------|--------------|---------------------------------|
| Q2 2025  | ⚠️ Slowdown   | Fewer job openings, tighter credit  
| Q3 2025  | ⚠️ Slowdown   | Slower retail sales, more unsold goods  
| Q4 2025  | 📉 Recession  | Falling GDP, higher unemployment  

🧠 *Let’s show a few simple charts of these shifts + what drove them*

---

### 🧪 Slide 7: Why This Model?

We used **XGBoost**, because:

✅ It worked best in tests  
✅ It understands messy, real-world data  
✅ It works well with SHAP, which helps us explain the “why”

| Score Type        | Value  |
|-------------------|--------|
| Overall Accuracy  | ~82%   |
| Recession Score   | ~72% F1  
| Evaluation Method | Repeated quarter-by-quarter testing  

📊 *We’ll also show a chart of which predictions were right or wrong*

---

### 🛠️ Slide 8: How We Built It (Simple Version)

**What We Used:**  
- Lagged data (looking back a few quarters)  
- Stats like rolling averages and changes over time  
- Special indicators like stress on households or inflation pressure  

**Steps We Took:**  
- Cleaned and prepped 30+ indicators  
- Fixed data imbalance with smart sampling  
- Forecasted indicators using proven tools  
- Trained the model to recognize patterns

---

### 📈 Slide 9: How We Checked If It Works

| What We Checked     | What It Told Us                   |
|---------------------|-----------------------------------|
| SHAP Timeline       | What indicators mattered most and when  
| Confusion Matrix    | Which predictions were wrong  
| Transition Matrix   | How often regime switches were caught  
| Lead Time Curve     | How early we spotted the shift  

📌 *Caught warning signs before the 2008 and 2020 downturns*

---

### 📌 Slide 10: Who This Helps

💼 **CFOs & Executives**: Adjust budgets, hiring, and investments early  
📈 **Hedge Fund Managers**: Rebalance portfolios *before* markets move  
🏛 **Central Banks**: Guide interest rate policy using early signals  
📱 **Fintech Teams**: Add economic alerts into user apps  

📊 *Clear visuals show confidence levels + reasons behind each prediction*

---

### 🚀 Slide 11: What’s Next?

| Timeframe   | What We’re Doing                          |
|-------------|--------------------------------------------|
| Right Now   | Finalizing code, charts, and documentation  
| Coming Soon | Launching a test dashboard or app  
| Long Term   | Adding more models to look further ahead  

---

### ❓ Slide 12: Wrap-Up & Q&A

> “The economy moves in cycles, not surprises.  
We built a way to *see what’s next*, understand *why*, and help you *stay ahead.*”

---

Let me know if you want slide notes to go along with these, or visual suggestions to match each!