# 👋 Hi there! I'm Anoushka

I work at the intersection of **finance, data and AI**: building models, research tools and analysis that hold up to scrutiny.

NTU Singapore graduate (2025) with a double degree in **Computer Science** and **Business** (Business Analytics and Data Science). CFA Level II candidate.

🔹 Equity and credit research built on primary sources and reproducible code  
🔹 Credit risk, portfolio analytics and machine learning in Python  
🔹 A habit of checking my own work: tie-outs, holdouts, planted-error tests, and saying what I couldn't verify  

## 🎓 Credentials
- **CFA Program** – Level II Candidate (May 2027); [Passed Level I](https://credentials.cfainstitute.org/66763036-be51-4e15-b098-e2f0195a48e1) (Sep 2026)
- [**CFA Investment Foundations Certificate**](https://credentials.cfainstitute.org/f79a9558-1943-48e5-9a3c-851b9257104b) (Oct 2025)
- [**AWS Certified AI Practitioner**](https://www.credly.com/badges/ba38a71f-a0cf-49d1-9468-d91fd1be7f92/linked_in_profile) (Jan 2026)

## 💼 Work Experience
- **Data Analyst – Risk Reporting (Freelance)**, Smriti Cooperative Bank, India (Nov 2025 – Feb 2026)  
  Built automated daily monitoring of SMA and NPA portfolios across 1,500+ loan accounts, replacing a manual Excel process, with early-warning indicators from repayment behaviour and automated validation and reconciliation in Python.

- **Business Analytics Consultant**, NTU–Aon Consulting Project, Singapore (Jan 2025 – Apr 2025)  
  Used PCA and K-Means clustering on financial, operating and transition-risk data to benchmark 15+ APAC power companies, with scenario analysis on carbon exposure and low-carbon investment.

- **Corporate Advisory Intern**, Risewell SG, Singapore (May 2023 – Jun 2023)  
  Researched industries, infrastructure and costs for a proposed economic zone using R and SQL, and recommended data centres as the anchor industry.

- **Process Analyst Intern**, Delta Electronics Int'l, Singapore (May 2022 – Jul 2022)  
  Drafted SOPs and governance documentation for inventory and fixed-asset processes, and cleaned and consolidated 200+ records.

## 🚀 Featured Projects

### [**Delta Electronics (2308.TW) – Initiation of Coverage**](https://github.com/Anou-shka/delta-volts) *(in progress)*
How much of Taiwan's power and liquid-cooling leader is now an AI bet, and what does the share price assume?
- Python pipeline extracting five years of audited financials from 39 primary filings, with 920 page-traced source entries and 422 automated tie-out checks.
- Linked three-statement Excel model (9 sheets, 1,195 formulas) with 18 integrity checks per period, all TRUE, rebuilt and tested in CI on every push.
- Segment analysis: Infrastructure profit rose from NT$5.5bn to NT$28.4bn in FY2025. I rejected widely quoted AI revenue splits that I couldn't trace to any company document.
- Next: forecasts, reverse DCF and the written report, after Q3 2026 results.

### [**Verity – Multi-Agent Equity Research with Independent Fact-Checking**](https://github.com/Anou-shka/Verity) *(in progress)*
A researcher–writer–fact-checker pipeline covering Delta's US-listed peers (Vertiv, Eaton, Trane and seven others), where every number must trace to a filing.
- Data layer built from raw SEC XBRL: about 11% of values rebuilt from other lines and checked against the 10-K, with non-December year-ends, restatements and a stock split handled explicitly.
- Plain Python with no agent framework, and the model never does arithmetic. Every number carries a source ID back to an XBRL fact and filing accession.
- An independent fact-checker re-fetches every number. Tested with 900 planted errors, it caught 98.2% with zero false alarms on 7,117 correct values. The main weakness is true numbers described as the wrong metric (87.7% caught).
- Found and fixed a revision loop that "laundered" fabricated figures into true-looking claims. Includes a pre-launch risk memo mapped to MAS FEAT principles, which recommends not launching yet.
- Status: headline results use the deterministic writer. LLM-writer runs are built and pending.

### [**Stagecraft – IFRS 9 Expected Credit Loss Engine**](https://github.com/Anou-shka/StageCraft)
End-to-end expected credit loss engine on Freddie Mac loan-level mortgage data (2005–2019 vintages), spanning the 2008 crisis and COVID.
- Three-stage staging with a 30-days-past-due backstop, a lifetime-PD significant-increase test and a watchlist, plus cure probation.
- Macro-linked discrete-time hazard PD model (champion) with a Markov roll-rate challenger; downturn LGD from realised workout losses; amortising EAD with prepayment as a competing exit.
- Probability-weighted ECL across base, upside and downside scenarios, a severe stress test, and a provision waterfall that reconciles exactly.
- Mapped to India's SMA/NPA buckets and compared with the RBI's ECL framework. Delivered as a Streamlit dashboard and model documentation.

### [**Ethena (USDe / ENA) – Due Diligence Report**](LINK)
A risk assessment of a synthetic dollar backed by crypto and hedged with short perpetual futures.
- Rated USDe medium risk and ENA high risk, with a risk register of explicit triggers that would change the view.
- Showed USDe supply tracks funding rates through three boom-bust cycles, and that the mechanism held through the October 2025 crash (~$8.3B redeemed, no on-chain depeg).
- Quantified funding risk (reserve covers ~8 weeks at −20% funding), and modelled ENA vesting in Python with self-checks against reported unlocks.

### [**Credyte – Credit Default Risk Model**](https://github.com/Anou-shka/credyte)
Calibrated probability-of-default model on the UCI credit card default dataset (30,000 accounts).
- XGBoost model at 0.78 ROC-AUC on held-out data, against a 0.743 logistic regression baseline. Isotonic calibration cut Brier score by 25%.
- Found and fixed calibration data leakage that had inflated earlier metrics, then rebuilt the pipeline so training, calibration and evaluation never overlap.
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
Three-statement modelling, financial statement analysis, IFRS 9 expected credit loss (PD/LGD/EAD, staging, stress testing), credit risk, portfolio analytics, VaR/ES, tokenomics and on-chain analysis  

**AI & Agents:**  
Multi-agent LLM pipelines with tool use, LLM evaluation (planted-error testing), AI governance (MAS FEAT)  

**Languages:**  
Python, SQL, R, Java  

**Data & ML:**  
pandas, Polars, NumPy, SciPy, scikit-learn, XGBoost, PyTorch, SHAP, LSTM, transformers (DeBERTa)  

**Data & Databases:**  
PostgreSQL, MySQL, Parquet, SEC XBRL, ETL/ELT, PDF data extraction, Dune SQL  

**BI & Apps:**  
Excel (advanced), Power BI, Tableau, Streamlit, Plotly  

**Engineering:**  
Git/GitHub, CI/CD (GitHub Actions), cloud deployment (Render), AWS  

## 📫 Contact
- [**Email**](mailto:nahatanoushka@gmail.com)  
- [**LinkedIn**](https://linkedin.com/in/anoushka-nahata)  
- [**Website**](https://anoushkanahata-portfolio.vercel.app/?utm_source=github&utm_medium=profilepage&utm_campaign=portfolio)
