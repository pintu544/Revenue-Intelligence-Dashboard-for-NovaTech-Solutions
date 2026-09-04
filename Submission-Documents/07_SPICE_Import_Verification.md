# SPICE Import Verification Documentation
## NovaTech Solutions — Amazon QuickSight Dashboard

**Tool:** Amazon QuickSight (SPICE In-Memory Engine)  
**Analyst:** Michael Adedayo-Dami  
**Date:** June 2025  

---

## Overview

Three CSV source datasets were imported into Amazon QuickSight SPICE. Each dataset was verified for correct row counts, column counts, and data types before the unified joined dataset was created as a fourth SPICE dataset.

---

## Dataset 1 — Marketing Leads (marketing_leads.csv)

| Property | Value |
|---|---|
| **Dataset Name** | NovaTech_Marketing_Leads |
| **Source File** | marketing_leads.csv |
| **SPICE Status** | ✅ Imported Successfully |
| **Row Count** | 1,250 rows |
| **Column Count** | 12 columns |
| **Import Date** | June 2025 |
| **Unique Key Field** | lead_id |

### Columns Imported

| Column Name | Raw Type | Corrected Type | Notes |
|---|---|---|---|
| lead_id | String | String | Primary key — used for join |
| first_name | String | String | — |
| last_name | String | String | — |
| company | String | String | — |
| industry | String | String | — |
| lead_source | String | String | Web / Referral / Event / Paid |
| job_title | String | String | — |
| lead_score | String | **Integer** | ⚠ Corrected: imported as String; changed to Integer |
| created_date | String | **Date (YYYY-MM-DD)** | ⚠ Corrected: text date parsed to Date type |
| region | String | String | AMER / EMEA / APAC |
| email | String | String | — |
| status | String | String | New / Contacted / Qualified / Disqualified |

### Data Type Corrections Applied
- `lead_score`: String → Integer (required for aggregation and KPI cards)
- `created_date`: String → Date (required for time-series visualisations and date filters)

### Verification Screenshot Reference
> **Screenshot:** `SPICE_Import_Marketing_Leads.png` — shows dataset preview with 1,250 rows, 12 columns, SPICE ingestion status "Complete", and data type icons confirming Integer on lead_score and Date on created_date.

---

## Dataset 2 — Sales Opportunities (sales_opportunities.csv)

| Property | Value |
|---|---|
| **Dataset Name** | NovaTech_Sales_Opportunities |
| **Source File** | sales_opportunities.csv |
| **SPICE Status** | ✅ Imported Successfully |
| **Row Count** | 22 rows |
| **Column Count** | 10 columns |
| **Import Date** | June 2025 |
| **Unique Key Field** | opportunity_id (links to lead_id) |

### Columns Imported

| Column Name | Raw Type | Corrected Type | Notes |
|---|---|---|---|
| opportunity_id | String | String | Foreign key — joins to lead_id |
| opportunity_name | String | String | — |
| account_name | String | String | — |
| stage | String | String | Prospecting / Qualification / Proposal / Negotiation / Closed Won / Closed Lost |
| amount | String | **Decimal** | ⚠ Corrected: currency string ($105,000) parsed to Decimal |
| probability | String | **Decimal** | ⚠ Corrected: percentage string (75%) divided by 100 → 0.75 |
| close_date | String | **Date (YYYY-MM-DD)** | ⚠ Corrected: text date parsed to Date type |
| region | String | String | AMER / EMEA / APAC |
| rep_name | String | String | — |
| weighted_amount | String | **Decimal** | ⚠ Corrected: derived field, stored as String; converted to Decimal |

### Data Type Corrections Applied
- `amount`: String (with $ symbol and commas) → Decimal
- `probability`: String ("75%") → Decimal (0.75)
- `close_date`: String → Date
- `weighted_amount`: String → Decimal

### Verification Screenshot Reference
> **Screenshot:** `SPICE_Import_Sales_Opportunities.png` — shows dataset preview with 22 rows, 10 columns, SPICE ingestion status "Complete", and data type corrections visible in the field list panel.

---

## Dataset 3 — Customer Health (customer_health.csv)

| Property | Value |
|---|---|
| **Dataset Name** | NovaTech_Customer_Health |
| **Source File** | customer_health.csv |
| **SPICE Status** | ✅ Imported Successfully |
| **Row Count** | 22 rows |
| **Column Count** | 9 columns |
| **Import Date** | June 2025 |
| **Unique Key Field** | account_id (links to opportunity_id) |

### Columns Imported

| Column Name | Raw Type | Corrected Type | Notes |
|---|---|---|---|
| account_id | String | String | Foreign key — joins to opportunity_id |
| account_name | String | String | — |
| health_score | String | **Integer** | ⚠ Corrected: String → Integer (0–100 scale) |
| contract_value | String | **Decimal** | ⚠ Corrected: currency string → Decimal |
| renewal_date | String | **Date (YYYY-MM-DD)** | ⚠ Corrected: text date → Date |
| support_tickets_open | String | **Integer** | ⚠ Corrected: String → Integer |
| last_login_days_ago | String | **Integer** | ⚠ Corrected: String → Integer |
| csm_owner | String | String | Customer Success Manager name |
| risk_flag | String | String | At Risk / Healthy / Monitor |

### Data Type Corrections Applied
- `health_score`: String → Integer
- `contract_value`: String → Decimal
- `renewal_date`: String → Date
- `support_tickets_open`: String → Integer
- `last_login_days_ago`: String → Integer

### Verification Screenshot Reference
> **Screenshot:** `SPICE_Import_Customer_Health.png` — shows dataset preview with 22 rows, 9 columns, SPICE status "Complete", and all five corrected fields showing correct type icons (# for integers, decimal for currency, calendar for dates).

---

## Dataset 4 — Unified Joined Dataset

| Property | Value |
|---|---|
| **Dataset Name** | NovaTech_Unified_Dashboard |
| **SPICE Status** | ✅ Saved to SPICE |
| **Row Count** | 22 rows (joined on shared Opportunity/Account key) |
| **Column Count** | 28 columns (all source columns combined, duplicates removed) |
| **Join Type** | Left Join (Opportunities → Customer Health) + Left Join (→ Marketing Leads) |

### Join Diagram

```
┌──────────────────────────────────┐
│   NovaTech_Marketing_Leads       │
│   (1,250 rows)                   │
│                                  │
│   lead_id  ◄──────────────────┐  │
│   lead_source                 │  │
│   industry                    │  │
│   lead_score                  │  │
│   region                      │  │
│   status                      │  │
└──────────────────────────────────┘
                                │
                    LEFT JOIN on lead_id = opportunity_id
                                │
┌──────────────────────────────────┐
│  NovaTech_Sales_Opportunities    │  ◄── Primary (left) table
│  (22 rows)                       │
│                                  │
│  opportunity_id  ◄────────────┐  │
│  account_name                 │  │
│  stage                        │  │
│  amount                       │  │
│  probability                  │  │
│  close_date                   │  │
│  region                       │  │
│  rep_name                     │  │
│  weighted_amount              │  │
└──────────────────────────────────┘
                                │
                    LEFT JOIN on opportunity_id = account_id
                                │
┌──────────────────────────────────┐
│   NovaTech_Customer_Health       │
│   (22 rows)                      │
│                                  │
│   account_id                     │
│   health_score                   │
│   contract_value                 │
│   renewal_date                   │
│   support_tickets_open           │
│   last_login_days_ago            │
│   risk_flag                      │
│   csm_owner                      │
└──────────────────────────────────┘
                │
                ▼
┌──────────────────────────────────────┐
│   NovaTech_Unified_Dashboard (SPICE) │
│   22 rows × 28 columns               │
│   Status: ✅ Saved to SPICE           │
└──────────────────────────────────────┘
```

### Join Configuration Detail

| Join # | Left Table | Right Table | Left Key | Right Key | Join Type |
|---|---|---|---|---|---|
| 1 | Sales_Opportunities | Customer_Health | opportunity_id | account_id | Left Join |
| 2 | (Result of Join 1) | Marketing_Leads | opportunity_id | lead_id | Left Join |

**Why Left Join:** Left joins preserve all 22 Opportunity records even if a matching Customer Health or Marketing Lead record does not exist, preventing data loss in the unified view.

### Verification Screenshot Reference
> **Screenshot:** `SPICE_Join_Diagram.png` — shows the QuickSight dataset join editor with both joins configured, field mapping lines connecting opportunity_id → account_id and opportunity_id → lead_id, join type dropdowns set to "Left", and the unified dataset preview showing 22 rows and 28 columns.

---

## SPICE Summary — All Four Datasets

| Dataset | Rows | Columns | SPICE Status |
|---|---|---|---|
| NovaTech_Marketing_Leads | 1,250 | 12 | ✅ Complete |
| NovaTech_Sales_Opportunities | 22 | 10 | ✅ Complete |
| NovaTech_Customer_Health | 22 | 9 | ✅ Complete |
| NovaTech_Unified_Dashboard | 22 | 28 | ✅ Complete |

---

*All SPICE imports performed in Amazon QuickSight. Data type corrections applied in the QuickSight dataset edit view before SPICE ingestion was triggered.*
