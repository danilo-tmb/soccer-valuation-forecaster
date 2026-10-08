Transfer Market Valuation Forecaster ⚽📈
OPIM 5671: Data Mining and Time Series Forecasting — Team 7

An end-to-end time-series forecasting framework and decision-support prototype designed to predict European professional soccer player market valuations 6 to 12 months (2 to 4 quarters) ahead. The system evaluates quoted transfer fees against projected market trends to guide sporting directors in Buy, Hold/Extend, and Sell decisions.

🔗 Live Interactive Prototype
Check out the interactive decision-support tool: 
https://uconn-my.sharepoint.com/:u:/r/personal/pwc25003_uconn_edu/Documents/Data%20Mining%20-%20Project%201/Team7_Transfer_Fee_Check.html?d=w488b6676ceb94776a34d2abf3f5506ed&csf=1&web=1&e=IcBKpT

📌 Project Overview
In professional soccer, technical and sporting directors face a fundamental dilemma during every transfer window: "Is a player worth the quoted price today given where their value will be in 6 to 12 months?"

This project addresses that challenge by:

Standardizing noisy, irregular Transfermarkt valuation updates into a uniform quarterly panel.
Filtering historical records to build an elite 15-player modeling cohort across Europe's "Big 5" leagues.
Benchmarking multiple time-series models (Damped Holt, SARIMAX, Pooled Age Drift, Persistence) across validation, main test, and holdout periods.
Constructing 80% uncertainty bands around point forecasts to quantify market volatility.
Deploying an interactive Buy / Hold / Sell decision prototype based on player trajectory and quoted transfer fees.
📊 Dataset & Cohort Scouting
Source: Public Kaggle dataset sourced from Transfermarkt (2009–2026), containing 508 players and 9,764 individual valuation updates.
Data Architecture:
Diary of Price Tags: Fluctuating records containing date, market value (€M), and player age.
Player Card: Static metadata including player ID, name, league, position, and club.
Quarterly Panel Conversion: Standardized irregular valuation dates into uniform calendar quarters (Q1–Q4), carrying forward values across quiet quarters.
Cohort Selection Criteria: Applied four strict checks to isolate 15 well-covered players (3 best-covered players per Big 5 league: Premier League, La Liga, Serie A, Bundesliga, Ligue 1):
$\ge 6$ years of recorded valuation history.
$\ge 55%$ real (non-filled) quarterly valuations.
First valued by early 2019.
Actively valued through recent periods.
⚙️ Methodology & Model Performance
We evaluated candidate models against a Persistence benchmark across three evaluation windows:

Validation Origins (2020–2022 origins): Model selection stage.
Main Test Window (2023Q1–2024Q4): Out-of-sample performance evaluation.
Extra Holdout Period (2025Q2 & 2025Q4): Market regime shift stress test.
Model	Validation Log MAE	Test (2023–24) Log MAE	2025 Holdout Log MAE	Notes
Damped Holt (Selected)	0.424	0.297	0.335	Top performer in rising markets; dampens upward trend slope
SARIMAX AIC	0.427	0.311	0.356	Incorporates seasonal quarterly update structure
Persistence (Benchmark)	0.445	0.377	0.326	Standard baseline
Pooled Age Drift (Log)	0.485	0.344	0.279	Best performer during broad market downturns
Key Findings & Market Regime Shifts
Rising Market Champion: Damped Holt won the test window (2023–2024), beating the persistence benchmark by capturing upward trends without overshooting peaks.
The 2025 Market Downturn: In 2025, 11 of 15 cohort players lost value (median decline: −25%). In this declining regime, age-decay models (Pooled Age Drift) outperformed trend-extrapolation models.
80% Uncertainty Bands: Calibrated error ranges contained 93% of 2023–2024 test values and 20/30 of 2025 values. All 10 forecast misses fell below the lower bound, highlighting market downside risks.
🎯 Decision Support Prototype (Buy, Hold, Sell)
The interactive decision tool translates 6- and 12-month point forecasts and uncertainty bands into actionable executive guidance:

🟢 BUY / UNDERVALUED: Quoted fee sits below the 80% forecast uncertainty range (discount opportunity).
🟡 HOLD / EXTEND: Player value is projected to appreciate or remain steady relative to baseline (€M).
🔴 SELL WINDOW: Player market value is projected to decline below baseline (€M), signalling an opportunity to monetize before further asset depreciation.
Case Studies
Phil Foden (Premier League): Baseline value €140M. 12-month forecast €158.5M (80% range: €97M–€460M). A quoted fee of €475.4M is flagged as Overvalued, but Manchester City's core recommendation is Hold/Extend as a rising asset.
Ronald Araujo (La Liga): Baseline value €55M. 12-month forecast drops to €38M. Triggers a Sell Window recommendation to monetize before projected value depreciation.
⚠️ Limitations & Future Work
Selective Sample Size: Cohort restricted to 15 well-covered players; results may vary for younger or lower-tier players.
Market Value $\neq$ Negotiated Fee: Transfermarkt estimates theoretical worth; real transfer fees depend on contract leverage, injuries, club urgency, and bidding wars.
Regime Sensitivity: Models require dynamic recalibration across changing macroeconomic and market cycles.
Future Enhancements: Expand player coverage, integrate actual transfer transaction fees, incorporate on-pitch performance/injury metrics, and implement dynamic uncertainty bands.


📜 Project Info & Credits
Developed for OPIM 5671: Data Mining and Time Series Forecasting — Team 7.
