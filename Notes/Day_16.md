# Day 16 – Reshaping Data with `melt()`, `stack()`, `unstack()` & `explode()`

**Date:** July 21, 2026

**Study Duration:** ~6–7 Hours

**Status:** ✅ Completed

---

# 🎯 Objective

Learn how to reshape datasets between wide and long formats using Pandas. These techniques help organize data into structures that are easier to analyze, visualize, summarize, and prepare for machine learning.

---

# 📚 1. Wide vs Long Data

## Wide Format

Stores measurements across multiple columns.

Example:

| Product | Jan | Feb | Mar |
|----------|-----|-----|-----|

Suitable for human readability but less flexible for analysis.

---

## Long Format

Stores measurements as rows.

| Product | Month | Sales |
|----------|--------|------|

Preferred for visualization, aggregation, and machine learning.

---

# 📚 2. `melt()`

## Function

```python
pd.melt()
```

### Purpose

Converts wide-format data into long-format data.

### Important Parameters

- `id_vars`
- `value_vars`
- `var_name`
- `value_name`

### Industry Uses

- Sales data
- Survey responses
- Monthly reports
- Dashboard preparation

---

# 📚 3. `stack()`

## Function

```python
stack()
```

### Purpose

Moves DataFrame columns into index levels.

### Best Used For

- MultiIndex analysis
- Hierarchical data
- Advanced reshaping

---

# 📚 4. `unstack()`

## Function

```python
unstack()
```

### Purpose

Moves index levels back into columns.

Useful for reconstructing tabular layouts from hierarchical indexes.

---

# 📚 5. `explode()`

## Function

```python
explode()
```

### Purpose

Expands list-like values into individual rows.

### Industry Uses

- Customer purchases
- Product lists
- Tags and keywords
- Survey responses

---

# 📚 6. Choosing the Right Technique

| Requirement | Technique |
|-------------|-----------|
| Wide → Long | `melt()` |
| Columns → Index | `stack()` |
| Index → Columns | `unstack()` |
| Lists → Rows | `explode()` |

---

# ✅ Best Practices

- Identify the current data structure before reshaping.
- Preserve identifier columns when using `melt()`.
- Verify row counts after reshaping.
- Use descriptive column names.
- Confirm that no data has been lost.

---

# ⚠️ Common Mistakes

- Using `stack()` instead of `melt()`.
- Forgetting identifier columns.
- Confusing wide and long formats.
- Exploding non-list columns.
- Ignoring MultiIndex behavior.

---

# 🎤 Interview Questions & Answers

## What is data reshaping?

Changing the structure of a dataset without changing the underlying information.

---

## When should `melt()` be used?

When converting wide-format datasets into long-format datasets.

---

## Difference between `stack()` and `melt()`?

`melt()` reshapes columns into rows, while `stack()` reshapes columns into index levels.

---

## When is `explode()` useful?

When a column contains list-like values that need to become individual rows.

---

## Why is long-format data preferred?

It simplifies filtering, visualization, grouping, and machine learning.

---

# 🌍 Industry Usage

- ETL Pipelines
- Business Intelligence
- Dashboard Development
- Machine Learning
- Time Series Analysis
- Survey Analytics

---

# 🧠 Revision Cheat Sheet

## Key Functions

- `pd.melt()`
- `stack()`
- `unstack()`
- `explode()`

---

## Quick Decision Guide

| Scenario | Function |
|----------|----------|
| Wide → Long | `melt()` |
| Long → Wide (MultiIndex) | `unstack()` |
| Columns → Index | `stack()` |
| Lists → Rows | `explode()` |

---

# 📌 What I Should Remember 6 Months From Now

- `melt()` converts wide data into long data.
- `stack()` creates hierarchical indexes.
- `unstack()` restores columns from indexes.
- `explode()` expands nested list values.
- Reshaping prepares data for visualization, reporting, and machine learning.