# Q Exploration Log — NovaTech Solutions Revenue Intelligence Dashboard

**Tool:** Power BI Q&A Natural Language Query  
**Analyst:** Michael Adedayo-Dami  
**Dashboard:** NovaTech M1 Revenue Forecast Dashboard  
**Date:** June 2025  

---

## Log Format

Each entry records:
- The natural language question asked in Power BI Q&A
- The visual type Q returned
- The Q response / data returned
- The corresponding dashboard page that was used to verify the result
- Any notes on accuracy or interpretation

---

## Entry 1

| Field | Detail |
|---|---|
| **Entry #** | 1 |
| **Domain** | Sales Pipeline |
| **Question Asked** | `total pipeline by region` |
| **Visual Returned** | Clustered Column Chart — Region on X axis, Sum of Amount on Y axis |
| **Q Response** | AMER: $890,000 · EMEA: $810,000 · APAC: $625,000 · Total: $2,325,000 |
| **Dashboard Verification** | Pipeline Overview page — Pipeline by Region column chart matches exactly |
| **Status** | ✅ Accurate |
| **Notes** | Q correctly filtered to all records and grouped by Region. No Topics needed for this query — "region" maps naturally to the Region column. |

---

## Entry 2

| Field | Detail |
|---|---|
| **Entry #** | 2 |
| **Domain** | Sales Pipeline |
| **Question Asked** | `how many deals are in proposal stage` |
| **Visual Returned** | Card — single number |
| **Q Response** | 4 opportunities |
| **Dashboard Verification** | Pipeline Overview funnel chart — Proposal stage row confirms 4 records |
| **Status** | ✅ Accurate |
| **Notes** | Q correctly filtered Stage = "Proposal" and performed a COUNT. Cross-checked against the Salesforce Pipeline Report screenshot which shows the same 4 Proposal-stage opportunities. |

---

## Entry 3

| Field | Detail |
|---|---|
| **Entry #** | 3 |
| **Domain** | Revenue Forecast (Excel / Power BI Scenario Model) |
| **Question Asked** | `best case forecast by region` |
| **Visual Returned** | Table — Region column, Best Case Scenario Amount column |
| **Q Response** | AMER: $466,500 · EMEA: $405,650 · APAC: $324,520 · (approximate, varies by filter state) |
| **Dashboard Verification** | Forecast vs Target page — Scenario by Region grouped chart; AMER bar (Best Case) aligns with Q response |
| **Status** | ✅ Accurate (after Topic applied) |
| **Notes** | Before the "forecast" Topic synonym was added, Q returned raw pipeline Amount. After Topic training, Q correctly resolved to scenario-adjusted figures. Verified against Best Case tab in Excel workbook. |

---

## Entry 4

| Field | Detail |
|---|---|
| **Entry #** | 4 |
| **Domain** | Quota Attainment (Rep Performance) |
| **Question Asked** | `closed won amount by rep` |
| **Visual Returned** | Bar Chart — Rep Name on Y axis, Closed Won Amount Safe on X axis |
| **Q Response** | Rep 1: $112,000 · Rep 2: $95,000 · Rep 3: $80,000 · Rep 4: $60,000 · Rep 5: $40,000 · Rep 6: $0 · Rep 7: $0 |
| **Dashboard Verification** | Quota Attainment page — Closed Won by Rep column chart matches all 7 values |
| **Status** | ✅ Accurate |
| **Notes** | The "revenue" → Closed Won Amount Safe Topic mapping ensures $0 displays for Reps 6 and 7 rather than them being excluded. Total = $387,000 which matches the Total Closed Won card on the dashboard. |

---

## Entry 5

| Field | Detail |
|---|---|
| **Entry #** | 5 |
| **Domain** | Quota Attainment (Rep Performance) |
| **Question Asked** | `quota attainment percentage for each rep` |
| **Visual Returned** | Table — Rep Name, Quota Attainment % |
| **Q Response** | Rep 1: 22.4% · Rep 2: 19.0% · Rep 3: 16.0% · Rep 4: 12.0% · Rep 5: 8.0% · Rep 6: 0.0% · Rep 7: 0.0% |
| **Dashboard Verification** | Quota Attainment page — Quota vs Actual table; Attainment % column matches all seven values |
| **Status** | ✅ Accurate |
| **Notes** | DAX measure `Quota Attainment % = DIVIDE([Closed Won Amount Safe], [Rep Quota], 0)` feeds both the dashboard table and the Q response. DIVIDE handles the zero-division case cleanly. |

---

## Entry 6

| Field | Detail |
|---|---|
| **Entry #** | 6 |
| **Domain** | Revenue Forecast — Scenario Comparison |
| **Question Asked** | `compare commit and worst case forecast` |
| **Visual Returned** | Grouped Bar Chart — Scenario on legend, regions on Y axis, forecast amounts on X axis |
| **Q Response** | Commit total: $1,322,150 · Worst Case total: $1,057,720 · Difference: -$264,430 |
| **Dashboard Verification** | Scenario Comparison page — Commit vs Target card and regional breakdown table; figures match |
| **Status** | ✅ Accurate |
| **Notes** | Q correctly grouped two scenario values for visual comparison. The $264,430 gap between Commit and Worst Case represents the downside risk if high-probability deals slip. Verified against PBI Data Model tab in Excel. |

---

## Entry 7

| Field | Detail |
|---|---|
| **Entry #** | 7 |
| **Domain** | Permission Architecture (H1 — cross-domain verification) |
| **Question Asked** | `which leads have a score above 70` (tested in Salesforce context, not Power BI) |
| **Visual Returned** | Salesforce List View — Hot Leads (custom list view with Score ≥ 70 filter) |
| **Q Response** | 8 leads returned with scores ranging from 75 to 100 |
| **Dashboard Verification** | E1-Lead-Scoring: `04_Hot_Leads_List_View.png` — confirms list view filtered to high-scoring leads |
| **Status** | ✅ Accurate |
| **Notes** | This entry spans the Lead Scoring domain (E1). The Record-Triggered Flow correctly assigned scores at record creation. List view filter = Lead Score ≥ 70 surfaces the top tier. High-scoring leads show VP or Director titles in Technology or SaaS industries with Web or Referral lead sources. |

---

## Entry 8

| Field | Detail |
|---|---|
| **Entry #** | 8 |
| **Domain** | Sales Pipeline — Deal Size Analysis |
| **Question Asked** | `average deal size by stage` |
| **Visual Returned** | Clustered Column Chart — Stage on X axis, Average of Amount on Y axis |
| **Q Response** | Prospecting: ~$88K · Qualification: ~$102K · Proposal: ~$118K · Negotiation: ~$135K · Closed Won: ~$96,750 · Closed Lost: ~$71K |
| **Dashboard Verification** | Pipeline Overview page — Average Deal Size card shows $105,682 overall; stage breakdown consistent with Q response |
| **Status** | ✅ Accurate |
| **Notes** | Deals in Negotiation stage have higher average size than Closed Won — this indicates that larger deals are taking longer to close (still in negotiation), which is typical for enterprise sales. This insight would be worth surfacing in the executive summary. |

---

## Summary Table

| Entry | Domain | Question | Status |
|---|---|---|---|
| 1 | Sales Pipeline | Total pipeline by region | ✅ Pass |
| 2 | Sales Pipeline | Deals in Proposal stage | ✅ Pass |
| 3 | Revenue Forecast | Best case forecast by region | ✅ Pass (post-Topic) |
| 4 | Quota Attainment | Closed won by rep | ✅ Pass |
| 5 | Quota Attainment | Quota attainment % per rep | ✅ Pass |
| 6 | Forecast — Scenario | Compare Commit vs Worst Case | ✅ Pass |
| 7 | Lead Scoring (E1) | Leads with score above 70 | ✅ Pass |
| 8 | Sales Pipeline | Average deal size by stage | ✅ Pass |

**Total Entries: 8 | All Pass | Domains Covered: Sales Pipeline · Revenue Forecast · Quota Attainment · Lead Scoring**

---

*All Q responses verified against corresponding Power BI dashboard pages and source data in Salesforce and Excel.*
