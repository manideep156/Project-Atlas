# Day 2 - NumPy Fundamentals Deep Dive

**Date:** July 7, 2026  
**Study Duration:** ~4 hours  
**Status:** ✅ Completed

---

# 🎯 Objective

Continue building a strong NumPy foundation by understanding:

- Array operations
- Indexing
- Slicing
- Reshaping
- Aggregation functions

The goal is to become comfortable manipulating arrays before moving into Pandas and Data Analysis.

---

# 📚 Topics Covered

## 1. NumPy Array Operations

### Concepts Learned

NumPy allows mathematical operations directly on arrays.

Unlike normal Python lists, NumPy performs operations element-wise.

Example:

```python
a = np.array([1,2,3])
b = np.array([4,5,6])

a + b
```

Output:

```
[5 7 9]
```

---

### Operations Practiced

- Addition
- Subtraction
- Multiplication
- Division
- Squaring elements

Example:

```python
a ** 2
```

---

# 2. NumPy Indexing

## Concepts Learned

Indexing is used to access individual elements from an array.

For 1D arrays:

```python
arr[index]
```

For 2D arrays:

```python
arr[row, column]
```

---

## Practiced

- Accessing first element
- Accessing last element
- Accessing rows
- Accessing columns
- Accessing specific positions

Example:

```python
matrix[1,2]
```

---

# 3. NumPy Slicing

## Concept

Slicing allows extracting sections of an array.

Syntax:

```python
array[start:end:step]
```

---

## Practiced

### 1D Slicing

Practiced:

- First few elements
- Last few elements
- Skipping elements
- Reversing arrays

Example:

```python
arr[::-1]
```

---

### 2D Slicing

Practiced extracting:

- Specific rows
- Specific columns
- Sub-matrices
- Top-left blocks
- Bottom-right blocks

Example:

```python
arr[:2,:2]
```

---

# 4. Reshaping Arrays

## Concept

Reshaping changes the structure of an array without changing its data.

Example:

```python
arr.reshape(2,5)
```

---

## Learned

### reshape()

Changes dimensions.

Example:

```
10 elements

reshape(2,5)

2 rows × 5 columns
```

---

### flatten()

Converts multi-dimensional arrays into a 1D array.

Example:

```python
arr.flatten()
```

---

### transpose

Switches rows and columns.

Example:

```python
arr.T
```

---

# 5. Aggregation Functions

## Concept

Aggregation functions summarize data.

---

## Functions Practiced

### Sum

```python
np.sum(arr)
```

Finds total value.

---

### Mean

```python
np.mean(arr)
```

Finds average.

---

### Maximum

```python
np.max(arr)
```

Finds highest value.

---

### Minimum

```python
np.min(arr)
```

Finds lowest value.

---

### Standard Deviation

```python
np.std(arr)
```

Measures spread of data.

---

# Axis Concept

One important concept learned:

## axis=0

Operations happen column-wise.

Example:

```python
np.sum(arr, axis=0)
```

Returns sum of each column.

---

## axis=1

Operations happen row-wise.

Example:

```python
np.sum(arr, axis=1)
```

Returns sum of each row.

---

# 🧪 Practice Completed

## Exercises

✅ Array arithmetic

✅ Extracting even numbers

✅ Reshaping arrays

✅ Finding array properties

✅ Indexing practice

✅ Slicing practice

✅ Aggregation functions

---

# ⭐ Bonus Challenge Completed

Completed additional NumPy practice using a 10×10 matrix.

```python
arr = np.arange(1, 101).reshape(10, 10)
```

---

## Tasks Completed

### ✅ Printed the diagonal elements

Concept practiced:

- Advanced indexing
- Understanding matrix positions

---

### ✅ Extracted the last three rows

Concept practiced:

- Row slicing

Example:

```python
arr[-3:]
```

---

### ✅ Extracted the first three columns

Concept practiced:

- Column slicing

Example:

```python
arr[:, :3]
```

---

### ✅ Calculated the average of each row

Concept practiced:

- Aggregation with axis

Example:

```python
np.mean(arr, axis=1)
```

---

### ✅ Found the maximum value in each column

Concept practiced:

- Column-wise aggregation

Example:

```python
np.max(arr, axis=0)
```

---

# 💻 Practical Work

Notebook:

```
02_NumPy/Day01_NumPy_Basics.ipynb
```

Completed practical exercises:

- Array operations
- Indexing exercises
- Slicing exercises
- Reshaping practice
- Aggregation functions
- Bonus matrix challenge

---

# 💡 Key Learnings

- NumPy operations are faster because they use vectorized operations instead of manually looping through elements.
- Array shapes are important when working with structured data.
- Indexing and slicing are essential skills for data manipulation.
- Aggregation functions help summarize datasets quickly.
- Understanding axes is important for working with Pandas and ML datasets.
- NumPy arrays provide efficient mathematical operations for large amounts of data.
- Understanding dimensions and axes is essential before moving into real-world datasets.

---

# 🤔 Challenges

- Understanding axis initially required practice.
- Remembering row vs column operations.
- Building confidence with slicing notation.

---

# 📊 Self Assessment

| Topic | Confidence |
|---|---|
| Array creation | 🟢 Strong |
| Array operations | 🟢 Strong |
| Indexing | 🟢 Comfortable |
| Slicing | 🟢 Comfortable |
| Reshaping | 🟡 Need more practice |
| Axis operations | 🟡 Improving |
| Aggregations | 🟢 Comfortable |

---

# 🔄 Revision Needed

Practice more:

- Advanced slicing
- Boolean indexing
- Broadcasting
- Vectorized operations

---

# 🚀 Next Steps

## Day 3 Preview

Focus:

Building deeper understanding of NumPy's power.

Topics planned:

- Broadcasting
- Vectorized operations
- Boolean masking
- Conditional filtering
- Random number generation
- More NumPy problem solving
- Mini data analysis exercise