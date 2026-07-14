# Day 9 – Pandas Data Import & Data Selection

**Date:** July 14, 2026

**Study Duration:** ~6 Hours

**Status:** ✅ Completed

---

# 🎯 Objective

Learn how to work with real-world datasets using Pandas by importing, inspecting, selecting, and filtering data.

The focus today was on understanding the first steps of every data analysis workflow before performing any statistical analysis or data cleaning.

---

# 📚 Topics Covered

## 1. Reading CSV Files

### Definition

CSV (Comma-Separated Values) is a plain-text file format used to store tabular data where each row represents a record and each value is separated by a delimiter (commonly a comma).

### Why CSV?

CSV is one of the most widely used formats because it is:

- Lightweight
- Human-readable
- Platform independent
- Supported by almost every programming language
- Easy to exchange between applications

### Pandas Function

```python
pd.read_csv()
```

### Why `read_csv()`?

`read_csv()` imports structured data into a Pandas DataFrame, allowing it to be inspected, manipulated, analyzed, and prepared for machine learning.

### Common Parameters

- `filepath`
- `sep`
- `header`
- `names`
- `index_col`
- `usecols`
- `dtype`
- `nrows`
- `skiprows`

### Best Practices

- Always verify that the dataset has been imported correctly.
- Use relative paths whenever possible.
- Store the imported DataFrame in a meaningful variable such as `df`.

---

# 2. Dataset Inspection

## Purpose

Before performing any analysis, understand the structure and quality of the dataset.

Functions practiced:

- `head()`
- `tail()`
- `shape`
- `columns`
- `index`
- `dtypes`
- `info()`
- `describe()`
- `memory_usage()`

### Why inspect first?

Inspection helps answer:

- What does the dataset contain?
- How many rows and columns exist?
- What are the data types?
- Does the dataset appear complete?

---

# 3. Column Selection

Covered:

- Selecting a single column
- Selecting multiple columns

### Key Learning

Selecting only the required columns improves readability and reduces unnecessary processing.

---

# 4. Row Selection using `loc[]`

## Definition

`loc[]` performs **label-based indexing**.

### Characteristics

- Uses row labels.
- Uses column names.
- Supports slicing.
- Supports Boolean conditions.

### Best Use Cases

- Working with meaningful indexes.
- Selecting rows using labels.
- Updating specific records.

---

# 5. Row Selection using `iloc[]`

## Definition

`iloc[]` performs **integer position-based indexing**.

### Characteristics

- Uses row positions.
- Uses column positions.
- Behaves similarly to NumPy indexing.

### Best Use Cases

- Working with row numbers.
- Selecting ranges by position.
- Accessing data when labels are unknown.

---

# 6. Data Filtering

Covered:

- Single conditions
- Multiple conditions
- AND (`&`)
- OR (`|`)
- NOT (`~`)
- `isin()`
- `between()`
- `query()`

### Key Learning

Filtering allows analysts to isolate only the records relevant to a specific business question.

---

# 🧠 Key Learnings

- Every data analysis project begins with understanding the dataset before performing analysis.
- Data inspection is an essential first step for identifying the structure and characteristics of the data.
- `loc[]` and `iloc[]` serve different purposes even though they may appear similar with a default integer index.
- Filtering is one of the most frequently used operations in data analysis.
- Working with real datasets provides significantly more practical experience than manually created examples.

---

# 💼 Professional Takeaway

Professional Data Analysts rarely begin by writing complex analysis.

Instead, they first:

1. Import the dataset.
2. Understand the business problem.
3. Inspect the data.
4. Identify useful features.
5. Begin exploration.

Developing this workflow early builds strong analytical habits that scale to larger projects.

---

# 🔄 Revision Needed

Continue practicing:

- `loc[]` on custom indexes.
- `iloc[]` for positional indexing.
- Combining multiple filtering conditions.
- Reading different file formats in Pandas.

---

# 🚀 Tomorrow's Plan

Topics planned:

- Missing Values
- `isnull()`
- `notnull()`
- `fillna()`
- `dropna()`
- Data Cleaning Fundamentals

Tomorrow's session will focus on improving data quality before performing analysis.