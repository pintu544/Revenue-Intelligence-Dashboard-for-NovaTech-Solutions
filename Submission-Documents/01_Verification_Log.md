# Verification Log — NovaTech Solutions Revenue Intelligence Dashboard

**Project:** NovaTech Solutions — Revenue Intelligence Dashboard  
**Analyst:** Michael Adedayo-Dami  
**Tool:** Power BI (with Salesforce + Excel data sources)  
**Date Completed:** June 2025  

---

## Template Key

| Column | Description |
|---|---|
| Entry # | Sequential log number |
| Domain | Which knowledge base / data domain was tested |
| Question Asked | The natural language question or query tested |
| Expected Result | What the correct answer should be based on source data |
| Actual Result | What the dashboard or Q returned |
| Status | PASS / FAIL / PARTIAL |
| Notes | Any discrepancies or follow-up actions |

---

## Verification Entries

---

### Entry 1

| Field | Value |
|---|---|
| **Entry #** | 1 |
| **Domain** | Sales Pipeline (Salesforce Opportunities) |
| **Question Asked** | What is the total pipeline value across all regions? |
| **Expected Result** | $2,325,000 (sum of all 22 opportunities across AMER, EMEA, APAC) |
| **Actual Result** | $2,325,000 |
| **Status** | ✅ PASS |
| **Notes** | Dashboard Pipeline Overview card matches Excel Pipeline Data tab SUMPRODUCT total exactly. |

---

### Entry 2

| Field | Value |
|---|---|
| **Entry #** | 2 |
| **Domain** | Sales Pipeline (Salesforce Opportunities) |
| **Question Asked** | How many open opportunities are currently in the pipeline? |
| **Expected Result** | 22 opportunities (all manually entered in Salesforce Developer Edition) |
| **Actual Result** | 22 |
| **Status** | ✅ PASS |
| **Notes** | Salesforce Pipeline Report Q2 Q3 2025 confirms all 22 rows. Power BI funnel stage breakdown accounts for all 22 records. |

---

### Entry 3

| Field | Value |
|---|---|
| **Entry #** | 3 |
| **Domain** | Revenue Forecast (Excel Scenario Model) |
| **Question Asked** | What is the Best Case forecast for the full team? |
| **Expected Result** | $1,520,473 (weighted pipeline × 1.15 multiplier) |
| **Actual Result** | $1,520,473 |
| **Status** | ✅ PASS |
| **Notes** | Best Case tab in Excel workbook matches the Best Case headline card on the Forecast vs Target Power BI page. DAX measure pulls correctly from PBI Data Model flat table. |

---

### Entry 4

| Field | Value |
|---|---|
| **Entry #** | 4 |
| **Domain** | Revenue Forecast (Excel Scenario Model) |
| **Question Asked** | What is the Worst Case forecast and how does it compare to the team quota? |
| **Expected Result** | Worst Case = $1,057,720; Team Quota = $3,500,000; Gap = -$2,442,280 |
| **Actual Result** | Worst Case $1,057,720 displayed; Quota $3,500,000 confirmed; gap visible in Scenario Comparison page |
| **Status** | ✅ PASS |
| **Notes** | Gap to Quota DAX measure (Gap to Quota = Rep Quota - Closed Won Amount Safe) confirms the shortfall per rep. Aggregate matches hand-calculated total. |

---

### Entry 5

| Field | Value |
|---|---|
| **Entry #** | 5 |
| **Domain** | Quota Attainment (Rep-level Performance) |
| **Question Asked** | Which rep has the highest closed-won revenue and what is their attainment percentage? |
| **Expected Result** | Top rep varies by close date filter; overall Closed Won to date = $387,000; overall attainment = 11.1% |
| **Actual Result** | $387,000 Closed Won; 11.1% attainment shown on Quota Attainment page |
| **Status** | ✅ PASS |
| **Notes** | Closed Won Amount Safe DAX measure correctly returns $0 for reps with no closed deals rather than BLANK, preventing visual errors in the column chart. Attainment % formula = Closed Won / (Rep Quota × 7 reps) confirmed manually. |

---

### Entry 6

| Field | Value |
|---|---|
| **Entry #** | 6 |
| **Domain** | Permission & Security Architecture (H1) |
| **Question Asked** | Does the Sales Rep role have access to view all Opportunity records org-wide? |
| **Expected Result** | No — OWD for Opportunity is set to Private. Sales Reps see only their own records unless a sharing rule grants additional access. |
| **Actual Result** | Confirmed Private OWD in Salesforce Setup (screenshot: 02_OWD_Settings.jpg). Sales Rep role sits below Sales Manager in role hierarchy so manager roll-up gives manager visibility, not peers. |
| **Status** | ✅ PASS |
| **Notes** | H1 Permission Architecture decision matrix documents the exact business reason: reps should not see competitor colleagues' pipeline to prevent sandbagging or cherry-picking. |

---

### Entry 7

| Field | Value |
|---|---|
| **Entry #** | 7 |
| **Domain** | Lead Scoring Automation (E1) |
| **Question Asked** | Does a Lead with Job Title = "VP", Industry = "Technology", and Lead Source = "Web" receive the maximum score? |
| **Expected Result** | Score = 100 (VP title = 30pts, Technology industry = 25pts, company size bonus = 20pts, Web lead source = 25pts) |
| **Actual Result** | Flow correctly assigns 100 when all four high-value criteria are met simultaneously. Confirmed via Flow debug trace and Hot Leads list view (score filter ≥ 70). |
| **Status** | ✅ PASS |
| **Notes** | Record-Triggered Flow uses assignment elements with cumulative score logic. Each criterion adds to the score independently so there is no override risk between branches. |

---

## Summary

| Domain | Entries | All Pass? |
|---|---|---|
| Sales Pipeline (Salesforce) | 1, 2 | ✅ Yes |
| Revenue Forecast (Excel / Power BI) | 3, 4 | ✅ Yes |
| Quota Attainment (Power BI DAX) | 5 | ✅ Yes |
| Permission Architecture (H1) | 6 | ✅ Yes |
| Lead Scoring Automation (E1) | 7 | ✅ Yes |

**Total Entries: 7 | Pass: 7 | Fail: 0**

---

*Verification completed against source data in Salesforce Developer Edition, Excel workbook tabs, and Power BI report pages.*
