# 📊 Vendor Performance Analysis Project

## 📌 Overview
This project analyzes **vendor performance** using procurement, sales, and invoice data.  
It covers the full pipeline from **data ingestion → cleaning → exploratory analysis → business insights → statistical testing**.  
The goal is to identify vendor efficiency, profitability, inventory risks, and opportunities for cost optimization.

---

## ⚙️ Project Workflow

### 1. Data Ingestion
- Raw CSV files are ingested into a **SQLite database (`inventory.db`)**.
- Automated ingestion script:
  - Reads files from `data/` folder.
  - Saves each file as a table named after the filename.
  - Logs ingestion progress and timing in `logs/ingestion_db.log`.
### 2.Exploratory Data Analysis (EDA)

- Connected to SQLite DB and explored tables (purchases, purchase_prices, vendor_invoice, sales).
- Created summary tables:
- Purchase Summary
- Sales Summary
- Freight Summary
- Built an aggregated vendor_sales_summary table combining purchase, sales, and freight data.
  
### 3.Data Cleaning & Feature Engineering
- Added new KPIs:
- GrossProfit = TotalSalesDollars - TotalPurchaseDollars
- ProfitMargin = (GrossProfit / TotalSalesDollars) * 100
- StockTurnover = TotalSalesQuantity / TotalPurchaseQuantity
- SalesToPurchaseRatio = TotalSalesDollars / TotalPurchaseDollars
- Cleaned categorical fields (trimmed spaces).
- Filled missing values with 0.
- Saved cleaned data back into DB (**vendor_sales_summary**)
  
### 4.Exploratory Visualizations
- **Distribution plots** for numerical features.
- **Boxplots** for outlier detection.
- **Count plots** for top vendors & brands.
- **Correlation heatmap** to identify relationships among KPIs.

### 5.Business Insights
🔹 Brand Performance
- Identified brands with low sales but high profit margins → candidates for promotion or pricing adjustments.
- Scatterplot with thresholds (low sales, high margin).
🔹 Top Vendors & Brands
- Ranked top 10 vendors and brands by sales performance.
- Bar plots with formatted labels (K/M notation).
🔹 Vendor Purchase Contribution
- Pareto chart showing vendor contribution to total purchase dollars.
- Highlighted dependency risk on top vendors.
🔹 Procurement Dependence
- Donut chart showing share of top 10 vendors vs. others.
🔹 Bulk Purchasing Analysis
- Grouped purchases into Small, Medium, Large.
- Boxplot showed impact of bulk orders on unit purchase price.
🔹 Inventory Turnover
- Identified vendors with StockTurnover < 1 → slow-moving inventory and excess stock.
🔹 Capital Locked in Unsold Inventory
- Calculated unsold inventory value:
df["UnsoldInventoryValue"] = (df["TotalPurchaseQuantity"] - df["TotalSalesQuantity"]) * df["PurchasePrice"]
- Ranked vendors by capital locked in unsold stock.

6. Statistical Analysis
📈 Confidence Intervals
- Computed 95% confidence intervals for profit margins:
- Top-performing vendors (top 25% sales).
- Low-performing vendors (bottom 25% sales).
- Visualized distributions with CI bounds.
📉 Hypothesis Testing
- Two-sample t-test compared profit margins of top vs. low vendors.
- Result:
- If p < 0.05 → significant difference in margins.
- Else → no significant difference.

📊 Key Findings
- High-margin but low-sales brands → promotional opportunities.
- Top vendors dominate procurement → dependency risk.
- Bulk purchasing reduces unit price → cost optimization strategy.
- Slow-moving inventory vendors → excess capital locked in stock.
- Profit margins differ significantly between top and low-performing vendors (validated via t-test).

🛠️ Tech Stack
- Python (Pandas, NumPy, Matplotlib, Seaborn, SciPy, SQLAlchemy)
- SQLite for database management
- Logging for ingestion tracking
- Statistical Analysis (confidence intervals, t-tests)

🚀 Next Steps
- Extend analysis with predictive modeling (sales forecasting, vendor risk scoring).
- Automate reporting for procurement and finance teams.

📂 Repository Structure
├── data/                  # Raw CSV files
├── logs/                  # Ingestion logs
├── inventory.db           # SQLite database
├── vendor_sales_summary.csv  # Cleaned dataset
├── ingestion.py           # Data ingestion script
├── analysis.ipynb         # EDA & insights notebook
└── README.md              # Project documentation



📌 Author
👤 Prabhu
Aspiring Data Scientist




