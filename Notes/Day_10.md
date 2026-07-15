# Day 10 – Missing Values & Data Cleaning Fundamentals

**Date:** July 15, 2026

**Study Duration:** ~5–6 Hours

**Status:** ✅ Completed

---

# 🎯 Objective

Learn how to identify, inspect, and handle missing values using Pandas while understanding when different data cleaning strategies should be applied.

The focus today was on developing a systematic approach to preparing real-world datasets for analysis and machine learning rather than simply applying functions.

---

# 📚 1. Missing Values

## Definition

Missing values represent unavailable, unknown, or incomplete information within a dataset.

In Pandas, missing values are generally represented as:

- `NaN` (Not a Number)
- `None` (primarily in object-type columns)

---

## Why Do Missing Values Occur?

Missing values may occur because of:

- Human error during data collection.
- Equipment or sensor failures.
- Corrupted data.
- Optional survey questions.
- Data integration from multiple sources.
- Privacy restrictions or intentionally withheld information.

---

## Why Are Missing Values Important?

Ignoring missing values can:

- Produce inaccurate statistical calculations.
- Mislead data visualizations.
- Reduce machine learning model performance.
- Introduce bias into analysis.
- Lead to incorrect business decisions.

Handling missing values is therefore one of the first and most important steps in data preprocessing.

---

# 📚 2. Types of Missing Data

## MCAR (Missing Completely At Random)

Missing values occur randomly and are unrelated to any other variable.

### Example

A survey response is accidentally lost.

---

## MAR (Missing At Random)

Missing values depend on another observed variable.

### Example

Older passengers are less likely to report their income.

---

## MNAR (Missing Not At Random)

Missing values depend on the missing value itself.

### Example

People with very high salaries choose not to disclose their income.

---

# 📚 3. Detecting Missing Values

## `isnull()`

### Purpose

Detects missing values within a DataFrame.

### Returns

- `True` → Missing value
- `False` → Valid value

### Common Uses

- Identify missing values.
- Count missing values.
- Filter incomplete records.

---

## `notnull()`

### Purpose

Returns the opposite of `isnull()`.

### Returns

- `True` → Valid value
- `False` → Missing value

### Common Uses

- Identify complete records.
- Filter rows containing valid information.

---

# 📚 4. Quantifying Missing Values

Finding missing values is only the first step.

A Data Analyst should also measure:

- Total missing values.
- Missing values per column.
- Percentage of missing values.
- Overall dataset completeness.

These metrics help determine the most suitable cleaning strategy.

---

# 📚 5. Removing Missing Values

## Function

```python
dropna()
```

### Purpose

Removes rows or columns containing missing values.

---

### Important Parameters

- `axis`
- `how`
- `subset`
- `thresh`
- `inplace`

---

### Advantages

- Removes incomplete records.
- Produces a cleaner dataset.
- Easy to apply.

---

### Limitations

- May result in significant data loss.
- Can reduce model performance if too much data is removed.
- May introduce bias if missing values are not random.

---

### Best Use Cases

Use `dropna()` when:

- Only a small number of records are affected.
- Missing values cannot be estimated reliably.
- The removed information is not important.

---

# 📚 6. Filling Missing Values

## Function

```python
fillna()
```

### Purpose

Replaces missing values instead of removing records.

---

## Common Filling Techniques

### Constant Value

Used when a placeholder such as:

- `"Unknown"`
- `0`

is acceptable.

---

### Mean

Suitable for:

- Numerical data
- Approximately symmetric distributions

---

### Median

Suitable for:

- Numerical data
- Skewed distributions
- Presence of outliers

---

### Mode

Suitable for:

- Categorical variables

---

### Forward Fill (`ffill`)

Uses the previous valid observation.

Best suited for sequential or time-series data.

---

### Backward Fill (`bfill`)

Uses the next valid observation.

Useful when later observations are more reliable.

---

# 📚 7. Choosing the Right Cleaning Strategy

There is no universal solution.

Choosing the correct strategy depends on:

- Percentage of missing values.
- Type of feature.
- Importance of the feature.
- Business objective.
- Machine learning requirements.

Data cleaning decisions should always be driven by context rather than convenience.

---

# 💼 Industry Example (Titanic Dataset)

| Column | Recommended Strategy | Reason |
|----------|---------------------|--------|
| Age | Fill using Median | Median is robust against outliers while preserving records. |
| Cabin | Drop the column (or create a separate "Missing" category if required) | A large percentage of values are missing, making reliable imputation difficult. |
| Embarked | Fill using Mode | Only a few values are missing, so mode preserves the dataset with minimal impact. |

---

# ✅ Best Practices

- Always inspect missing values before cleaning.
- Measure the percentage of missing values.
- Preserve data whenever possible.
- Choose the filling strategy based on the data type and distribution.
- Document every cleaning decision.
- Compare the dataset before and after cleaning.

---

# ⚠️ Common Mistakes

- Dropping data without measuring its impact.
- Filling categorical data using mean or median.
- Ignoring missing values before analysis.
- Applying the same cleaning strategy to every dataset.
- Forgetting to verify the results after cleaning.

---

# 🎤 Interview Questions & Answers

## 1. Why are missing values important?

Missing values can negatively affect statistical analysis, data visualization, and machine learning models. If they are not handled properly, they may introduce bias, reduce model accuracy, or lead to incorrect business conclusions. Therefore, identifying and handling missing values is an essential step in data preprocessing.

---

## 2. What is the difference between `isnull()` and `notnull()`?

- `isnull()` returns **True** for missing values (`NaN`) and **False** for valid values.
- `notnull()` returns **True** for valid values and **False** for missing values.

They are complementary functions used to identify incomplete and complete records within a dataset.

---

## 3. When would you use Median instead of Mean?

Median should be used when the numerical data is **skewed** or contains **outliers**.

Unlike the mean, the median is not affected by extreme values, making it a better representation of the central tendency in such cases.

---

## 4. When would you choose `dropna()` instead of `fillna()`?

`dropna()` should be used when only a small number of records contain missing values, when missing values cannot be estimated reliably, or when the missing information is not important for the analysis.

If removing the data results in significant information loss, `fillna()` is generally a better option.

---

## 5. Why is data cleaning important before Machine Learning?

Machine learning algorithms require clean and consistent data.

Missing values can prevent certain algorithms from running, reduce prediction accuracy, and introduce bias into the model.

Cleaning the data ensures that the model learns meaningful patterns from reliable information.

---

## 6. Which filling strategy would you recommend for numerical data?

The choice depends on the data distribution.

- Use **Mean** for symmetric numerical data with few outliers.
- Use **Median** for skewed numerical data or data containing outliers.

Median is generally considered the safer choice in real-world datasets.

---

## 7. Which filling strategy would you recommend for categorical data?

The **Mode** is the preferred choice because it replaces missing values with the most frequently occurring category while preserving the categorical nature of the feature.

---

## 8. Why shouldn't you always remove rows containing missing values?

Removing rows may significantly reduce the size of the dataset and lead to the loss of valuable information. If the missing values are not random, removing records may also introduce bias into the analysis.

Whenever possible, preserving useful information through appropriate imputation is preferred.

---

# 🌍 Industry Usage

Handling missing values is one of the first tasks performed in:

- Data Analytics
- Business Intelligence
- Data Engineering
- Machine Learning
- Artificial Intelligence

Most real-world datasets require some level of preprocessing before meaningful analysis can begin.

---

# 🧠 Revision Cheat Sheet

## Key Functions

- `isnull()`
- `notnull()`
- `dropna()`
- `fillna()`

---

## Remember

- Always inspect missing values before cleaning.
- Measure missing values before deciding on a strategy.
- Mean → Symmetric numerical data.
- Median → Skewed numerical data or data with outliers.
- Mode → Categorical data.
- Forward Fill → Previous valid observation.
- Backward Fill → Next valid observation.
- There is no single best cleaning strategy for every dataset.

---

## Quick Decision Guide

| Situation | Recommended Strategy |
|-----------|----------------------|
| Few missing rows | `dropna()` |
| Numerical (normal distribution) | Mean |
| Numerical (skewed / outliers) | Median |
| Categorical | Mode |
| Sequential / Time-series | Forward Fill / Backward Fill |
| Large percentage of missing values | Consider dropping the column or using advanced imputation |

---

# 📌 What I Should Remember 6 Months From Now

- Always inspect missing values before cleaning.
- Never apply the same cleaning strategy to every dataset.
- Preserve valuable data whenever possible.
- Median is generally safer than Mean when outliers exist.
- Mode is the preferred choice for categorical features.
- Data cleaning decisions should always be based on context and business requirements.
- Cleaning data is one of the most important steps before analysis and machine learning.