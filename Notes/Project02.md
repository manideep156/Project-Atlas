# 🏆 Project 02 – Business Sales Analytics

## Project Overview

Business Sales Analytics is an end-to-end Pandas portfolio project built using the Sample Superstore dataset.

The project focuses on transforming raw retail transaction data into meaningful business insights through data cleaning, exploratory analysis, aggregation, KPI calculation, profitability analysis, and management-level recommendations.

---

## Project Objective

The objective of this project is to analyze retail sales performance and identify:

- High-performing categories and sub-categories
- Profitable and unprofitable customer segments
- Strong and weak geographic markets
- Shipping-mode usage and profitability
- The impact of discounts on profit
- Opportunities to improve business performance

---

## Dataset Overview

The cleaned dataset contains:

- **9,977 transaction records**
- **531 cities**
- **49 states**
- **4 regions**
- **3 categories**
- **17 sub-categories**

### Dataset Features

- Ship Mode
- Segment
- Country
- City
- State
- Postal Code
- Region
- Category
- Sub-Category
- Sales
- Quantity
- Discount
- Profit
- Profit Margin

---

## Tools Used

- Python
- Pandas
- Jupyter Notebook
- Git
- GitHub

---

## Pandas Concepts Applied

- `read_csv()`
- `head()` and `tail()`
- `shape`
- `info()`
- `describe()`
- Missing-value inspection
- Duplicate detection and removal
- Column creation
- Boolean filtering
- `groupby()`
- `agg()`
- `sort_values()`
- `idxmax()` and `idxmin()`
- `nlargest()` and `nsmallest()`
- `value_counts()`
- `query()`
- Correlation analysis
- Feature engineering
- KPI calculation

---

## Data Cleaning Performed

- Inspected dataset dimensions and columns.
- Checked data types.
- Checked for missing values.
- Identified duplicate records.
- Removed duplicate records.
- Created a `Profit_Margin` column.
- Verified numerical fields before analysis.

The dataset was reduced from **9,994 records to 9,977 records** after duplicate removal.

---

## Key Performance Indicators

- **Total Sales:** $2,296,195.59
- **Total Profit:** $286,241.42
- **Total Quantity Sold:** 37,820
- **Average Sales per Record:** $230.15
- **Average Profit per Record:** $28.69
- **Average Discount:** 15.63%
- **Overall Profit Margin:** approximately 12.47%

---

## Category Analysis

### Highest Sales Category

**Technology**

Technology generated the highest category-level sales.

### Highest Profit Category

**Technology**

Technology also generated the highest category-level profit.

### Lowest Profit Category

**Furniture**

Furniture generated substantial sales but comparatively low profit.

### Most Sold Category

**Furniture**, based on the metric used during the project analysis.

---

## Sub-Category Analysis

### Highest Sales Sub-Category

**Phones**

### Highest Profit Sub-Category

**Copiers**

### Lowest Profit Sub-Category

**Tables**

Tables represented one of the largest profitability concerns in the dataset.

---

## Customer Segment Analysis

### Highest Sales Segment

**Consumer**

### Highest Total Profit Segment

**Consumer**

The Consumer segment generated the highest overall sales and profit because of its larger transaction volume.

Corporate and Home Office should also be evaluated using profit margin rather than only total contribution.

---

## Regional Analysis

### Highest Revenue Region

**West**

### Lowest Revenue Region

**South**

### Highest Profit Region

**West**

The West was the strongest overall region based on sales, profit, quantity, and profit margin.

---

## State Analysis

### Highest Profit State

**California**

### Lowest Profit State

**Texas**

Texas generated substantial sales but recorded the largest state-level loss.

Other unprofitable states included:

- Ohio
- Pennsylvania
- Illinois
- North Carolina
- Colorado
- Tennessee
- Arizona
- Florida
- Oregon

---

## City Analysis

### Highest Revenue City

**New York City**

### Highest Profit City

**New York City**

New York City was the strongest city based on both sales and profit.

---

## Shipping Analysis

### Most Frequently Used Ship Mode

**Standard Class**

### Records by Ship Mode

- Standard Class: 5,955
- Second Class: 1,943
- First Class: 1,537
- Same Day: 542

### Highest Average Sales by Ship Mode

**Same Day**, with average sales of approximately $236.76 per record.

### Highest Average Profit by Ship Mode

**First Class**, with average profit of approximately $31.85 per record.

---

## Discount Analysis

- **Average Discount:** 15.63%
- **Maximum Discount:** 80%
- **Discount–Profit Correlation:** approximately -0.2197

The negative correlation indicates that profit generally decreases as discounts increase.

Average profit remained positive between 0% and 20% discount levels but became negative from approximately 30% onward.

This suggests that aggressive discounting creates a significant profitability risk.

---

## Major Business Insights

1. Technology was the strongest category by sales and profit.
2. Furniture generated strong sales but very weak profitability.
3. Copiers were the most profitable sub-category.
4. Tables were the least profitable sub-category.
5. The West was the strongest-performing region.
6. New York City was the strongest city.
7. Texas recorded the largest state-level loss.
8. Standard Class was the most commonly used shipping mode.
9. The Consumer segment generated the highest total sales and profit.
10. Discounts above 20% require closer profitability checks.

---

## Business Recommendations

1. Increase investment in profitable Technology products.
2. Review Furniture pricing, costs, and discount policies.
3. Reassess Tables and Bookcases due to poor profitability.
4. Require approval for discounts above 20%.
5. Investigate losses in Texas and other underperforming states.
6. Replicate successful practices used in the West.
7. Use profit margin alongside sales when evaluating performance.
8. Create segment-specific marketing and discount strategies.
9. Monitor loss-making transactions regularly.
10. Expand high-margin products such as Copiers and Accessories.

---

## Main Learning

The most important learning from this project was that high sales do not automatically indicate strong business performance.

Furniture generated substantial revenue but contributed very little profit. Similarly, several states produced meaningful sales while still recording losses.

Business performance must therefore be evaluated using multiple metrics, including:

- Sales
- Profit
- Profit margin
- Quantity
- Discount
- Geographic performance
- Product mix

---

## Major Challenge

The largest challenge was not writing the Pandas code.

The major challenge was interpreting numerical outputs and converting them into clear business insights and recommendations.

This required moving beyond questions such as:

> Which value is highest?

and instead asking:

> Why is it high, is it profitable, and what action should management take?

---

## Enterprise Connection

This project follows a realistic analyst workflow:

1. Understand the business problem.
2. Inspect the raw dataset.
3. Clean and validate the data.
4. Define business KPIs.
5. Analyze products, customers, and regions.
6. Identify risks and opportunities.
7. Create recommendations.
8. Present findings through an executive summary.

The same business analysis can later be rebuilt using:

- SQL
- PySpark
- Azure Databricks
- Matplotlib
- Seaborn
- Machine Learning

---

## Deferred Enhancements

The following improvements are intentionally postponed:

- Matplotlib visualizations
- Seaborn statistical plots
- SQL implementation
- PySpark implementation
- Azure Databricks implementation
- Machine-learning extensions
- Executive dashboard

These enhancements are tracked in:

```text
Projects/Project02_Business_Sales_Analytics/Future_Enhancements.md