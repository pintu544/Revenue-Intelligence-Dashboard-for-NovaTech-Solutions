# Annotated Dashboard Screenshots
## NovaTech Solutions — Amazon QuickSight Dashboard

**Tool:** Amazon QuickSight  
**Analyst:** Michael Adedayo-Dami  
**Date:** June 2025  

---

## Purpose

Text annotations were added directly to each dashboard sheet to provide business context, highlight key insights, and guide stakeholders to the most important data points. This document describes the content and placement of all annotations across the three sheets.

Each sheet contains 3–5 text annotations. Annotations are implemented as QuickSight "Insight" visuals or free-form text boxes placed adjacent to the relevant chart.

---

## Sheet 1 — Marketing Funnel Annotations

### Annotation 1 — Lead Volume Context

**Placement:** Top of sheet, below the KPI cards row  
**Visual type:** Text box / Insight tile  
**Annotation text:**

> "NovaTech generated 1,250 leads across Q2–Q3 2025. Web and Referral channels account for 61% of total volume. However, average lead score for Paid leads (72.4) outperforms Web leads (61.8), suggesting Paid channel quality exceeds its volume share."

**Purpose:** Provides immediate context for the lead source donut chart and score distribution histogram. Flags the quality vs. quantity trade-off visible in the data.

---

### Annotation 2 — Funnel Drop-Off Alert

**Placement:** Beside the Lead Conversion Funnel chart  
**Visual type:** Callout annotation with arrow pointing to Qualified stage  
**Annotation text:**

> "⚠ Funnel Alert: Only 25% of leads (312 of 1,250) reach Qualified status. The largest drop-off occurs between Contacted and Qualified — 58% of contacted leads do not qualify. Review qualification criteria or sales rep follow-up cadence."

**Purpose:** Directs attention to the single biggest conversion problem in the marketing funnel. Provides an actionable recommendation directly on the dashboard.

---

### Annotation 3 — Regional Lead Imbalance

**Placement:** Beside the Leads by Region or Industry bar chart  
**Visual type:** Text annotation  
**Annotation text:**

> "APAC leads represent only 19% of total volume despite being one of three equal sales regions. APAC-targeted campaign investment is recommended to bring regional pipeline parity."

**Purpose:** Surfaces a strategic gap that would not be obvious from the chart alone, connecting lead generation volume to the regional sales targets visible on Sheet 2.

---

### Annotation 4 — Top Performing Industry

**Placement:** Beside the Leads by Industry horizontal bar chart  
**Visual type:** Highlight annotation on the top bar  
**Annotation text:**

> "Technology leads are the highest volume (287 leads) AND highest average score (68.1) — the ideal profile for NovaTech's ICP. Prioritise Technology outreach in Q3 pipeline-building campaigns."

**Purpose:** Identifies the primary Ideal Customer Profile segment and provides a concrete Q3 action.

---

### Annotation 5 — Lead Score Benchmark

**Placement:** Below the Lead Score Distribution histogram  
**Visual type:** Reference line annotation  
**Annotation text:**

> "Leads scoring 70+ are classified as Hot Leads and routed directly to senior reps. Currently 31% of all leads (388 records) meet this threshold. The record-triggered scoring flow in Salesforce assigns scores automatically on lead creation."

**Purpose:** Explains the business logic behind the 70-point threshold visible as a reference line on the histogram, connecting this QuickSight view back to the Salesforce E1 Lead Scoring automation.

---

## Sheet 2 — Sales Pipeline Annotations

### Annotation 1 — Pipeline Gap Warning

**Placement:** Beside the Quota Attainment bullet chart  
**Visual type:** Callout annotation  
**Annotation text:**

> "⚠ Pipeline Gap: Even at Best Case (×1.15 multiplier), the team reaches only 43.4% of the $3.5M annual quota. An additional $2M+ in new qualified pipeline is required to close the gap. Immediate top-of-funnel acceleration is critical."

**Purpose:** The single most important insight on the dashboard. Placed next to the quota chart so it is impossible to miss.

---

### Annotation 2 — Stage Concentration Risk

**Placement:** Beside the Pipeline by Stage funnel  
**Visual type:** Text annotation  
**Annotation text:**

> "63% of pipeline by value sits in Prospecting and Qualification stages — the earliest two stages. This top-heavy distribution means most deals are 3–6 months from closing. The team needs to accelerate mid-funnel progression to protect Q3 forecast targets."

**Purpose:** Flags concentration risk that the funnel chart visualises but does not interpret. Gives the sales manager an immediate understanding of timing risk.

---

### Annotation 3 — Negotiation Stage Opportunity

**Placement:** Beside the Deal Size vs Probability scatter plot  
**Visual type:** Callout annotation on the top-right cluster of dots  
**Annotation text:**

> "3 deals in Negotiation stage (avg. size $131K, avg. probability 75%) represent $393K of near-term Commit revenue. Executive sponsorship or deal desk support for these accounts could accelerate close by 30–60 days."

**Purpose:** Highlights the highest-priority deals by combining size and probability context that is visible in the scatter plot but not explicitly called out.

---

### Annotation 4 — Rep Performance Disparity

**Placement:** Above the Quota Attainment bullet chart  
**Visual type:** Text annotation  
**Annotation text:**

> "Rep performance varies 4× from top to bottom. Rep 1 has closed $112K (22.4% attainment) while Reps 6 and 7 have $0 Closed Won. A structured deal review and pipeline coaching programme should be initiated immediately for the bottom two reps."

**Purpose:** Makes the performance gap actionable rather than just observable. Provides a recommended intervention.

---

### Annotation 5 — Weighted Pipeline Methodology

**Placement:** Beside the Weighted Pipeline KPI card  
**Visual type:** Info tooltip annotation  
**Annotation text:**

> "Weighted Pipeline = Deal Amount × Stage Probability. Commit Forecast = Weighted Pipeline × 1.00. Best Case = ×1.15. Worst Case = ×0.80. All figures sourced from NovaTech Salesforce CRM export as of June 2025."

**Purpose:** Documents the calculation methodology directly on the dashboard so any stakeholder can understand how the KPI is derived without needing to read the Excel workbook.

---

## Sheet 3 — Customer Health Annotations

### Annotation 1 — At-Risk Account Alert

**Placement:** Beside the Risk Distribution donut chart  
**Visual type:** Callout annotation on the "At Risk" segment  
**Annotation text:**

> "⚠ 5 accounts (23% of customer base) are flagged At Risk. Combined contract value at risk: $487,000. Immediate CSM outreach is required. Risk factors: health score < 50, 3+ open support tickets, no login in 30+ days."

**Purpose:** Quantifies the financial risk represented by the "At Risk" segment, making the business impact concrete for leadership.

---

### Annotation 2 — Health Score Methodology

**Placement:** Beside the Health Score by Account bar chart  
**Visual type:** Text annotation  
**Annotation text:**

> "Health Score (0–100): 70–100 = Healthy (Green) · 50–69 = Monitor (Amber) · 0–49 = At Risk (Red). Score is calculated from: login frequency (40%), open support tickets (30%), and contract engagement (30%). Scores updated weekly from CRM data."

**Purpose:** Explains the scoring methodology so that the colour coding is self-explanatory. Prevents misinterpretation of the RAG (Red/Amber/Green) status.

---

### Annotation 3 — Renewal Risk Window

**Placement:** Beside the Renewals Timeline chart  
**Visual type:** Callout annotation on near-term renewals  
**Annotation text:**

> "6 accounts have renewal dates within the next 90 days, representing $621,000 in ARR. Of these, 2 are currently At Risk. CSM priority for Q3: stabilise these 2 at-risk accounts before renewal conversations begin."

**Purpose:** Connects the health data to the commercial risk of upcoming renewals — the most time-sensitive insight on Sheet 3.

---

### Annotation 4 — Support Ticket Correlation

**Placement:** Beside the Health vs Tickets scatter plot  
**Visual type:** Trend line annotation  
**Annotation text:**

> "Clear negative correlation: accounts with 4+ open tickets have an average health score of 42 (At Risk), while accounts with 0–1 tickets average 81 (Healthy). Reducing ticket backlog is the single highest-leverage action to improve health scores."

**Purpose:** Provides the analytical insight the scatter plot implies but does not state. Gives CSMs a clear priority action.

---

### Annotation 5 — CSM Portfolio Imbalance

**Placement:** Beside the Contract Value by CSM bar chart  
**Visual type:** Text annotation  
**Annotation text:**

> "CSM portfolio sizes range from $180K to $520K in contract value — a 2.9× imbalance. Consider rebalancing CSM account assignments to ensure at-risk accounts receive adequate coverage proportional to their ARR."

**Purpose:** Surfaces a resource allocation problem visible in the contract value distribution, with a specific management recommendation.

---

## Annotation Summary

| Sheet | Annotation Count | Key Themes |
|---|---|---|
| Marketing Funnel | 5 | Lead quality vs. volume · Funnel drop-off · APAC gap · ICP identification · Scoring logic |
| Sales Pipeline | 5 | Quota gap · Stage concentration risk · Negotiation opportunity · Rep disparity · Methodology |
| Customer Health | 5 | At-risk financial exposure · Scoring methodology · Renewal risk window · Ticket correlation · CSM balance |

**Total annotations: 15 across 3 sheets (5 per sheet)**

---

*Annotations implemented as QuickSight free-form text visuals and built-in Insight visuals placed within each sheet's canvas. Text is directly visible on the published dashboard without requiring hover or click interactions.*
