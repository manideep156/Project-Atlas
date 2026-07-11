# Project 01 – Retail Store Sales Analytics (Revision Notes)

**Date:** July 11, 2026

**Status:** ✅ Completed

---

# 🎯 Project Objective

Analyze a retail sales dataset using **NumPy only** to answer business questions, simulate business scenarios, and generate actionable insights.

---

# 📚 Theory Revision

## 1. Broadcasting

### Definition

Broadcasting allows NumPy to perform arithmetic operations on arrays with compatible shapes without explicitly copying data.

### Why it was used

To simulate promotional increases for selected products without writing loops.

### Code Reviewed

```python
total_average = np.mean(sales)

prods_below_overall = np.where(product_average < total_average, 1.12, 1.0)

new_sales = sales * prods_below_overall
```

### Working

* Compute overall average.
* Compare each product average.
* Create multiplier array.
* Apply broadcasting across columns.

### Remember

* Broadcasting requires compatible dimensions.
* It avoids explicit iteration.
* It is one of NumPy's biggest performance advantages.

---

## 2. Boolean Counting

### Code Reviewed

```python
prod4_95 = (sales[:,3] > 95)

np.sum(prod4_95)
```

### Working

* Select Product 4.
* Create Boolean array.
* Sum `True` values.

### Remember

`True = 1`

`False = 0`

---

## 3. Row-wise Logical Operations

### Code Reviewed

```python
np.where(np.all(sales > 70, axis=1))[0]
```

### Working

* Compare every value.
* Check each row using `np.all()`.
* Return matching row indices.

### Remember

`axis=1`

means

**Row-wise operation**

---

## 4. Summary Table

### Goal

Combine multiple statistics into a single structured table.

Statistics included:

* Product Total
* Product Average
* Product Maximum
* Product Minimum
* Product Standard Deviation

### Learning

Instead of calculating statistics individually every time, build one consolidated summary table for faster analysis.

---

# 💡 Key Learnings

* Business problems require combining multiple NumPy concepts.
* Broadcasting simplifies large-scale transformations.
* Boolean masking enables efficient filtering.
* Aggregation functions provide quick statistical summaries.
* Summary tables improve readability and reporting.

---

# ⚠️ Common Mistakes

* Confusing `axis=0` and `axis=1`.
* Forgetting broadcasting rules.
* Using `hstack()` when column-wise stacking is required.
* Forgetting that a 1-D array transpose has no effect.
* Using Python loops where NumPy vectorization is more efficient.

---

# ⚡ Quick Revision

### Broadcasting

✔ Compatible shapes

✔ Automatic expansion

✔ Eliminates loops

---

### Boolean Masking

✔ Returns Boolean arrays

✔ `True = 1`

✔ Combine conditions with `&` and `|`

---

### Aggregations

✔ `axis=0` → Columns

✔ `axis=1` → Rows

---

### Summary Tables

✔ Calculate statistics

✔ Combine into one structured array

✔ Makes business reporting easier

---

# 🚀 Next Step

Transition to **Pandas**, where these same analytical concepts will be applied to real-world tabular datasets with much greater flexibility.
