# 🛒 Blinkit Grocery Sales Analysis

A data analytics project exploring BlinkIT grocery sales data to uncover insights into outlet performance, product category trends, fat-content preferences, and store-format effectiveness — using **Power BI** (and **Excel** as the source layer).

---

## 📌 Project Overview

This project analyzes **8,523 product-level sales records** across BlinkIT outlets. The goal is to derive actionable insights that guide inventory planning, outlet-format strategy, and product-category investment through an interactive Power BI dashboard.

---

## 📂 Dataset Summary

| Property | Details |
|---|---|
| Total Rows | 8,523 |
| Total Columns | 12 |
| Missing Data | 1,463 nulls in `Item Weight` (~17% of rows) |
| Data Quality Issues | `Item Fat Content` has inconsistent labels (`Low Fat`, `low fat`, `LF`, `Regular`, `reg`) |

**Key Features:**
- **Product Details** — Item Identifier, Item Type, Item Weight, Item Fat Content, Item Visibility
- **Outlet Details** — Outlet Identifier, Outlet Establishment Year, Outlet Size, Outlet Location Type, Outlet Type
- **Performance Metrics** — Sales, Rating

---

## 🔧 Tools & Technologies

| Tool | Purpose |
|---|---|
| Microsoft Excel | Source data storage (`.xlsx`) |
| Power BI Desktop | Data modeling, DAX measures, and dashboard visualization |
| Power Query | Data import and transformation layer within Power BI |
| DAX (Data Analysis Expressions) | Calculated measures for KPIs |

---

## 🧹 Data Preparation

- **Data Loading** — Imported `BlinkIT Grocery Data.xlsx` into Power BI as a single flat table
- **Data Model** — Single-table model (`BlinkIT Grocery Data`) with 12 columns; no relationships required
- **Missing Data** — `Item Weight` left null for ~17% of records (not imputed in current model — flagged as a follow-up improvement)
- **Categorical Inconsistency** — `Item Fat Content` contains 5 raw label variants for what are really only 2 categories (Low Fat / Regular); cleanup recommended via Power Query `Replace Values`
- **Calculated Measures (DAX)**
  - `Total Sales` = `SUM('BlinkIT Grocery Data'[Sales])`
  - `Avg Sales` = `AVERAGE('BlinkIT Grocery Data'[Sales])`
  - `No. of Items` = `COUNTROWS('BlinkIT Grocery Data')`
  - `Avg Rating` = `AVERAGE('BlinkIT Grocery Data'[Rating])`

---

## 📊 Dashboard Design (Power BI)

A single-page interactive dashboard (`Blinkit_Sales_Dashboard.pbix`) was built with the following layout:

| Section | Visual Type | Field(s) |
|---|---|---|
| KPI Header | Card visuals | Total Sales, Avg Sales, No. of Items, Avg Rating |
| Fat Content Split | Donut chart | `Item Fat Content` |
| Fat by Outlet | Clustered bar chart | `Item Fat Content` × `Outlet Identifier` |
| Item Type Performance | Bar chart | `Item Type` vs Sales |
| Outlet Establishment Trend | Line chart | `Outlet Establishment Year` vs Sales |
| Outlet Size Split | Donut chart | `Outlet Size` |
| Outlet Location Funnel | Funnel chart | `Outlet Location Type` |
| Outlet Type Summary | Pivot table | Total Sales, No. of Items, Avg Sales, Avg Rating, Item Visibility by `Outlet Type` |
| Filters | Slicers | Metrics toggle, Outlet Location Type, Outlet Size, Item Type |

---

## 💡 Key Business Insights

1. **Total Revenue** — $1,201,681 in sales across 8,523 items; average sale value $141 per item
2. **Low Fat dominates volume** — Low Fat items generate ~$776,320 (≈65%) of total sales vs ~$425,362 for Regular — once label variants are merged
3. **Supermarket Type1 is the revenue engine** — drives $787,550 (~66% of total sales) across 5,577 items, far ahead of Grocery Stores and Type2/Type3 formats
4. **Grocery Stores underperform on revenue but not on average ticket** — fewer total sales, yet avg sale per item is close to other formats, suggesting a footfall/assortment gap rather than a pricing one
5. **Tier 3 locations lead** — $472,133 in sales, ahead of Tier 2 ($393,151) and Tier 1 ($336,398) — demand is strongest outside metro "Tier 1" markets
6. **Medium-sized outlets generate the most revenue** ($507,896), followed by Small ($444,794) and High ($248,992) — store footprint doesn't scale linearly with sales
7. **Fruits & Vegetables and Snack Foods are the top categories**, each contributing over $175,000 in sales — strong candidates for prioritized shelf space and stocking
8. **2018 stands out as an outlier establishment year** — almost 1.5x the item count of any other year (1,463 vs ~930 average), which inflates that year's totals and should be normalized before drawing trend conclusions
9. **Ratings cluster narrowly** — Avg Rating sits at ~3.97 across the board with little variance, suggesting the rating field carries limited discriminating power for outlet/category comparisons in its current form
10. **~17% of records lack Item Weight** — a meaningful gap for any future weight-based pricing or logistics analysis

---

## 📁 Project Structure

```
blinkit-sales-analysis/
│
├── 1_BlinkIT_Grocery_Data.xlsx        # Raw dataset (8,523 rows × 12 columns)
├── 2_Blinkit_Sales_Dashboard.pbix     # Power BI dashboard (KPIs, charts, slicers)
├── 3 images/
│   └── dashboard_preview.png         # Dashboard screenshot
└── README.md
```

### Dashboard Preview

![BlinkIT Sales Dashboard](images/dashboard_preview.png)
