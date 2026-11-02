**# 🚀 Project Atlas**

**# ⚡ Day 22 – Spark Architecture & DataFrame Fundamentals**

**Date:** November 2, 2026

**Status:** ✅ Completed

**Phase:** Phase 4 – PySpark

**Theme:** Understanding Spark Architecture and Working with Spark DataFrames

**Difficulty:** ⭐⭐☆☆☆

---

**# 🎯 Objective**

Understand how Apache Spark processes data, how PySpark provides a Python interface, and how to create and work with Spark DataFrames.

Today's session focuses on:

- Spark Architecture
- Driver and Executors
- Cluster Manager
- SparkSession
- Spark DataFrames
- Schema and Data Types
- Basic DataFrame Operations
- Transformations and Actions
- Lazy Evaluation

By the end of this session, I should be able to explain the basic Spark execution model, create a Spark DataFrame, inspect its schema, and perform fundamental DataFrame operations.

---

**# 📚 Part 1 – Understanding Apache Spark Architecture**

Apache Spark is a distributed data-processing engine designed to process large datasets efficiently through parallel computing.

Instead of processing an entire dataset sequentially on a single processing unit, Spark can divide the workload into smaller tasks and execute them across available resources.

**## 1.1 Main Components of Spark Architecture**

**### 1. Driver**

The Driver is responsible for coordinating a Spark application.

Responsibilities:

- Runs the main application logic.
- Creates and manages the Spark execution plan.
- Schedules tasks.
- Coordinates Executors.
- Monitors application execution.

**### 2. Executors**

Executors are responsible for executing tasks assigned by the Driver.

Responsibilities:

- Execute tasks.
- Process data partitions.
- Store intermediate data when required.
- Return results and execution information.

**### 3. Cluster Manager**

The Cluster Manager manages and allocates computing resources to Spark applications.

Examples:

- Spark Standalone
- YARN
- Kubernetes

In local mode, Spark uses resources available on the local machine.

**### 4. Partitions**

A partition is a logical division of a dataset.

Spark can process multiple partitions in parallel, depending on available resources and the execution plan.

**## 1.2 Simplified Spark Execution Flow**

1. The application creates a `SparkSession`.
2. The Driver receives DataFrame operations.
3. Spark builds and optimizes an execution plan.
4. The workload is divided into tasks.
5. Tasks are assigned to available execution resources.
6. Executors process the relevant data partitions.
7. Results are returned or written to storage.

**## 1.3 Why Spark Architecture Matters**

Understanding Spark architecture helps explain:

- Parallel data processing.
- How large datasets are divided into partitions.
- How tasks are distributed.
- Why some operations are expensive.
- Why collecting large datasets to the Driver can cause memory problems.

---

**# 📚 Part 2 – Understanding PySpark**

PySpark is the Python API for Apache Spark.

It allows Python developers to work with Spark's distributed data-processing capabilities using Python syntax.

**## 2.1 Apache Spark vs PySpark**

| Apache Spark | PySpark |
|---|---|
| Distributed data-processing engine | Python API for Spark |
| Provides execution capabilities | Provides Python interfaces |
| Supports multiple language APIs | Allows Python developers to use Spark |

**## 2.2 Local vs Distributed Execution**

For our local development environment, we use:

    .master("local[*]")

Understanding the configuration:

| Configuration | Meaning |
|---|---|
| `local` | Uses one local execution thread |
| `local[*]` | Uses available logical CPU cores |
| Cluster deployment | Can distribute workloads across multiple machines |

**Important:** `local[*]` uses local machine resources. It does not mean Spark is running across multiple machines.

---

**# 📚 Part 3 – Creating a SparkSession**

`SparkSession` is the main entry point for working with Spark DataFrames and Spark SQL.

Before creating DataFrames or performing Spark operations, we generally create a SparkSession.

**## 3.1 Creating a SparkSession**

    from pyspark.sql import SparkSession

    spark = (
        SparkSession.builder
        .appName("ProjectAtlas")
        .master("local[*]")
        .getOrCreate()
    )

**## 3.2 Understanding the Methods**

| Method | Purpose |
|---|---|
| `builder` | Starts SparkSession configuration |
| `appName()` | Defines the application name |
| `master()` | Specifies the execution environment |
| `getOrCreate()` | Reuses an existing session or creates a new one |

**## 3.3 Checking Spark Version**

    spark.version

**## 3.4 Stopping a SparkSession**

    spark.stop()

A SparkSession should be stopped when the application or notebook work is finished and the session is no longer needed.

---

**# 📚 Part 4 – Understanding Spark DataFrames**

A Spark DataFrame is a distributed collection of data organized into named columns.

It is conceptually similar to a relational database table, but designed for distributed data processing.

**## 4.1 Creating a DataFrame**

    employees = [
        (101, "Arjun", "IT", 55000, 3),
        (102, "Priya", "HR", 42000, 2),
        (103, "Rahul", "IT", 65000, 5),
        (104, "Sneha", "Finance", 48000, 4),
        (105, "Kiran", "IT", 39000, 1)
    ]

    columns = [
        "employee_id",
        "name",
        "department",
        "salary",
        "experience"
    ]

    employee_df = spark.createDataFrame(employees, columns)

    employee_df.show()

`show()` displays rows from the DataFrame.

**## 4.2 Pandas vs PySpark**

| Pandas | PySpark |
|---|---|
| Primarily local processing | Designed for distributed processing |
| Eager execution for ordinary operations | Lazy evaluation for transformations |
| Best suited to data that fits local memory | Suitable for large-scale processing |
| Operations execute locally | Operations are planned and executed by Spark |

A Spark DataFrame is not simply a Pandas DataFrame stored differently. Their execution models are different.

---

**# 📚 Part 5 – Understanding DataFrame Schema**

A schema defines the structure of a DataFrame, including column names and their data types.

**## 5.1 Inspecting the Schema**

    employee_df.printSchema()

This displays the column names and corresponding data types.

**## 5.2 Getting Column Names**

    employee_df.columns

**## 5.3 Getting Data Types**

    employee_df.dtypes

**## 5.4 Counting Rows**

    employee_df.count()

**## 5.5 Common Spark Data Types**

| Data Type | Description |
|---|---|
| `StringType` | Text values |
| `IntegerType` | Integer values |
| `LongType` | Large integer values |
| `DoubleType` | Decimal values |
| `BooleanType` | True or False |
| `DateType` | Date values |
| `TimestampType` | Date and time values |

Explicit schemas are useful in production pipelines because they make expected input structures clear and help prevent unexpected data-type issues.

---

**# 📚 Part 6 – Basic DataFrame Operations**

Spark DataFrames provide several operations for selecting, filtering, and sorting data.

**## 6.1 Selecting Columns**

    employee_df.select(
        "name",
        "department",
        "salary"
    ).show()

`select()` returns a DataFrame containing the requested columns.

**## 6.2 Filtering Rows**

    employee_df.filter(
        employee_df.salary > 40000
    ).show()

This returns employees whose salary is greater than ₹40,000.

**## 6.3 Using where()**

`where()` is an alias for `filter()`.

    employee_df.where(
        employee_df.department == "IT"
    ).show()

**## 6.4 Combining Conditions**

    from pyspark.sql.functions import col

    employee_df.filter(
        (col("department") == "IT") &
        (col("salary") > 40000)
    ).show()

Use parentheses around individual conditions when combining expressions with `&` or `|`.

**## 6.5 Sorting Data**

Ascending order:

    employee_df.orderBy("salary").show()

Descending order:

    employee_df.orderBy(
        col("salary").desc()
    ).show()

**## 6.6 Basic Operations Summary**

| Operation | Purpose |
|---|---|
| `select()` | Select columns |
| `filter()` | Filter rows |
| `where()` | Filter rows |
| `orderBy()` | Sort rows |
| `show()` | Display rows |
| `count()` | Count rows |

---

**# 📚 Part 7 – Transformations, Actions & Lazy Evaluation**

One of the most important concepts in Apache Spark is the distinction between transformations and actions.

**## 7.1 Transformations**

Transformations define a new DataFrame from an existing DataFrame.

Examples:

- `select()`
- `filter()`
- `where()`
- `orderBy()`

A transformation does not normally execute the complete computation immediately. It defines what Spark needs to do.

**## 7.2 Actions**

Actions trigger execution and either return results to the Driver or write results to an external destination.

Examples:

- `show()`
- `count()`
- `collect()`
- `take()`

**## 7.3 Transformations vs Actions**

| Transformations | Actions |
|---|---|
| Define a new DataFrame or computation | Trigger execution |
| Usually lazy | Trigger computation |
| Example: `filter()` | Example: `count()` |
| Example: `select()` | Example: `show()` |

**## 7.4 Understanding Lazy Evaluation**

Lazy evaluation means Spark does not immediately execute every transformation when it is defined.

Instead, Spark records the operations and builds an execution plan.

When an action is called, Spark executes the required computation.

Example:

    high_salary_df = employee_df.filter(
        col("salary") > 40000
    )

    selected_df = high_salary_df.select(
        "name",
        "salary"
    )

    selected_df.show()

The `filter()` and `select()` operations define the computation. The `show()` action triggers execution.

**## 7.5 Why Lazy Evaluation Is Important**

- Allows Spark to optimize execution plans.
- Avoids unnecessary computation.
- Helps combine compatible operations.
- Supports efficient execution of complex data pipelines.

**## 7.6 Understanding collect()**

    employee_df.collect()

`collect()` returns all rows from a DataFrame to the Driver as a list of Row objects.

**Important:** Avoid using `collect()` on large datasets because the entire result must fit in the Driver's memory.

For limited inspection, prefer:

    employee_df.show(5)

    employee_df.take(5)

---

**# 🧪 Part 8 – Mini Challenge: Employee Data Analysis**

**Objective:** Create an Employee DataFrame and perform basic business analysis using PySpark.

**Requirements**

1. Create a SparkSession.
2. Create an Employee DataFrame containing at least five employees.
3. Inspect the DataFrame schema.
4. Display the employee records.
5. Filter employees earning more than ₹40,000.
6. Filter employees belonging to the IT department.
7. Sort employees by salary in descending order.
8. Count the total number of employees.
9. Select employee names and experience.
10. Stop the SparkSession after completing the exercise.

**## 8.1 Example Solution**

    from pyspark.sql import SparkSession
    from pyspark.sql.functions import col

    spark = (
        SparkSession.builder
        .appName("EmployeeAnalysis")
        .master("local[*]")
        .getOrCreate()
    )

    employees = [
        (101, "Arjun", "IT", 55000, 3),
        (102, "Priya", "HR", 42000, 2),
        (103, "Rahul", "IT", 65000, 5),
        (104, "Sneha", "Finance", 48000, 4),
        (105, "Kiran", "IT", 39000, 1)
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

    employee_df.filter(
        col("salary") > 40000
    ).show()

    employee_df.filter(
        col("department") == "IT"
    ).show()

    employee_df.orderBy(
        col("salary").desc()
    ).show()

    print("Total Employees:", employee_df.count())

    employee_df.select(
        "name",
        "experience"
    ).show()

    spark.stop()

**## 8.2 Challenge Completion**

✅ Created SparkSession.

✅ Created Employee DataFrame.

✅ Inspected schema.

✅ Performed filtering operations.

✅ Sorted employee records.

✅ Counted records.

✅ Selected specific columns.

---

**# 🏢 Part 9 – Enterprise Connection**

The concepts learned today form the foundation of enterprise data engineering.

Consider an organization processing millions of retail transactions.

A typical workflow might involve:

1. Loading transaction data from storage.
2. Creating Spark DataFrames.
3. Inspecting schemas and data types.
4. Filtering invalid or irrelevant records.
5. Selecting required columns.
6. Executing transformations across partitions.
7. Writing processed data to a storage layer.

In Azure Databricks, these operations can be performed using Spark notebooks and managed compute resources.

The architecture and DataFrame concepts learned today will be useful when building the Retail ETL Pipeline in Project Atlas.

---

**# ⚠️ Part 10 – Common Mistakes**

| Mistake | Correct Approach |
|---|---|
| Confusing Spark with PySpark | Spark is the processing engine; PySpark is its Python API |
| Assuming `local[*]` means a cluster | It uses available local CPU cores |
| Treating transformations as immediate execution | Transformations are generally lazy |
| Using `collect()` on huge datasets | Use distributed operations and limited inspection |
| Forgetting to create a SparkSession | Create or reuse a SparkSession before DataFrame work |
| Ignoring schemas | Inspect and validate column types |
| Combining conditions without parentheses | Use parentheses with `&` and `|` |

---

**# 🎯 Part 11 – Interview Preparation**

**## Basic Questions**

**1. What is Apache Spark?**

Apache Spark is a distributed data-processing engine used for large-scale data processing and analytics.

**2. What is PySpark?**

PySpark is the Python API for Apache Spark.

**3. What is a SparkSession?**

SparkSession is the entry point for working with Spark DataFrames and Spark SQL.

**4. What is the Driver?**

The Driver coordinates the Spark application, creates execution plans, and schedules tasks.

**5. What are Executors?**

Executors execute tasks and process data partitions.

**6. What is a partition?**

A partition is a logical division of a dataset that Spark can process independently.

**## Intermediate Questions**

**7. What is the difference between transformations and actions?**

Transformations define computations, while actions trigger their execution.

**8. What is lazy evaluation?**

Lazy evaluation means Spark delays execution of transformations until an action requires the result.

**9. What is the difference between Pandas and PySpark?**

Pandas primarily processes data locally, whereas PySpark supports distributed data processing.

**10. Why should collect() be used carefully?**

Because it transfers all selected records to the Driver, potentially causing memory problems.

**11. What does local[*] mean?**

It configures Spark to use the available logical CPU cores on the local machine.

---

**# 🧾 Part 12 – Revision Cheat Sheet**

| Concept | Key Takeaway |
|---|---|
| Apache Spark | Distributed data-processing engine |
| PySpark | Python API for Spark |
| Driver | Coordinates application execution |
| Executors | Execute tasks |
| Cluster Manager | Allocates resources |
| Partitions | Divide data for parallel processing |
| SparkSession | Entry point for Spark operations |
| DataFrame | Distributed, column-oriented data structure |
| Schema | Defines columns and data types |
| Transformation | Defines a computation |
| Action | Triggers execution |
| Lazy Evaluation | Delays execution until required |
| collect() | Transfers all rows to the Driver |

---

**# 🧠 Part 13 – What I Should Remember 6 Months From Now**

- Spark is a distributed processing engine, not simply another Python library.
- PySpark allows Python developers to use Spark.
- The Driver coordinates the application, while Executors process tasks.
- Data is divided into partitions for parallel processing.
- SparkSession is the starting point for DataFrame operations.
- Spark DataFrames are distributed and schema-based.
- Transformations define operations; actions trigger execution.
- Lazy evaluation gives Spark opportunities to optimize execution.
- Avoid bringing large datasets to the Driver using `collect()`.

---

**# 🏆 Part 14 – Day 22 Achievements**

✅ Understood Apache Spark architecture.

✅ Learned the responsibilities of Driver and Executors.

✅ Understood partitions and parallel processing.

✅ Created and configured SparkSession.

✅ Created Spark DataFrames.

✅ Inspected DataFrame schemas and data types.

✅ Practiced basic DataFrame operations.

✅ Understood transformations and actions.

✅ Learned lazy evaluation.

✅ Completed the Employee Data Analysis Mini Challenge.

---

**# 📅 Part 15 – Day Summary**

**Status:** 🟢 Successfully Completed

Today's session established the conceptual and practical foundation for working with Apache Spark.

I now understand the basic Spark execution architecture, can create Spark DataFrames, inspect their schemas, and perform fundamental operations.

The next step is to move beyond basic DataFrame operations and learn how to modify, enrich, and clean datasets using PySpark transformations.

**### Focus for Day 23**

- `withColumn()`
- `withColumnRenamed()`
- `drop()`
- `when()` and `otherwise()`
- Null value handling
- Chaining transformations
- Employee Data Transformation Challenge

---

**🚀 Project Atlas – Building Scalable Data Engineering and AI Skills**