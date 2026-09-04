# Dashboard Interactive Features Documentation
## NovaTech Solutions — Amazon QuickSight Dashboard

**Tool:** Amazon QuickSight  
**Analyst:** Michael Adedayo-Dami  
**Date:** June 2025  

---

## Overview

This document evidences the interactive features built across all three dashboard sheets:
- KPI summary cards on every sheet
- Filter controls on at least two sheets
- One-click filtering actions (Actions) on at least one sheet
- Cross-sheet navigation between sheets

---

## Sheet 1 — Marketing Funnel

### KPI Summary Cards

| Card | Metric | Value | Field Used |
|---|---|---|---|
| Total Leads | COUNT(lead_id) | 1,250 | Marketing_Leads.lead_id |
| Average Lead Score | AVG(lead_score) | 64.3 | Marketing_Leads.lead_score |
| Qualified Leads | COUNT where status = "Qualified" | 312 | Marketing_Leads.status |
| Top Lead Source | MODE(lead_source) | Web | Marketing_Leads.lead_source |

### Visualisations

| Visual | Type | X Axis / Dimension | Y Axis / Metric | Purpose |
|---|---|---|---|---|
| Leads by Source | Donut Chart | lead_source | COUNT(lead_id) | Shows which channels drive the most leads |
| Lead Score Distribution | Histogram | lead_score (binned) | COUNT(lead_id) | Reveals score concentration and quality spread |
| Leads by Industry | Horizontal Bar | industry | COUNT(lead_id) | Identifies highest-volume industries |
| Lead Conversion Funnel | Funnel Chart | status (New→Contacted→Qualified) | COUNT(lead_id) | Visualises drop-off at each funnel stage |
| Leads Over Time | Line Chart | created_date (monthly) | COUNT(lead_id) | Tracks lead volume trend over time |
| Lead Score by Source | Box Plot | lead_source | lead_score | Compares quality (score) across channels |

### Filter Controls ✅

| Filter | Type | Field | Scope |
|---|---|---|---|
| Region Filter | Dropdown (multi-select) | region | All visuals on this sheet |
| Date Range Filter | Date Picker (relative range) | created_date | Lead trend line + funnel |
| Lead Source Filter | Checkbox list | lead_source | All visuals on this sheet |

**Screenshot Reference:** `Filter_Controls_Marketing_Funnel.png` — shows the filter panel on the left side of Sheet 1 with all three filter controls visible and a region dropdown open showing AMER / EMEA / APAC options.

### One-Click Filter Action ✅

**Action configured:** Click on any bar in the "Leads by Industry" bar chart → filters ALL other visuals on the sheet to show only leads from that industry.

**Action configuration:**
- Action type: Filter action
- Source visual: Leads by Industry (bar chart)
- Target visuals: All other visuals on Sheet 1 (Donut, Histogram, Funnel, Line, Box Plot)
- Field used: industry
- Trigger: Click on bar segment

**Screenshot Reference:** `OneClick_Filter_Action_Sheet1.png` — shows the Actions configuration panel with "Filter same-sheet visuals" enabled and all target visuals checked, plus a second screenshot showing the sheet after clicking "Technology" bar — all other charts filtered to Technology industry only.

### Cross-Sheet Navigation ✅

**Navigation button:** "View Sales Pipeline →" button in the top-right corner of Sheet 1.

- Button type: Custom navigation action
- Destination sheet: Sheet 2 — Sales Pipeline
- Behaviour: Clicking the button takes the user to Sheet 2 and passes the currently selected Region filter as a cross-sheet parameter

**Screenshot Reference:** `Navigation_Button_Sheet1_to_Sheet2.png` — shows the button visible on Sheet 1 and the navigation action configuration panel showing destination = "Sales Pipeline" sheet.

---

## Sheet 2 — Sales Pipeline

### KPI Summary Cards

| Card | Metric | Value | Field Used |
|---|---|---|---|
| Total Pipeline Value | SUM(amount) | $2,325,000 | Opportunities.amount |
| Average Deal Size | AVG(amount) | $105,682 | Opportunities.amount |
| Open Opportunities | COUNT(opportunity_id) | 22 | Opportunities.opportunity_id |
| Weighted Pipeline | SUM(weighted_amount) | $1,322,150 | Opportunities.weighted_amount |

### Visualisations

| Visual | Type | X Axis / Dimension | Y Axis / Metric | Purpose |
|---|---|---|---|---|
| Pipeline by Stage | Funnel Chart | stage | SUM(amount) | Shows deal volume and value at each stage |
| Pipeline by Region | Clustered Bar | region | SUM(amount) | Compares regional pipeline strength |
| Quota Attainment by Rep | Bullet Chart | rep_name | Closed Won vs $500K quota | Shows each rep's progress to target |
| Deal Size vs Probability | Scatter Plot | probability | amount | Identifies high-value high-probability deals |
| Pipeline Trend | Line Chart | close_date (monthly) | SUM(amount) | Forecast timing of expected revenue |
| Stage Breakdown Table | Table | opportunity_name, stage, amount, rep, close_date | — | Detailed deal list for manager review |

### Filter Controls ✅

| Filter | Type | Field | Scope |
|---|---|---|---|
| Region Filter | Dropdown (multi-select) | region | All visuals on this sheet |
| Stage Filter | Checkbox list | stage | Funnel, scatter, table |
| Rep Filter | Dropdown (multi-select) | rep_name | Quota chart, table, pipeline by region |
| Close Date Range | Date slider | close_date | Pipeline trend, table |

**Screenshot Reference:** `Filter_Controls_Sales_Pipeline.png` — shows all four filter controls visible in the filter panel with the Stage filter open, showing all six pipeline stages as checkboxes.

### One-Click Filter Action ✅

**Action configured:** Click on any region bar in "Pipeline by Region" → filters the Stage Breakdown Table and Quota Attainment chart to show only deals from that region.

**Action configuration:**
- Action type: Filter action
- Source visual: Pipeline by Region (bar chart)
- Target visuals: Stage Breakdown Table + Quota Attainment Bullet Chart
- Field used: region
- Trigger: Click on bar

**Screenshot Reference:** `OneClick_Filter_Action_Sheet2.png` — shows Sheet 2 after clicking the EMEA bar; the table below filters to EMEA deals only and the quota chart updates to show EMEA reps.

### Cross-Sheet Navigation ✅

**Navigation button 1:** "← Back to Marketing Funnel" button in top-left of Sheet 2  
**Navigation button 2:** "View Customer Health →" button in top-right of Sheet 2

Both buttons pass the active Region filter as a cross-sheet parameter to maintain filter context when navigating.

**Screenshot Reference:** `Navigation_Buttons_Sheet2.png` — shows both navigation buttons visible on Sheet 2, with the navigation action configuration panel open for the "Customer Health" button.

---

## Sheet 3 — Customer Health

### KPI Summary Cards

| Card | Metric | Value | Field Used |
|---|---|---|---|
| Average Health Score | AVG(health_score) | 71.4 | Customer_Health.health_score |
| At-Risk Accounts | COUNT where risk_flag = "At Risk" | 5 | Customer_Health.risk_flag |
| Total Contract Value | SUM(contract_value) | $2,187,000 | Customer_Health.contract_value |
| Open Support Tickets | SUM(support_tickets_open) | 34 | Customer_Health.support_tickets_open |

### Visualisations

| Visual | Type | X Axis / Dimension | Y Axis / Metric | Purpose |
|---|---|---|---|---|
| Health Score by Account | Horizontal Bar (colour-coded) | account_name | health_score | Red/Amber/Green coded by risk tier |
| Risk Distribution | Donut Chart | risk_flag | COUNT(account_id) | At Risk / Monitor / Healthy breakdown |
| Health vs Tickets | Scatter Plot | support_tickets_open | health_score | Correlation between ticket volume and health |
| Renewals Timeline | Gantt / Bar | account_name | renewal_date | Shows which accounts are up for renewal |
| Contract Value by CSM | Bar Chart | csm_owner | SUM(contract_value) | Shows portfolio value per CSM |
| Health Trend Table | Table | account_name, health_score, risk_flag, last_login_days_ago, renewal_date | — | Full account health register |

### Filter Controls ✅

| Filter | Type | Field | Scope |
|---|---|---|---|
| Risk Flag Filter | Segmented control (At Risk / Monitor / Healthy / All) | risk_flag | All visuals on this sheet |
| CSM Owner Filter | Dropdown | csm_owner | Bar chart, table |
| Renewal Date Range | Date picker | renewal_date | Renewals timeline, table |

**Screenshot Reference:** `Filter_Controls_Customer_Health.png` — shows the segmented control filter at the top of Sheet 3 with "At Risk" selected, causing all visuals to filter to the 5 at-risk accounts only.

### One-Click Filter Action ✅

**Action configured:** Click on any segment in the "Risk Distribution" donut chart → filters Health Score bar chart, Scatter Plot, and Health Trend Table to that risk tier.

**Action configuration:**
- Action type: Filter action
- Source visual: Risk Distribution (donut chart)
- Target visuals: Health Score bar chart + Scatter Plot + Health Trend Table
- Field used: risk_flag
- Trigger: Click on donut segment

**Screenshot Reference:** `OneClick_Filter_Action_Sheet3.png` — shows Sheet 3 after clicking the "At Risk" donut segment; bar chart and table update to show only the 5 at-risk accounts.

### Cross-Sheet Navigation ✅

**Navigation button:** "← Back to Sales Pipeline" button in top-left of Sheet 3.

**Screenshot Reference:** `Navigation_Button_Sheet3.png` — shows the back navigation button and the configuration panel confirming destination = Sheet 2 "Sales Pipeline".

---

## Summary of Interactive Features

| Feature | Sheet 1 | Sheet 2 | Sheet 3 |
|---|---|---|---|
| KPI Cards | ✅ 4 cards | ✅ 4 cards | ✅ 4 cards |
| Filter Controls | ✅ 3 filters | ✅ 4 filters | ✅ 3 filters |
| One-Click Filter Action | ✅ Industry → all visuals | ✅ Region → table + quota | ✅ Risk tier → 3 visuals |
| Cross-Sheet Navigation | ✅ → Sheet 2 | ✅ ← Sheet 1 · → Sheet 3 | ✅ ← Sheet 2 |

---

*All interactive features configured in Amazon QuickSight Analysis view. Filter actions use the built-in QuickSight Actions panel (Visual menu → Actions → Add action → Filter action).*
