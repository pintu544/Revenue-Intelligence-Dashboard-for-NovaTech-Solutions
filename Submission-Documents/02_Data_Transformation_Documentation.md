# Data Transformation Documentation — NovaTech Solutions

**Project:** NovaTech Solutions — Revenue Intelligence Dashboard  
**Analyst:** Michael Adedayo-Dami  
**Tool:** Microsoft Excel → Power BI  
**Date:** June 2025  

---

## Overview

Raw pipeline data was entered into Salesforce, exported to Excel, transformed across five tabs, and then loaded into Power BI via a flat data model table. This document covers the join structure, transformation steps, calculated fields, and data type corrections applied throughout the process.

---

## 1. Join Diagram

```
┌─────────────────────────────────┐
│   Salesforce Opportunities      │
│   (22 records exported)         │
│                                 │
│  Opportunity Name               │
│  Account Name                   │
│  Stage                          │
│  Amount                         │
│  Close Date                     │
│  Probability %                  │
│  Region (AMER / EMEA / APAC)    │
│  Rep Name                       │
│  Lead Source                    │
└────────────┬────────────────────┘
             │
             │ Manual export → paste into Excel
             ▼
┌─────────────────────────────────┐
│   Excel: Pipeline Data Tab      │ ◄── Primary fact table
│                                 │
│  + Weighted Amount (calculated) │
│  + Close Month (derived)        │
└────────────┬────────────────────┘
             │
             │ SUMPRODUCT / scenario logic joins
             ├──────────────────────────────────────┐
             ▼                                      ▼
┌────────────────────────┐          ┌────────────────────────┐
│ Excel: Best Case Tab   │          │ Excel: Worst Case Tab  │
│ Multiplier: ×1.15      │          │ Multiplier: ×0.80      │
└────────────┬───────────┘          └────────────┬───────────┘
             │                                   │
             │         ┌──────────────────────┐  │
             └────────►│ Excel: Commit Tab    │◄─┘
                        │ Multiplier: ×1.00    │
                        └──────────┬───────────┘
                                   │
                                   │ Denormalized flatten
                                   ▼
                        ┌──────────────────────────┐
                        │ Excel: PBI Data Model Tab │ ◄── Power BI source
                        │                           │
                        │  One row per Opportunity  │
                        │  per Scenario (3 rows     │
                        │  per opportunity = 66 rows│
                        │  total)                   │
                        └──────────┬────────────────┘
                                   │
                                   │ Direct query (Import mode)
                                   ▼
                        ┌──────────────────────────┐
                        │    Power BI Data Model    │
                        │                           │
                        │  All DAX measures built   │
                        │  on top of this table     │
                        └──────────────────────────┘
```

---

## 2. Join Configuration

### Excel: Pipeline Data → Scenario Tabs

The three scenario tabs (Best Case, Worst Case, Commit) reference the Pipeline Data tab using structured table references. There is no traditional SQL-style JOIN — instead SUMPRODUCT aggregates weighted amounts by Region and by Rep from the Pipeline Data table.

| Join Type | From | To | Key Field | Purpose |
|---|---|---|---|---|
| Aggregation (SUMPRODUCT) | Pipeline Data | Best Case | Region | Sum weighted pipeline per region at 1.15× |
| Aggregation (SUMPRODUCT) | Pipeline Data | Worst Case | Region | Sum weighted pipeline per region at 0.80× |
| Aggregation (SUMPRODUCT) | Pipeline Data | Commit | Region | Sum weighted pipeline per region at 1.00× |
| Aggregation (SUMPRODUCT) | Pipeline Data | Best Case | Rep Name | Quota attainment per rep at 1.15× |
| Row-level reference | Pipeline Data | PBI Data Model | Opportunity Name | One row per opportunity, scenario column added |

### Power BI: Single-Table Model

Power BI imports the PBI Data Model tab as a single flat table. No relationships are required since all dimensions (Region, Rep, Stage, Scenario) are columns in the same table.

---

## 3. Calculated Fields

### Excel Calculated Columns (Pipeline Data Tab)

| Field Name | Formula | Description |
|---|---|---|
| Weighted Amount | `=Amount * Probability` | Probability-adjusted deal value |
| Close Month | `=TEXT(Close Date, "MMM YYYY")` | Month label for time-series grouping |
| Scenario Amount (Best) | `=Weighted Amount * 1.15` | Best Case scenario value per deal |
| Scenario Amount (Worst) | `=Weighted Amount * 0.80` | Worst Case scenario value per deal |
| Scenario Amount (Commit) | `=Weighted Amount * 1.00` | Commit (base) scenario value per deal |

### Excel Aggregations (Scenario Tabs — Best Case / Worst Case / Commit)

| Field Name | Formula | Description |
|---|---|---|
| Pipeline by Region | `=SUMPRODUCT((Region=X)*ScenarioAmount)` | Total forecast per region under each scenario |
| Quota Attainment % | `=Closed Won / Rep Quota` | Percentage of $500,000 quota achieved per rep |
| Gap to Quota | `=Rep Quota - Closed Won` | Remaining revenue needed to hit quota |
| Team Total Forecast | `=SUM(all region scenario amounts)` | Full team forecast under each scenario |

### Power BI DAX Measures

| Measure Name | DAX Formula | Description |
|---|---|---|
| Closed Won Amount | `CALCULATE(SUM('PBI Data Model'[Amount]), 'PBI Data Model'[Stage] = "Closed Won")` | Total revenue from closed deals |
| Closed Won Amount Safe | `IF(ISBLANK([Closed Won Amount]), 0, [Closed Won Amount])` | Returns $0 instead of BLANK for reps with no closed deals |
| Rep Quota | `500000` | Flat annual quota per rep ($500,000) |
| Quota Attainment % | `DIVIDE([Closed Won Amount Safe], [Rep Quota], 0)` | Attainment percentage; returns 0 on divide-by-zero |
| Gap to Quota | `[Rep Quota] - [Closed Won Amount Safe]` | Revenue gap remaining per rep |

---

## 4. Data Type Corrections

The following data type issues were identified and corrected during transformation from Salesforce export → Excel → Power BI.

| Field | Original Type | Corrected Type | Where Fixed | Issue |
|---|---|---|---|---|
| Amount | Text (Salesforce export includes $ and commas) | Currency / Decimal Number | Excel Pipeline Data tab | Salesforce exports amounts as formatted text strings; stripped symbols and converted to numeric |
| Probability | Text ("75%") | Decimal (0.75) | Excel Pipeline Data tab | Percentage exported as string; divided by 100 for formula use |
| Close Date | Text ("06/30/2025") | Date | Excel Pipeline Data tab | Date serial formatting applied so time-series grouping works correctly |
| Close Date | Date | Date (Short Date) | Power BI | Ensured Power BI recognized the column as Date not DateTime to avoid duplicate axis labels |
| Weighted Amount | General | Currency | Excel Pipeline Data tab | Explicitly formatted as Currency to prevent accidental text concatenation in SUMPRODUCT |
| Scenario | Not present in source | Text | PBI Data Model tab (added column) | New column added manually to denote Best Case / Worst Case / Commit per row |
| Rep Quota | Not present in source | Whole Number | Power BI DAX | Static measure defined in DAX rather than a column to avoid duplication across scenario rows |

---

## 5. Data Quality Notes

- **Duplicate check:** All 22 Opportunity Names were verified as unique. No duplicates found in Salesforce export.
- **Null values:** No null amounts or probabilities. Reps with $0 Closed Won are handled by the Safe DAX measure.
- **Region coverage:** All 22 opportunities are tagged AMER, EMEA, or APAC. No untagged records.
- **Probability alignment:** Salesforce stage-default probabilities were used (e.g., Prospecting = 10%, Proposal = 50%, Closed Won = 100%). No manual overrides applied.

---

*Documentation reflects transformations applied to NovaTech Solutions fictional dataset for portfolio demonstration purposes.*
