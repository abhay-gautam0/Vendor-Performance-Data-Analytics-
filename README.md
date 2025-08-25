<div align="center">

<h1>Vendor Performance & Inventory Analytics 📊🚀</h1>

<p><strong>From raw CSVs ➜ clean SQLite database ➜ actionable KPIs ➜ insightful notebooks ➜ optional Power BI dashboard</strong></p>

<p>
  <a href="#-quickstart">
    <img alt="Made with Python" src="https://img.shields.io/badge/Made%20with-Python-3776AB?logo=python&logoColor=white">
  </a>
  <a href="#-project-structure">
    <img alt="Pandas" src="https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white">
  </a>
  <a href="#-data-requirements">
    <img alt="SQLite" src="https://img.shields.io/badge/SQLite-003B57?logo=sqlite&logoColor=white">
  </a>
  <a href="#-notebooks">
    <img alt="Jupyter" src="https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white">
  </a>
  <a href="#-power-bi-dashboard-optional">
    <img alt="Power BI" src="https://img.shields.io/badge/Power%20BI-F2C811?style=flat&logoColor=000">
  </a>
</p>


<p>
  <img alt="Python" title="Python" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" height="48" />
  <img alt="Pandas" title="Pandas" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/pandas/pandas-original.svg" height="48" />
  <img alt="Jupyter" title="Jupyter" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/jupyter/jupyter-original.svg" height="48" />
  <img alt="SQLite" title="SQLite" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/sqlite/sqlite-original.svg" height="48" />
  <img alt="Seaborn" title="Seaborn" src="https://seaborn.pydata.org/_images/logo-mark-lightbg.svg" height="48" />
  <img alt="Power BI" title="Power BI" 
     src="https://upload.wikimedia.org/wikipedia/commons/c/cf/New_Power_BI_Logo.svg" 
     height="48" />
</p>

</div>

---

## ✨ Highlights
- ⚡ One‑click ingestion of CSV files into a clean SQLite database (inventory.db)
- 🧠 Vendor sales summary with profitability and efficiency KPIs
- 📒 Insight‑rich Jupyter notebooks for EDA and performance analysis
- 📈 Optional Power BI dashboard for interactive exploration
- 🧰 Solid logging, reproducible environment, and clear project structure


## 🧭 Table of Contents
- 🔧 [Quickstart](#-quickstart)
- 🗂️ [Project Structure](#-project-structure)
- 🧾 [Data Requirements](#-data-requirements)
- ▶️ [Usage](#%EF%B8%8F-usage)
- 📒 [Notebooks](#-notebooks)
- 📊 [Power BI Dashboard (optional)](#-power-bi-dashboard-optional)
- 🧮 [KPIs Computed](#-kpis-computed)
- 🗃️ [Outputs](#-outputs)
- 🧪 [Known Issues / TODO](#-known-issues--todo)
- 📜 [License & Attribution](#-license--attribution)


## 🔧 Quickstart
1) Create and activate a virtual environment (Windows PowerShell)
- python -m venv .venv
- .venv\\Scripts\\Activate.ps1
- python -m pip install --upgrade pip
- pip install pandas sqlalchemy jupyter seaborn matplotlib

2) (Optional) Freeze dependencies
- pip freeze > requirements.txt

3) Ensure your CSVs are ready (see Data Requirements below)


## 🗂️ Project Structure
```
project/
├─ ingestion_db.py                 # Ingests CSVs ➜ SQLite tables
├─ get_vendor_summary.py           # Builds & cleans vendor summary table
├─ Exploratory_data_analysis.ipynb # EDA notebook
├─ vendor_performance_analysis.ipynb
├─ inventory.db                    # SQLite DB (generated)
├─ vendor.pbix                     # Power BI report (optional)
├─ logs/                           # Script logs
├─ csv_export/                     # Exports (optional)
└─ README.md                       # You are here
```


## 🧾 Data Requirements
The ingestion script creates one table per CSV with the filename (without .csv) as the table name. The summary expects these tables/fields:

1) vendor_invoice (from vendor_invoice.csv)
- VendorNumber, Freight

2) purchases (from purchases.csv)
- VendorNumber, VendorName, Brand, Description, PurchasePrice, Quantity, Dollars

3) purchase_prices (from purchase_prices.csv)
- Brand, Price, Volume

4) sales (from sales.csv)
- VendorNo, Brand, SalesQuantity, SalesDollars, SalesPrice, ExciseTax

Tip: Keep filenames exactly matching the table names for frictionless ingestion.


## ▶️ Usage
1) Configure the raw data directory
- ingestion_db.py reads CSVs from a hardcoded path:
  - C:/Users/asus/Desktop/project/data/data
- Options:
  - Edit load_raw_data() to your actual directory, or
  - Move/symlink your CSVs into that folder

2) Ingest CSVs ➜ SQLite
- python ingestion_db.py
- Output: inventory.db and logs/ingestion_db.log

3) Build the Vendor Summary table
- python get_vendor_summary.py
- Output: vendor_sales_summary in inventory.db and logs/get_vendor_summary.log

4) Explore in notebooks
- jupyter notebook
- Open Exploratory_data_analysis.ipynb or vendor_performance_analysis.ipynb

5) Optional: Open the Power BI dashboard
- Open vendor.pbix in Power BI Desktop and point it to inventory.db in this folder


## 📒 Notebooks
- Exploratory_data_analysis.ipynb — Data profiling, distributions, trends, correlations
- vendor_performance_analysis.ipynb — Vendor KPIs, margins, turnover, and brand insights

Tip: Run after the database has been created so queries and joins resolve.


## 📊 Power BI Dashboard
- Open vendor.pbix and verify the SQLite connection path.
- Refresh to explore vendor‑level performance interactively.
  <p>
 <img src="https://raw.githubusercontent.com/abhay-gautam0/Vendor-Performance-Data-Analytics-/main/Dashboard.jpg" width="700">
</p>


## 🧮 KPIs Computed
- GrossProfit = TotalSalesDollars − TotalPurchaseDollars
- ProfitMargin = (GrossProfit / TotalSalesDollars) × 100
- StockTurnover = TotalSalesQuantity / TotalPurchaseQuantity
- SalesToPurchaseRatio = TotalSalesDollars / TotalPurchaseDollars


## 🗃️ Outputs
- Database: inventory.db with purchases, sales, vendor_invoice, purchase_prices, vendor_sales_summary
- Logs: logs/ingestion_db.log, logs/get_vendor_summary.log
- Visuals: Use the assets/ folder (create it) to export and store plots used in posts or reports


## 🧪 Known Issues / TODO
- ingestion_db.py uses a hardcoded data directory — parameterize with a CLI flag (e.g., --data-dir)
- get_vendor_summary.py cleanup:
  - Validate indentation for return statements
  - Use the df parameter consistently in clean_data() (avoid referencing outer variables)
  - Consider using SQLAlchemy engine uniformly for ingestion
- Add argparse CLIs and unit tests for key transformations
- Add .gitignore (ignore .ipynb_checkpoints/, __pycache__/, .venv/, logs/, large data, inventory.db if you don’t want to commit it)


## 🖼️ Social‑Ready Visuals (Placeholders)
Use these as placeholders in your README or LinkedIn post, then replace with your own charts saved under assets/.

<p>
  <img src="https://github.com/abhay-gautam0/Vendor-Performance-Data-Analytics-/blob/main/Top_Vendors_by_Sales.png" alt="Top Vendors by Sales" />
</p>
<p>
  <img src="https://github.com/abhay-gautam0/Vendor-Performance-Data-Analytics-/blob/main/Gross_profit.png" alt="Gross Profit and Margin Trends" />
</p>
<p>
  <img src="https://github.com/abhay-gautam0/Vendor-Performance-Data-Analytics-/blob/main/heat_map.png" alt="Correlation Heatmap" />
</p>


## 📜 License & Attribution
- Consider adding an MIT LICENSE file for clarity.
- If your dataset is public, cite the source and its license.

---

<div align="center">
📩 Feel free to connect with me on [LinkedIn](https://www.linkedin.com/in/abhaygautam01)  
📧 Or drop an email: **agabhay2005@gmail.com**
Made with ❤️ using Python, Pandas, Jupyter, SQLite, Seaborn, and Power BI. <br/>
<strong>Feedback welcome!</strong> Open an issue or reach out with ideas and improvements.

</div>
