# ☕ Starbucks Global Retail Analytics

### Executive Sales, Customer & Payment Risk Analysis | Power BI • SQL • Excel • DAX

> An end-to-end retail analytics case study built around **10,000 orders and 10,000 customers**, combining data preparation, relational data analysis, Power BI modeling, DAX and executive dashboard storytelling.

[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-SQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Excel](https://img.shields.io/badge/Excel-Data%20Preparation-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)](https://www.microsoft.com/microsoft-365/excel)
[![DAX](https://img.shields.io/badge/DAX-Analytics-107C10?style=for-the-badge)](https://learn.microsoft.com/dax/)

---

## 📌 Project Overview

This project was developed as an **executive business review for Starbucks Global Retail Operations**. The analysis is structured around four business questions from the VP of Finance & Global Retail Operations:

1. 🌍 Which country markets should be considered for the next round of marketing / store investment?
2. 💳 Do payment methods show different payment-gap or refund-risk patterns?
3. 🎯 Which membership tier generates the highest net revenue, both in total and per customer?
4. 🔎 How large is the order-without-payment-record gap, and where is it concentrated?

The final Power BI decision layer combines **market performance, financial risk, customer economics and payment coverage** into an interactive executive report.

📄 **Full case study:** [case_study_starbucks.pdf](case_study_starbucks.pdf)

🎥 **Dashboard walkthrough:** [record.mp4](record.mp4)

---

## 📊 Executive Snapshot

| Metric | Result |
|---|---:|
| 💰 Gross Revenue | **$256.61K** |
| 💵 Net Revenue | **$200.10K** |
| 🔄 Total Refunds | **$40.19K** |
| 📦 Orders | **10,000** |
| 👥 Customers | **10,000** |
| 💳 Revenue Records | **9,652** |
| ⚠️ Payment Gap | **348 orders / 3.48%** |
| 📉 Refund Rate | **15.66%** |
| 🌎 Countries | **6** |
| 💳 Payment Methods | **4** |
| 🎯 Membership Tiers | **3** |
| 📅 Analysis Window | **2023–2025** |

These figures are verified against the case-study report. The Revenue dataset contains **9,652 records compared with 10,000 order records**, creating a 348-order payment-record gap that is treated as a business problem rather than simply removed during cleaning.

---

## 🗂️ Repository Contents

This repository contains the actual project deliverables:

| File | Purpose |
|---|---|
| 📄 [`cusotmers.csv`](cusotmers.csv) | Customer-level source data including country, membership tier and signup information |
| 📄 [`orders.csv`](orders.csv) | Order-level data including product category, payment method and order status |
| 📄 [`Revenue.csv`](Revenue.csv) | Revenue, refund and payment-status records |
| 📊 [`my_work.pbix`](my_work.pbix) | Interactive Power BI report, semantic model and DAX measures |
| 🎥 [`record.mp4`](record.mp4) | Dashboard walkthrough / project demonstration |
| 📘 [`case_study_starbucks.pdf`](case_study_starbucks.pdf) | Complete 13-page analytical case study and documented findings |

> **Note:** The repository intentionally contains the final project artifacts above. The case study documents the Excel and PostgreSQL stages of the analytical workflow; separate Excel/SQL source files are not included as repository deliverables.

---

# 🖥️ Power BI Dashboard

The Power BI report contains three main analytical pages plus **six country drill-through views**.

## 1️⃣ Country Market Investment 🌍

**Business objective:** Evaluate market scale, net economics, refund exposure and revenue trends before considering investment decisions.

### Verified market metrics

| Market | Gross Revenue | Net Revenue | Refund Rate | Customers | 2023 → 2025 |
|---|---:|---:|---:|---:|---:|
| 🇺🇸 US | $43.76K | $35.37K | 13.95% | 1,673 | $14.0K → $15.9K |
| 🇨🇳 China | $44.50K | $35.01K | 14.48% | 1,742 | $16.8K → $14.2K |
| 🇩🇪 Germany | $43.70K | $33.94K | 17.54% | 1,674 | $15.0K → $14.2K |
| 🇯🇵 Japan | $41.79K | $33.13K | 15.22% | 1,636 | $13.7K → $12.9K |
| 🇬🇧 UK | $41.45K | $31.68K | 16.09% | 1,662 | $13.1K → $14.6K |
| 🇨🇦 Canada | $41.41K | $30.97K | 16.79% | 1,613 | $13.3K → $15.3K |

### 🔍 What the dashboard shows

- 🇺🇸 **US** records the highest net revenue at **$35.37K** and the lowest refund rate at **13.95%**.
- 🇨🇳 **China** records the highest gross revenue at **$44.50K** and second-highest net revenue at **$35.01K**.
- 🇩🇪 **Germany** combines strong gross revenue with the highest refund rate at **17.54%**.

The case study therefore evaluates market economics using **scale + net revenue + refund exposure**, rather than gross revenue alone.

---

## 2️⃣ Payment & Refund Risk 💳

**Business objective:** Separate payment-gap exposure from refund exposure instead of treating them as one generic risk metric.

| Payment Method | Payment Gap | Share of Gap | Refund $ | Refund Rate |
|---|---:|---:|---:|---:|
| 💳 Credit Card | 104 | 29.9% | $9.29K | ~16.2% |
| 📱 Mobile App | 94 | 27.0% | $10.64K | ~16.3% |
| 💵 Cash | 81 | 23.3% | $9.78K | ~14.7% |
| 🟩 Starbucks Card | 69 | 19.8% | $10.49K | ~16.5% |

### 🚨 Critical control finding

**214 of the 348 payment-gap orders are marked `Delivered`.**

That means the source data contains orders where the product is recorded as delivered but no matching Revenue record exists. The case study identifies this as the **highest-severity exposure** in the dataset.

### Recommended control response

- 🔄 Automate daily order-to-revenue reconciliation.
- 🚨 Alert on `Delivered` orders with no matching payment record.
- 💰 Track Pending payments as **Revenue at Risk**, not confirmed Net Revenue.
- 💳 Monitor payment-gap remediation and refund rates as separate control queues.

---

## 3️⃣ Loyalty & Payment Gap 🎯

**Business objective:** Measure customer economics by membership tier rather than membership volume alone.

| Membership Tier | Net Revenue | Customers | Net Revenue / Customer |
|---|---:|---:|---:|
| Non-Member | $76.56K | 3,652 | $20.96 |
| Starbucks Rewards | $63.29K | 3,175 | $19.93 |
| Starbucks Rewards Gold | $60.25K | 3,173 | $18.99 |

### Interpretation

Non-Member has the highest net revenue and net revenue per customer **in this dataset**.

⚠️ This is a **revenue finding, not an ROI verdict** on the loyalty programme. The dataset does not contain programme cost, retention lift or incremental revenue, so those variables would need to be added before making a loyalty ROI conclusion.

### Payment gap by country

| Country | Gap Orders |
|---|---:|
| 🇬🇧 UK | 66 |
| 🇨🇦 Canada | 65 |
| 🇩🇪 Germany | 62 |
| 🇺🇸 US | 62 |
| 🇨🇳 China | 54 |
| 🇯🇵 Japan | 43 |

The payment gap is therefore treated as a **distributed operational issue**, rather than a problem isolated to one market.

---

# 🔎 Country Drill-Through Analysis

The Power BI report contains one drill-through profile for each market:

🇺🇸 **United States**  
🇨🇳 **China**  
🇩🇪 **Germany**  
🇯🇵 **Japan**  
🇬🇧 **United Kingdom**  
🇨🇦 **Canada**

Each profile uses the same semantic model and analytical logic while filtering the report to the selected country.

### Country-level observations documented in the case study

- 🇺🇸 **US:** $43.76K gross, $35.37K net, 13.95% refund; 2025 revenue reaches approximately $15.9K.
- 🇨🇳 **China:** $44.50K gross, $35.01K net, 14.48% refund; highest gross revenue, with the trend cooling into 2025.
- 🇩🇪 **Germany:** $43.70K gross, $33.94K net, 17.54% refund; refund-control focus is required.
- 🇯🇵 **Japan:** $41.79K gross, $33.13K net, 15.22% refund; 2024 peak followed by a 2025 pullback.
- 🇬🇧 **UK:** $41.45K gross, $31.68K net, 16.09% refund; revenue rises across the period while payment-gap exposure is highest.
- 🇨🇦 **Canada:** $41.41K gross, $30.97K net, 16.79% refund; 2025 rebound but lowest net realization among the six markets.

---

# 🧹 Data Quality & Governance

The project follows the principle:

> **Clean first. Analyze second.**

The case study documents the following analytical treatments:

| Issue | Treatment |
|---|---|
| **348 Revenue coverage gap** | Reconciled against the 10,000-order universe |
| **643 Pending payments** | Excluded from Net Revenue and tracked as Revenue at Risk |
| **282 Unknown order statuses** | Quarantined from delivery / attrition KPIs |
| **214 Delivered + no payment** | Escalated as highest-severity exposure |
| **15.66% refund rate** | Calculated using `SUM(refund) / SUM(amount paid)` |
| **Duplicate Revenue order IDs** | Order-level anti-join used for payment-gap validation |

### 🔐 Order-grain control

The raw Revenue export contains duplicate `order_id` values. Because of this, the payment-gap analysis should not simply assume one Revenue row equals one order.

The case study uses an **order-level anti-join / `NOT EXISTS` approach** to identify orders with no matching Revenue record. This avoids silently overstating or understating the payment gap through row-level joins.

---

# 🗄️ Analytical Data Model

The documented relational model contains three tables:

```text
CUSTOMERS
customer_id (PK)
country
membership_tier
signup_date
       │
       │ 1 : many
       ▼
ORDERS
order_id (PK)
customer_id (FK)
product_category
payment_method
order_status
order_date
       │
       │ 1 : many
       ▼
REVENUE
order_id (FK, non-unique)
amount_paid_usd
refund_amount_usd
payment_status
```

This model is reflected in the Power BI semantic layer and preserves the source-table grain documented in the case study.

---

# 📐 Core DAX Measures

### Total Revenue

```DAX
Total Revenue =
SUM(revenue[amount_paid_usd])
```

### Total Refund

```DAX
Total Refund =
SUM(revenue[refund_amount_usd])
```

### Net Revenue

```DAX
Net Revenue =
CALCULATE(
    SUM(revenue[amount_paid_usd]) - SUM(revenue[refund_amount_usd]),
    revenue[payment_status] <> "Pending"
)
```

### Refund Rate

```DAX
Refund Rate =
DIVIDE([Total Refund], [Total Revenue])
```

### Total Orders

```DAX
Total Orders =
DISTINCTCOUNT(orders[order_id])
```

### Total Customers

```DAX
Total Customers =
DISTINCTCOUNT(customers[customer_id])
```

### AOV

```DAX
AOV =
DIVIDE([Total Revenue], [Total Orders])
```

### Payment Gap

```DAX
Payment Gap =
CALCULATE(
    DISTINCTCOUNT(orders[order_id]),
    NOT(orders[order_id] IN VALUES(revenue[order_id]))
)
```

### Payment Gap %

```DAX
Payment Gap % =
DIVIDE([Payment Gap], [Total Orders])
```

---

# 🧪 SQL Validation Logic

The case study validates the data before the Power BI reporting layer.

### Order-level payment-gap validation

```SQL
SELECT o.order_id, o.order_status
FROM orders o
WHERE NOT EXISTS (
    SELECT 1
    FROM revenue r
    WHERE r.order_id = o.order_id
);
```

This returns **348 orders**, including **214 with `Delivered` status**.

### Net Revenue validation

```SQL
SELECT
    SUM(amount_paid_usd - refund_amount_usd) AS net_revenue
FROM revenue
WHERE payment_status <> 'Pending';
```

---

# 🔄 End-to-End Workflow

```text
Customers.csv ─────┐
Orders.csv ────────┼──► Data Preparation & Reconciliation
Revenue.csv ──────┘              │
                                  ▼
                           PostgreSQL Model
                                  │
                                  ▼
                         Power BI Semantic Model
                                  │
                           DAX Measures
                                  │
                                  ▼
                      Executive Power BI Report
                                  │
              ┌───────────────────┼───────────────────┐
              ▼                   ▼                   ▼
       Market Analysis     Payment Risk       Loyalty Economics
                                  │
                                  ▼
                         Country Drill-Through
```

The documented workflow moves from **Excel data cleaning → PostgreSQL relational modeling → Power BI semantic modeling → executive decision reporting**.

---

# 💡 Key Business Findings

### 01 · Market Economics 🌍

US records the highest net revenue at **$35.37K** and the lowest refund rate at **13.95%**. China records the highest gross revenue at **$44.50K** and $35.01K net revenue.

Germany records **$43.70K gross revenue** but also the highest refund rate at **17.54%**, demonstrating why scale and refund exposure need to be evaluated together.

### 02 · Payment Coverage 💳

The **348-order payment gap** represents **3.48%** of the 10,000-order universe. The **214 Delivered-with-no-payment** subset represents the most severe operational exposure identified in the dataset.

### 03 · Loyalty Economics 🎯

Non-Member has the highest net revenue at **$76.56K** and the highest net revenue per customer at **$20.96** in the current dataset.

The analysis does **not** claim that Rewards or Rewards Gold are under-performing because programme cost, retention and incrementality are unavailable.

### 04 · Payment Method Risk 💳

Credit Card has the highest payment-gap count at **104**, while Starbucks Card has the lowest gap count at **69** but the highest refund rate at approximately **16.5%**.

### 05 · Geographic Payment Gap 🔎

UK has **66** gap orders and Canada **65**, while Japan has **43**. The issue is distributed across all six markets.

---

# 🎯 Recommended Operating Actions

The case study converts the analytical findings into operational actions:

- 🔄 Automate daily order-to-revenue reconciliation.
- 🚨 Alert immediately when a Delivered order has no matching payment record.
- 💳 Run payment-gap remediation and refund monitoring as separate control queues.
- 💰 Track Pending payments as **Revenue at Risk**, not confirmed Net Revenue.
- 🧹 Quarantine invalid / unknown order-status values at source.
- 🎯 Add retention, incremental revenue and programme cost before making loyalty ROI claims.
- 🏪 Add cost-to-serve, payment settlement timestamps and store-level operational metadata in the next iteration.

---

# 🛠️ Tech Stack

| Area | Technology |
|---|---|
| Data Preparation | **Microsoft Excel** |
| Database / SQL Analysis | **PostgreSQL** |
| Data Analysis | **SQL + DAX** |
| Visualization | **Power BI** |
| Data Modeling | **Relational model + Power BI semantic model** |
| Reporting | **Executive dashboard + drill-through analysis** |

---

# 🎥 Project Demo

Want to see the dashboard in action?

▶️ **[Watch the Power BI dashboard walkthrough](record.mp4)**

The video demonstrates the interactive Power BI report, including the executive pages and drill-through analysis.

---

# 📘 Case Study

The complete case study contains **13 pages** covering:

- Executive summary
- Business problem and scope
- Excel data-quality workflow
- PostgreSQL data model
- SQL validation
- Power BI semantic model
- DAX measures
- Country Market Investment dashboard
- Payment & Refund Risk dashboard
- Loyalty & Payment Gap dashboard
- Six-country drill-through analysis
- Verified market metrics
- Findings and operating recommendations

📄 **[Read the complete Starbucks Global Retail Analytics Case Study](case_study_starbucks.pdf)**

---

# 🚀 What This Project Demonstrates

- 📊 Executive dashboard storytelling
- 🧹 Practical data cleaning and governance
- 🗃️ Relational data modeling
- 🔍 Order-level reconciliation and anti-join logic
- 📐 DAX measure development
- 💳 Payment and refund risk analysis
- 🎯 Customer and loyalty economics
- 🌍 Multi-country performance analysis
- 🔎 Power BI drill-through design
- 🧠 Translating analytics into operational actions

---

## ⭐ Project Philosophy

> **Clean first. Analyze second. Turn charts into decisions.**

The dashboard is treated as the **final decision layer**, not the starting point. Major KPIs are tied back to defined business questions, explicit data-quality treatments and validation logic.

---

### 📎 Quick Access

**Data:** [`cusotmers.csv`](cusotmers.csv) · [`orders.csv`](orders.csv) · [`Revenue.csv`](Revenue.csv)  
**Power BI:** [`my_work.pbix`](my_work.pbix)  
**Demo:** [`record.mp4`](record.mp4)  
**Case Study:** [`case_study_starbucks.pdf`](case_study_starbucks.pdf)
