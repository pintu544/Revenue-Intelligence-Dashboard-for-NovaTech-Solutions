# Revenue Intelligence Dashboard — Written Report
## Prepared for VP of Sales: Sarah Chen
### NovaTech Solutions | Q2–Q3 2025

**Prepared by:** Michael Adedayo-Dami, CRM Business Analyst  
**Tool:** Amazon QuickSight (SPICE)  
**Date:** June 2025  
**Classification:** Internal — Leadership Review  

---

## Executive Summary

This report documents the design, build, and findings of the NovaTech Solutions Revenue Intelligence Dashboard, built in Amazon QuickSight using data from three business domains: Marketing (lead generation), Sales (pipeline and quota), and Customer Success (account health and retention).

The dashboard was designed to answer the three questions you raised in the Q1 review:

1. **Where are our best leads coming from, and are we doing enough with them?**
2. **Are we on track to hit quota, and which deals should we prioritise?**
3. **Which customers are at risk, and what is the financial exposure?**

The short answers: our lead quality is strong but conversion is poor; the team is significantly behind quota with a structural pipeline gap; and five accounts representing $487K in ARR need immediate intervention before their renewal windows open.

---

## Section 1 — Data Strategy

### Data Sources

Three CSV datasets were imported into Amazon QuickSight SPICE, NovaTech's in-memory analytics engine:

| Dataset | Records | Key Fields |
|---|---|---|
| Marketing Leads | 1,250 rows | lead_id, lead_source, industry, lead_score, region, status |
| Sales Opportunities | 22 rows | opportunity_id, stage, amount, probability, rep_name, close_date |
| Customer Health | 22 rows | account_id, health_score, risk_flag, contract_value, renewal_date |

These three datasets were unified into a single joined SPICE dataset (NovaTech_Unified_Dashboard) using left joins on shared keys, giving us a complete view from lead creation through to customer retention in a single data model.

### Why SPICE?

SPICE (Super-fast, Parallel, In-memory Calculation Engine) was chosen over direct query mode for three reasons:

- **Speed:** Dashboard load times under 2 seconds even with 1,250 lead records
- **Resilience:** Dashboard remains available even if the underlying data source is temporarily offline
- **Refresh cadence:** SPICE can be scheduled to refresh from Salesforce exports daily, keeping the dashboard current without manual intervention

### Data Governance Decisions

- All personally identifiable information (full names, emails) was excluded from the SPICE datasets used in the published dashboard
- Region and rep-level data is available but controlled via row-level security (RLS) so individual reps see only their own pipeline; managers see their full team; VP level sees all regions
- Currency is standardised to USD throughout; no multi-currency conversion is required as NovaTech operates in USD for all regional reporting

---

## Section 2 — Design Rationale

### Three-Sheet Structure

The dashboard is structured as a deliberate narrative, not a data dump:

**Sheet 1 (Marketing Funnel)** answers the question: *Where does our pipeline come from?*  
This is the starting point of the revenue story. A lead enters the funnel here, and the sheet shows which channels, industries, and regions generate the most and best leads. A 25% lead-to-qualified conversion rate tells us immediately that the top of funnel is healthy in volume but weak in conversion.

**Sheet 2 (Sales Pipeline)** answers the question: *What is the current state of our revenue engine?*  
This sheet is designed for the weekly sales team review meeting. It gives managers an instant read on total pipeline value ($2.33M), quota attainment by rep, and which deals are most likely to close. The three-scenario forecast model (Best/Commit/Worst) was built because a single forecast number gives false precision — the range of $1.06M to $1.52M is more honest and more useful for planning.

**Sheet 3 (Customer Health)** answers the question: *Are we protecting the revenue we already have?*  
New business gets most of the attention, but retention is where margin lives. Five accounts flagged At Risk with $487K of combined ARR is a material risk that deserved its own dashboard sheet rather than a footnote. This sheet is designed for the weekly CSM team review.

### Visual Design Choices

- **Colour coding is consistent across sheets:** Green = healthy/on-track, Amber = monitor/at-risk, Red = critical/off-track. No visual uses these colours for decorative purposes.
- **KPI cards are always at the top** of each sheet so a stakeholder can get the headline numbers without scrolling or interacting.
- **Filter controls are on the left panel**, consistent with QuickSight's standard navigation pattern, so users who have used any QuickSight dashboard before will find filters intuitively.
- **One-click filter actions** are configured on the primary chart of each sheet (industry bar, region bar, risk donut) so drilling into a segment is a single click, not a multi-step filter operation.

### Cross-Sheet Navigation

Navigation buttons were added to connect the three sheets in sequence (Marketing → Pipeline → Health), reflecting the natural business flow of a customer from lead to closed deal to retained account. The active Region filter is passed as a parameter when navigating, so a manager who filters to EMEA on Sheet 1 will see EMEA data when they navigate to Sheet 2 — the context travels with them.

---

## Section 3 — Topic Configuration and AI Effects

### What Is a QuickSight Topic?

A QuickSight Topic is a semantic layer built on top of a dataset that teaches the Q&A (Quick Chat) natural language engine to understand NovaTech-specific terminology. Without a Topic, Q interprets questions using raw field names and generic rules — "revenue" might map to the Amount field (total pipeline) rather than Closed Won revenue. With a Topic, we define exactly what business terms mean in the context of NovaTech data.

### Baseline Q Behaviour (Before Topic)

Before configuring the Topic, three baseline questions were tested:

**Q1:** "Show me revenue by rep"  
- Before: Q returned total pipeline Amount by rep — $2.33M distributed, overstating revenue and missing two reps entirely (BLANK issue)
- Problem: "Revenue" was not defined; Q defaulted to the most prominent numeric field

**Q2:** "What is our forecast for EMEA?"  
- Before: Q returned raw pipeline sum for EMEA ($810K) with no scenario context
- Problem: "Forecast" was not mapped to scenario-adjusted figures

**Q3:** "Which reps are behind on quota?"  
- Before: Q returned a pipeline ranking with no quota comparison
- Problem: "Quota" and "behind" were undefined concepts

### Topic Configuration Applied

The following definitions were added to the NovaTech QuickSight Topic:

| Term Defined | Mapping | Type |
|---|---|---|
| "revenue" | Closed Won Amount (Stage = "Closed Won") | Metric synonym |
| "forecast" | Scenario-weighted Amount (Commit scenario) | Metric synonym |
| "quota" | $500,000 per rep (static value) | Metric definition |
| "behind on quota" | Quota Attainment % < 100% | Filter phrase |
| "at risk" | risk_flag = "At Risk" | Filter phrase |
| "hot leads" | lead_score ≥ 70 | Filter phrase |
| "rep" | rep_name field | Field synonym |
| "region" | region field | Field synonym |
| "pipeline" | SUM(amount) where Stage ≠ "Closed Won" and Stage ≠ "Closed Lost" | Metric definition |

**Screenshot Reference:** `Topic_Configuration_Setup.png` — shows the QuickSight Topic editor with the NovaTech_Unified_Dashboard dataset selected, all synonym and phrase definitions visible in the left panel, and the test Q&A interface on the right.

### Post-Topic Q Behaviour (After Topic)

The same three baseline questions were re-asked after Topic configuration:

**Q1:** "Show me revenue by rep" (post-Topic)  
- After: Bar chart of Closed Won Amount by rep name, all 7 reps shown including $0 bars for Reps 6 and 7
- Improvement: Accurate, complete, matches the Quota Attainment sheet exactly

**Q2:** "What is our forecast for EMEA?" (post-Topic)  
- After: Three-value response showing Best Case ($466K), Commit ($406K), Worst Case ($325K) for EMEA
- Improvement: Scenario context provided; result is immediately actionable for regional planning

**Q3:** "Which reps are behind on quota?" (post-Topic)  
- After: Table of all 7 reps with Closed Won, Quota, Attainment %, and Gap to Quota sorted by largest gap first
- Improvement: Directly answers the question with all relevant context; all 7 reps shown (all below 100%)

### AI Comparison — Q&A vs Dashboard

| Dimension | Dashboard Visuals | Q&A / Quick Chat |
|---|---|---|
| **Speed of insight** | Immediate — KPI cards visible on load | Fast — but requires the user to know what to ask |
| **Exploratory use** | Limited to pre-built visuals and filters | High — users can ask questions not anticipated at build time |
| **Accuracy** | Controlled — visuals use defined calculated fields | Requires Topic configuration to be accurate |
| **Stakeholder accessibility** | High — no training required for executives | Medium — requires comfort with natural language querying |
| **Drill-down depth** | Limited to configured filter actions | Unlimited — any dimension, any metric, any filter |
| **Annotation context** | High — text annotations explain what data means | Low — Q returns data without business interpretation |

**Recommendation:** Use the dashboard for regular review meetings where the business questions are known. Use Q&A for ad-hoc investigation and for answering questions that arise during the review meeting itself. The two modes are complementary, not competing.

---

## Section 4 — Key Insights and Recommended Actions

### Insight 1 — Pipeline is critically insufficient to hit quota

Even under Best Case assumptions, the team reaches 43.4% of the $3.5M quota. The current $2.33M pipeline, even fully converted at 100% probability, would only deliver 66% of quota. **The pipeline gap is structural, not a closing problem.**

**Recommended action:** Launch a pipeline-building initiative targeting 15–20 new qualified opportunities by end of Q3. Focus on Technology and SaaS industries (highest lead scores) via the Web and Referral channels (best quality-to-conversion ratio).

### Insight 2 — Two reps have zero closed revenue

Reps 6 and 7 have not closed any deals in the period reviewed. Combined quota gap: $1,000,000. This is not a pipeline timing issue — both reps have active opportunities but none have progressed to close.

**Recommended action:** Schedule a deal-by-deal pipeline review with both reps in the next 5 business days. Assess whether deals are stalled on customer side or rep side, and assign a senior deal coach or manager co-sell for the top two opportunities each.

### Insight 3 — APAC is underrepresented across the entire funnel

APAC generates 19% of leads, 27% of pipeline, and requires the most development investment relative to its quota allocation. The pattern is consistent from top of funnel (leads) through to bottom (closed won).

**Recommended action:** Allocate an additional marketing budget to APAC-targeted campaigns for Q3. Review whether APAC rep headcount and territory coverage is appropriate relative to the market opportunity.

### Insight 4 — Five at-risk accounts need intervention before renewal

Five accounts (23% of customers) have health scores below 50, combined ARR of $487K, and two have renewal dates within 90 days. The leading indicator is support ticket backlog — accounts with 4+ open tickets average a health score of 42.

**Recommended action:** CSM team to prioritise ticket resolution for at-risk accounts above all new business support activity for the next 30 days. Assign executive sponsorship (VP-level relationship) for the two accounts with sub-60-day renewal windows.

### Insight 5 — Lead scoring is working but conversion needs investment

31% of leads (388 records) score 70+, and the Salesforce record-triggered flow is correctly routing these to senior reps. However, only 25% of all leads reach Qualified status. The scoring identifies the right leads — the conversion process is where the opportunity is lost.

**Recommended action:** Audit the lead follow-up process for hot leads (score ≥ 70). Measure time-to-first-contact and number of touches before disqualification. Benchmark against industry standard (5–7 touches for B2B SaaS). If contact cadence is below benchmark, implement an automated outreach sequence for hot leads.

---

## Appendix — Dashboard File References

| File | Description |
|---|---|
| `07_SPICE_Import_Verification.md` | Dataset import screenshots, row/column counts, data type corrections |
| `08_Dashboard_Interactive_Features.md` | KPI cards, filter controls, one-click actions, navigation buttons |
| `09_Annotated_Dashboard_Screenshots.md` | 15 text annotations across 3 sheets |
| `04_Before_After_Topic_QA_Documentation.md` | Baseline and post-Topic Q responses |
| `05_Q_Exploration_Log.md` | 8 Q exploration entries across all data domains |
| `01_Verification_Log.md` | 7 data verification entries |
| `NovaTech_M1_Revenue_Forecast_Dashboard.pbix` | Power BI dashboard source file |
| `NovaTech_M1_Revenue_Forecast_Model.xlsx` | Excel forecast model |

---

*Report prepared for internal leadership use. Data sourced from NovaTech Solutions Salesforce Developer Edition org and Excel forecast model. All figures are based on a fictional company created for portfolio demonstration.*

*LinkedIn: https://www.linkedin.com/in/michael-adedayo-dami/*
