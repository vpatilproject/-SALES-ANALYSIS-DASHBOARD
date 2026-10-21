# Sales Analysis Dashboard (Power BI)

An interactive Power BI dashboard that analyses sales, profit, customers, products, regions, shipping modes and discounts for an organization's order data from 2016 to 2019.

**Project type:** Data Analytics / Business Intelligence
**Tool:** Microsoft Power BI Desktop (Power Query + DAX)
**Program:** CoachX Data Analytics Project

---

## 1. Objectives

- Evaluate total sales and profit over time to find trends.
- Find top-performing products, categories, customers, regions and cities.
- Assess the effect of shipping modes on sales.
- Study the relationship between discount and profit to find a profitable discount level.
- Support decisions on pricing, inventory and regional strategy.

## 2. Dataset

| Item | Detail |
|---|---|
| Source file | `Sales_Analysis.xlsx` (sheet: `Sales`) |
| Rows / columns | 9,994 order lines / 21 columns |
| Period | January 2016 to December 2019 |
| Customers / products / cities | 793 / 1,850 / 531 |
| Regions | Central, East, South, West |
| Segments | Consumer, Corporate, Home Office |
| Categories | Furniture, Office Supplies, Technology (17 sub-categories) |

Only the `Sales` sheet is used. Sheet2, Sheet3 and Sheet4 contain no analysis data and are not loaded.

## 3. Data Cleaning (Power Query)

- Converted `Order Date` and `Ship Date` from text to Date (English US locale).
- Set `Postal Code` to Text and filled 11 blanks (Burlington, VT) with `05401`.
- Kept `Sales`, `Profit` and `Discount` as Decimal Number (a Whole Number type rounds Avg Discount to 8.6% instead of 15.6%).
- Removed the `Row ID` column.
- Added columns: `Sales Tax` (10% of Sales), `Sales Category` (High if Sales > 100, else Low), `Discount Flag` (With / Without Discount), `First Name`, `Last Name`.
- Created separate reference queries: `Sales_NoDup` (unique Order ID) and `Sales_Discounted` (Discount > 0).

## 4. Data Model

- A `Calendar` table (Date, Year, Month No, Month, Quarter, YearMonth) marked as the date table.
- Relationship: `Calendar[Date]` to `Sales[Order Date]` (one to many, single direction).
- `Month` is sorted by `Month No`.

## 5. DAX Measures

| Measure | Purpose |
|---|---|
| Total Sales, Total Profit, Total Quantity | Basic totals |
| Profit Margin % | Total Profit / Total Sales |
| Avg Discount, Avg Profit, Avg Quantity | Averages |
| Total Customers, Avg Sales per Customer | Customer metrics |
| Sales PY, YoY Growth % | Year-over-year growth |
| Running Total Sales | Cumulative sales over time |
| Sales Contribution % | Share of sales by region |
| Customer Rank | Top N customers |
| Sales 2019, Total Sales Tax, Total Sales NoDup | Power Query task results |
| Sales With Discount / Without Discount | Discount comparison |

## 6. Report Pages

| Page | Contents |
|---|---|
| Index | Navigation page |
| Executive Overview | KPI cards, monthly sales trend, sales by ship mode, profit by region, sales vs profit by category |
| Customer & Product | Top customers and products, sub-category sales and profit, segment sales, average quantity |
| Time & Region Analysis | YoY growth, sales vs quantity, cumulative sales, sales by year and category, profit by month, city map, region contribution |
| Discount & Profit | Discount vs profit scatter, average profit by discount, sales categories, with vs without discount, sales tax, before vs after duplicates |
| Power Query Analysis | 2019 sales, discounted orders, sales tax by category, average sales by year, sales by first name, running total |

**Interactivity:** Year, Region and Segment slicers, page navigation bar, a Reset Filters button and cross-filtering between visuals.

**Colour theme:** Navy `#1F3A5F`, Blue `#2E75B6` (sales), Green `#2BA58B` (profit), Orange `#F2A33A`, Red `#D64550` (loss).

## 7. Key Insights

| KPI | Value |
|---|---|
| Total Sales | 2.30M |
| Total Profit | 286K |
| Profit Margin | 12.5% |
| Total Quantity | 37,873 |
| Average Discount | 15.6% |

- Sales grew from 484K (2016) to 733K (2019). YoY growth: 2017 -2.8%, 2018 +29.5%, 2019 +20.4%.
- Technology is the top category (836K sales, 145K profit). Furniture has 742K sales but only 18K profit (about 2.5% margin).
- Tables (-17.7K), Bookcases and Supplies lose money.
- West leads in profit (108K). Central has 501K sales but only 40K profit.
- Standard Class carries about 59% of sales.
- **Discounts up to 20% keep profit positive; from 30% the average profit turns negative.** Orders with a discount made a net loss of 34.6K, while orders without a discount earned 321K.
- Removing duplicate Order IDs cuts sales from 2.30M to 1.20M, because one order contains several products.

## 8. Recommendations

1. Cap discounts at 20 to 25%.
2. Review pricing and sourcing for Tables, Bookcases and Supplies.
3. Improve Furniture margin.
4. Review Central region costs and discounting.
5. Focus growth on Technology and the Consumer segment.
6. Run a loyalty program for top customers.

## 9. Project Files

```
Sales_Analysis_Project/
├── Sales_Analysis.xlsx                  # source data
├── SALES_ANALYSIS_PROJECT.pbix          # Power BI report
├── Sales_Analysis_Presentation.pptx     # presentation (20 slides)
├── Sales_Analysis_Documentation.pdf     # project documentation
└── README.md
```

## 10. How to Open

1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free, Windows).
2. Open `SALES_ANALYSIS_PROJECT.pbix`.
3. If Power BI asks for the data source, point it to `Sales_Analysis.xlsx` (Home > Transform data > Data source settings).
4. Use the navigation bar to move between pages and the slicers to filter.

## Author

**Name:** _Your name_
**Course:** CoachX Data Analytics
**Date:** October 2026
