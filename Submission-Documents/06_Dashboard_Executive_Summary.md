# Dashboard Executive Summary
## NovaTech Solutions — Revenue Intelligence Dashboard
### Q2/Q3 2025 Pipeline & Forecast Report

**Prepared by:** Michael Adedayo-Dami  
**Dashboard Tool:** Power BI  
**Data Sources:** Salesforce CRM · Excel Forecast Model  
**Report Date:** June 2025  
**Reporting Period:** Q2–Q3 2025  

---

## Executive Overview

NovaTech Solutions currently has **$2,325,000 in active pipeline** across 22 opportunities spanning three regions — AMER, EMEA, and APAC. Seven sales representatives are working this pipeline against a combined annual quota of **$3,500,000**.

To date, the team has closed **$387,000 in revenue**, representing **11.1% quota attainment**. Under the Commit scenario — the most likely outcome based on current pipeline probabilities — the team is projected to reach **$1,322,150 by end of period**, or **37.8% of the annual quota target**.

Even in the Best Case scenario (×1.15 multiplier), the team reaches only **$1,520,473 — 43.4% of quota** — indicating a significant pipeline gap that must be addressed through accelerated deal creation, particularly in APAC and among underperforming reps.

---

## Key Metrics at a Glance

| Metric | Value |
|---|---|
| Total Pipeline | $2,325,000 |
| Average Deal Size | $105,682 |
| Total Opportunities | 22 |
| Regions Active | 3 (AMER, EMEA, APAC) |
| Sales Reps | 7 |
| Closed Won (to date) | $387,000 |
| Overall Quota Attainment | 11.1% |
| Team Annual Quota | $3,500,000 |
| Best Case Forecast | $1,520,473 |
| Commit Forecast | $1,322,150 |
| Worst Case Forecast | $1,057,720 |
| Best Case Attainment | 43.4% |
| Commit Attainment | 37.8% |
| Worst Case Attainment | 30.2% |

---

## Regional Performance Summary

| Region | Pipeline | Commit Forecast | % of Total Forecast |
|---|---|---|---|
| AMER | ~$890,000 | ~$502,000 | 38.0% |
| EMEA | ~$810,000 | ~$462,000 | 34.9% |
| APAC | ~$625,000 | ~$358,000 | 27.1% |

**AMER leads** in both pipeline volume and forecast contribution. **APAC is the weakest region** and represents the largest growth opportunity if rep activity and pipeline creation can be increased.

---

## Rep Performance Summary

| Rep | Closed Won | Attainment % | Gap to Quota |
|---|---|---|---|
| Rep 1 | $112,000 | 22.4% | -$388,000 |
| Rep 2 | $95,000 | 19.0% | -$405,000 |
| Rep 3 | $80,000 | 16.0% | -$420,000 |
| Rep 4 | $60,000 | 12.0% | -$440,000 |
| Rep 5 | $40,000 | 8.0% | -$460,000 |
| Rep 6 | $0 | 0.0% | -$500,000 |
| Rep 7 | $0 | 0.0% | -$500,000 |

**All seven reps are below quota.** Reps 6 and 7 have not closed any revenue to date and require immediate pipeline review and coaching intervention.

---

## Pipeline Health Analysis

### Stage Distribution
The pipeline is currently **top-heavy** — the majority of deals are sitting in early stages (Prospecting and Qualification). This indicates strong top-of-funnel activity but a risk of deals stalling before close.

| Stage | Opportunity Count | Est. Value |
|---|---|---|
| Prospecting | 6 | ~$520,000 |
| Qualification | 5 | ~$485,000 |
| Proposal | 4 | ~$440,000 |
| Negotiation | 3 | ~$393,000 |
| Closed Won | 4 | $387,000 |
| Closed Lost | 0 | $0 |

### Deal Size Insight
Average deal size increases through the pipeline stages, with **Negotiation-stage deals averaging ~$135K** — significantly above the $105,682 portfolio average. This suggests NovaTech's largest and most strategic deals are close to closing and represent a near-term revenue catalyst.

---

## Forecast Scenario Analysis

Three forecast scenarios were modeled to capture the range of possible outcomes:

| Scenario | Multiplier | Rationale | Full-Year Forecast | Attainment |
|---|---|---|---|---|
| Best Case | ×1.15 | All high-probability deals close; some upside deals accelerate | $1,520,473 | 43.4% |
| Commit | ×1.00 | Base expectation; deals close as probability-weighted | $1,322,150 | 37.8% |
| Worst Case | ×0.80 | Slippage in late-stage deals; Q3 deals push to Q4 | $1,057,720 | 30.2% |

**The gap between Best Case and Worst Case is $462,753** — representing the forecast risk range. Management should focus on protecting the 3 Negotiation-stage deals (combined value ~$393,000) from slipping, as these have an outsized impact on the Commit scenario.

---

## Strategic Recommendations

1. **Address the pipeline gap.** Even in Best Case, the team reaches only 43% of quota. A pipeline expansion initiative targeting 10–15 new qualified opportunities is needed to have a realistic path to quota.

2. **Activate Reps 6 and 7 immediately.** Zero Closed Won revenue from two reps by mid-year is a critical risk. A rep-level pipeline review, deal coaching, and potentially territory reassignment should be prioritised.

3. **Invest in APAC pipeline creation.** APAC contributes only 27% of total pipeline despite being one of three equal regions. Targeted outbound campaigns or partner-sourced leads should be directed to APAC reps.

4. **Protect Negotiation-stage deals.** Three deals worth ~$393,000 are in the final stage before close. Executive sponsorship or deal desk support for these opportunities should be engaged to prevent Q3 slippage.

5. **Refresh forecast monthly.** As new deals enter the pipeline and stage progression occurs, the Power BI model should be refreshed against the updated Salesforce export to keep scenarios current.

---

## Data Sources & Methodology

| Source | Description |
|---|---|
| Salesforce Developer Edition | 22 Opportunities across 22 Accounts; pipeline data entered manually; exported via NovaTech Pipeline Report Q2 Q3 2025 |
| Excel Workbook (5 tabs) | Pipeline Data · Best Case · Worst Case · Commit · PBI Data Model — weighted probability calculations and scenario modeling |
| Power BI Desktop | 4 report pages · 5 DAX measures · Import mode from Excel PBI Data Model tab |

**Weighted probability formula:** `Weighted Amount = Deal Amount × Stage Probability %`  
**Scenario formula:** `Scenario Forecast = SUM(Weighted Amount) × Scenario Multiplier`  
**Quota:** Flat $500,000 per rep annually × 7 reps = $3,500,000 team quota

---

## Deliverables Included in This Submission

| # | Deliverable | File |
|---|---|---|
| 1 | Salesforce Pipeline Report Screenshot | `M1-Revenue-Forecast/NovaTech_Pipeline_Report_Screenshot.png` |
| 2 | Power BI Pipeline Overview (Marketing Funnel) | `M1-Revenue-Forecast/NovaTech_Pipeline_Overview_Screenshot.png` |
| 3 | Power BI Quota Attainment (Sales Pipeline) | `M1-Revenue-Forecast/NovaTech_Quota_Attainment_Screenshot.png` |
| 4 | Power BI Forecast vs Target (Customer Health) | `M1-Revenue-Forecast/NovaTech_Forecast_vs_Target_Screenshot.png` |
| 5 | Power BI Scenario Comparison | `M1-Revenue-Forecast/NovaTech_Scenario_Comparison_Screenshot.png` |
| 6 | Excel Forecast Workbook | `M1-Revenue-Forecast/NovaTech_M1_Revenue_Forecast_Model.xlsx` |
| 7 | Power BI Dashboard File | `M1-Revenue-Forecast/NovaTech_M1_Revenue_Forecast_Dashboard.pbix` |
| 8 | Verification Log (7 entries) | `Submission-Documents/01_Verification_Log.md` |
| 9 | Data Transformation Documentation | `Submission-Documents/02_Data_Transformation_Documentation.md` |
| 10 | Dashboard Summary — All 3 Sheets | `Submission-Documents/03_Dashboard_Summary_All_Sheets.md` |
| 11 | Before/After Topic Q&A Documentation | `Submission-Documents/04_Before_After_Topic_QA_Documentation.md` |
| 12 | Q Exploration Log (8 entries) | `Submission-Documents/05_Q_Exploration_Log.md` |
| 13 | This Executive Summary | `Submission-Documents/06_Dashboard_Executive_Summary.md` |
| 14 | Permission Architecture (H1) | `H1-Permission-Architecture/` folder |
| 15 | Lead Scoring Configuration (E1) | `E1-Lead-Scoring/` folder |

---

*NovaTech Solutions is a fictional B2B SaaS company created for portfolio demonstration purposes. All data, opportunities, accounts, and revenue figures are fabricated for educational use.*

*LinkedIn: https://www.linkedin.com/in/michael-adedayo-dami/*
