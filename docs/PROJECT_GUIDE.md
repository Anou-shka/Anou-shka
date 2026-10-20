# My Projects: Quick Guide

A quick guide to my six featured projects. For each one: a summary to learn, an elevator pitch to say out loud, the numbers to know, how to explore and run it, and one small edit to commit.

> Checked on 20 Oct 2026: the test suites for Credyte (4), Verity (56), Stagecraft (20) and Delta Volts (15) all pass from a fresh clone.

---

## 0. One-time setup (do this once)

1. Install **Python 3.11+**, **Git** and **VS Code**.
2. Make a folder for your projects and clone all six:
   ```bash
   mkdir ~/projects && cd ~/projects
   git clone https://github.com/Anou-shka/portfolio_risk_and_return_dashboard
   git clone https://github.com/Anou-shka/credyte
   git clone https://github.com/Anou-shka/Verity
   git clone https://github.com/Anou-shka/StageCraft
   git clone https://github.com/Anou-shka/Ethena
   git clone https://github.com/Anou-shka/delta-volts
   ```
3. For each project, make a virtual environment inside its folder:
   ```bash
   cd <project>
   python -m venv .venv
   source .venv/bin/activate        # Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```
4. **How to commit an edit (the same every time):**
   ```bash
   git checkout -b my-first-edit     # optional: work on a branch
   # ... make your edit ...
   git add -A
   git commit -m "Short description of what I changed"
   git push                          # or: git push -u origin my-first-edit
   ```

**How to explore any repo in 10 minutes:**
1. Read the README.
2. Open the one diagram (the `mermaid` flowchart) and trace it left to right.
3. Open the one file that matters most (listed below).
4. Run it.
5. Change one number and run it again.

---

## The 1-line story that ties it all together

> "I work on finance plus code. I build things a bank or fund would actually use, and I test my own work: every number traces to a source, and I measure where my models fail."

| Project | Area | One line |
|---|---|---|
| Portfolio Pulse | Portfolio and market risk | Live dashboard for portfolio risk, return and optimisation |
| Credyte | Retail credit risk (ML) | Calibrated, explainable credit-card default model |
| Stagecraft | Credit risk and accounting (IFRS 9) | Bank-style expected-credit-loss engine on 750k mortgages |
| Delta Volts | Equity research | Initiation on Delta Electronics, built from primary filings |
| Verity | AI and agents | Multi-agent research writer with an independent fact-checker |
| Ethena | Crypto and DeFi due diligence | Risk report on the USDe synthetic dollar and the ENA token |

**How they connect:** Delta Volts covers the company → Verity covers Delta's US peers → Stagecraft and Credyte cover credit → Portfolio Pulse covers portfolio risk → Ethena covers crypto.

---

## 1. Portfolio Pulse: Portfolio Risk Dashboard

**Repo:** `portfolio_risk_and_return_dashboard` · **Live:** https://portfolio-pulse.onrender.com

### Summary
A deployed Streamlit app. You build a portfolio of stocks, ETFs and crypto, and it shows how much risk you are taking for the return you get. It computes more than 15 metrics: Sharpe, Sortino, Treynor, Calmar, beta, tracking error, information ratio, max drawdown, and historical and Monte Carlo VaR/ES. It optimises weights (max-Sharpe or min-variance, using SciPy SLSQP), draws the efficient frontier, splits risk by asset, and has a live 1-minute view against the S&P 500.

### Elevator pitch (30 sec)
> "Brokerage apps show prices, not risk. Portfolio Pulse answers the questions a PM asks: how much risk am I taking for this return, which holding drives my volatility, and is there a better mix of the same assets? The hard part was mixing crypto, which trades 365 days a year, with stocks, which trade about 252. Naively, every weekend shows up as a fake 0% stock return. I aligned everything to one calendar. I also fixed a timezone bug: Yahoo stamps crypto bars in UTC, and that was zeroing out daily returns. It runs on a free 512 MB server."

### Numbers and words to know
- 252-day annualisation · risk-free rate = live 10-year Treasury yield (4% fallback in config)
- Covariance shrinkage toward the diagonal · Euler risk contributions
- Monte Carlo VaR assumes normal returns, so it understates fat tails. That's why historical VaR is shown next to it.

### Explore → Run → Edit
1. **Explore:** `src/metrics_core.py`, which holds every formula (Sharpe at line ~100, optimisers at ~255). Read `docs/formulas.md` next to it.
2. **Run:** `pip install -r requirements.txt` → `streamlit run app/app.py` → open http://localhost:8501
3. **Play:** pick 5 tickers, switch to "max-Sharpe", then open the Risk & Frontier tab.
4. **Edit and commit:** in `config/portfolio.yaml`, change `risk_free_rate_annual: 0.04` to the current rate, or add a benchmark under `benchmarks:` (e.g. `"^NDX": "Nasdaq 100"`). Rerun, see it in the dropdown, commit.

---

## 2. Credyte: Explainable Credit Default Model

**Repo:** `credyte`

### Summary
Predicts the probability that a credit-card customer defaults next month, on the UCI dataset (30,000 Taiwanese cardholders, 22.1% default rate). XGBoost beats a logistic regression baseline. Isotonic calibration makes the probabilities trustworthy, so "16%" really means about 16 in 100. SHAP explains every prediction, and a Streamlit dashboard shows each borrower's risk drivers.

### Elevator pitch
> "A credit model has three jobs: rank risky borrowers first, give probabilities you can price with, and explain itself. Credyte does all three. XGBoost gets 0.78 ROC-AUC against 0.74 for logistic regression. Calibration cut the Brier score by 25%. The part I'm proudest of is a leak I found: my calibrator had been fitted on training rows, which made it look better than it was. I rebuilt the splits so training, calibration and evaluation never overlap."

### Numbers to know
| | |
|---|---|
| ROC-AUC (holdout, 6,000 rows) | XGBoost **0.779** vs LR **0.743** |
| Brier score | 0.181 → **0.136** after isotonic calibration (−25%) |
| Decision threshold (F1-optimal) | **0.26** → precision 0.52, recall 0.55 |
| Features | 16 engineered features (utilisation, repay ratio, payment-status EMA…) · `SEX` excluded |
| Splits | 24k train / 3k calibrate / 3k evaluate |

Top drivers: **recent payment status**, then payment amounts and utilisation. Demographics matter little.

### Explore → Run → Edit
1. **Explore:** `src/features.py` (one feature code path shared by training and the app; this is the "no train/serve skew" point) and `models/metrics.json`.
2. **Run:** `pip install -r requirements.txt` → `streamlit run app.py`. Models are pre-trained, so it opens straight away.
3. **Test:** `pip install pytest && python -m pytest tests` → 4 passed.
4. **Edit and commit:** in the app sidebar, move the risk-band threshold and watch borrowers change bands. For a commit, add a "What I'd do next" bullet to the README Limitations (e.g. "time-based validation", "fairness review of AGE").

---

## 3. Stagecraft: IFRS 9 Expected Credit Loss Engine

**Repo:** `StageCraft` · **Your own prep doc:** `docs/interview-prep.md` (read this one first!)

### Summary
Does what a bank's impairment model does, on **750,000 real Freddie Mac mortgages** (2005–2019 vintages, 48.5 million loan-months, including 2008 and COVID). It puts each loan in **Stage 1/2/3**. It estimates PD with a macro-linked **hazard model** (champion) and a **Markov roll-rate** model (challenger), LGD from real foreclosure losses, and EAD from amortisation and prepayment. It then produces **probability-weighted ECL** across base, upside and downside scenarios, plus a severe stress test, and a provision waterfall that reconciles exactly. It is also mapped to India's SMA/NPA buckets and the RBI's 2027 ECL rules.

### Elevator pitch
> "At the cooperative bank I tracked SMA and NPA, which is backward-looking. IFRS 9, and the RBI from April 2027, wants *expected* losses: forward-looking and weighted across scenarios. So I built that end to end on 750,000 real mortgages. At December 2019 the allowance is $207 million on a $58 billion book. The PD model has an out-of-time AUC of 0.88. The weighted ECL sits 4.9% above the base case because losses are convex: the downside adds $59m while the upside saves only $10m."

### Numbers to know (31 Dec 2019)
| | |
|---|---|
| Book | 318,602 loans, **$58.5bn** |
| Weighted ECL | **$207.4m** (0.35% coverage); was $251.3m in 2018 |
| Stage mix | S1 97.3% · S2 2.1% · S3 0.6% (coverage 0.10% / 4.5% / 26%) |
| Severe stress | $368m = **1.8×** the allowance |
| Out-of-time AUC | hazard **0.88** vs Markov 0.85 |
| SICR rule | 30 DPD backstop, or lifetime PD ≥ **2×** origination **and +50bp**, or a watchlist flag |
| LGD | ~59% severity before cures · judicial states +12pts |

**Weakness to own before they raise it:** the 2019 backtest is "red" (0.60% predicted vs 4.0% observed) because COVID forbearance counted as default. That is the textbook case for a management overlay.

### Explore → Run → Edit
1. **Explore:** `config/assumptions.yaml` holds every judgment call with its reason. Then `src/stagecraft/staging.py` and `ecl.py`.
2. **Run:** `pip install -e ".[dev]"` → `pytest` (20 passed) → `streamlit run app/streamlit_app.py`. From a fresh clone the dashboard uses **synthetic demo data**; the real Freddie data needs a free registration.
3. **Play:** in the dashboard, change scenario weights or the SICR multiple and watch ECL and the stage mix move.
4. **Edit and commit:** fill in a few answers in `docs/defence.md` (it is blank on purpose, for your own words). Writing them is the best way to learn the project.

---

## 4. Delta Volts: Delta Electronics (2308.TW) Initiation

**Repo:** `delta-volts` · Status: **M2 of 6 done** (data and historical model); forecasts, valuation and report still to come

### Summary
Equity research on Taiwan's power and liquid-cooling leader. The question: *how much of Delta is now an AI bet, and what is the market paying for?* A Python pipeline reads **39 primary PDFs**, rebuilds the tables from word coordinates, and logs **920 page-traced sources**. **422 tie-out checks** prove the extraction. The output is an Excel three-statement model generated by code (**1,195 live formulas**, 18 checks per period, all TRUE), rebuilt in CI on every push.

### Elevator pitch
> "Delta makes the power and cooling that go inside AI server racks. Revenue grew 32% in FY2025, and Infrastructure profit went from NT$5.5bn to NT$28.4bn. I built the historicals from Delta's own filings: every number traces to a page, and 422 automated checks prove the extraction. I deliberately rejected the AI revenue splits quoted in the press because I couldn't trace them to any company document. I anchor on management's own disclosures instead: data centre is over half of 1H26 revenue, and AI products will be over 25% of FY2026."

### Numbers to know
| | FY2025 | 1H26 |
|---|---|---|
| Revenue | NT$554.9bn (+32%) | NT$342.6bn (+41%) |
| Gross margin | 34.3% | 36.3% |
| EBIT margin | 15.1% | 17.2% |
| EPS | NT$23.14 | NT$17.59 (+89% y/y) |
- ROE 16% → **24%** · net cash (cash NT$182bn vs debt NT$71bn) · FY2026 capex guided to **~NT$70bn**
- Weak spots: Mobility (EV) is loss-making; Automation's margin is about 1%

### Explore → Run → Edit
1. **Explore:** open `model/delta_model.xlsx` in Excel and look at the **Checks** and **Segments** sheets. Then read `docs/decisions.md` (why each modelling choice was made).
2. **Run:** `pip install -r requirements.txt` → `make test` (15 passed). `make all` rebuilds everything; it needs LibreOffice for the Excel recalc.
3. **Edit and commit:** search `src/delta/build_excel.py` (or the Excel file) for `ANALYST TO REVIEW` and sign off one judgment call (agree, or change it and write why in `docs/decisions.md`). That is genuinely your job as the analyst.

---

## 5. Verity: Multi-Agent Equity Research with a Fact-Checker

**Repo:** `Verity` · **Your own prep docs:** `docs/case-study.md`, `docs/milestone-notes.md` (each milestone lists likely interview questions)

### Summary
Three agents (**Researcher → Writer → Fact-checker**) write a comps table and a ~600-word note on each of Delta's 10 US peers (Vertiv, Eaton, Trane, GE Vernova…) from **raw SEC XBRL data**. Rules: plain Python with no agent framework, **the LLM never does arithmetic**, and every number carries a source ID (`[S7]`) back to an XBRL fact and filing. The fact-checker re-fetches every number with its **own** tools. Tested on **900 planted errors**, it caught **98.2%**, with **0 false alarms** on 7,117 correct values. A governance memo, mapped to **MAS FEAT**, recommends *not launching yet*.

### Elevator pitch
> "LLMs write fluent research, but fluency isn't accuracy, and one wrong year ruins a note. So I built a system where a separate fact-checker independently re-verifies every number against SEC filings, and I measured it. I planted 900 errors: it caught 98.2% with zero false alarms. Its weak spot is meaning. A true number described as the wrong metric ('data-centre revenue' quoting total revenue) is caught only 87.7% of the time. I also found that my first revision loop 'laundered' fabricated figures into true-looking ones, and fixed it by deleting fabrications instead of patching them."

### Numbers to know
- 10 companies · 663 core values · **11%** rebuilt from other XBRL lines (e.g. Eaton has no operating-income tag, so EBIT = pre-tax + interest)
- Recall **98.2%** (884/900) · false alarms **0%** · left after revision **2.7%**
- Tolerance: 0.5% for reported figures, 0.1pp for ratios · max 2 revision rounds
- **Caveat to say yourself:** the headline numbers come from the *deterministic* template writer. LLM-writer runs are built but pending (they need an API key).

### Explore → Run → Edit
1. **Explore:** `outputs/VRT-demo/` (a note with 4 planted errors, then its fact-check log). Then `src/verity/agents/fact_checker.py` and `src/verity/orchestrator.py`.
2. **Run:** `pip install -r requirements.txt` → `make test` (56 passed) → `make demo` → `make app` (opens the Streamlit viewer). All offline, no API key needed.
3. **Edit and commit:** (a) answer questions in `docs/defence.md`; or (b) change `tolerance: reported_rel: 0.005` in `config/settings.yaml` to `0.02`, run `make eval`, and see how recall and false alarms move. Revert or keep, then commit your finding.
4. **Bigger next step:** add an Anthropic API key and run `VERITY_PROVIDER=anthropic make eval notes` to get the real LLM numbers.

---

## 6. Ethena (USDe / ENA): Due Diligence Report

**Repo:** `Ethena` · **Deliverable:** `report/Ethena_Due_Diligence_Report.pdf` (15 pages)

### Summary
An independent risk assessment of crypto's largest synthetic dollar. USDe is backed by crypto collateral hedged with short perpetual futures; its yield comes mostly from funding rates. **Verdict: USDe/sUSDe medium risk, ENA high risk.** The report includes a 7-risk register with explicit triggers that would change the view, 5 Dune SQL queries, 9 charts generated from source-tagged CSVs, and a Python vesting model that **asserts** it reproduces Ethena's reported unlocks.

### Elevator pitch
> "USDe is a carry trade wrapped as a token. Its supply has followed funding rates through three boom-bust cycles and is 68% below its peak. The mechanism did hold under real stress: about $8.3bn was redeemed after the October 2025 crash with no on-chain depeg. I turned 'funding risk' into a number: the reserve fund covers about 8 weeks at −20% funding. That number became a falsifiable trigger in my conclusion."

### Numbers to know
- Supply **$4.76bn** (−68% from peak) · **~$8.3bn** redeemed in Oct 2025, no depeg
- ~90–95% of backing with **two custodians** (Ceffu, Copper) · BaFin forced a German wind-down
- sUSDe 5% APY with 26% staked ≈ **1.3%** net yield on the whole backing
- Reserve runway: ~16 weeks at −10% funding, **~8 weeks at −20%**
- ENA fee switch kicks in only once USDe supply reaches **$7.5bn**
- Data as of 16 Oct 2026. **Own it:** the Dune queries are written but not yet run.

### Explore → Run → Edit
1. **Explore:** read the 1-page executive summary in the PDF, then `data/risk_register.csv` and `scripts/build_unlock_schedule.py`.
2. **Run:** `pip install -r requirements.txt` → `make all` (vesting model → charts → PDF; the PDF step needs `python -m playwright install chromium`).
3. **Edit and commit:** paste `dune/01_usde_supply_daily.sql` into dune.com, run it, save the output to `data/`, and commit. That closes the report's own "Dune outputs pending" limitation.

---

## Fix this first: profile README

In this repo's `README.md`, the Ethena project link is still the placeholder `(LINK)`. Change it to `https://github.com/Anou-shka/Ethena` and commit. That is your easiest first commit, and recruiters click that link.

---

## Email blurbs (copy and paste)

- **Quant / risk:** "I built Stagecraft, an IFRS 9 ECL engine on 750k Freddie Mac mortgages ($207m allowance on a $58bn book, out-of-time AUC 0.88), and Credyte, a calibrated credit default model (0.78 AUC, Brier score −25%)."
- **Equity research:** "I'm writing an initiation on Delta Electronics from primary filings (920 page-traced sources, 422 tie-out checks, a 1,195-formula three-statement model), with a companion AI project, Verity, that fact-checks research notes on its US peers."
- **AI / tech:** "Verity is a three-agent research system where an independent fact-checker caught 98.2% of 900 planted errors with zero false alarms, plus a MAS FEAT governance memo."
- **Crypto / digital assets:** "My Ethena due diligence rates USDe medium and ENA high risk, with on-chain SQL and a reserve-runway model (about 8 weeks at −20% funding)."

## How to practise (15 minutes a day)
1. Day 1–6: one project a day. Read the summary, say the pitch out loud 3 times, then run it.
2. Write answers to 5 questions from that repo's `docs/defence.md` (Verity, Stagecraft) or from "Numbers to know" (the others).
3. Make the suggested edit and commit it. Now you have touched every project yourself.
