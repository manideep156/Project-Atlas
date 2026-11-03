# 🚀 Project Atlas

# ⚡ Day 23 – PySpark DataFrame Transformations & Data Cleaning

**Date:** November 3, 2026

**Status:** ✅ Completed

**Phase:** Phase 4 – PySpark

**Theme:** Transforming, Enriching, and Cleaning PySpark DataFrames

**Difficulty:** ⭐⭐⭐☆☆

---

# 🎯 Objective

Understand how to modify existing Spark DataFrames, create new columns, rename and remove columns, apply conditional expressions, and handle missing values.

Today's session focuses on:

- DataFrame Transformations
- withColumn()
- withColumnRenamed()
- drop()
- Conditional Expressions
- when() and otherwise()
- NULL Value Identification
- Missing Value Handling
- na.fill(), na.drop(), and na.replace()
- Chaining Transformations
- Employee Data Transformation Challenge

By the end of this session, I should be able to transform raw employee data into a cleaner and more structured DataFrame using PySpark.

---

# 📚 Part 1 – Understanding DataFrame Transformations

A DataFrame transformation creates a new DataFrame based on an existing DataFrame.

Spark DataFrames are immutable. This means that an existing DataFrame is not modified directly.

Instead, transformations return a new DataFrame containing the requested changes.

## 1.1 Understanding Immutability

Example:

    updated_df = employee_df.withColumn(
        "annual_salary",
        col("salary") * 12
    )

Here:

- employee_df remains unchanged.
- updated_df contains the additional annual_salary column.
- Spark records the transformation for execution.

**Important:** Transformations are generally lazy. The computation is executed when an action requires the result.

## 1.2 Common DataFrame Transformations

| Transformation | Purpose |
|---|---|
| withColumn() | Add or modify a column |
| withColumnRenamed() | Rename an existing column |
| drop() | Remove one or more columns |
| filter() | Filter rows |
| select() | Select columns |
| when() | Apply conditional logic |
| na.fill() | Fill missing values |
| na.drop() | Remove rows containing missing values |
| na.replace() | Replace specified values |

---

# 📚 Part 2 – Adding and Modifying Columns

## 2.1 Understanding withColumn()

The withColumn() method adds a new column or replaces an existing column with a transformed expression.

Syntax:

    df.withColumn("new_column", expression)

Example:

    from pyspark.sql.functions import col

    employee_df = employee_df.withColumn(
        "annual_salary",
        col("salary") * 12
    )

This creates an annual_salary column by multiplying monthly salary by 12.

## 2.2 Modifying an Existing Column

If the specified column already exists, withColumn() replaces its expression.

Example:

    employee_df = employee_df.withColumn(
        "salary",
        col("salary") + 5000
    )

This creates a new DataFrame in which salary contains the updated values.

## 2.3 Creating Multiple Derived Columns

    employee_df = employee_df.withColumn(
        "annual_salary",
        col("salary") * 12
    ).withColumn(
        "bonus",
        col("salary") * 0.10
    )

Multiple transformations can be chained to create additional columns.

---

# 📚 Part 3 – Renaming and Removing Columns

## 3.1 Renaming Columns using withColumnRenamed()

The withColumnRenamed() method renames an existing column.

Syntax:

    df.withColumnRenamed("old_name", "new_name")

Example:

    employee_df = employee_df.withColumnRenamed(
        "employee_id",
        "emp_id"
    )

This changes employee_id to emp_id.

## 3.2 Removing Columns using drop()

The drop() method removes one or more columns from a DataFrame.

Example:

    employee_df = employee_df.drop("department")

Removing multiple columns:

    employee_df = employee_df.drop(
        "department",
        "experience"
    )

**Important:** drop() returns a new DataFrame. It does not modify the original DataFrame directly.

## 3.3 Transformation Summary

| Method | Purpose |
|---|---|
| withColumn() | Add or replace columns |
| withColumnRenamed() | Rename columns |
| drop() | Remove columns |

---

# 📚 Part 4 – Conditional Transformations

Conditional transformations allow us to create or modify column values based on specified conditions.

PySpark provides when() and otherwise() for conditional expressions.

## 4.1 Understanding when() and otherwise()

The when() function evaluates a condition and returns a specified value when that condition is true.

The otherwise() function provides the alternative value when the condition is false or no preceding condition matches.

Example:

    from pyspark.sql.functions import when, col

    employee_df = employee_df.withColumn(
        "experience_level",
        when(col("experience") >= 5, "Senior")
        .otherwise("Junior")
    )

This creates an experience_level column.

Employees with at least five years of experience are classified as Senior. Others are classified as Junior.

## 4.2 Multiple Conditional Expressions

Multiple conditions can be chained using when().

Example:

    employee_df = employee_df.withColumn(
        "experience_level",
        when(col("experience") >= 8, "Expert")
        .when(col("experience") >= 5, "Senior")
        .when(col("experience") >= 2, "Intermediate")
        .otherwise("Fresher")
    )

Conditions are evaluated in order.

The first matching condition determines the resulting value.

## 4.3 Conditional Salary Classification

    employee_df = employee_df.withColumn(
        "salary_category",
        when(col("salary") >= 60000, "High")
        .when(col("salary") >= 40000, "Medium")
        .otherwise("Low")
    )

This categorizes employees based on salary.

## 4.4 Why Conditional Transformations Matter

Conditional expressions are useful for:

- Creating business categories.
- Assigning customer segments.
- Classifying employee experience.
- Identifying high-value transactions.
- Creating eligibility flags.
- Implementing business rules in ETL pipelines.

---

# 📚 Part 5 – Handling NULL and Missing Values

Missing values are common in real-world datasets.

They may occur because of incomplete data entry, unavailable information, failed data collection, or inconsistencies between source systems.

PySpark provides several methods to identify and handle missing values.

## 5.1 Identifying NULL Values

Using isNull():

    employee_df.filter(
        col("salary").isNull()
    ).show()

This returns rows where salary is NULL.

Using isNotNull():

    employee_df.filter(
        col("salary").isNotNull()
    ).show()

This returns rows where salary contains a non-NULL value.

## 5.2 Filling Missing Values using na.fill()

The fill() method replaces NULL values with a specified value.

Example:

    employee_df = employee_df.na.fill({
        "salary": 30000
    })

This replaces NULL salary values with 30000.

Multiple columns can be filled using a dictionary.

    employee_df = employee_df.na.fill({
        "salary": 30000,
        "department": "Unknown",
        "experience": 0
    })

Different replacement values can be specified for different columns.

**Important:** Choose replacement values based on business meaning. Filling missing salary with zero or an arbitrary amount may introduce misleading results.

## 5.3 Removing Missing Values using na.drop()

The drop() method removes rows containing NULL values.

Example:

    employee_df = employee_df.na.drop()

This removes rows containing NULL values in any column.

Removing rows based on a specific column:

    employee_df = employee_df.na.drop(
        subset=["salary"]
    )

This removes only rows where salary is NULL.

## 5.4 Replacing Values using na.replace()

The replace() method replaces specified values in a DataFrame.

Example:

    employee_df = employee_df.na.replace(
        "Tech",
        "IT",
        subset=["department"]
    )

This replaces Tech with IT in the department column.

## 5.5 NULL Handling Summary

| Method | Purpose |
|---|---|
| isNull() | Identify NULL values |
| isNotNull() | Identify non-NULL values |
| na.fill() | Fill missing values |
| na.drop() | Remove rows containing missing values |
| na.replace() | Replace specified values |

## 5.6 Choosing the Correct Missing Value Strategy

| Situation | Possible Approach |
|---|---|
| Missing department | Fill with Unknown if appropriate |
| Missing salary | Apply a justified business rule |
| Critical identifier missing | Consider removing or quarantining the record |
| Inconsistent category | Standardize using replace() |
| Incomplete records | Evaluate whether dropping is appropriate |

Missing value handling should be based on data quality requirements and business context.

---

# 📚 Part 6 – Chaining DataFrame Transformations

Transformation chaining allows multiple operations to be applied sequentially.

Instead of creating a separate variable for every operation, we can combine transformations into a readable pipeline.

## 6.1 Basic Transformation Chaining

    cleaned_df = (
        employee_df
        .withColumnRenamed("employee_id", "emp_id")
        .withColumn("annual_salary", col("salary") * 12)
        .withColumn("bonus", col("salary") * 0.10)
        .drop("department")
    )

Each operation returns a new DataFrame that becomes the input to the next transformation.

## 6.2 Combining Conditional Logic and Cleaning

    cleaned_df = (
        employee_df
        .withColumn(
            "experience_level",
            when(col("experience") >= 5, "Senior")
            .otherwise("Junior")
        )
        .withColumn(
            "salary_category",
            when(col("salary") >= 60000, "High")
            .otherwise("Standard")
        )
    )

## 6.3 Why Chaining Is Useful

- Makes transformation pipelines easier to organize.
- Reduces unnecessary intermediate variables.
- Improves readability when properly formatted.
- Helps structure ETL workflows.
- Makes business transformation logic easier to follow.

**Important:** Chaining does not mean Spark executes every operation immediately. Transformations remain lazy until an action is triggered.

---

# 🧪 Part 7 – Mini Challenge: Employee Data Transformation

**Objective:** Transform and clean an employee dataset using PySpark DataFrame operations.

## 7.1 Dataset

Create an Employee DataFrame containing the following records:

    employees = [
        (101, "Arjun", "IT", 55000, 3),
        (102, "Priya", "HR", None, 2),
        (103, "Rahul", "Tech", 65000, 6),
        (104, "Sneha", "Finance", 48000, 4),
        (105, "Kiran", "IT", None, 1),
        (106, "Meera", "Tech", 72000, 8),
        (107, "Vikram", "HR", 39000, 2)
    ]

    columns = [
        "employee_id",
        "name",
        "department",
        "salary",
        "experience"
    ]

## 7.2 Requirements

1. Create a SparkSession.
2. Create the Employee DataFrame.
3. Inspect the schema and display the records.
4. Standardize the Tech department as IT.
5. Rename employee_id to emp_id.
6. Identify employees with missing salaries.
7. Fill missing salary values with 30000.
8. Create annual_salary using salary multiplied by 12.
9. Create bonus using 10% of salary.
10. Classify employees by experience:
    - Senior: 5 or more years.
    - Junior: Less than 5 years.
11. Classify salary:
    - High: 60000 or more.
    - Standard: Less than 60000.
12. Create salary_status before filling missing salaries to identify originally missing values.
13. Remove the department column.
14. Display the final DataFrame and inspect its schema.

## 7.3 Example Solution

    from pyspark.sql import SparkSession
    from pyspark.sql.functions import col, when

    spark = (
        SparkSession.builder
        .appName("EmployeeTransformation")
        .master("local[*]")
        .getOrCreate()
    )

    employees = [
        (101, "Arjun", "IT", 55000, 3),
        (102, "Priya", "HR", None, 2),
        (103, "Rahul", "Tech", 65000, 6),
        (104, "Sneha", "Finance", 48000, 4),
        (105, "Kiran", "IT", None, 1),
        (106, "Meera", "Tech", 72000, 8),
        (107, "Vikram", "HR", 39000, 2)
    ]

    columns = [
        "employee_id",
        "name",
        "department",
        "salary",
        "experience"
    ]

    employee_df = spark.createDataFrame(employees, columns)

    employee_df.printSchema()
    employee_df.show()

    # Standardize department values
    employee_df = employee_df.na.replace(
        "Tech",
        "IT",
        subset=["department"]
    )

    # Rename employee identifier
    employee_df = employee_df.withColumnRenamed(
        "employee_id",
        "emp_id"
    )

    # Identify originally missing salaries
    employee_df = employee_df.withColumn(
        "salary_status",
        when(col("salary").isNull(), "Missing")
        .otherwise("Available")
    )

    # Fill missing salary values
    employee_df = employee_df.na.fill({
        "salary": 30000
    })

    # Create derived columns and classifications
    employee_df = (
        employee_df
        .withColumn(
            "annual_salary",
            col("salary") * 12
        )
        .withColumn(
            "bonus",
            col("salary") * 0.10
        )
        .withColumn(
            "experience_level",
            when(col("experience") >= 5, "Senior")
            .otherwise("Junior")
        )
        .withColumn(
            "salary_category",
            when(col("salary") >= 60000, "High")
            .otherwise("Standard")
        )
    )

    # Remove department column
    employee_df = employee_df.drop("department")

    # Display final results
    employee_df.show()

    employee_df.printSchema()

## 7.4 Challenge Completion

✅ Created the Employee DataFrame.

✅ Standardized department values.

✅ Renamed employee_id.

✅ Identified originally missing salaries.

✅ Filled missing salary values.

✅ Created annual_salary and bonus.

✅ Classified employee experience.

✅ Classified salary categories.

✅ Removed the department column.

✅ Displayed the final DataFrame and schema.

---

# 🏢 Part 8 – Enterprise Connection

Data transformation and cleaning are essential parts of enterprise data engineering.

Consider an organization receiving employee information from multiple source systems.

The incoming data may contain:

- Inconsistent department names.
- Missing salary information.
- Different employee identifier formats.
- Incomplete records.
- Values that require business classification.

A typical processing workflow could involve:

1. Reading raw employee records.
2. Standardizing inconsistent values.
3. Renaming columns to follow a common naming convention.
4. Identifying and handling missing values.
5. Creating derived business columns.
6. Applying conditional business rules.
7. Removing unnecessary columns.
8. Producing a cleaned DataFrame for downstream processing.

In Azure Databricks, these transformations can be incorporated into Spark notebooks and ETL pipelines.

These concepts will be useful when building the Retail ETL Pipeline in Project Atlas.

---

# ⚠️ Part 9 – Common Mistakes

| Mistake | Correct Approach |
|---|---|
| Assuming DataFrames are mutable | Transformations return new DataFrames |
| Forgetting to assign transformation results | Store the returned DataFrame |
| Using withColumn() incorrectly | Pass a column name and expression |
| Forgetting otherwise() | Define a fallback when required |
| Using incorrect condition ordering | Evaluate more specific conditions first |
| Filling NULL values without business reasoning | Choose an appropriate data quality strategy |
| Filling NULL before identifying missing records | Create a missing-value indicator first if needed |
| Confusing NULL with ordinary text | Use isNull() for actual NULL values |
| Assuming drop() modifies the original DataFrame | Assign the returned DataFrame |
| Creating excessively long chains | Keep transformation pipelines readable |

---

# 🎯 Part 10 – Interview Preparation

## Basic Questions

**1. What is a DataFrame transformation?**

A transformation creates a new DataFrame based on an existing DataFrame.

**2. Are Spark DataFrames mutable?**

No. Spark DataFrames are immutable. Transformations return new DataFrames.

**3. What is withColumn()?**

withColumn() adds a new column or replaces an existing column using a specified expression.

**4. What is withColumnRenamed()?**

It renames an existing DataFrame column.

**5. What is drop()?**

It removes one or more columns from a DataFrame.

## Intermediate Questions

**6. What is the purpose of when() and otherwise()?**

They implement conditional expressions and return values based on specified conditions.

**7. How do you identify NULL values in PySpark?**

Use isNull() and isNotNull().

**8. What is the difference between na.fill() and na.drop()?**

na.fill() replaces missing values, whereas na.drop() removes rows containing missing values.

**9. What is na.replace()?**

It replaces specified values in a DataFrame, optionally limited to selected columns.

**10. Why should missing values be handled carefully?**

Because an inappropriate replacement or deletion strategy can introduce bias, distort calculations, or remove valuable information.

**11. What is transformation chaining?**

It is the process of applying multiple DataFrame transformations sequentially.

**12. Does transformation chaining trigger immediate execution?**

No. Transformations are generally lazy. An action triggers the required computation.

## Practical Questions

**13. How would you create an annual salary column?**

    employee_df.withColumn(
        "annual_salary",
        col("salary") * 12
    )

**14. How would you classify employees based on experience?**

    employee_df.withColumn(
        "level",
        when(col("experience") >= 5, "Senior")
        .otherwise("Junior")
    )

**15. How would you fill missing salary values?**

    employee_df.na.fill({"salary": 30000})

---

# 🧾 Part 11 – Revision Cheat Sheet

| Concept | Key Takeaway |
|---|---|
| Immutability | Transformations return new DataFrames |
| withColumn() | Add or modify a column |
| withColumnRenamed() | Rename a column |
| drop() | Remove columns |
| when() | Evaluate a condition |
| otherwise() | Define the fallback value |
| isNull() | Identify NULL values |
| isNotNull() | Identify non-NULL values |
| na.fill() | Replace missing values |
| na.drop() | Remove rows with missing values |
| na.replace() | Replace specified values |
| Chaining | Apply multiple transformations sequentially |
| Lazy Evaluation | Execution is delayed until required |

---

# 🧠 Part 12 – What I Should Remember 6 Months From Now

- Spark DataFrames are immutable.
- Every transformation returns a new DataFrame.
- withColumn() is used to create or modify columns.
- withColumnRenamed() changes column names.
- drop() removes unnecessary columns.
- when() and otherwise() implement conditional business logic.
- isNull() and isNotNull() identify missing values.
- na.fill() replaces missing values.
- na.drop() removes rows containing missing values.
- na.replace() standardizes specified values.
- Missing value strategies should follow business requirements.
- Transformation chaining helps organize ETL pipelines.
- Transformations remain lazy until an action requires execution.

---

# 🏆 Part 13 – Day 23 Achievements

✅ Understood DataFrame immutability.

✅ Learned how to add and modify columns using withColumn().

✅ Practiced renaming columns using withColumnRenamed().

✅ Learned how to remove columns using drop().

✅ Applied conditional expressions using when() and otherwise().

✅ Identified NULL values using isNull() and isNotNull().

✅ Practiced missing value handling using na.fill() and na.drop().

✅ Standardized values using na.replace().

✅ Practiced chaining multiple transformations.

✅ Completed the Employee Data Transformation Challenge.

---

# 📅 Part 14 – Day Summary

**Status:** 🟢 Successfully Completed

Today's session focused on transforming and cleaning Spark DataFrames.

I learned how to modify existing columns, create derived columns, rename and remove unnecessary columns, apply conditional business logic, and handle missing values.

I also practiced combining these operations into a structured transformation pipeline through the Employee Data Transformation Challenge.

These concepts establish the foundation for building more advanced data-processing workflows using PySpark.

### Focus for Day 24

- DataFrame filtering using filter() and where().
- Selecting columns and working with column expressions.
- distinct() and dropDuplicates().
- Sorting using orderBy() and sort().
- Grouping records using groupBy().
- Aggregation functions: count(), sum(), avg(), min(), and max().
- Employee Department Analytics Challenge.

---

**🚀 Project Atlas – Building Scalable Data Engineering and AI Skills**