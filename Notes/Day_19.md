# 📅 Day 19 – Advanced Pandas & Performance Optimization

**Date:** July 29, 2026  
**Status:** ✅ Completed  
**Phase:** Pandas

---

# 🎯 Objective

Learn advanced Pandas techniques for sorting, ranking, retrieving top or bottom records, filtering data with readable expressions, and creating calculated columns efficiently.

The objective of this session was not only to learn additional functions but also to understand how to choose efficient and readable approaches for common business-analysis tasks.

---

# 📚 1. Sorting Data

## Definition

Sorting arranges DataFrame records according to the values of one or more columns.

Pandas provides the `sort_values()` method for sorting rows based on column values.

---

## Basic Syntax

```python
df.sort_values(by="Sales")
```

By default, values are sorted in ascending order.

---

## Descending Order

```python
df.sort_values(
    by="Sales",
    ascending=False
)
```

---

## Sorting by Multiple Columns

```python
df.sort_values(
    by=["Region", "Sales"],
    ascending=[True, False]
)
```

This operation:

1. Sorts regions alphabetically.
2. Sorts sales from highest to lowest within each region.

---

## Important Parameters

| Parameter | Purpose |
|---|---|
| `by` | Column or columns used for sorting |
| `ascending` | Controls ascending or descending order |
| `inplace` | Modifies the original DataFrame when set to `True` |
| `na_position` | Places missing values first or last |
| `ignore_index` | Resets the resulting index |

---

## Business Uses

- Arranging sales reports
- Finding high-performing employees
- Ordering transactions by value
- Preparing data for dashboards
- Comparing regional performance

---

# 📚 2. Ranking Data

## Definition

Ranking assigns a relative position to each value in a Series.

The highest or lowest value can receive the first rank depending on the value of the `ascending` parameter.

---

## Rank Sales from Highest to Lowest

```python
df["Sales_Rank"] = df["Sales"].rank(
    ascending=False
)
```

The highest sales value receives Rank 1.

---

## Rank as Integers

```python
df["Sales_Rank"] = df["Sales"].rank(
    ascending=False,
    method="dense"
).astype(int)
```

---

## Ranking Methods

| Method | Behaviour with Ties |
|---|---|
| `average` | Gives tied values their average rank |
| `min` | Gives tied values the lowest available rank |
| `max` | Gives tied values the highest available rank |
| `first` | Ranks tied values according to row order |
| `dense` | Gives tied values the same rank without gaps |

---

## Example

Consider these values:

```text
100, 90, 90, 80
```

### Standard Ranking

```text
1, 2.5, 2.5, 4
```

### Dense Ranking

```text
1, 2, 2, 3
```

---

## Business Uses

- Employee leaderboards
- Product-performance rankings
- Customer-value rankings
- Regional sales comparisons
- Bonus and incentive programmes

---

# 📚 3. Selecting Top and Bottom Records

## `nlargest()`

Returns the rows containing the largest values in a column.

```python
df.nlargest(5, "Revenue")
```

---

## `nsmallest()`

Returns the rows containing the smallest values in a column.

```python
df.nsmallest(3, "Revenue")
```

---

## Why Use These Functions?

The following code sorts the entire DataFrame:

```python
df.sort_values(
    by="Revenue",
    ascending=False
).head(5)
```

When only a limited number of top records is required, this is usually clearer:

```python
df.nlargest(5, "Revenue")
```

Similarly:

```python
df.nsmallest(3, "Revenue")
```

is preferable when retrieving only the lowest records.

---

## Business Uses

- Top-selling products
- Highest-value customers
- Lowest-performing branches
- Most expensive transactions
- Top employee performers

---

# 📚 4. Filtering with `query()`

## Definition

The `query()` method filters DataFrame records using an expression written as a string.

It can make multi-condition filtering more readable.

---

## Standard Boolean Filtering

```python
df[
    (df["Sales"] > 80000) &
    (df["Region"] == "East")
]
```

---

## Equivalent `query()` Expression

```python
df.query(
    "Sales > 80000 and Region == 'East'"
)
```

---

## Using Multiple Conditions

```python
df.query(
    "Sales > 80000 and Orders > 100"
)
```

---

## Using `or`

```python
df.query(
    "Region == 'East' or Region == 'West'"
)
```

---

## Using `in`

```python
df.query(
    "Region in ['East', 'West']"
)
```

---

## Referencing External Variables

Use `@` to access a Python variable inside `query()`.

```python
minimum_sales = 80000

df.query(
    "Sales > @minimum_sales"
)
```

---

## Columns Containing Spaces

Column names containing spaces must be placed inside backticks.

```python
df.query(
    "`Customer Rating` > 4.5"
)
```

---

## Advantages

- Improves readability
- Simplifies complex conditions
- Reduces repeated DataFrame references
- Makes business rules easier to understand

---

## When Standard Boolean Filtering May Be Better

Use standard filtering when:

- Column names are generated dynamically.
- Conditions are constructed programmatically.
- String operations are required.
- The expression is easier to understand with explicit masks.

---

# 📚 5. Evaluating Expressions with `eval()`

## Definition

The `eval()` method evaluates arithmetic or logical expressions using DataFrame columns.

It can be used to create calculated columns.

---

## Standard Column Calculation

```python
df["Revenue_Per_Unit"] = (
    df["Revenue"] / df["Units Sold"]
)
```

---

## Equivalent `eval()` Operation

```python
df.eval(
    "Revenue_Per_Unit = Revenue / `Units Sold`",
    inplace=True
)
```

---

## Multiple Arithmetic Operations

```python
df.eval(
    "Performance_Score = Sales * 0.7 + Orders * 0.3",
    inplace=True
)
```

---

## Important Parameters

| Parameter | Purpose |
|---|---|
| `expr` | Expression to evaluate |
| `inplace` | Stores the result in the original DataFrame |
| `engine` | Selects the expression-execution engine |
| `parser` | Controls how the expression is interpreted |

---

## Advantages

- Produces concise expressions
- Improves readability for calculations
- Reduces repeated DataFrame references
- Can help with memory efficiency on sufficiently large numerical datasets

---

## Important Limitation

`eval()` is most suitable for arithmetic and logical expressions.

It should not be used merely to replace every standard Pandas column operation. A normal expression is often easier to debug for small or moderately sized datasets.

---

# 📚 6. Calculated Business Metrics

Calculated columns convert raw values into useful business indicators.

---

## Average Order Value

```python
df["Average_Order_Value"] = (
    df["Sales"] / df["Orders"]
)
```

---

## Revenue per Unit

```python
df["Revenue_Per_Unit"] = (
    df["Revenue"] / df["Units Sold"]
)
```

---

## Performance Score

A performance score can combine multiple business measures.

```python
df["Performance_Score"] = (
    df["Monthly_Sales"] * 0.6
    + df["Orders_Completed"] * 100 * 0.2
    + df["Customer_Rating"] * 10000 * 0.2
)
```

The exact formula depends on business requirements.

Before combining metrics, analysts should consider:

- Different measurement scales
- Appropriate weights
- Business priorities
- Possible normalization
- Whether the final metric is interpretable

---

## Bonus Eligibility

```python
df["Bonus_Eligible"] = (
    (df["Monthly_Sales"] >= 40000) &
    (df["Customer_Rating"] >= 4.5)
)
```

---

## Premium Product Flag

```python
df["Premium_Performer"] = (
    (df["Revenue"] >= 40000) &
    (df["Customer Rating"] >= 4.5)
)
```

---

# ⚡ 7. Performance Optimization

## Prefer Vectorized Operations

Vectorized operations work on an entire Series or DataFrame column.

```python
df["Total"] = df["Price"] * df["Quantity"]
```

Avoid unnecessary row-by-row loops:

```python
for index, row in df.iterrows():
    df.loc[index, "Total"] = (
        row["Price"] * row["Quantity"]
    )
```

---

## Prefer Built-In Pandas Methods

Use:

```python
df.nlargest(5, "Revenue")
```

instead of unnecessarily sorting the entire dataset when only five records are needed.

---

## Filter Before Expensive Operations

```python
filtered_df = df.query("Revenue > 20000")

result = filtered_df.groupby("Category")["Revenue"].mean()
```

Reducing the dataset before complex operations can decrease unnecessary processing.

---

## Select Only Required Columns

```python
analysis_df = df[
    ["Product", "Category", "Revenue"]
]
```

This improves readability and may reduce memory usage.

---

## Avoid Unnecessary Copies

Creating repeated DataFrame copies consumes additional memory.

Create copies only when the original dataset must remain unchanged.

```python
analysis_df = df.copy()
```

---

## Use Appropriate Data Types

Examples:

```python
df["Category"] = df["Category"].astype("category")

df["Units Sold"] = df["Units Sold"].astype("int32")
```

Appropriate data types can reduce memory consumption.

---

## Avoid Excessive Use of `apply()`

Prefer vectorized operations when possible.

Instead of:

```python
df["Revenue_Per_Unit"] = df.apply(
    lambda row: row["Revenue"] / row["Units Sold"],
    axis=1
)
```

Use:

```python
df["Revenue_Per_Unit"] = (
    df["Revenue"] / df["Units Sold"]
)
```

---

# 🧩 Mini Challenge – Employee Performance Dashboard

## Dataset Purpose

The dataset represented ten employees from different departments and included:

- Employee name
- Department
- Monthly sales
- Customer rating
- Orders completed

---

## Analysis Performed

- Ranked employees by monthly sales.
- Retrieved the top five performers.
- Identified the bottom two performers.
- Filtered employees with customer ratings above 4.5.
- Created a performance score.
- Applied business rules to identify bonus eligibility.

---

## Summary

The employee performance analysis demonstrated how ranking, filtering, and calculated metrics can support performance reviews and incentive decisions.

Monthly sales measured direct financial contribution, while customer ratings and completed orders provided additional context about service quality and productivity. Combining these measures produced a more balanced evaluation than assessing employees through sales alone.

---

# 🚀 Bonus Challenge – E-Commerce Product Performance

## Dataset Purpose

The dataset represented ten products across categories such as:

- Electronics
- Furniture
- Home and Kitchen
- Fitness
- Apparel
- Appliances

The analysis used:

- Revenue
- Units sold
- Customer rating

---

## Analytical Insights

1. **The Adjustable Standing Desk generated the highest revenue at $85,000**, making it the strongest product by total revenue despite selling only 170 units.

2. **The Organic Cotton T-Shirt recorded the highest sales volume with 500 units**, but produced only $12,500 in revenue, indicating a high-volume and relatively low-priced product.

3. **The Ceramic Coffee Mug Set achieved the highest customer rating of 4.9**, but generated the lowest revenue at $4,200. High satisfaction did not translate into strong overall revenue.

4. **Electronics was a major revenue contributor**, led by the Smart Fitness Watch at $62,000 and the Wireless Noise-Canceling Earbuds at $45,000.

5. **Revenue per unit differed significantly among products.** Premium products such as the Adjustable Standing Desk generated much more revenue per sale than high-volume products such as the Organic Cotton T-Shirt.

---

# 🌟 Analyst Extension – Function Selection

| Scenario | Appropriate Function |
|---|---|
| Sort employees by descending sales | `sort_values()` |
| Retrieve five highest revenue records | `nlargest()` |
| Assign product revenue ranks | `rank()` |
| Apply readable multi-condition filtering | `query()` |
| Create an arithmetic column expression | `eval()` |
| Retrieve three smallest order values | `nsmallest()` |
| Compare tie-handling methods | `rank(method=...)` |
| Retrieve top records without full sorting | `nlargest()` |

---

# 🏢 Enterprise Connection

## Pandas

```python
df.nlargest(5, "Revenue")
```

```python
df.query("Revenue > 20000")
```

```python
df["Revenue_Rank"] = (
    df["Revenue"].rank(ascending=False)
)
```

---

## PySpark Equivalents

### Sorting

```python
df.orderBy(
    col("Revenue").desc()
)
```

### Filtering

```python
df.filter(
    col("Revenue") > 20000
)
```

### Top Records

```python
df.orderBy(
    col("Revenue").desc()
).limit(5)
```

### Ranking

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import dense_rank, col

window_spec = Window.orderBy(
    col("Revenue").desc()
)

df.withColumn(
    "Revenue_Rank",
    dense_rank().over(window_spec)
)
```

---

## Azure Databricks Usage

These operations are frequently used in Databricks for:

- Product-performance dashboards
- Customer segmentation
- Employee KPI reporting
- Transaction prioritization
- ETL business rules
- Large-scale ranking and filtering
- Preparing curated reporting tables

Understanding the Pandas versions makes the later transition to Spark DataFrames more intuitive.

---

# ⚠️ Common Mistakes

## 1. Forgetting `ascending=False`

```python
df["Sales"].rank()
```

This gives the smallest value the first rank.

For highest-value-first ranking:

```python
df["Sales"].rank(
    ascending=False
)
```

---

## 2. Sorting the Entire Dataset Unnecessarily

Avoid:

```python
df.sort_values(
    "Revenue",
    ascending=False
).head(5)
```

when only the top five records are needed.

Prefer:

```python
df.nlargest(5, "Revenue")
```

---

## 3. Incorrect Logical Operators

Inside standard Boolean filtering, use:

```python
&
|
~
```

Inside `query()`, readable keywords such as these can be used:

```text
and
or
not
```

---

## 4. Missing Parentheses in Boolean Filtering

Incorrect:

```python
df[df["Sales"] > 80000 & df["Orders"] > 100]
```

Correct:

```python
df[
    (df["Sales"] > 80000) &
    (df["Orders"] > 100)
]
```

---

## 5. Ignoring Spaces in Column Names

Inside `query()` and `eval()`, columns containing spaces require backticks.

```python
df.query(
    "`Customer Rating` > 4.5"
)
```

---

## 6. Combining Metrics Without Considering Scale

Sales may contain values in tens of thousands, while ratings may range from 1 to 5.

Directly adding them can cause sales to dominate the result. Metrics may need weighting or normalization before creating a meaningful score.

---

## 7. Modifying the Original DataFrame Accidentally

Methods such as `eval(..., inplace=True)` change the original DataFrame.

Use `inplace=True` only when that behaviour is intended.

---

# 🎤 Interview Questions

## 1. What does `sort_values()` do?

It sorts DataFrame records based on one or more columns.

---

## 2. What is the difference between `sort_values()` and `nlargest()`?

`sort_values()` sorts the entire dataset, while `nlargest()` directly retrieves a specified number of highest-value records.

---

## 3. What does `rank()` do?

It assigns a relative position to each value in a Series.

---

## 4. What is dense ranking?

Dense ranking gives tied values the same rank and does not leave gaps in later ranks.

---

## 5. What is the purpose of `query()`?

It filters DataFrame records using readable string expressions.

---

## 6. How can a Python variable be used inside `query()`?

Prefix the variable name with `@`.

```python
limit = 50000

df.query("Revenue > @limit")
```

---

## 7. What is the purpose of `eval()`?

It evaluates arithmetic or logical expressions involving DataFrame columns and can create calculated columns.

---

## 8. Why are vectorized operations preferred?

They are generally faster, more concise, and more memory-efficient than Python-level row-by-row loops.

---

## 9. Why should analysts avoid unnecessary full sorting?

Full sorting processes every row. Functions such as `nlargest()` and `nsmallest()` are more suitable when only a limited number of extreme values is required.

---

## 10. What should be considered when creating a performance score?

- Business objectives
- Metric importance
- Measurement scales
- Appropriate weights
- Normalization
- Interpretability

---

# 🧠 Revision Cheat Sheet

| Requirement | Pandas Operation |
|---|---|
| Sort ascending | `sort_values()` |
| Sort descending | `sort_values(ascending=False)` |
| Sort by multiple columns | `sort_values(by=[...])` |
| Rank values | `rank()` |
| Dense ranking | `rank(method="dense")` |
| Top records | `nlargest()` |
| Bottom records | `nsmallest()` |
| Readable filtering | `query()` |
| Calculated expressions | `eval()` |
| External variable in query | `@variable` |
| Column name with spaces | Backticks |
| Fast column calculations | Vectorized operations |

---

# 📌 What I Should Remember 6 Months From Now

- Use `sort_values()` when the complete dataset must be ordered.
- Use `nlargest()` or `nsmallest()` when only top or bottom records are required.
- Use `rank()` to build leaderboards and relative performance measures.
- Use `method="dense"` when tied ranks should not create gaps.
- Use `query()` for readable business filtering rules.
- Use backticks for column names containing spaces.
- Use `@variable` to reference Python variables inside `query()`.
- Use `eval()` mainly for clear arithmetic and logical expressions.
- Prefer vectorized operations over loops and row-wise `apply()`.
- Business scores should account for metric scale, weighting, and interpretability.
- These operations translate directly into PySpark DataFrame transformations and window functions.