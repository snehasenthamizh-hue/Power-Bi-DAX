E-Commerce Sales Analysis Using Power BI and DAX

Project Overview

This project focuses on analyzing an E-Commerce Sales Dataset using **Microsoft Power BI and DAX (Data Analysis Expressions)**.

The main goal is to create calculated columns, measures, and interactive visualizations to understand sales performance, profitability, order counts, and sales targets.

This project builds on the data transformation and data modeling work completed in the previous assignment. It uses the existing tables and relationships to prepare meaningful business reports.

Objectives

- Create calculated columns using DAX.
- Calculate important business metrics using DAX measures.
- Analyze sales, profit, and order counts.
- Compare actual sales with sales targets.
- Identify monthly sales trends.
- Analyze sales performance across categories, sub-categories, cities, and states.
- Build interactive Power BI visualizations for business reporting.

Dataset Description

The project uses three tables:

| Table Name | Description | Main Columns |
|---|---|---|
| List of Orders | Contains order dates and customer and location information, along with sales and profit details. | Order ID, Order Date, Customer Name, City, State, Category, Amount, Profit |
| Order Details | Contains product category details and order-level sales information. | Order ID, Category, Sub-Category, Quantity, Amount, Profit |
| Sales Target | Contains sales targets for categories and months. | Category, Month of Order Date, Target |

The existing data model and relationships are used to connect these tables for analysis.

 Tools and Technologies

- **Microsoft Power BI Desktop** – Data modeling, DAX calculations, and visualizations.
- **DAX** – Creating calculated columns and measures.
- **Power BI Visualizations** – Presenting sales, profit, targets, and order data.

 DAX Calculations

1. Calculated Columns

Calculated columns create new fields in the `Order Details` table.

 Category Type

Combines the category and sub-category into a single column.

```dax
Category Type =
'Order Details'[Category] & " - " &
'Order Details'[Sub-Category]
```

**Purpose:** Makes it easier to identify products using their category and sub-category together.

 Revenue per Order

Calculates revenue using the Amount and Quantity columns.

```dax
Revenue per Order =
'Order Details'[Amount] *
'Order Details'[Quantity]
```

**Purpose:** Creates a new value for each row by multiplying the amount by the quantity.

*Note: This follows the assignment formula. Confirm the meaning of the Amount column before interpreting this calculation as total revenue, because Amount may already represent the sales value.*

Sales Category

Classifies each row as Above Average or Below Average by comparing its Amount with the overall average Amount.

```dax
Sales Category =
IF(
    'Order Details'[Amount] >
        CALCULATE(
            AVERAGE('Order Details'[Amount]),
            ALL('Order Details')
        ),
    "Above Average",
    "Below Average"
)
```

**Purpose:** Helps distinguish rows with amounts above the overall average from those at or below it. Values equal to the average are classified as `Below Average` by this formula.

2. Calculated Measures

Measures calculate values for use in reports and visualizations.

Order Count

Counts the distinct order IDs in the `Order Details` table.

```dax
Order Count =
DISTINCTCOUNT('Order Details'[Order ID])
```

**Purpose:** Measures the number of unique orders rather than counting every row.

Average Profit in Delhi

Calculates the average profit for orders associated with Delhi.

```dax
Average Profit in Delhi =
CALCULATE(
    AVERAGE('Order Details'[Profit]),
    'List of Orders'[City] = "Delhi"
)
```

**Purpose:** Helps analyze average profit for Delhi orders, assuming the existing model relationships correctly propagate the city filter.

#### Year-to-Date (YTD) Sales

Calculates cumulative sales from the beginning of the year through the current date in the report's date context.

```dax
YTD Sales =
TOTALYTD(
    SUM('Order Details'[Amount]),
    'List of Orders'[Order Date]
)
```

**Purpose:** Helps track sales performance throughout the year.

*Note: The YTD calculation depends on the date relationship and the date context in the Power BI model.*

Data Visualization

The project includes the following visualizations.

| No. | Visualization | Power BI Chart | Purpose |
|---|---|---|---|
| 1 | Sales Target Achievement by Category | Clustered Column Chart | Compares actual sales and sales targets across categories. |
| 2 | Max Profit Margin by Sub-Category | Donut Chart | Displays the maximum Profit Margin for each sub-category. |
| 3 | Monthly Sales Trend | Line Chart | Shows how sales change over time by month. |
| 4 | Profit and Quantity by Sub-Category | Scatter Chart | Compares quantity sold with profit for different sub-categories. |
| 5 | Total Sales Amount and Sales Target | Cards | Displays total sales amount and total sales target separately. |
| 6 | Minimum Target by Segment | Multi-row Card | Displays the minimum target for each segment. |
| 7 | Sales Performance Matrix | Matrix | Compares sales and targets across categories and months. |
| 8 | Geographic Sales Analysis | Map | Shows sales distribution across cities. |
| 9 | Sales Distribution by Sub-Category | Treemap | Represents sales distribution using rectangles of different sizes. |
| 10 | Order Count Analysis by State | Funnel Chart | Displays distinct order counts for different states. |

Visualization Details

- **Clustered Column Chart:** Uses Category on the X-axis and sales Amount and Target as values to compare performance against targets.
- **Donut Chart:** Uses Sub-Category as the legend and Profit Margin with the Maximum aggregation. The Profit Margin field must exist in the model.
- **Line Chart:** Uses Order Date at the month level and sales Amount to show monthly trends. The year should remain identifiable when multiple years are present.
- **Scatter Chart:** Uses Quantity on the X-axis, Profit on the Y-axis, and Sub-Category as the detail field.
- **Cards:** Displays the sum of Amount and the sum of Target in separate cards.
- **Multi-row Card:** Displays the minimum target for each segment, using the appropriate segment field and minimum aggregation.
- **Matrix:** Uses Category as rows, month as columns, and summed Amount and Target as values.
- **Map:** Uses City for location and summed Amount for bubble size to compare sales geographically.
- **Treemap:** Uses Sub-Category and summed Amount to show the relative distribution of sales.
- **Funnel Chart:** Uses State as the category and distinct Order ID count as the value, sorted in descending order.

Key Business Questions

This project is designed to help answer questions such as:

- How do actual sales compare with the sales targets?
- How do sales change from month to month?
- Which sub-categories have higher or lower profit values?
- How does quantity sold relate to profit?
- What is the average profit for orders from Delhi?
- How many unique orders are recorded?
- How are sales distributed across cities?
- How do order counts differ across states?

The actual answers depend on the data in the Power BI file and the results displayed in the report.

Project Workflow

1. Use the existing E-Commerce Sales Dataset and data model.
2. Review the three tables and their relationships.
3. Create the calculated columns in the `Order Details` table.
4. Create the Order Count, Average Profit in Delhi, and YTD Sales measures.
5. Build the required Power BI charts, cards, matrix, map, and funnel.
6. Configure field aggregations and visual formatting.
7. Check that the calculations and relationships produce appropriate results.
8. Save the Power BI project file.

Skills Demonstrated

- DAX calculated columns and measures
- Conditional logic using `IF`
- Filter context using `CALCULATE` and `ALL`
- Aggregation functions such as `AVERAGE`, `SUM`, and `DISTINCTCOUNT`
- Year-to-date calculations using `TOTALYTD`
- Sales target comparison
- Time-based sales analysis
- Geographic and category-based analysis
- Power BI data modeling and visualization

Project Files

- `Power bi DAX.pbix` – Power BI project file.
- `Power bi DAX.docx` – Assignment instructions and DAX formulas.

Conclusion

This project demonstrates how DAX and Power BI can be used to turn e-commerce order data into useful business reports. It combines calculated columns, measures, and interactive visualizations to support the analysis of sales performance, profitability, order counts, and sales targets.

The project also provides practical experience with DAX expressions, data relationships, aggregations, and visual storytelling in Power BI.
