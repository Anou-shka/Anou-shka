# 👋 Hi there! I'm Anoushka

I work at the intersection of **finance, data and AI**: building models, research tools and analysis that hold up to scrutiny.

NTU Singapore graduate (2025) with a double degree in **Computer Science** and **Business** (Business Analytics and Data Science). CFA Level II candidate.

🔹 Equity and credit research built on primary sources and reproducible code  
🔹 Risk modelling, portfolio analytics and machine learning in Python  
🔹 A habit of checking my own work: tie-outs, holdouts, and saying what I couldn't verify  

## 🎓 Credentials
- [**CFA Program** – Level II Candidate (May 2027); Passed Level I (Sep 2026)](https://credentials.cfainstitute.org/66763036-be51-4e15-b098-e2f0195a48e1#acc.cAzQ8IHE)
- [**CFA Investment Foundations Certificate**](https://credentials.cfainstitute.org/f79a9558-1943-48e5-9a3c-851b9257104b) (Oct 2025)
- [**AWS Certified AI Practitioner**](https://www.credly.com/badges/ba38a71f-a0cf-49d1-9468-d91fd1be7f92/linked_in_profile) (Jan 2026)

## 💼 Work Experience
- **Data Analyst – Risk Reporting (Freelance)**, Smriti Cooperative Bank, India (Nov 2025 – Feb 2026)  
  Built daily monitoring of SMA and NPA loan portfolios with early-warning indicators from customer payment behaviour, and automated portfolio reporting, validation and reconciliation in Python.

- **Business Analytics Consultant**, NTU–Aon Consulting Project, Singapore (Jan 2025 – Apr 2025)  
  Applied ML-based segmentation to financial, operating and transition-risk data for 15+ APAC power companies, with scenario analysis on carbon exposure and low-carbon investment.

- **Corporate Advisory Intern**, Risewell SG, Singapore (May 2023 – Jun 2023)  
  Researched industries, infrastructure and costs for a proposed economic zone using R and SQL, and recommended data centres as a target industry.

- **Process Analyst Intern**, Delta Electronics Int'l, Singapore (May 2022 – Jul 2022)  
  Standardised processes through SOPs and governance documentation, and streamlined 200+ inventory and fixed-asset records.

## 🚀 Featured Projects

### [**Delta Electronics (2308.TW) – Initiation of Coverage**](https://github.com/Anou-shka/delta-volts) *(in progress)*
How much of Taiwan's power and liquid-cooling leader is now an AI bet, and what does the share price assume?
- Python pipeline extracting five years of audited financials from 39 primary filings, with 920 page-traced source entries and 422 automated tie-out checks.
- Linked three-statement Excel model (9 sheets, 1,195 formulas) with 18 integrity checks per period, all TRUE, rebuilt and tested in CI on every push.
- Segment analysis: Infrastructure profit rose from NT$5.5bn to NT$28.4bn in FY2025. I rejected widely quoted AI revenue splits that I couldn't trace to any company document.
- Next: forecasts, reverse DCF and the written report, after Q3 2026 results.

### [**Ethena (USDe / ENA) – Due Diligence Report**](https://github.com/Anou-shka/Ethena)
A risk assessment of a synthetic dollar backed by crypto and hedged with short perpetual futures.
- Rated USDe medium risk and ENA high risk, with a risk register of explicit triggers that would change the view.
- Showed USDe supply tracks funding rates through three boom-bust cycles, and that the mechanism held through the October 2025 crash (~$8.3B redeemed, no on-chain depeg).
- Quantified funding risk (reserve covers ~8 weeks at −20% funding), and modelled ENA vesting in Python with self-checks against reported unlocks.

### [**Credyte – Credit Default Risk Model**](https://github.com/Anou-shka/credyte)
Calibrated probability-of-default model for 30,000 credit card accounts.
- XGBoost model at 0.78 ROC-AUC on held-out data, against a 0.743 logistic regression baseline. Isotonic calibration cut Brier score by 25%.
- Found and fixed calibration data leakage that had inflated reported metrics, then rebuilt the pipeline so training, calibration and evaluation never overlap.
- SHAP explanations per borrower, a Streamlit dashboard, and unit tests in CI to prevent train/serve skew.

### [**Portfolio Pulse – Portfolio Risk Dashboard**](https://portfolio-pulse.onrender.com)
Deployed risk and optimisation dashboard on live stock, ETF and crypto data.
- 15+ metrics including Sharpe, Sortino, beta, information ratio, max drawdown, and historical and Monte Carlo VaR/ES.
- Max-Sharpe and min-variance optimisation (SciPy SLSQP) along the efficient frontier, with covariance shrinkage and asset-level risk contributions.
- 1-minute intraday view across mixed calendars. Diagnosed and fixed a UTC vs exchange-session bug that zeroed daily returns, and cut memory use to run on a 512 MB instance.

## 🧪 Other Projects
- [**Digital Twins for Infection Risk in Elevators**](https://github.com/Anou-shka/Digital-Twins): ML on IoT sensor data (CO₂, temperature, humidity) to classify infection-risk zones at >90% F1-score, with Wells-Riley risk estimates.
- [**NLP Sentiment Analysis**](https://github.com/Anou-shka/SC4002_NLP): fine-tuned DeBERTaV3 to 90.24% test accuracy, after RNN and BiGRU baselines.
- [**POI Co-occurrence and Next-Location Prediction**](https://github.com/Anou-shka/SC4020_Project_2): Apriori association rules (e.g. 3.49 lift between hair salons and laundry services) and an LSTM next-location model.
- [**Clustering Algorithms: Comparative Analysis**](https://github.com/lliangmengg/SC4020-Data-Analytics-Mining-Project): K-means, DBSCAN, GMM and agglomerative clustering compared across four dataset patterns.
- [**Query Execution Plan Optimisation**](https://github.com/FaizRsl/Database_System_Principles_Project_2): PostgreSQL QEP generator and visualiser, reducing query costs by up to 93% on a 6M+ row TPC-H dataset.
- [**Database System Design**](https://github.com/FaizRsl/Database_System_Principles_Project_1): custom storage engine with B+ tree indexing.
- [**Restaurant Search and Reservation System**](https://github.com/Anou-shka/SC2006-Software-Eng) and [**FYP Management System**](https://github.com/its-naptime/SC2002-FYPManager): software engineering coursework projects.

## 🔧 Tech Stack

**Finance & Research:**  
Three-statement modelling, financial statement analysis, credit risk (PD, calibration), portfolio analytics, VaR/ES, tokenomics and on-chain analysis  

**Languages:**  
Python, SQL, R, Java

**Data & ML:**  
pandas, NumPy, SciPy, scikit-learn, XGBoost, PyTorch, SHAP, LSTM, transformers (DeBERTa)  

**Data & Databases:**  
PostgreSQL, MySQL, ETL/ELT, PDF data extraction, Dune SQL  

**BI & Apps:**  
Excel (advanced), Power BI, Tableau, Streamlit, Plotly  

**Engineering:**  
Git/GitHub, CI/CD (GitHub Actions), cloud deployment (Render), AWS  

## 📫 Contact
- [**Email**](mailto:nahatanoushka@gmail.com)  
- [**LinkedIn**](https://linkedin.com/in/anoushka-nahata)  
- [**Website**](https://www.linkedin.com/safety/go/?url=https%3A%2F%2Fanoushkanahata-portfolio.vercel.app%2F%3Futm_source%3Dgithub%26utm_medium%3Dprofile%26utm_campaign%3Dpage&urlhash=-9wo&mt=nZVeC1QCayZOV5itPifV2YDdwbgNjWe0XcUBERGa8qhGqoD50yzG33f-GfUBFvI5mOPMn-8Qp4NHvT4BYVaSsU9p7GY&isSdui=true&lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3B9%2B2%2BX%2BDDRxuAXkjhukQp8w%3D%3D)
