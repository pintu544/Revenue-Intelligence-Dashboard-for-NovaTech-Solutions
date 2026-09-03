# NovaTech Solutions - Salesforce Portfolio
### A real-world Salesforce build across multiple projects on one org

---

## What This Is

This repo contains a series of Salesforce projects all built inside the same Developer Edition org for a fictional B2B SaaS company called NovaTech Solutions. The company has 500 users across Sales, Support, Finance, Marketing and Management.

Rather than building random disconnected projects, everything here follows one continuous story. The permission architecture was designed first, then automation was built on top of it, then analytics on top of that. That is how real Salesforce work actually happens and that is how this portfolio is structured.

---

## The Company

**NovaTech Solutions** sells software to mid-market companies. They have a Sales team split across EMEA, APAC and AMER, a Support team handling customer cases, a Finance team managing contracts and billing, and a Management layer that needs visibility across everything.

When this build started, the org had no real permission structure, no lead prioritisation, and no way for managers to see accurate pipeline data. Each project in this portfolio solves a specific business problem.

---

## Projects

### H1 - Permission Architecture Design
`H1-Permission-Architecture/`

The foundation of the entire org. Covers role hierarchy, org-wide defaults, permission sets, permission set groups and sharing rules for all 500 users. Built and documented with a full decision matrix showing every access decision and the business reason behind it.

Also includes an implementation of the Spring 25 feature that lets you manage Permission Set Group membership directly from the Permission Set Summary page.

Skills shown: Salesforce Administration, Security Model Design, Business Analysis, Documentation

---

### E1 - Lead Scoring Configuration
`E1-Lead-Scoring/`

A weighted lead scoring model built with a Record-Triggered Flow. Every Lead record gets automatically scored between 0 and 100 based on job title, industry, company size and lead source. A custom list view surfaces the highest scoring leads at the top so reps know exactly who to contact first.

Skills shown: Salesforce Flow Builder, Process Automation, Sales Operations

---

### M1 - Revenue Forecast Model
`M1-Revenue-Forecast/`

A full revenue forecast model built across three tools. 22 opportunities were entered directly into Salesforce across AMER, EMEA and APAC, then exported into a structured Excel workbook with weighted probability calculations and three scenario models: Best Case, Worst Case and Commit. Power BI connects to the Excel data model and visualises pipeline health, quota attainment by rep, forecast vs target, and scenario comparisons across all regions.

Five DAX measures were built from scratch to handle closed revenue tracking, quota attainment percentages, and gap to quota per rep.

Skills shown: Salesforce Reporting, Excel Financial Modelling, Power BI, DAX, Sales Analytics

---

## What Is Coming

These projects are planned for the same NovaTech org and will be added to this repo as they are completed:

- **M7** - Sales Process Automation with additional Flow builds
- **T-M1** - Salesforce connected directly to Tableau for live reporting

---

## Tools Used Across This Portfolio

- Salesforce Developer Edition
- Salesforce Flow Builder
- Salesforce Setup (Roles, OWDs, Permission Sets, Sharing Rules)
- Microsoft Excel
- Power BI
- Tableau (upcoming)

---

## About Me

I am a Salesforce Administrator and CRM Business Analyst building a portfolio of real-world projects across Salesforce administration, Flow automation, CRM configuration and sales analytics.

LinkedIn: https://www.linkedin.com/in/michael-adedayo-dami/
