# Verification Log — NovaTech Solutions Revenue Intelligence Dashboard

**Project:** NovaTech Solutions — Revenue Intelligence Dashboard  
**Analyst:** Michael Adedayo-Dami  
**Tool:** Amazon QuickSight (SPICE) + Power BI  
**Data Sources (Knowledge Bases):**  
- Knowledge Base 1: Marketing Leads (`marketing_leads.csv` — 1,250 rows, 12 columns)  
- Knowledge Base 2: Sales Opportunities (`sales_opportunities.csv` — 22 rows, 10 columns)  
- Knowledge Base 3: Customer Health (`customer_health.csv` — 22 rows, 9 columns)  
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

---

## Additional Entries — Explicit Knowledge Base Coverage

---

### Entry 8 — Knowledge Base 1: Marketing Leads CSV

| Field | Value |
|---|---|
| **Entry #** | 8 |
| **Knowledge Base** | KB1 — Marketing Leads (`marketing_leads.csv`) |
| **Question Asked** | What is the total lead count and average lead score across all 1,250 records? |
| **Expected Result** | Total leads = 1,250; Average lead score = 64.3 (calculated from source CSV) |
| **Actual Result** | SPICE dataset shows 1,250 rows imported; QuickSight KPI card shows AVG(lead_score) = 64.3 |
| **Status** | ✅ PASS |
| **Notes** | Row count verified in SPICE dataset preview. `lead_score` was corrected from String to Integer before SPICE ingestion — confirms data type correction was applied correctly. Screenshot: `SPICE_Import_Marketing_Leads.png` |

---

### Entry 9 — Knowledge Base 1: Marketing Leads CSV — Funnel Conversion

| Field | Value |
|---|---|
| **Entry #** | 9 |
| **Knowledge Base** | KB1 — Marketing Leads (`marketing_leads.csv`) |
| **Question Asked** | How many leads have a status of "Qualified" and what percentage of total leads does this represent? |
| **Expected Result** | 312 Qualified leads = 24.96% of 1,250 total |
| **Actual Result** | QuickSight filter on status = "Qualified" returns 312; KPI card shows 25% conversion rate |
| **Status** | ✅ PASS |
| **Notes** | Verified by applying status filter in SPICE dataset preview and cross-checking against the Funnel chart on Sheet 1 (Marketing Funnel). |

---

### Entry 10 — Knowledge Base 2: Sales Opportunities CSV

| Field | Value |
|---|---|
| **Entry #** | 10 |
| **Knowledge Base** | KB2 — Sales Opportunities (`sales_opportunities.csv`) |
| **Question Asked** | Does the total pipeline value in QuickSight match the source CSV after data type correction on the Amount field? |
| **Expected Result** | SUM(amount) = $2,325,000 across 22 rows; matches Excel Pipeline Data tab |
| **Actual Result** | QuickSight SPICE dataset SUM(amount) = $2,325,000; Pipeline Overview KPI card confirms |
| **Status** | ✅ PASS |
| **Notes** | `amount` field was corrected from formatted String ("$105,000") to Decimal before SPICE ingestion. Post-correction sum matches the source data exactly. Screenshot: `SPICE_Import_Sales_Opportunities.png` |

---

### Entry 11 — Knowledge Base 2: Sales Opportunities CSV — Probability Field

| Field | Value |
|---|---|
| **Entry #** | 11 |
| **Knowledge Base** | KB2 — Sales Opportunities (`sales_opportunities.csv`) |
| **Question Asked** | Are probability values stored as decimals (0.75) rather than percentages (75%) after data type correction? |
| **Expected Result** | All probability values between 0.0 and 1.0; weighted_amount = amount × probability |
| **Actual Result** | QuickSight field preview shows probability values as decimals; SUM(weighted_amount) = $1,322,150 (Commit scenario) confirms correct calculation |
| **Status** | ✅ PASS |
| **Notes** | `probability` was corrected from String "75%" to Decimal 0.75 during dataset edit. Weighted amount formula verified: $105,000 × 0.75 = $78,750 for one sample record — confirmed in SPICE preview. |

---

### Entry 12 — Knowledge Base 3: Customer Health CSV

| Field | Value |
|---|---|
| **Entry #** | 12 |
| **Knowledge Base** | KB3 — Customer Health (`customer_health.csv`) |
| **Question Asked** | How many accounts are flagged "At Risk" and what is their combined contract value? |
| **Expected Result** | 5 At Risk accounts; combined contract_value ≈ $487,000 |
| **Actual Result** | QuickSight filter on risk_flag = "At Risk" returns 5 accounts; SUM(contract_value) for this segment = $487,000 |
| **Status** | ✅ PASS |
| **Notes** | `contract_value` was corrected from String to Decimal. `health_score` corrected from String to Integer. Both corrections confirmed in SPICE dataset field type preview. Screenshot: `SPICE_Import_Customer_Health.png` |

---

### Entry 13 — Knowledge Base 3: Customer Health CSV — Join Verification

| Field | Value |
|---|---|
| **Entry #** | 13 |
| **Knowledge Base** | KB3 — Customer Health (via Unified Join) |
| **Question Asked** | Does the unified joined dataset preserve all 22 opportunity records when joined to Customer Health? |
| **Expected Result** | Left join on opportunity_id = account_id preserves all 22 rows; no records dropped |
| **Actual Result** | NovaTech_Unified_Dashboard SPICE dataset shows 22 rows with all Customer Health columns populated |
| **Status** | ✅ PASS |
| **Notes** | Left join configuration confirmed in join diagram screenshot (`SPICE_Join_Diagram.png`). All 22 accounts have matching records in both datasets — no nulls in joined Customer Health fields. |

---

## Updated Summary

| Entry | Knowledge Base | Domain | Status |
|---|---|---|---|
| 1 | KB2 | Sales Pipeline — Total Value | ✅ Pass |
| 2 | KB2 | Sales Pipeline — Opportunity Count | ✅ Pass |
| 3 | KB2 | Revenue Forecast — Best Case | ✅ Pass |
| 4 | KB2 | Revenue Forecast — Worst Case | ✅ Pass |
| 5 | KB2 | Quota Attainment — Rep Level | ✅ Pass |
| 6 | KB2/H1 | Permission Architecture | ✅ Pass |
| 7 | KB1/E1 | Lead Scoring Automation | ✅ Pass |
| 8 | **KB1** | Marketing Leads — Row Count & Score | ✅ Pass |
| 9 | **KB1** | Marketing Leads — Funnel Conversion | ✅ Pass |
| 10 | **KB2** | Sales Opportunities — Amount Field | ✅ Pass |
| 11 | **KB2** | Sales Opportunities — Probability Field | ✅ Pass |
| 12 | **KB3** | Customer Health — At-Risk Accounts | ✅ Pass |
| 13 | **KB3** | Customer Health — Join Integrity | ✅ Pass |

**Total Entries: 13 | All Pass | All 3 Knowledge Bases Explicitly Covered ✅**
