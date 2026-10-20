# Portfolio Project 3: Executive Power BI Dashboard & Operational KPI Suite

## 🎯 Executive Summary
An interactive, multi-page executive dashboard built using Power BI and connected to a cleaned relational SQL star-schema (`superstore`). Designed to provide stakeholders with instant macro-level visibility into revenue trends, product performance, and discount efficiency. 

---

## 📊 Dashboard Architecture & Page Structure

### Page 1: Executive Overview
* **Purpose:** A high-level, 3-second snapshot for executive leadership to gauge macro business health.
* **Key Components:**
  * **Global Slicer Header:** Interactive filtering by Region/State.
  * **Core KPI Cards:** `Total Revenue` ($2.30M) and `Total Orders` (5K unique transactions).
  * **Hero Time-Series Trend Line:** Continuous monthly revenue trend (2014–2017) exposing seasonal Superstore spikes and growth trajectories.
  * **Category Breakdown:** Clustered bar chart showing revenue distribution across Technology, Furniture, and Office Supplies with data labels.
  * **Sub-Category Distribution:** Detailed donut chart highlighting segment weights and exact financial shares.

### Page 2: Product & Customer Deep-Dive
* **Purpose:** Operational analytics for category managers and inventory teams to investigate granular performance.
* **Key Components:**
  * **Granular Product Matrix:** Table tracking individual `product_name` performance alongside total orders and revenue.
  * **Top Customers Bar Chart:** Identifies highest-value clients driving regional sales.
  * **Discount Impact Analysis:** Column chart evaluating revenue against discount brackets, revealing that the vast majority of revenue is generated at 0% and 20% discounts, proving heavy discounting yields diminishing returns.

---

## 🛠️ Technical Implementation & DAX Modeling
* **Data Model:** Star-schema architecture built from local PostgreSQL tables (`orders`, `products`, `customers`) with enforced primary and foreign keys.
* **Key DAX Measures:**
  * **Total Revenue:** Evaluated row-by-row using `SUMX` combined with relationship traversal to account for item-level quantities, unit prices, and dynamic discounts:
    ```dax
    Total Revenue = SUMX( orders, orders[quantity] * RELATED( products[unit_price] ) * (1 - orders[discount]) )
    ```
  * **Total Orders:** Utilized `DISTINCTCOUNT` on `order_id` to ensure accurate transaction counts without multi-line item inflation.

---

## 🚀 Deliverables & Files Included
* **`Superstore_Executive_Overview.pbix`**: The complete, fully interactive Power BI source file.
* **`Executive_Overview.pdf`**: Stakeholder-ready export for offline viewing.
* **Visual Documentation**: Full-resolution screenshots embedded below.

### Visual Preview
**Executive Overview Page:**
![Executive Overview Page](assets/executive-overview.png)

**Product & Customer Deep-Dive Page:**
![Product & Customer Deep-Dive Page](assets/product-deep-dive.png)
