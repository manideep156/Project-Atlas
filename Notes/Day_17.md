# 📅 Day 17 – Date & Time Handling with Pandas

**Date:** July 27, 2026

**Status:** ✅ Completed

---

# 🎯 Objective

Learn how to work with date and time data in Pandas by converting string values into datetime objects, extracting useful date components, filtering records based on dates, and performing date arithmetic. These skills are essential for business reporting, trend analysis, forecasting, and enterprise ETL pipelines.

---

# 📚 1. Datetime Objects

## Definition

Datetime objects represent dates and timestamps in a format that Pandas can understand and manipulate.

Instead of treating dates as plain text, Pandas stores them using a specialized datetime data type.

---

## Why They Exist

Without datetime objects:

- Dates cannot be sorted correctly.
- Time differences cannot be calculated.
- Date components cannot be extracted.
- Time-series analysis becomes impossible.

Datetime objects solve these limitations.

---

# 📚 2. `pd.to_datetime()`

## Definition

Converts strings, integers, or other supported formats into Pandas datetime objects.

## Syntax

```python
pd.to_datetime(column)
```

---

## Common Parameters

| Parameter | Purpose |
|------------|---------|
| errors | Handle invalid dates |
| format | Specify custom date format |
| dayfirst | Interpret day before month |
| utc | Convert to UTC timezone |

---

## Best Practices

- Convert date columns immediately after loading data.
- Use explicit formats when known.
- Validate invalid dates using `errors="coerce"`.

---

# 📚 3. Datetime Components (`.dt`)

Common attributes:

- `.year`
- `.month`
- `.day`
- `.hour`
- `.minute`
- `.second`
- `.day_name()`
- `.month_name()`
- `.weekday`
- `.quarter`

These features simplify grouping, filtering, and reporting.

---

# 📚 4. Date Filtering

Datetime columns support comparison operators.

Examples:

- Before a date
- After a date
- Between two dates
- Quarterly reports
- Monthly reports

Business Uses:

- Monthly revenue
- Employee attendance
- Customer purchases
- Sales trends

---

# 📚 5. Date Arithmetic

Datetime values support subtraction.

Common calculations:

- Days since first sale
- Customer age
- Delivery duration
- Employee tenure
- Subscription period

Results are stored as Timedelta objects.

---

# 📚 6. Timedelta Objects

Timedelta represents the difference between two datetime values.

Useful for:

- Duration analysis
- Delivery tracking
- Customer retention
- Time-to-resolution metrics

---

# 🏢 Enterprise Connection

## Pandas

```python
pd.to_datetime(df["Date"])
```

↓

## PySpark

```python
from pyspark.sql.functions import to_timestamp

df.withColumn(
    "Date",
    to_timestamp("Date")
)
```

↓

## Azure Databricks

Used in ETL pipelines to standardize timestamps before:

- Data Cleaning
- Aggregation
- Time Series Analysis
- Delta Lake Storage

The same concepts learned in Pandas directly translate to enterprise-scale Spark workloads.

---

# ⚠️ Common Mistakes

- Forgetting to convert strings to datetime.
- Comparing strings instead of dates.
- Ignoring invalid date values.
- Mixing date formats.
- Extracting components before conversion.

---

# 🎤 Interview Questions

## Why should date columns be converted to datetime?

Datetime objects enable filtering, sorting, arithmetic, grouping, and time-series analysis.

---

## What is the purpose of `pd.to_datetime()`?

It converts strings or other supported formats into Pandas datetime objects.

---

## What is `.dt`?

A Pandas accessor used to retrieve date and time components.

---

## What is Timedelta?

A duration representing the difference between two datetime values.

---

## Why are datetime objects important in ETL pipelines?

They standardize timestamps for downstream processing, reporting, and analytics.

---

# 🌍 Industry Usage

- Banking
- Retail Analytics
- Healthcare
- Manufacturing
- Insurance
- IoT
- Web Analytics
- Financial Markets

---

# 🧠 Revision Cheat Sheet

## Functions

- `pd.to_datetime()`
- `.dt.year`
- `.dt.month`
- `.dt.day`
- `.dt.day_name()`
- `.dt.month_name()`
- `.dt.quarter`
- `.min()`
- `.max()`

---

## Quick Decision Guide

| Scenario | Function |
|----------|----------|
| Convert strings | `pd.to_datetime()` |
| Month | `.dt.month` |
| Day Name | `.dt.day_name()` |
| Quarter | `.dt.quarter` |
| Earliest Date | `.min()` |
| Latest Date | `.max()` |
| Days Between Dates | Date subtraction |

---

# 📌 What I Should Remember 6 Months From Now

- Always convert date columns immediately after loading data.
- `.dt` is the gateway to extracting useful date components.
- Date arithmetic produces Timedelta objects.
- Datetime operations are heavily used in reporting and forecasting.
- These concepts directly transfer to PySpark and Azure Databricks.