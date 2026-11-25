
# Project Atlas — Day 24
## PySpark DataFrame Filtering, Sorting & Aggregations

**Date:** November 24, 2026  
**Status:** Completed  
**Phase:** Phase 4 — PySpark  
**Theme:** DataFrame Filtering, Sorting & Aggregations  
**Difficulty:** 3/5  
**Duration:** 2–3 Hours  

---

## 1. Objective

Day 24 focused on analytical operations using PySpark DataFrames.

Building upon Day 23's transformations and cleaning operations, this session introduced filtering, selecting expressions, deduplication, sorting, grouping, aggregations, and multi-step analytical pipelines.

### Learning Outcomes

- Filter records using single and multiple conditions.
- Apply logical operators to DataFrame columns.
- Use `isin()` and `between()`.
- Select columns and construct calculated expressions.
- Understand `distinct()` and `dropDuplicates()`.
- Sort DataFrames using one or multiple columns.
- Group data using `groupBy()`.
- Perform multiple aggregations using `agg()`.
- Combine transformations into analytical pipelines.
- Perform employee, department, and city-level analytics.

---

## 2. Environment & Dataset

### Spark Setup

```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col

spark = (
    SparkSession.builder
    .appName("ProjectAtlas_Day24")
    .master("local[*]")
    .getOrCreate()
)
```

### Employee Dataset

```python
employees = [
    (101, "Arjun", "IT", 55000, 3, "Hyderabad"),
    (102, "Priya", "HR", 42000, 2, "Chennai"),
    (103, "Rahul", "IT", 65000, 6, "Bangalore"),
    (104, "Sneha", "Finance", 48000, 4, "Hyderabad"),
    (105, "Kiran", "IT", 39000, 1, "Chennai"),
    (106, "Meera", "HR", 72000, 8, "Bangalore"),
    (107, "Vikram", "Finance", 58000, 5, "Hyderabad"),
    (108, "Ananya", "IT", 82000, 9, "Bangalore"),
    (109, "Rohit", "Sales", 45000, 3, "Chennai"),
    (110, "Divya", "Sales", 60000, 6, "Hyderabad")
]

columns = [
    "employee_id",
    "name",
    "department",
    "salary",
    "experience",
    "city"
]

employee_df = spark.createDataFrame(employees, columns)
```

### Dataset Structure

| Column | Description |
|---|---|
| employee_id | Unique employee identifier |
| name | Employee name |
| department | Employee's department |
| salary | Monthly salary |
| experience | Years of experience |
| city | Employee location |

---

## 3. Filtering DataFrames

### Concept

Filtering retrieves records that satisfy a specified condition.

PySpark supports `filter()` and `where()`, both of which perform the same operation.

```python
employee_df.filter(
    col("salary") > 60000
).show()
```

Equivalent operation:

```python
employee_df.where(
    col("department") == "IT"
).show()
```

### Comparison Operators

| Operator | Meaning |
|---|---|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

### Logical Operators

| Operator | Meaning |
|---|---|
| `&` | AND |
| `\|` | OR |
| `~` | NOT |

### Combining Conditions

```python
employee_df.filter(
    (col("department") == "IT") &
    (col("salary") > 50000)
).show()
```

### Using OR

```python
employee_df.filter(
    (col("city") == "Chennai") |
    (col("city") == "Bangalore")
).show()
```

### Using NOT

```python
employee_df.filter(
    ~(col("department") == "HR")
).show()
```

### Using isin()

`isin()` checks whether a column value belongs to a specified collection of values.

```python
employee_df.filter(
    col("department").isin("IT", "Finance")
).show()
```

### Using between()

`between()` checks whether a value falls within an inclusive range.

```python
employee_df.filter(
    col("salary").between(45000, 65000)
).show()
```

### Important Notes

- `filter()` and `where()` are interchangeable.
- PySpark column conditions should use `&`, `|`, and `~`, rather than Python's `and`, `or`, and `not`.
- Individual conditions must be enclosed in parentheses when combined.
- `between()` includes both boundary values.
- `isin()` is useful for filtering categorical columns against multiple values.

---

## 4. Selecting Columns & Expressions

### select()

`select()` retrieves specific columns from a DataFrame.

```python
employee_df.select(
    "name",
    "department",
    "city"
).show()
```

### Calculated Expressions

Column expressions can be used to calculate values without modifying the original DataFrame.

```python
employee_df.select(
    "name",
    "salary",
    (col("salary") * 12).alias("annual_salary")
).show()
```

### alias()

`alias()` assigns a name to a column or calculated expression in the resulting DataFrame.

```python
employee_df.select(
    col("name").alias("employee_name"),
    col("salary").alias("monthly_salary"),
    (col("salary") * 12).alias("annual_salary")
).show()
```

### expr()

`expr()` enables SQL-style expressions within DataFrame operations.

```python
from pyspark.sql.functions import expr

employee_df.select(
    "name",
    expr("salary * 12 AS annual_salary"),
    expr("experience + 1 AS projected_experience")
).show()
```

### Key Takeaways

- `select()` controls the columns returned.
- Column expressions support arithmetic calculations.
- `alias()` provides output column names.
- `expr()` allows SQL-style expressions.
- Expressions are evaluated as part of Spark's execution plan.

---

## 5. Deduplication

### distinct()

`distinct()` removes duplicate rows by considering all columns in the DataFrame.

```python
employee_df.select(
    "department"
).distinct().show()
```

### dropDuplicates()

`dropDuplicates()` allows duplicate identification using selected columns.

```python
employee_df.dropDuplicates(
    ["department"]
).show()
```

### Duplicate Dataset

```python
duplicate_data = [
    (101, "Arjun", "IT", 55000),
    (102, "Priya", "HR", 42000),
    (103, "Rahul", "IT", 65000),
    (101, "Arjun", "IT", 55000),
    (104, "Sneha", "Finance", 48000),
    (102, "Priya", "HR", 42000)
]

duplicate_columns = [
    "employee_id",
    "name",
    "department",
    "salary"
]

duplicate_df = spark.createDataFrame(
    duplicate_data,
    duplicate_columns
)
```

### Removing Fully Duplicated Records

```python
duplicate_df.distinct().show()
```

### Deduplicating by Employee ID

```python
duplicate_df.dropDuplicates(
    ["employee_id"]
).show()
```

### Difference

| Operation | Behavior |
|---|---|
| `distinct()` | Removes duplicate rows considering all columns |
| `dropDuplicates()` | Removes duplicates based on all columns or specified columns |

### Important Consideration

When records sharing a key contain conflicting values, `dropDuplicates()` does not guarantee which record will be retained.

For deterministic deduplication, a business rule must be defined, such as retaining the latest record based on a timestamp. Window functions are commonly used for this purpose.

---

## 6. Sorting DataFrames

### Ascending Sorting

```python
employee_df.orderBy(
    col("salary").asc()
).show()
```

### Descending Sorting

```python
employee_df.orderBy(
    col("salary").desc()
).show()
```

### Multiple Column Sorting

```python
employee_df.orderBy(
    col("department").asc(),
    col("salary").desc()
).show()
```

### Using sort()

```python
employee_df.sort(
    col("experience").desc()
).show()
```

### Sorting Reference

| Operation | Purpose |
|---|---|
| `asc()` | Ascending order |
| `desc()` | Descending order |
| `orderBy()` | Sort by one or more columns |
| `sort()` | Alternative sorting method |

### Important Consideration

Global sorting may require data redistribution between partitions, which can result in a shuffle.

Sorting large datasets can therefore be expensive.

---

## 7. Grouping & Aggregations

### groupBy()

`groupBy()` divides records into logical groups based on one or more columns.

Aggregations are applied to these groups to generate summary statistics.

### Employee Count

```python
from pyspark.sql.functions import count

employee_df.groupBy(
    "department"
).agg(
    count("*").alias("employee_count")
).show()
```

### Average Salary

```python
from pyspark.sql.functions import avg

employee_df.groupBy(
    "department"
).agg(
    avg("salary").alias("average_salary")
).show()
```

### Total Salary

```python
from pyspark.sql.functions import sum

employee_df.groupBy(
    "department"
).agg(
    sum("salary").alias("total_salary")
).show()
```

### Minimum & Maximum Salary

```python
from pyspark.sql.functions import min, max

employee_df.groupBy(
    "department"
).agg(
    min("salary").alias("minimum_salary"),
    max("salary").alias("maximum_salary")
).show()
```

### Multiple Aggregations

```python
employee_df.groupBy(
    "department"
).agg(
    count("*").alias("employee_count"),
    avg("salary").alias("average_salary"),
    sum("salary").alias("total_salary"),
    min("salary").alias("minimum_salary"),
    max("salary").alias("maximum_salary")
).show()
```

### Grouping by Multiple Columns

```python
employee_df.groupBy(
    "department",
    "city"
).agg(
    avg("salary").alias("average_salary"),
    count("*").alias("employee_count")
).show()
```

### Overall Aggregation

```python
employee_df.agg(
    count("*").alias("total_employees"),
    avg("salary").alias("overall_average_salary"),
    max("salary").alias("highest_salary"),
    min("salary").alias("lowest_salary")
).show()
```

### Aggregation Reference

| Function | Purpose |
|---|---|
| `count()` | Counts records |
| `sum()` | Calculates total |
| `avg()` | Calculates average |
| `min()` | Identifies minimum |
| `max()` | Identifies maximum |
| `agg()` | Applies aggregate expressions |

### Key Takeaways

- `groupBy()` creates groups based on specified columns.
- `agg()` allows multiple aggregate expressions.
- Grouping by multiple columns creates more granular summaries.
- Aggregation without grouping summarizes the entire DataFrame.

---

## 8. Transformation Pipelines

### Employee Filtering & Annual Salary Calculation

```python
it_salary_analysis = (
    employee_df
    .filter(
        (col("department") == "IT") &
        (col("salary") > 50000)
    )
    .select(
        "name",
        "department",
        "salary",
        (col("salary") * 12).alias("annual_salary")
    )
    .orderBy(
        col("annual_salary").desc()
    )
)
```

### Department Summary Pipeline

```python
department_summary = (
    employee_df
    .groupBy("department")
    .agg(
        count("*").alias("employee_count"),
        avg("salary").alias("average_salary"),
        sum("salary").alias("total_salary")
    )
    .orderBy(
        col("total_salary").desc()
    )
)
```

### Concept

Spark transformations are generally lazy.

Instead of executing each transformation immediately, Spark builds a logical execution plan.

Actions such as `show()`, `count()`, and `collect()` trigger execution.

Chaining transformations creates readable, maintainable, and scalable analytical workflows.

---

## 9. Practical Challenge — Employee Department Analytics

### Business Requirement

The HR analytics team requires a consolidated analytical report containing employee-level and department-level insights.

### Requirements

1. Filter employees with at least 3 years of experience and a salary of at least ₹45,000.
2. Calculate annual salary.
3. Categorize experience:
   - Junior: Below 3 years.
   - Mid-Level: 3–6 years inclusive.
   - Senior: Above 6 years.
4. Calculate department-level employee count, average salary, total salary, maximum salary, and minimum salary.
5. Calculate city-level employee count, average salary, and total salary.
6. Calculate average salary for each department-city combination.
7. Sort departments by total salary expenditure in descending order.
8. Generate a filtered employee report sorted by annual salary in descending order.

### Reference Solution

#### Task 1 — Filter Employees

```python
filtered_employees = employee_df.filter(
    (col("experience") >= 3) &
    (col("salary") >= 45000)
)
```

#### Task 2 — Calculated Columns

```python
from pyspark.sql.functions import when

filtered_employees = (
    filtered_employees
    .withColumn(
        "annual_salary",
        col("salary") * 12
    )
    .withColumn(
        "experience_category",
        when(col("experience") < 3, "Junior")
        .when(col("experience") <= 6, "Mid-Level")
        .otherwise("Senior")
    )
)
```

#### Task 3 — Department Analytics

```python
department_analytics = (
    employee_df
    .groupBy("department")
    .agg(
        count("*").alias("employee_count"),
        avg("salary").alias("average_salary"),
        sum("salary").alias("total_salary"),
        max("salary").alias("maximum_salary"),
        min("salary").alias("minimum_salary")
    )
    .orderBy(
        col("total_salary").desc()
    )
)
```

#### Task 4 — City Analytics

```python
city_analytics = (
    employee_df
    .groupBy("city")
    .agg(
        count("*").alias("employee_count"),
        avg("salary").alias("average_salary"),
        sum("salary").alias("total_salary")
    )
)
```

#### Task 5 — Department-City Analytics

```python
department_city_analytics = (
    employee_df
    .groupBy("department", "city")
    .agg(
        avg("salary").alias("average_salary"),
        count("*").alias("employee_count")
    )
)
```

#### Task 6 — Ranking Departments

```python
department_analytics.orderBy(
    col("total_salary").desc()
).show()
```

#### Task 7 — Final Employee Report

```python
final_employee_report = (
    filtered_employees
    .select(
        "name",
        "department",
        "city",
        "salary",
        "annual_salary",
        "experience_category"
    )
    .orderBy(
        col("annual_salary").desc()
    )
)
```

### Challenge Takeaways

- Filtering can be performed before downstream operations when the business requirement allows it.
- Calculated columns can be created using expressions and conditional logic.
- Aggregations provide department and city-level insights.
- Multiple transformations can be chained into a single analytical pipeline.
- Sorting can be applied at the end of an analytical workflow.

---

## 10. Bonus Challenge — HR Workforce Insights

### Business Questions

1. Which department has the highest average salary?
2. Which city has the highest total salary expenditure?
3. Identify employees earning more than the overall average salary.
4. Identify employees earning more than their department's average salary.
5. Which department has the largest employee headcount?
6. Find the top three highest-paid employees.
7. Which department has the highest maximum salary?
8. Calculate each department's percentage contribution to the organization's total salary expenditure.

### Reference Solutions

#### 1. Department with Highest Average Salary

```python
department_avg = (
    employee_df
    .groupBy("department")
    .agg(
        avg("salary").alias("average_salary")
    )
    .orderBy(
        col("average_salary").desc()
    )
)

department_avg.show(1)
```

#### 2. City with Highest Salary Expenditure

```python
city_salary = (
    employee_df
    .groupBy("city")
    .agg(
        sum("salary").alias("total_salary")
    )
    .orderBy(
        col("total_salary").desc()
    )
)

city_salary.show(1)
```

#### 3. Employees Earning Above Overall Average

```python
overall_avg = employee_df.agg(
    avg("salary").alias("overall_avg")
).first()["overall_avg"]

above_overall_avg = employee_df.filter(
    col("salary") > overall_avg
)

above_overall_avg.show()
```

#### 4. Employees Earning Above Their Department Average

```python
department_avg_salary = (
    employee_df
    .groupBy("department")
    .agg(
        avg("salary").alias("department_avg_salary")
    )
)

employee_department_avg = employee_df.join(
    department_avg_salary,
    on="department",
    how="inner"
)

above_department_avg = employee_department_avg.filter(
    col("salary") > col("department_avg_salary")
)

above_department_avg.show()
```

#### 5. Department with Largest Headcount

```python
department_headcount = (
    employee_df
    .groupBy("department")
    .agg(
        count("*").alias("employee_count")
    )
    .orderBy(
        col("employee_count").desc()
    )
)

department_headcount.show(1)
```

#### 6. Top Three Highest-Paid Employees

```python
employee_df.orderBy(
    col("salary").desc()
).limit(3).show()
```

#### 7. Department with Highest Maximum Salary

```python
department_max_salary = (
    employee_df
    .groupBy("department")
    .agg(
        max("salary").alias("maximum_salary")
    )
    .orderBy(
        col("maximum_salary").desc()
    )
)

department_max_salary.show(1)
```

#### 8. Percentage Contribution to Total Salary

```python
department_salary = (
    employee_df
    .groupBy("department")
    .agg(
        sum("salary").alias("department_salary")
    )
)

overall_salary = employee_df.agg(
    sum("salary").alias("overall_salary")
).first()["overall_salary"]

department_salary_percentage = department_salary.withColumn(
    "salary_percentage",
    (col("department_salary") / overall_salary) * 100
)

department_salary_percentage.show()
```

### Bonus Challenge Takeaways

- Aggregations can be used to generate rankings.
- Aggregate results can be retrieved and reused in subsequent operations.
- Joining aggregate results back to the original DataFrame enables record-level comparisons.
- Percentage calculations can be performed using global aggregate values.
- Analytical pipelines can combine filtering, grouping, joining, sorting, and calculated columns.

---

## 11. Enterprise Connection

### Real-World Applications

| PySpark Concept | Enterprise Application |
|---|---|
| Filtering | Extracting records relevant to business requirements |
| Column selection | Optimizing datasets for downstream processing |
| Expressions | Calculating derived business metrics |
| Deduplication | Preventing duplicate records in data pipelines |
| Sorting | Ranking and reporting |
| Grouping | Department, region, customer, or product analysis |
| Aggregations | Revenue, expenditure, performance, and operational metrics |
| Transformation pipelines | Building ETL/ELT workflows |

### Insurance Data Engineering Example

In an insurance data pipeline, these operations could be used to:

- Filter active policies.
- Deduplicate policy records.
- Calculate annual premiums.
- Group policies by region.
- Aggregate premiums by product.
- Analyze claim expenditure by location.
- Generate reports for downstream analytics.

These concepts are applicable to large-scale processing using Apache Spark.

---

## 12. Common Mistakes

### Incorrect Logical Operators

Incorrect:

```python
employee_df.filter(
    col("salary") > 50000 and col("experience") > 3
)
```

Correct:

```python
employee_df.filter(
    (col("salary") > 50000) &
    (col("experience") > 3)
)
```

### Forgetting Parentheses

Always wrap individual conditions when combining logical expressions.

### Confusing Deduplication Operations

- `distinct()` considers the entire row.
- `dropDuplicates()` supports deduplication using selected columns.

### Forgetting Aggregations

`groupBy()` should be followed by an aggregation or an appropriate grouped operation.

### Assuming Immediate Execution

Spark transformations are generally lazy.

Actions trigger execution.

### Expensive Global Sorting

Sorting can cause shuffles. Avoid unnecessary global ordering on large datasets.

### Excessive collect()

`collect()` transfers all returned records to the driver. Avoid it on large datasets unless the result is known to be small.

---

## 13. Interview Preparation

1. What is the difference between `filter()` and `where()`?
2. How do you combine multiple conditions in PySpark?
3. Why are `&`, `|`, and `~` used instead of Python logical operators?
4. What is the difference between `distinct()` and `dropDuplicates()`?
5. What is the difference between `orderBy()` and `sort()`?
6. How do you sort a DataFrame using multiple columns?
7. What is the purpose of `groupBy()`?
8. What is the difference between `count()` and `sum()`?
9. Can multiple aggregations be performed in a single `agg()`?
10. What is the difference between a transformation and an action?
11. What is lazy evaluation?
12. Why can sorting large DataFrames be expensive?
13. Why should `collect()` be used cautiously?
14. How can aggregate results be joined back to an original DataFrame?
15. What is a transformation pipeline?

---

## 14. Revision Cheat Sheet

| Requirement | PySpark Operation |
|---|---|
| Filter records | `filter()` / `where()` |
| Select columns | `select()` |
| Create expressions | `expr()` |
| Rename expressions | `alias()` |
| Remove full duplicates | `distinct()` |
| Remove duplicates by key | `dropDuplicates()` |
| Ascending sorting | `asc()` |
| Descending sorting | `desc()` |
| Sort records | `orderBy()` / `sort()` |
| Group records | `groupBy()` |
| Multiple aggregations | `agg()` |
| Count records | `count()` |
| Total | `sum()` |
| Average | `avg()` |
| Minimum | `min()` |
| Maximum | `max()` |
| Conditional expression | `when()` / `otherwise()` |
| Join DataFrames | `join()` |

---

## 15. Knowledge Retention

Concepts to recall without referring to the notebook:

- Filtering using multiple conditions.
- Logical operators in PySpark.
- `isin()` and `between()`.
- Selecting and calculating columns.
- Difference between `distinct()` and `dropDuplicates()`.
- Sorting by multiple columns.
- Grouping and multiple aggregations.
- Transformation pipelines.
- Lazy evaluation.
- Actions and execution.
- Aggregation-based analytics.

---

## 16. Achievements

- Completed PySpark DataFrame filtering.
- Practiced conditional filtering and logical operators.
- Learned column selection and expressions.
- Practiced duplicate identification and removal.
- Learned sorting and multi-column ordering.
- Performed grouping and multiple aggregations.
- Built analytical transformation pipelines.
- Completed Employee Department Analytics.
- Completed HR Workforce Insights bonus challenge.

---

## 17. Summary

Day 24 strengthened analytical capabilities using PySpark DataFrames.

The session moved beyond cleaning and modifying data into retrieving, organizing, summarizing, and analyzing datasets.

The concepts learned today form the foundation for more advanced Spark workflows involving joins, windows, partitioning, optimization, and distributed data processing.

### Next Session

**Day 25 — PySpark Joins & Combining DataFrames**

---

**Project Atlas | Phase 4 — PySpark**

*Learn. Build. Analyze. Engineer.*
```

---

# 2. `Progress.md`

<text color="secondary">Update your existing Progress.md — preserve the existing layout.</text>

### Update these metrics

| Metric | Updated value |
|---|---|
| Sessions completed | 24/60 |
| Projects completed | 2 |
| Overall roadmap progress | 40% |
| Phase 1 — Python | <text color="success" inline>Completed</text> |
| Phase 2 — NumPy | <text color="success" inline>Completed</text> |
| Phase 3 — Pandas | <text color="success" inline>Completed</text> |
| Phase 4 — PySpark | <text color="warning" inline>In Progress</text> |
| Latest session | Day 24 |
| Latest session date | November 24, 2026 |
| Latest topic | PySpark DataFrame Filtering, Sorting & Aggregations |

<text weight="medium">Add/update your latest progress entry:</text>

<CodeBlock language="markdown" editable>
### Day 24 — PySpark DataFrame Filtering, Sorting & Aggregations
- **Date:** November 24, 2026
- **Status:** Completed
- **Phase:** Phase 4 — PySpark
- **Topics Covered:**
  - DataFrame filtering using filter() and where()
  - Logical operators and compound conditions
  - isin() and between()
  - Column selection and expressions
  - distinct() and dropDuplicates()
  - Sorting and multi-column ordering
  - groupBy() and aggregations
  - Transformation pipelines
  - Department and city-level analytics
- **Challenges:** Employee Department Analytics; HR Workforce Insights
- **Outcome:** Successfully completed the session, mini-checks, practical challenge, and bonus challenge.
