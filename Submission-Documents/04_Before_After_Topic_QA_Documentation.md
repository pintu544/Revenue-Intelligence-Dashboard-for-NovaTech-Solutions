# Before & After Topic — Q&A Documentation
## NovaTech Solutions Revenue Intelligence Dashboard

**Tool:** Amazon QuickSight — Q (Natural Language Query) with Topic Configuration  
**Analyst:** Michael Adedayo-Dami  
**Date:** June 2025  

---

## Topic Setup — Configuration Screenshots

### Step 1 — Create a New Topic
**Navigation path:** QuickSight → Topics (left nav) → New Topic  
**Dataset selected:** NovaTech_Unified_Dashboard (SPICE)  
**Topic name:** NovaTech Revenue Intelligence  

> **Screenshot:** `Topic_Setup_01_Create_Topic.png` — shows the "Create a new topic" dialog with dataset NovaTech_Unified_Dashboard selected and the topic name field filled in.

---

### Step 2 — Field Configuration
Each field in the dataset was reviewed and configured with business-friendly names and descriptions:

| Field (Raw) | Friendly Name | Description Added | Type |
|---|---|---|---|
| lead_id | Lead ID | Unique identifier for each marketing lead | Dimension |
| lead_score | Lead Score | Weighted score 0–100 assigned by Salesforce Flow | Metric |
| amount | Deal Amount | Full contract value of the opportunity | Metric |
| weighted_amount | Weighted Pipeline | Amount adjusted by stage probability | Metric |
| probability | Close Probability | Likelihood of deal closing (0.0–1.0) | Metric |
| health_score | Health Score | Customer account health rating 0–100 | Metric |
| contract_value | Contract Value | Annual recurring revenue for this account | Metric |
| support_tickets_open | Open Support Tickets | Number of unresolved support cases | Metric |
| risk_flag | Risk Status | At Risk / Monitor / Healthy classification | Dimension |
| rep_name | Sales Rep | Assigned sales representative | Dimension |
| stage | Pipeline Stage | Current opportunity stage in the sales cycle | Dimension |

> **Screenshot:** `Topic_Setup_02_Field_Configuration.png` — shows the Topics field editor with the above fields listed, friendly names applied, and field type (metric vs dimension) correctly set for each column.

---

### Step 3 — Synonyms and Named Metrics

The following synonyms and named metrics were defined to teach QuickSight Q the NovaTech business vocabulary:

**Synonyms (field-level):**

| Term | Maps To |
|---|---|
| revenue | weighted_amount (Closed Won only) |
| forecast | weighted_amount (all stages) |
| pipeline | SUM(amount) excluding Closed Won / Lost |
| rep | rep_name |
| quota | $500,000 (per rep, static) |
| at risk | risk_flag = "At Risk" |
| hot leads | lead_score ≥ 70 |
| qualified | status = "Qualified" |

> **Screenshot:** `Topic_Setup_03_Synonyms.png` — shows the QuickSight Topic synonym editor with all eight synonyms listed and their field/filter mappings visible.

---

### Step 4 — Test in Q Panel

After configuring synonyms, each synonym was tested in the Q panel to verify correct interpretation:

> **Screenshot:** `Topic_Setup_04_Q_Test_Panel.png` — shows the QuickSight Q test interface with the NovaTech Revenue Intelligence topic selected, a test question typed in ("show me revenue by rep"), and the Q response showing Closed Won Amount by rep name with all 7 reps displayed.

---

## What Is a Topic?

In Power BI Q&A, a **Topic** (also referred to as Q&A linguistic schema or Q&A setup / synonyms) allows report authors to teach the AI natural language engine to:
- Recognize company-specific terminology (e.g., "reps" = "Rep Name" field)
- Understand business concepts (e.g., "on target" = Quota Attainment % ≥ 100%)
- Correct misinterpretations in default Q responses

This document shows baseline Q responses **before** Topics were configured, and improved responses **after** Topics were applied.

---

## Question 1 — "Show me revenue by rep"

### Before Topic (Baseline)

**Question typed:** `show me revenue by rep`

**Q Response:**  
Power BI returned a table showing **all Amount values** by Rep Name including open pipeline deals, not just Closed Won revenue. The visual included every stage (Prospecting, Qualification, Proposal, etc.) which overstated "revenue" significantly.

**Problem:**  
- Q interpreted "revenue" as the raw Amount field rather than the Closed Won Amount measure.
- Result showed $2,325,000 distributed across reps — this is total pipeline, not revenue.
- Two reps with no closed deals were **missing from the visual** entirely (BLANK issue).

```
Before Topic Result:
Rep 1    $415,000  ← includes all pipeline stages
Rep 2    $390,000
Rep 3    $310,000
Rep 4    $280,000
Rep 5    $225,000
[Rep 6 and Rep 7 not shown — BLANK]
```

---

### After Topic (Post-Configuration)

**Topic configuration applied:**
- Synonym added: `revenue` → maps to `[Closed Won Amount Safe]` measure
- Synonym added: `rep` → maps to `Rep Name` field
- Phrasing added: "show [measure] by [field]" pattern taught to Q&A engine

**Q Response after Topic:**  
Q now returns a bar chart of **Closed Won Amount Safe by Rep Name**, with $0 bars for reps with no closed deals.

```
After Topic Result:
Rep 1    $112,000  ← Closed Won only
Rep 2    $95,000
Rep 3    $80,000
Rep 4    $60,000
Rep 5    $40,000
Rep 6    $0        ← now correctly shown
Rep 7    $0        ← now correctly shown
```

**Improvement:** Result is now accurate, complete, and matches the Quota Attainment dashboard page exactly.

---

## Question 2 — "What is our forecast for EMEA?"

### Before Topic (Baseline)

**Question typed:** `what is our forecast for EMEA`

**Q Response:**  
Power BI did not recognize "forecast" as a defined concept. It returned total **pipeline Amount** for EMEA region records — $810,000 — with no scenario context. The Q visual showed a single card with no scenario breakdown.

**Problem:**  
- "Forecast" was not mapped to any scenario measure (Best Case / Commit / Worst Case).
- Q defaulted to raw Amount sum for the EMEA filter.
- No indication of which scenario this represented or what the target was.

```
Before Topic Result:
EMEA Amount: $810,000
[No scenario context. No target comparison.]
```

---

### After Topic (Post-Configuration)

**Topic configuration applied:**
- Synonym added: `forecast` → maps to Scenario Amount fields in PBI Data Model
- Phrase taught: "forecast for [region]" → filter Region = selected value, show Best/Commit/Worst cards
- Synonym added: `EMEA` recognized as a value of the Region field (not just text)

**Q Response after Topic:**  
Q returns a grouped card or table showing all three scenario values filtered to EMEA.

```
After Topic Result:
EMEA — Best Case:    $466,500
EMEA — Commit:       $405,650
EMEA — Worst Case:   $324,520
[Target comparison shown against EMEA quota allocation]
```

**Improvement:** Response now provides actionable scenario context instead of a raw pipeline sum. Matches the Forecast vs Target page regional breakdown exactly.

---

## Question 3 — "Which reps are behind on quota?"

### Before Topic (Baseline)

**Question typed:** `which reps are behind on quota`

**Q Response:**  
Q did not understand "behind on quota" as a conditional concept. It returned a table of all reps sorted by Amount descending — no quota comparison, no attainment percentage, no filtering by who is below target.

**Problem:**  
- "Quota" was not defined in the model as a field — it exists only as a DAX measure (Rep Quota = 500000).
- "Behind" is a comparative concept Q cannot resolve without a taught phrase.
- Result was misleading — ranked reps by pipeline, not by performance gap.

```
Before Topic Result:
Rep 1    $415,000
Rep 2    $390,000
...
[No quota context. No attainment % shown.]
```

---

### After Topic (Post-Configuration)

**Topic configuration applied:**
- Synonym added: `quota` → maps to `[Rep Quota]` measure
- Synonym added: `behind` → taught as a filter condition meaning Quota Attainment % < 100%
- Phrase taught: "reps behind on quota" → show Rep Name, Closed Won Amount Safe, Rep Quota, Quota Attainment %, Gap to Quota, filtered to Attainment % < 1

**Q Response after Topic:**  
Q returns a table of all reps with attainment below 100%, sorted by Gap to Quota descending (largest gap first).

```
After Topic Result:
Rep 6    $0         $500,000    0.0%    -$500,000
Rep 7    $0         $500,000    0.0%    -$500,000
Rep 5    $40,000    $500,000    8.0%    -$460,000
Rep 4    $60,000    $500,000   12.0%    -$440,000
Rep 3    $80,000    $500,000   16.0%    -$420,000
Rep 2    $95,000    $500,000   19.0%    -$405,000
Rep 1   $112,000    $500,000   22.4%    -$388,000
[All 7 reps shown — all are below 100% attainment at this stage]
```

**Improvement:** Response is now directly actionable for a sales manager. It matches the Quota Attainment page table and confirms all reps are currently below quota, with the correct gap values.

---

## Summary of Topic Improvements

| Question | Before Topic | After Topic | Key Fix |
|---|---|---|---|
| "Show me revenue by rep" | Total pipeline by rep; 2 reps missing | Closed Won only; all 7 reps shown | Revenue synonym mapped to Closed Won Amount Safe |
| "What is our forecast for EMEA?" | Raw pipeline sum, no scenario context | 3-scenario breakdown for EMEA | Forecast mapped to scenario measures |
| "Which reps are behind on quota?" | Pipeline ranking, no quota comparison | Full attainment table with gap to quota | Quota and "behind" concepts taught |

---

*Q&A Topic configuration was applied in Power BI Desktop via the Q&A Setup panel under Modeling → Q&A Setup → Teach Q&A.*
