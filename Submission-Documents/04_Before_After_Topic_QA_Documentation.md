# Before & After Topic — Q&A Documentation
## NovaTech Solutions Revenue Intelligence Dashboard

**Tool:** Power BI Q&A (Natural Language Query)  
**Analyst:** Michael Adedayo-Dami  
**Date:** June 2025  

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
