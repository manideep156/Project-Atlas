# 📅 Day 18 – Time Series Analysis with Pandas

**Date:** July 28, 2026

**Status:** ✅ Completed

---

# 🎯 Objective

Learn how to organize, analyze, and summarize chronological data using Pandas time-series features. Understand how datetime indexes, time-based indexing, resampling, rolling statistics, and trend analysis help transform raw timestamped data into meaningful business insights.

---

# 📚 1. Time Series

## Definition

A time series is a sequence of observations collected over time, where each record is associated with a specific date or timestamp.

Examples include:

- Daily sales
- Stock prices
- Website traffic
- Weather data
- Electricity consumption
- Sensor readings

---

## Why It Exists

Many business decisions depend on identifying trends over time rather than analyzing isolated records.

Time-series analysis helps answer questions such as:

- Is revenue increasing?
- Which month performs best?
- Are there seasonal patterns?
- Is customer activity declining?

---

# 📚 2. Datetime Index

## Definition

A Datetime Index replaces the default integer index with dates, enabling Pandas to recognize the dataset as chronological.

## Syntax

```python
df.set_index("Date")
```

---

## Benefits

- Faster date filtering
- Time-based slicing
- Resampling
- Rolling calculations
- Time-series analysis

---

# 📚 3. Time-Based Indexing

Instead of row numbers, data can be accessed using dates.

Examples:

```python
df.loc["2026-01-15"]

df.loc["2026-01-10":"2026-01-20"]
```

---

## Best Practices

- Always convert Date to datetime first.
- Set Date as the index before time-series analysis.
- Use `.loc[]` for date selection.

---

# 📚 4. Resampling

## Definition

Resampling changes the frequency of time-series data by grouping observations into larger or smaller time intervals.

Examples:

Daily → Weekly

Weekly → Monthly

Monthly → Quarterly

---

## Common Frequencies

| Code | Meaning |
|------|---------|
| D | Daily |
| W | Weekly |
| M | Monthly |
| Q | Quarterly |
| Y | Yearly |

---

## Examples

```python
df.resample("W").sum()

df.resample("M").mean()
```

---

## Business Uses

- Weekly Sales Reports
- Monthly Revenue
- Quarterly Financial Reports
- Yearly Business Performance

---

# 📚 5. Rolling Window

## Definition

A rolling window calculates statistics over a fixed number of consecutive observations.

Example:

7-day average

30-day average

90-day average

---

## Syntax

```python
df["Revenue"].rolling(7).mean()
```

---

## Common Functions

- mean()
- sum()
- max()
- min()
- std()

---

## Business Uses

- Forecasting
- Sales Trends
- Demand Planning
- Stock Analysis
- Website Traffic Monitoring

---

# 📚 6. Trend Analysis

Trend analysis measures how business performance changes over time.

Common techniques:

- Daily Difference (`diff()`)
- Rolling Mean
- Percentage Change (`pct_change()`)
- Highest Value (`idxmax()`)
- Lowest Value (`idxmin()`)

---

# 🏢 Enterprise Connection

## Pandas

```python
df.resample("W").sum()
```

↓

## PySpark

```python
from pyspark.sql.functions import window, sum

df.groupBy(
    window("Date", "7 days")
).agg(
    sum("Revenue")
)
```

↓

## Azure Databricks

Time-series analysis is commonly used for:

- Sales Reporting
- IoT Analytics
- Energy Consumption
- Financial Reporting
- Streaming Analytics
- Delta Lake Pipelines

The same concepts learned in Pandas scale directly to distributed Spark processing.

---

# ⚠️ Common Mistakes

- Forgetting to convert dates into datetime.
- Performing resampling without a datetime index.
- Using rolling windows on unsorted data.
- Mixing datetime formats.
- Ignoring missing dates in time-series datasets.

---

# 🎤 Interview Questions

## What is a time series?

A collection of observations recorded over time.

---

## Why is a Datetime Index important?

It enables efficient time-based indexing, slicing, resampling, and rolling calculations.

---

## What does `resample()` do?

Groups data into different time intervals such as weeks, months, or years.

---

## What is a rolling window?

A moving subset of observations used to calculate statistics over consecutive records.

---

## Difference between `groupby()` and `resample()`?

`groupby()` groups by values in a column, while `resample()` groups data based on time intervals.

---

# 🌍 Industry Usage

- Retail Sales Analytics
- Banking
- Insurance
- Manufacturing
- Power Consumption Analysis
- IoT Monitoring
- Stock Market Analysis
- Web Analytics

---

# 🧠 Revision Cheat Sheet

## Functions

- `set_index()`
- `loc[]`
- `resample()`
- `rolling()`
- `diff()`
- `pct_change()`
- `idxmax()`
- `idxmin()`

---

## Quick Decision Guide

| Scenario | Function |
|----------|----------|
| Set datetime index | `set_index()` |
| Date filtering | `loc[]` |
| Weekly summary | `resample("W")` |
| Monthly average | `resample("M").mean()` |
| Moving average | `rolling().mean()` |
| Daily change | `diff()` |
| Highest value | `idxmax()` |
| Lowest value | `idxmin()` |

---

# 📌 What I Should Remember 6 Months From Now

- Convert dates before performing time-series analysis.
- Use a Datetime Index for all chronological datasets.
- `resample()` summarizes data across time intervals.
- `rolling()` smooths fluctuations and identifies trends.
- These concepts directly translate to PySpark window operations and Azure Databricks analytics.