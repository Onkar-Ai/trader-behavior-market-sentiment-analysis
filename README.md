**Trader Performance vs Market Sentiment Analysis**

## 📌 Objective
This project analyzes how Bitcoin market sentiment (Fear/Greed) influences trader behavior and profitability on the Hyperliquid platform, concluding with actionable business rules and a predictive machine learning model.

## 🛠 Methodology & Data Preparation
1. **Data Cleaning & Alignment:** - Standardized column names and formats across both datasets.
   - Converted the raw Hyperliquid `Timestamp` (milliseconds) into daily datetime objects.
   - Merged tick-level trade data with daily Bitcoin sentiment data using a left join to preserve all trade executions.
2. **Feature Engineering:**
   - Aggregated data to create daily trader profiles containing: `daily_pnl`, `win_rate`, `avg_trade_size_usd`, `trade_count`, and `long_ratio`.
3. **Segmentation:**
   - Classified traders into archetypes: **Frequent vs. Infrequent** (based on median trade count) and **Consistent Winners vs. Inconsistent** (based on historical >50% win rates).

## 📊 Key Insights
1. **Sentiment Impact on Performance:** Market sentiment alone does not dictate average daily PnL, but it heavily influences *how* specific trader segments size their positions.
2. **The "Stubborn Long" Bias:** Inconsistent traders maintain a disproportionately high long-ratio during "Fear" days, leading to outsized drawdowns compared to Consistent Winners who dynamically adjust their bias.
3. **Drivers of Profitability (ML Insight):** A Random Forest model analyzing next-day profitability revealed that a trader's fundamental behavior (`trade_count` and `avg_trade_size_usd`) accounts for nearly 60% of predictive importance, far outweighing the raw market sentiment index.

## 💡 Actionable Output (Business Rules)
* **Strategy Idea 1 (Risk Management):** Implement an automated risk-management flag. When the Bitcoin sentiment index drops to "Fear," dynamically reduce the maximum allowed leverage or position size for accounts historically classified in the "Inconsistent" segment to prevent catastrophic liquidations.
* **Strategy Idea 2 (Signal Generation):** Build a "Smart Money" momentum signal. When the market is in "Greed," heavily weight copy-trading signals from the "Consistent Winner" segment only when they execute larger-than-average, low-frequency trades, filtering out retail noise.

## 🚀 Setup & Reproducibility
To run this notebook locally:
1. Clone this repository.
2. Ensure you have the datasets (`bitcoin_sentiment.csv` and `hyperliquid_trader_data.csv`) in the root directory.
3. Install dependencies: `pip install pandas numpy matplotlib seaborn scikit-learn`
4. Run all cells in `intern_assignment.ipynb`.
