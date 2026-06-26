# Yfinance_ActivityFinal.ipynb
A Python project that extracts financial data for 50 S&amp;P 500 companies using yfinance, builds a structured data model, and applies Markowitz portfolio optimization to identify optimal asset allocations.

Features


Multi-sector data extraction across 9 sectors (Technology, Financials, Healthcare, Consumer Cyclical, Consumer Defensive, Energy, Industrials, Utilities, Real Estate)
Structured data model with dimension and fact tables (star schema)
Sector performance & rotation analysis with visual heatmaps and rolling rankings
Markowitz portfolio optimization — Minimum Variance and Maximum Sharpe Ratio portfolios
Efficient Frontier generation with 50 optimal portfolio points
Macro context via market index tracking (S&P 500, NASDAQ, VIX, DXY, US 10Y Yield)
World Bank macroeconomic data integration (GDP, inflation, unemployment)
ETL audit logging for pipeline traceability
Excel export of all tables into a single workbook



Data Model

The project builds a star schema with 10 tables:

TableTypeDescriptiondim_tickerDimensionCompany metadata (name, sector, market cap, employees)dim_sector_industryDimensionUnique sectors and industriesdim_calendarDimensionFull date table with trading day flags and US holidaysdim_countryDimensionCountry-level economic indicators from the World Bankdim_security_accessDimensionRow-Level Security (RLS) user-role mappingfact_pricesFactDaily OHLCV prices + 20/50-day MAs, volatility, cumulative returnfact_financialsFactQuarterly income statement data (revenue, net income, EBITDA)fact_balance_sheetFactQuarterly balance sheet data (assets, debt, equity, cash)fact_market_indicesFactDaily closing values for major market indicesfact_load_logAuditETL log tracking row counts, timestamps, and load status


Analysis & Outputs

Sector Analysis (sector_analysis.png)


Cumulative returns per sector (equal-weighted)
Monthly returns heatmap (top 8 sectors)
Rolling 30-day volatility by sector
Sector rotation ranking (rolling 60-day performance)


Portfolio Optimization (efficient_frontier_optimized.png)


Efficient Frontier curve across 50 optimal portfolios
Minimum Variance Portfolio highlighted
Maximum Sharpe Ratio Portfolio highlighted
Individual stock risk/return scatter


Performance Comparison (portfolio_performance.png)


Cumulative returns: Min Variance vs Max Sharpe vs Equal Weight vs S&P 500
Annualized return, volatility, Sharpe ratio, and max drawdown summary



Tech Stack


Python 3.x
yfinance — market data
pandas, numpy — data manipulation
matplotlib, seaborn — visualization
scipy.optimize — portfolio optimization (SLSQP)
requests — World Bank API
openpyxl — Excel export



Setup & Usage

1. Clone the repository

bashgit clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

2. Install dependencies

bashpip install yfinance pandas numpy matplotlib seaborn scipy openpyxl requests

3. Run the notebook

Open Yfinance_ActivityFinal.ipynb in Jupyter or Google Colab and run all cells sequentially.

All outputs are saved to the tables/ directory.


Project Structure

├── Yfinance_ActivityFinal.ipynb   # Main notebook
├── tables/
│   ├── dim_ticker.csv
│   ├── dim_sector_industry.csv
│   ├── dim_calendar.csv
│   ├── dim_country.csv
│   ├── dim_security_access.csv
│   ├── fact_prices.csv
│   ├── fact_financials.csv
│   ├── fact_balance_sheet.csv
│   ├── fact_market_indices.csv
│   ├── fact_load_log.csv
│   ├── yfinance_data_model.xlsx
│   ├── sector_analysis.png
│   ├── efficient_frontier_optimized.png
│   └── portfolio_performance.png
└── README.md


Notes


Data is pulled in real time from Yahoo Finance; results will vary by run date.
The portfolio optimization assumes long-only positions (no short selling).
The Sharpe Ratio is calculated without a risk-free rate (simplified version).
US holiday dates are hardcoded through 2025; extend as needed for future runs.



License

This project is for educational purposes.
