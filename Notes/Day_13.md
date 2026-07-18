# Day 13 – Data Transformation with `map()`, `replace()` & `apply()`

**Date:** July 18, 2026

**Study Duration:** ~5–6 Hours

**Status:** ✅ Completed

---

# 🎯 Objective

Learn how to transform datasets using Pandas by mapping values, replacing existing data, and applying custom functions. These transformations improve data consistency, readability, and usability for analysis and machine learning.

---

# 📚 1. Data Transformation

## Definition

Data transformation is the process of modifying data into a more useful, consistent, or meaningful format before analysis.

It prepares raw datasets for reporting, visualization, statistical analysis, and machine learning.

---

# 📚 2. `map()`

## Function

```python
map()
```

### Purpose

Maps existing values in a Series to new values using a dictionary, Series, or function.

### Syntax

```python
df["Column"].map(mapping_dictionary)
```

### Common Uses

- Convert codes to descriptive labels.
- Encode categorical values.
- Create standardized representations.

---

# 📚 3. `replace()`

## Function

```python
replace()
```

### Purpose

Replaces one or more existing values with new values.

### Syntax

```python
df.replace(old_value, new_value)
```

or

```python
df.replace({
    "Old1": "New1",
    "Old2": "New2"
})
```

### Common Uses

- Standardizing text values.
- Correcting inconsistent entries.
- Updating outdated values.

---

# 📚 4. `apply()`

## Function

```python
apply()
```

### Purpose

Applies a custom function across a Series or DataFrame.

### Example

```python
df["Bonus"] = df["Salary"].apply(calculate_bonus)
```

### Advantages

- Supports custom business rules.
- Handles complex conditional logic.
- Extends beyond built-in Pandas operations.

---

# 📚 5. Row-wise Transformations (`axis=1`)

## Purpose

Processes an entire row at a time, allowing multiple columns to be used together.

### Example

```python
df.apply(custom_function, axis=1)
```

### Typical Applications

- Employee classification
- Customer segmentation
- Risk assessment
- Feature engineering

---

# 📚 6. Feature Engineering

## Definition

Feature engineering is the process of creating new columns from existing data to improve analysis or predictive modeling.

### Examples

- Age → Age Group
- Fare → Fare Category
- Salary → Salary Grade
- SibSp + Parch → Family Size

Feature engineering often captures information that is easier to interpret than raw values.

---

# ✅ Best Practices

- Preserve original data whenever possible.
- Use descriptive names for new columns.
- Keep transformation rules simple and consistent.
- Validate transformed values before analysis.
- Document business rules clearly.

---

# ⚠️ Common Mistakes

- Applying `map()` to multiple columns directly.
- Using `replace()` when conditional logic is required.
- Forgetting `axis=1` for row-wise transformations.
- Overwriting important raw data without keeping a backup.
- Creating unnecessary features that add little analytical value.

---

# 🎤 Interview Questions & Answers

## 1. What is data transformation?

Data transformation converts raw data into a more useful format for analysis, reporting, or machine learning.

---

## 2. When should `map()` be used?

Use `map()` when replacing or converting values in a single Series based on a mapping.

---

## 3. How is `replace()` different from `map()`?

`map()` works primarily on a Series and creates mapped values, while `replace()` substitutes existing values across a Series or DataFrame.

---

## 4. What is the purpose of `apply()`?

`apply()` executes custom functions on data when built-in Pandas operations are insufficient.

---

## 5. What is feature engineering?

Feature engineering is the creation of new variables from existing data to improve analysis or machine learning performance.

---

# 🌍 Industry Usage

Data transformation is widely used in:

- Data Cleaning
- ETL Pipelines
- Business Intelligence
- Feature Engineering
- Machine Learning
- Financial Reporting
- Customer Analytics

It is one of the most common stages in real-world data preprocessing.

---

# 🧠 Revision Cheat Sheet

## Key Functions

- `map()`
- `replace()`
- `apply()`
- `apply(axis=1)`

---

## Remember

- `map()` → Transform values in a Series.
- `replace()` → Substitute existing values.
- `apply()` → Apply custom logic.
- `axis=1` → Use multiple columns together.
- Feature engineering creates meaningful new columns.

---

## Quick Decision Guide

| Requirement | Function |
|-------------|----------|
| Map values | `map()` |
| Replace values | `replace()` |
| Apply custom logic | `apply()` |
| Use multiple columns | `apply(axis=1)` |
| Create new analytical features | Feature Engineering |

---

# 📌 What I Should Remember 6 Months From Now

- Data transformation prepares raw data for meaningful analysis.
- `map()` is ideal for one-to-one value mapping.
- `replace()` standardizes existing values efficiently.
- `apply()` enables custom business logic and row-wise transformations.
- Feature engineering often improves both analytical insights and machine learning performance.