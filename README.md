# 👥 Customer Segmentation & Lifetime Value Analysis

## Project Overview

This project consists of two related analyses completed as part of the **Turing College** data analytics program, using the `turing_data_analytics` dataset in BigQuery. Both tasks focus on understanding customer value — who the best customers are today, and how much revenue can be expected from users over time.

> ⚠️ **Note:** The database was provided by Turing College for educational purposes and is not available to third parties.

---

## Task 1: RFM Customer Segmentation

### What is RFM?
RFM is a customer segmentation method based on three behavioral dimensions:
- **Recency (R)** — how recently a customer made a purchase
- **Frequency (F)** — how often they purchase
- **Monetary (M)** — how much they spend in total

Each customer receives a score of 1–4 on each dimension, which are combined into an RFM score used to classify customers into segments.

### Segments & Outcomes

| Customer Segment | # Customers | % of Customers | Avg. Frequency | Avg. Sales per Customer | Avg. Recency (days) |
|---|---|---|---|---|---|
| Best Customer | 324 | 7.38% | 15 | $7,761 | -1 |
| Big Spender | 225 | 5.08% | 4 | $3,055 | 49 |
| Loyal Customer | 286 | 6.53% | 8 | $3,648 | 16 |
| Potential Loyalist | 967 | 22.28% | 3 | $758 | 42 |
| Lost Customer | 1,401 | 32.36% | 1 | $518 | 248 |
| Others | 1,135 | 26.37% | 1 | $288 | 47 |

**Key findings:**
- The largest segment is **Lost Customers** (32.36%) — customers who haven't purchased in a long time and spend very little
- **Best Customers** (7.38%) purchase 15× on average and generate $7,761 per customer — far above any other segment
- **Potential Loyalists** (22.28%) represent a strong re-engagement opportunity with moderate recency and frequency
- Total customer base: **4,338** with **$6.03M** in total sales and an average of **3 purchases per customer**

---

## Task 2: Customer Lifetime Value (CLV) via Cohort Analysis

### Approach
Rather than using a simplified CLV formula, this analysis uses **weekly cohort analysis** to produce more reliable and actionable estimates. All website visitors are included — not just those who made a purchase — using their first visit as the registration date (`user_pseudo_id`).

Three tables were produced:

**1. Weekly Average Revenue by Cohorts**
Revenue per week divided by the number of registrations in each cohort — showing how much each registered user generates week by week.

**2. Cumulative Revenue by Cohorts**
The same data expressed as a running total, showing how revenue accumulates per registered user over 12 weeks since registration.

**3. Revenue Prediction by Cohorts**
For cohorts with incomplete data (recently acquired users), future weeks are predicted using average cumulative growth rates derived from historical cohorts. This allows a full 12-week CLV estimate for every cohort.

### Key findings:
- Week 0 (registration week) generates the highest revenue per user — revenue drops significantly in subsequent weeks
- Cumulative revenue per registered user grows over 12 weeks but at a declining rate
- Including non-purchasing users significantly lowers the average CLV compared to purchase-only calculations — a more realistic estimate
- Cohort trends reveal whether newer cohorts are performing better or worse than older ones at the same stage

---

## SQL Queries

### RFM Query (summary)
Calculates recency, frequency, and monetary values per customer, scores each on a 1–4 scale, combines into an RFM score, and assigns a customer segment label.

📄 Full query available in the [RFM Spreadsheet](https://docs.google.com/spreadsheets/d/1rOKI-n7FwwBJ6lzQ5QuQQJ7UnKSfm_-pORW1QlFS0EE/edit?usp=sharing) — `Query` sheet

### CLV / Cohort Query (summary)
Identifies each user's first visit week as their registration cohort, then calculates total revenue per cohort per subsequent week, divided by cohort registration size to produce average revenue per user.

📄 Full query available in the [CLV Spreadsheet](https://docs.google.com/spreadsheets/d/1sXrqcoQWPFMo1E03e8WTPHIq-_t1s62EJc-ACr4SwBE/edit?usp=sharing) — `Query` sheet

---

## Project Links

### Task 1 — RFM Segmentation
| Resource | Link |
|---|---|
| 📈 Tableau Dashboard | [Tableau Public](https://public.tableau.com/views/RFM_17312556692500/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link) |
| 🗂 Query & Results | [Google Sheets](https://docs.google.com/spreadsheets/d/1rOKI-n7FwwBJ6lzQ5QuQQJ7UnKSfm_-pORW1QlFS0EE/edit?usp=sharing) |

### Task 2 — CLV Cohort Analysis
| Resource | Link |
|---|---|
| 🗂 Query, Results & Charts | [Google Sheets](https://docs.google.com/spreadsheets/d/1sXrqcoQWPFMo1E03e8WTPHIq-_t1s62EJc-ACr4SwBE/edit?usp=sharing) |

---

## Tools Used

| Tool | Purpose |
|---|---|
| Google BigQuery | SQL data extraction and metric calculation |
| Google Sheets | Data processing, cohort tables, conditional formatting, charts |
| Tableau Public | RFM dashboard visualization |
