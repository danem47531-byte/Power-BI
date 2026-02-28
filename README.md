# 👟 Adidas Customer Analytics — Power BI Project

![Power BI](https://img.shields.io/badge/Tool-Power%20BI-F2C811?logo=powerbi&logoColor=black) ![Status](https://img.shields.io/badge/Status-Completed-brightgreen) ![Domain](https://img.shields.io/badge/Domain-Customer%20Analytics-blue)

## 📌 Project Overview

This project is an end-to-end customer analytics dashboard built in **Microsoft Power BI** for **Adidas**. It analyses **1,000 customers** across demographics, transactions, store channels, loyalty tiers, and churn behavior to help the business make data-driven decisions around retention, loyalty program optimization, and channel strategy.

The project covers everything from **data cleaning in Power Query** to **DAX measures**, **interactive dashboards**, **CLV segmentation**, and **strategic business recommendations**.

---

## 🗂️ Dataset Overview

Two core datasets were used and merged within Power BI:

| Dataset | Description |
|---|---|
| `Customer_Demographics` | Customer ID, income level, region, membership date, loyalty tier, preferred channel, churn flag, churn reason |
| `Customer_Transactions` | Transaction ID, store type, product category, amount, promotion applied, points earned/redeemed, transaction date |

### 🌍 Regions Covered
Asia-Pacific · Europe · Middle East · North America · South America

### 🏪 Store Types
Flagship · Franchise · Online · Outlet

### 🎯 Loyalty Tiers
Base · Plus · Premium · Elite

---

## 🔧 Task 1 — Data Modeling & Cleaning (Power Query)

- Loaded datasets in **CSV format** into Power Query Editor
- Handled **duplicates and missing values**, and corrected data types across all columns
- Created a **calculated column** for Membership Duration:
  ```
  Membership Duration = Today – Membership Since
  (Using: Date.From(DateTime.LocalNow()))
  ```
- Extracted **Transaction Year** and **Transaction Month** using the Add Column → Date → Year/Month option in Power Query

---

## 📉 Task 2 — Churn Rate Analysis

**DAX Measures Used:**
```dax
Churn Rate % = CALCULATE(SUM(Churn_Flag)) / [Total Number Of Customer]
Total Number Of Customer = COUNT(Customer_ID)
```

**Key Findings:**
- Overall churn rate is **29.4%** — roughly 1 in 3 customers have disengaged
- **Elite customers** have the highest churn at **35%**, while **Base members** are most loyal at **28%**
- **High-income customers** show a striking **127% churn rate**, suggesting dissatisfaction or competitor switching
- **Online shoppers** (29%) churn slightly more than in-store customers (26%)
- Regionally, churn is highest in **Asia-Pacific (33%)** and lowest in **Europe (24%)**

---

## 🔁 Task 3 — Repeat Purchase Analysis

- Performed repeat purchase analysis in Power Query Editor
- Visualized average repeat purchases by **Age**, **Region**, and **Loyalty Tier**

**Key Findings:**
- **Elite customers** have the highest average repeat purchases (**3.77**), showing strong brand loyalty
- **Accessories and Footwear** are the top product categories among loyal customers
- **Europe and Asia-Pacific** show slightly higher repeat purchase rates (~3.6)
- **Younger customers (aged 20–30)** tend to purchase more frequently

---

## 🎁 Task 4 — Promotion & Loyalty Impact

- Analyzed the impact of promotions on spending and retention
- Visualized **Points Earned vs. Points Redeemed** by loyalty tier
- Compared average transaction amounts for promoted vs. non-promoted purchases

**Key Findings:**
- **52.7%** of transactions involved a promotion — offers are a major purchase driver
- Promotions boost average spending: **₹272 with promotions** vs. **₹259 without**
- **Elite and Premium members** have the lowest churn (28–32%), making them the most loyal groups
- **Base-tier members** earned the most points (207), followed by Plus (139), Premium (99), Elite (55)
- Higher-tier members are underutilizing their loyalty rewards — an area for improvement

---

## 🏪 Task 5 — Store & Channel Performance

- Merged store data with transaction data in Power BI
- Analyzed sales, transaction count, and churn rate across store types and regions

**Key Findings:**
- **Flagship stores and outlets** record the highest transactions and revenue, especially in Europe and South America
- Average transaction values are consistent across store types (**₹258–₹271**), with Franchise slightly ahead
- **Churn rates are similar across store types (~27%)**, but Flagship stores perform slightly better at **25.6%**
- Store opening year shows **no significant correlation with retention** — age of store doesn't impact loyalty
- The **online channel is underperforming** vs. physical stores — fewer locations and slower growth

---

## 💰 Task 6 — Customer Lifetime Value (CLV) Analysis

**DAX Measures Used:**
```dax
CLV = DIVIDE(
    CALCULATE(SUM(Amount)),
    Membership_Duration_in_Years
)

CVL Category =
VAR P25 = PERCENTILEX.INC(ALL(Demographics), CLV, 0.25)
VAR P70 = PERCENTILEX.INC(ALL(Demographics), CLV, 0.70)
RETURN
SWITCH(TRUE(),
    CLV < P25, "Low",
    CLV < P70, "Medium",
    "High"
)
```

- Segmented all customers into **Low, Medium, and High CLV** categories using DAX percentile logic

**Key Findings:**
- **Premium members** have the highest total CLV (~₹18.6K), followed by Plus (~₹11.1K) and Base (lowest)
- CLV peaks during certain months suggesting **seasonal shopping trends or successful promotion periods**
- **Asia-Pacific** shows higher CLV averages, creating strong targeted marketing opportunities
- High-CLV customers with frequent repeat purchases should be prioritized for retention campaigns

---

## 📊 Task 7 — Final Dashboard & KPIs

The final dashboard consolidates all analysis into a single interactive report with the following pages:

| Dashboard Page | Content |
|---|---|
| **KPIs** | Churn Rate %, Total CLV, Repeat Purchase Count with goal tracking |
| **Churn & Retention Metrics** | Churn by region, income level, channel, loyalty tier |
| **Repeat Purchase Analysis** | Repeat purchase trends by age, region, loyalty tier, product category |
| **Promotion & Loyalty Impact** | Promotion usage, points earned/redeemed, spending comparison |
| **Store & Channel Performance** | Sales by store type, region, transaction count, opening year trend |
| **CLV Analysis** | CLV over time, by loyalty tier and region, individual customer breakdown |
| **Loyalty & Promotion Impact** | Promotion count by tier, point engagement, spending with/without offers |
| **Segmentation** | Customer-level breakdown with CLV category, repeat purchases, and tier |
| **Slicers** | Interactive filters: Income Level, Loyalty Tier, Region, Preferred Channel |

### 📌 KPI Summary

| Metric | Value |
|---|---|
| Churn Rate % | 29.40% |
| Total CLV | ₹114,604.70 |
| Total Repeat Purchases | 282 |

---

## 💡 Top 3 Strategic Recommendations for Adidas

**1. Which customers to prioritize for retention?**
Prioritize customers with a **high CLV** by offering them exclusive deals and personalized incentives tied to their repeat purchase behavior.

**2. Which channels are underperforming?**
The **online channel** lags behind physical stores across most regions — fewer locations and slower year-over-year growth. Adidas should invest in strengthening its e-commerce presence and digital sales strategy.

**3. How to strengthen loyalty program engagement?**
**Premium and Elite members** are not redeeming points at significantly higher rates than Base members. Improving this requires better rewards, easier point redemption, and personalized offers to re-engage higher-tier customers.

---

## 🛠️ Power BI Features & Techniques Used

| Feature | Usage |
|---|---|
| Power Query | Data loading (CSV), deduplication, data type correction, column extraction |
| DAX Measures | Churn Rate %, CLV, CVL Category (percentile-based segmentation) |
| Calculated Columns | Membership Duration, Transaction Year/Month |
| Pivot/Matrix Visuals | Customer-level breakdowns by tier, region, and CLV category |
| Bar & Line Charts | Churn trends, CLV over time, repeat purchases by age/region |
| Scatter Plots | Store opening year vs. retention correlation |
| Slicers | Income Level, Loyalty Tier, Region, Preferred Channel |
| KPI Cards | Churn Rate %, CLV, Repeat Purchase Count with goal comparison |
| Decomposition | Churn breakdown by flag, income, and reason |

---

## 📁 Project Files

```
📦 POWER BI PROJECT
 ┣ 📊 POWER BI PROJECT.pbix         # Full interactive Power BI dashboard
 ┣ 📄 POWER BI PROJECT.pdf          # Dashboard screenshots (all pages)
 ┣ 📄 Key Findings.pdf              # Detailed task-by-task findings & DAX formulas
 ┗ 🔗 VIDEO LINK.pdf                # Video walkthrough link
```

---

## 🚀 How to Open

1. Download and install **[Microsoft Power BI Desktop](https://powerbi.microsoft.com/desktop/)** (free)
2. Open `POWER BI PROJECT.pbix`
3. Use the **slicer panels** (Income Level, Loyalty Tier, Region, Preferred Channel) to filter and explore the dashboards interactively
4. Refer to `Key Findings.pdf` for the DAX formulas and written analysis for each task

---

## 🎥 Project Walkthrough

A full video walkthrough is available here:
🔗 [Watch on Loom](https://www.loom.com/share/6993b7de980b4169b5463b9a6afb630d?sid=546d1284-d2d3-4936-85ef-7b19ed40fc31)

---

## 👤 Author

### Tridev Pal
📍 Calcutta, West Bengal, India

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?logo=linkedin)](https://www.linkedin.com/in/tridev-pal-74575a379/)

> Feel free to connect or raise issues via GitHub if you have suggestions or improvements!
