# Dashboard Summary — All Report Sheets
## NovaTech Solutions Revenue Intelligence Dashboard

**Tool:** Power BI Desktop  
**Source File:** `NovaTech_M1_Revenue_Forecast_Dashboard.pbix`  
**Analyst:** Michael Adedayo-Dami  
**Date:** June 2025  

> **Note:** Screenshots for each dashboard page are included in the `M1-Revenue-Forecast/` folder.  
> PDF export of all pages is represented by this structured summary document alongside the `.pbix` file.

---

## Sheet 1 — Marketing Funnel (Pipeline Overview)

**File Reference:** `NovaTech_Pipeline_Overview_Screenshot.png`

### Purpose
Provides a top-level view of the total sales pipeline and how deals are distributed across stages and regions. Answers the question: *How healthy is our pipeline right now?*

### Visuals on This Page

| Visual | Type | Key Data Points |
|---|---|---|
| Total Pipeline | Card | $2,325,000 |
| Average Deal Size | Card | $105,682 |
| Pipeline by Region | Clustered Column Chart | AMER: ~$890K · EMEA: ~$810K · APAC: ~$625K |
| Deal Stage Funnel | Funnel Chart | Prospecting → Qualification → Proposal → Negotiation → Closed Won → Closed Lost |

### Key Insights

- **AMER leads pipeline volume** at approximately 38% of total, followed by EMEA at ~35% and APAC at ~27%.
- **Average deal size of $105,682** reflects a mid-market B2B deal profile consistent with NovaTech's target segment.
- The funnel shows the largest volume sitting in **Prospecting and Qualification** stages, indicating a top-heavy pipeline that requires nurturing to convert.
- **Closed Won so far represents $387,000** out of $2,325,000 total pipeline — approximately 16.6% conversion of entered pipeline to date.

### Filters Available
- Region slicer (AMER / EMEA / APAC)
- Stage slicer
- Close Date range filter

---

## Sheet 2 — Sales Pipeline (Quota Attainment)

**File Reference:** `NovaTech_Quota_Attainment_Screenshot.png`

### Purpose
Shows individual rep performance against a $500,000 annual quota. Answers the question: *Who is on track, who is behind, and by how much?*

### Visuals on This Page

| Visual | Type | Key Data Points |
|---|---|---|
| Closed Won by Rep | Clustered Column Chart | Revenue closed per rep; reps with $0 show bar at zero (not blank) |
| Quota vs Actual Table | Table | Rep Name · Closed Won · Quota · Attainment % · Gap to Quota |
| Overall Attainment % | Card | 11.1% |
| Total Closed Won | Card | $387,000 |

### Quota Attainment by Rep

| Rep | Closed Won | Quota | Attainment % | Gap to Quota |
|---|---|---|---|---|
| Rep 1 | $112,000 | $500,000 | 22.4% | -$388,000 |
| Rep 2 | $95,000 | $500,000 | 19.0% | -$405,000 |
| Rep 3 | $80,000 | $500,000 | 16.0% | -$420,000 |
| Rep 4 | $60,000 | $500,000 | 12.0% | -$440,000 |
| Rep 5 | $40,000 | $500,000 | 8.0% | -$460,000 |
| Rep 6 | $0 | $500,000 | 0.0% | -$500,000 |
| Rep 7 | $0 | $500,000 | 0.0% | -$500,000 |
| **Total** | **$387,000** | **$3,500,000** | **11.1%** | **-$3,113,000** |

### Key Insights

- **No rep has exceeded 25% attainment** at this stage of the year, which is expected given Q2/Q3 pipeline timing.
- **Two reps have $0 Closed Won** — the Closed Won Amount Safe DAX measure ensures these display as $0 bars rather than disappearing from the chart.
- The overall **11.1% attainment rate** reflects early-stage pipeline; the Commit forecast of $1.32M would bring the team to approximately 37.8% attainment if all commit-stage deals close.

---

## Sheet 3 — Customer Health (Forecast vs Target + Scenario Comparison)

**File References:** `NovaTech_Forecast_vs_Target_Screenshot.png` · `NovaTech_Scenario_Comparison_Screenshot.png`

### Purpose
Projects final revenue outcomes under three scenarios and compares them against the team quota target. Answers the question: *Will we hit our number, and what does each scenario look like?*

---

### Sub-Sheet 3A — Forecast vs Target

| Visual | Type | Key Data Points |
|---|---|---|
| Best Case Forecast | Card | $1,520,473 |
| Commit Forecast | Card | $1,322,150 |
| Worst Case Forecast | Card | $1,057,720 |
| Total Team Quota | Card | $3,500,000 |
| Scenario by Region | Grouped Column Chart | Best / Commit / Worst per region side by side |

**Scenario Summary Table**

| Scenario | Forecast | vs Quota | Attainment |
|---|---|---|---|
| Best Case (×1.15) | $1,520,473 | -$1,979,527 | 43.4% |
| Commit (×1.00) | $1,322,150 | -$2,177,850 | 37.8% |
| Worst Case (×0.80) | $1,057,720 | -$2,442,280 | 30.2% |

**Regional Breakdown — Commit Scenario**

| Region | Commit Forecast |
|---|---|
| AMER | ~$502,000 |
| EMEA | ~$462,000 |
| APAC | ~$358,000 |

---

### Sub-Sheet 3B — Scenario Comparison

| Visual | Type | Key Data Points |
|---|---|---|
| Commit vs Target | Card pair | $1,322,150 vs $3,500,000 |
| Scenario Forecast by Rep | Horizontal Bar Chart | Best / Commit / Worst bars per rep |
| Regional Scenario Breakdown | Table | Region · Best · Commit · Worst columns |

### Key Insights

- **Even in the Best Case, the team reaches only 43.4% of quota.** This highlights that the current pipeline ($2.3M) is insufficient to hit $3.5M — the team needs either higher-probability deals in later stages or a larger top-of-funnel.
- **AMER consistently leads across all scenarios** due to the highest volume of opportunities by amount.
- The scenario comparison by rep shows **wide variance between reps** — top reps contribute 3–4× the weighted pipeline of bottom-tier reps.
- **Actionable insight:** Focus pipeline-building efforts on APAC (lowest regional contribution) and activate the two reps currently at $0 Closed Won.

---

## Dashboard Design Notes

- **Color scheme:** Blue primary (#0070C0), grey secondary (#595959), white background — consistent with NovaTech corporate branding guidelines.
- **Currency format:** All monetary values formatted as USD with comma separators, no decimal places on cards.
- **Responsiveness:** Dashboard built at standard 16:9 (1280×720) for presentation and PDF export compatibility.
- **Data refresh:** Currently import mode from Excel. For live use, the Excel file would be hosted on SharePoint with scheduled refresh configured in Power BI Service.

---

*Dashboard built in Power BI Desktop. Full interactive version available in `NovaTech_M1_Revenue_Forecast_Dashboard.pbix`.*
