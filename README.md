# inventory_analysis## 🚀 Project Overview

Managing retail operations requires real-time coordination across **sales velocity**, **inventory holding costs**, and **supplier reliability**. 

This project bridges transactional data with executive decision-making by structuring:
- **Product Catalog Management**: 34 SKUs across 4 major retail categories.
- **Multi-Channel Sales**: Granular transaction logs across Web, Marketplace, B2B, and Retail partners.
- **Supplier Quality Benchmarking**: Lead time, delivery rates, and vendor risk profiles.
- **Real-Time Interactive Dashboard**: An interactive executive view powered by dynamic filters and 3D visual models.

---

## 🗂️ Ecosystem & Workbook Architecture

The project is structured into 5 interconnected sheets designed for separation of concerns (Inputs → Modeling → Presentation):
### Tab Breakdown

| Tab Name | Role | Key Data & Columns |
| :--- | :--- | :--- |
| **`Dashboard`** | Executive UI | Interactive Category Dropdown (`D9`), 5 Metric Cards, 3D Pie Chart, Horizontal Velocity Bar Chart, Revenue/Margin Trendline, Vendor Performance Cards. |
| **`Inventory_Data`** | Catalog Master | `SKU`, `Product Name`, `Category`, `Unit Cost`, `Retail Price`, `Stock Units`, `Reorder Level`, `Units On Order`, `Total Inventory Value`, `Margin %`, `Restock Status`. |
| **`Sales_Orders`** | Sales Ledger | `Order ID`, `Date`, `SKU`, `Product Name`, `Category`, `Channel`, `Units Sold`, `Unit Price`, `Revenue`, `COGS`, `Gross Profit`. |
| **`Suppliers_Data`** | Vendor Operations | `Supplier ID`, `Supplier Name`, `Category`, `Lead Time Days`, `On-Time Delivery %`, `Reliability Rating`, `Active Orders`, `Total Spend`. |
| **`Calc_Data`** | Engine / Matrix | Aggregates KPIs, powers category filter matrices, and isolates dashboard formulas from raw user data. |

---

## 📈 Key Performance Indicators (KPIs)

The executive dashboard tracks 5 core health metrics:

1. **Total Revenue (`$35,454.49`)**: Aggregate gross revenue across all completed channel orders.
2. **Gross Profit Margin (`56.7%`)**: Overall margin efficiency calculated as `(Total Revenue - Total COGS) / Total Revenue`.
3. **Inventory Valuation (`$62,337.50`)**: Total capital tied up in warehouse inventory (`Stock Units × Unit Cost`).
4. **Units in Stock (`3,024 units`)**: Net physical inventory units available across all active product categories.
5. **Supplier Fulfillment Rate (`94.4%`)**: Weighted on-time fulfillment rate across tier-1 procurement partners.

---

## ⚙️ Data Modeling & Formula Logic

### 1. Dynamic Relational Lookups
Sales transactions pull live product metadata and pricing from `Inventory_Data` using structured `VLOOKUP`:
```excel
=VLOOKUP(C2, Inventory_Data!$A$2:$E$35, 2, FALSE)   ' Pulls Product Name
=VLOOKUP(C2, Inventory_Data!$A$2:$E$35, 5, FALSE)   ' Pulls Unit Retail Price
``` excel
=IF(F2 <= G2, "Needs Reorder", "Sufficient")

`````` excel
=IF(Dashboard!$D$9="All Categories", 
    SUM(Inventory_Data!I2:I35), 
    SUMIF(Inventory_Data!C2:C35, Dashboard!$D$9, Inventory_Data!I2:I35))

`````` excel
=FILTER(Inventory_Data!A2:K35, (Dashboard!$D$9="All Categories") + (Inventory_Data!C2:C35 = Dashboard!$D$9))

```[ Step 1: Stock Monitoring ] ──► [ Step 2: Purchase Order ] ──► [ Step 3: Quality Control ] ──► [ Step 4: Warehouse Restock ]
  • Dynamic threshold scan         • Auto-tally units on order      • Barcode scan verification      • Shelf intake & inventory sync
  • Restock alert triggered        • Vendor PO dispatched           • 99.2% QA compliance pass rate  • Live dashboard update### Project Explanation & Portfolio Presentation Tips

If you are using this project for your GitHub portfolio or resume, here is how to highlight your work:

1. **Clean Architecture (3-Tier Design)**:
   - **Data Tier (`Sales_Orders`, `Inventory_Data`, `Suppliers_Data`)**: Normalized transactional data with standardized data types, formatted currency/percentages, and frozen headers.
   - **Logic Tier (`Calc_Data`)**: Prevents clutter by housing all calculation matrices, dynamic `SUMIF`/`FILTER` formulas, and chart feeds off the main dashboard.
   - **Presentation Tier (`Dashboard`)**: Executive-ready layout with hidden gridlines, consistent typography, card-based KPIs, and 3D visual models.

2. **Core Skills Demonstrated**:
   - **Spreadsheet Data Modeling**: Multi-sheet lookups, relational data linking, dynamic arrays (`FILTER`), and nested conditional logic (`IF`, `SUMIFS`, `AVERAGEIFS`).
   - **Business Acumen & Supply Chain Analytics**: Translating operational metrics (Lead Time, Reorder Point, COGS, Stockout Risk) into actionable executive summaries.
   - **UI/UX in Spreadsheets**: Scorecard cards, visual flow diagrams, interactive cell-validation dropdowns, and dual-axis chart configurations.
