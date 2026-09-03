# Salesforce Lead Scoring Configuration
### NovaTech Solutions · Automated Lead Prioritisation with Flow Builder

---

## What This Project Is

This is a weighted lead scoring model I built inside Salesforce for NovaTech Solutions, a fictional B2B SaaS company. The scoring runs automatically on every Lead record using a Record-Triggered Flow and writes a score between 0 and 100 to a custom Lead Score field.

The idea is simple - not every lead deserves the same attention. A VP at a 500-person tech company who came through the website is a completely different conversation from an intern at a small agriculture business. This Flow makes that distinction automatically so reps know exactly who to call first thing every morning without having to think about it.

---

## The Problem

NovaTech's sales reps were treating every lead equally. The pipeline looked busy but conversion was low because there was no way to tell which leads were actually worth pursuing. Reps were spending time on cold, low-quality leads while high-potential ones sat untouched.

---

## How the Scoring Works

The Flow checks 4 factors and adds points based on what it finds. Every lead starts at 0 and can score a maximum of 100.

| Factor | Criteria | Points |
|---|---|---|
| Job Title | Contains VP or Director | 30 |
| Industry | Technology or Finance | 25 |
| Company Size | Annual Revenue above 1,000,000 | 25 |
| Lead Source | Web or Partner Referral | 20 |

A lead that hits all 4 criteria scores 100. A lead that hits none scores 0. Everything else falls somewhere in between depending on what it matches.

---

## What I Built

**Custom Field**

A number field called Lead Score on the Lead object. It sits on all 4 Lead page layouts so every team can see it. The field is written to by the Flow only - reps cannot manually change it.

**Record-Triggered Flow**

A Fast Field Updates Flow that runs every time a Lead is created or updated. It resets the score to 0 first, then checks each of the 4 factors in sequence. If a condition is met, the matching points get added to the score. If it is not met, the Flow skips that factor and moves to the next one. Every path through the Flow ends at the same point so no factor gets skipped regardless of what the previous checks returned.

The structure is 4 Decision elements chained together, each with an Assignment element on the matching path that adds the relevant points. Both the match path and the default path of every Decision reconnect before moving to the next Decision.

**Hot Leads by Score List View**

A custom list view on the Leads object that shows Name, Title, Company, Industry, Lead Source and Lead Score, sorted by Lead Score descending. Reps open this view and their highest priority leads are right at the top.

---

## Deliverables

| File | What It Contains |
|---|---|
| `01_Lead_Score_Field.png` | Lead Score custom field detail page in Object Manager |
| `02_Flow_Top.png` | Flow canvas top section - Start, Reset Score to Zero, Check Job Title |
| `02_Flow_Mid.png` | Flow canvas middle section - Check Industry, Check Company Size |
| `02_Flow_Bottom.png` | Flow canvas bottom section - Check Lead Source, End |
| `04_Hot_Leads_List_View.png` | Hot Leads by Score list view showing all 4 test leads ranked by score |

---

## Test Results

| Lead | Title | Industry | Lead Source | Score |
|---|---|---|---|---|
| Selita Hanaick | VP | Technology | Web | 100 |
| Test Lead One | VP of Sales | Technology | Web | 100 |
| Lead 2 | Marketing Executive | Finance | Partner Referral | 45 |
| Lead 3 | Intern | Agriculture | Other | 0 |

Revenue was used as the company size signal in the Flow logic but is not displayed in the list view. Leads with Annual Revenue above 1,000,000 get 25 points added to their score automatically.

---

## A Note on the Scoring Model

The weights in this model (30 / 25 / 25 / 20) are based on a typical B2B SaaS qualification framework where job title seniority is the strongest signal of conversion potential. In a real implementation these weights would be validated against historical win rate data and adjusted accordingly. The Flow structure supports easy weight changes - just update the value in the relevant Assignment element.

---

## Tools Used

- Salesforce Developer Edition
- Salesforce Flow Builder (Record-Triggered Flow)
- Salesforce Object Manager (Custom Field)

---

## About Me

I am a Salesforce Administrator and CRM Business Analyst building a portfolio of real-world Salesforce and analytics projects. This is part of a series built on the NovaTech Solutions Salesforce org covering permission architecture, Flow automation, sales analytics and CRM configuration.

Feel free to reach out on LinkedIn https://www.linkedin.com/in/michael-adedayo-dami/ if you want to talk about any of it.
