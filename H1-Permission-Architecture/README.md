# Salesforce Permission Architecture Design
### NovaTech Solutions · 500-User B2B SaaS Org

---

## What This Project Is

This is a full permission architecture I designed and built inside a Salesforce Developer Edition org for a fictional B2B SaaS company called NovaTech Solutions with 500 users across Sales, Support, Finance, Marketing and Management teams.

The goal was to figure out who should see what, why, and how to actually enforce that in Salesforce without it becoming a mess to manage as the company grows.

---

## The Problem I Was Solving

The org had no real permission structure. A few things that needed fixing:

- Support reps could see competitor pricing sitting inside Opportunity records
- Finance had zero visibility into Contracts, which was causing billing delays
- Regional Sales Managers could not see their full team's pipeline, so forecasting was guesswork
- Every time a new user joined, someone had to manually figure out what to give them access to
- Managing Permission Set Group membership required navigating each group individually - now handled from the Permission Set Summary page directly (Spring 25 feature)

---

## What I Built

**Role Hierarchy**

A 5-level role hierarchy covering all teams. VP Sales sits above regional Sales Managers, who sit above their reps. This controls record visibility up the chain automatically so managers see their team's records without needing individual sharing settings.

**Org-Wide Defaults (OWDs)**

Set the baseline access for every major object. Opportunities and Leads are Private, so reps only see their own records by default. Accounts and Cases are Public Read Only so teams can see context without editing records they don't own.

**Permission Sets and Permission Set Groups**

Built 5 permission sets covering each team's specific access needs and bundled them into 4 Permission Set Groups for easy assignment. Instead of managing 5 separate permission sets per user, you assign one group and everything is handled.

This also uses the Spring 25 feature where you can manage which Permission Set Groups a permission set belongs to directly from the permission set's own Summary page, rather than navigating to each group separately.

**Sharing Rules**

Three sharing rules to handle cases where the role hierarchy alone was not enough:

- EMEA Sales Manager gets read-only visibility into EMEA reps' Opportunities for forecasting
- Finance Director gets read access to Contracts without owning the records
- High-priority Cases are shared to the Support Team Lead with read/write access for escalation management

---

## Deliverables

| File | What It Contains |
|---|---|
| `H1_Permission_Architecture_NovaTech.xlsx` | Full decision matrix across 5 tabs |
| `01_Role_Hierarchy.jpg` | Full role hierarchy tree as built in Salesforce |
| `02_OWD_Settings.jpg` | Org-Wide Default settings for all objects |
| `03_Permission_Sets1.jpg` to `03_Permission_Sets4.jpg` | All 5 permission sets (split across 4 screenshots) |
| `04_Spring25_PSG_Summary.jpg` | Spring 25 PSG management via PS Summary page |
| `05_Sharing_Rules.jpg` | All 3 sharing rules |
| `06_PSG_List.jpg` | All 4 Permission Set Groups |

The Excel workbook has 5 tabs:

1. **Project Scope** - company background, business problems and a note on Developer Edition adjustments
2. **Access Matrix** - every object mapped against every user type with OWD, sharing rules and rationale
3. **Permission Set Inventory** - full CRUD breakdown for each permission set and group
4. **Sharing Rules Log** - each rule with criteria, who it shares to, access level and business justification
5. **Role Hierarchy** - full hierarchy with user counts and PSG assignments per role

---

## A Note on the Developer Edition

This was built in a Salesforce Developer Edition org which has a few limitations compared to a Production Enterprise org. The main ones I ran into:

- Account and Contract share the same OWD setting rather than having separate ones. In production Contract would be set to Private.
- Contact had to be set to Controlled by Parent rather than Public Read Only because Salesforce enforces this when Account access is not Public Read/Write.
- The Contract sharing rule could not use criteria-based filtering on Contract Status in this edition, so it was built as a record-owner based rule under Account Sharing Rules instead.

Each of these is documented in the workbook with a note on how the production implementation would differ.

---

## Tools Used

- Salesforce Developer Edition
- Salesforce Setup (Roles, Sharing Settings, Permission Sets, Permission Set Groups)
- Microsoft Excel

---

## About Me

I am a Salesforce Administrator and CRM Business Analyst. This project is part of a portfolio built on the NovaTech Solutions Salesforce org covering permission architecture, Flow automation, sales analytics and CRM configuration.

Feel free to reach out on LinkedIn https://www.linkedin.com/in/michael-adedayo-dami/ if you want to talk about any of it.
