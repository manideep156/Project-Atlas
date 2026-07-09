# Day 4 - Advanced NumPy Operations

**Date:** July 9, 2026  
**Study Duration:** ~5.5 Hours  
**Status:** ✅ Completed

---

# 🎯 Objective

Today's goal was to move beyond basic NumPy operations and understand advanced techniques used frequently in Data Analysis and Machine Learning.

Topics Covered:

- Copy vs View
- Sorting Arrays
- Unique Values
- Searching Arrays
- Stacking Arrays
- Splitting Arrays

---

# 📚 1. Copy vs View

## Theory

NumPy allows creating either a **view** or a **copy** of an array.

### View

A view shares the same memory as the original array.

If the view is modified, the original array is also modified.

Useful when:
- Working with large datasets
- Avoiding unnecessary memory usage
- Improving performance

---

### Copy

A copy creates an entirely new array with its own memory.

Changes made to the copy do not affect the original array.

Useful when:
- Preserving original data
- Independent modifications are required

---

## Important Functions

- `view()`
- `copy()`
- `.base`

---

## Key Points

- Views share memory.
- Copies allocate new memory.
- `.base` helps identify whether an array owns its data.

---

## Common Mistakes

❌ Assuming every assignment creates a new array.

❌ Accidentally modifying the original dataset through a view.

---

## Real-World Applications

- Data preprocessing
- Machine Learning pipelines
- Large dataset manipulation

---

# 📚 2. Sorting Arrays

## Theory

Sorting organizes data in ascending or descending order.

NumPy provides fast sorting algorithms optimized for numerical arrays.

---

## Functions Learned

- `np.sort()`
- `np.argsort()`

---

### Difference

**sort()**

Returns sorted values.

**argsort()**

Returns the indices that would sort the array.

---

## Key Points

- Useful before searching.
- Frequently used before ranking data.
- Essential in statistical analysis.

---

## Real-World Applications

- Ranking products
- Sorting salaries
- Sorting exam scores
- Organizing datasets

---

# 📚 3. Unique Values

## Theory

Unique values remove duplicates from a dataset.

Useful for understanding categorical data.

---

## Function Learned

- `np.unique()`

Optional parameters explored:

- Return counts
- Return indices

---

## Key Points

- Removes duplicates.
- Can calculate frequency of values.
- Helpful for identifying categories.

---

## Real-World Applications

- Product categories
- Customer IDs
- Survey responses
- Classification labels

---

# 📚 4. Searching Arrays

## Theory

Searching helps locate values or positions inside arrays.

---

## Functions Learned

- `np.where()`
- `np.argmax()`
- `np.argmin()`

---

### Purpose

**where()**

Finds indices satisfying a condition.

**argmax()**

Returns index of largest value.

**argmin()**

Returns index of smallest value.

---

## Key Points

- Faster than manual iteration.
- Useful for locating extreme values.
- Frequently combined with Boolean masking.

---

## Real-World Applications

- Finding highest sales
- Detecting lowest temperatures
- Identifying best-performing students

---

# 📚 5. Stacking Arrays

## Theory

Stacking combines multiple arrays into one.

---

## Functions Learned

- `np.vstack()`
- `np.hstack()`
- `np.column_stack()`

---

### Difference

Vertical Stack

Adds rows.

Horizontal Stack

Adds columns.

Column Stack

Stacks 1D arrays as columns.

---

## Key Points

- Arrays must have compatible dimensions.
- Shape compatibility is important.

---

## Real-World Applications

- Combining monthly reports
- Combining multiple datasets
- Feature engineering

---

# 📚 6. Splitting Arrays

## Theory

Splitting divides arrays into smaller arrays.

---

## Functions Learned

- `np.split()`
- `np.hsplit()`
- `np.vsplit()`

---

### Difference

split()

General splitting.

hsplit()

Splits columns.

vsplit()

Splits rows.

---

## Key Points

- Equal divisions are required.
- Often used before training Machine Learning models.

---

## Real-World Applications

- Train/Test split
- Batch processing
- Dataset partitioning

---

# ⭐ Mini Challenge Completed

Sales Data Analysis

Concepts Applied:

- Sorting
- Searching
- Unique values
- Statistical analysis
- Aggregation functions

---

# 🌟 Bonus Challenge Completed

Movie Ratings Analysis

Concepts Applied:

- Searching
- Sorting
- Frequency analysis
- Statistical calculations
- Boolean filtering

---

# 💡 Key Learnings

- Memory sharing matters when working with large datasets.
- argsort() is useful for ranking instead of sorting directly.
- Unique values simplify categorical analysis.
- Searching functions make data retrieval efficient.
- Stacking and splitting are fundamental preprocessing techniques.

---

# ⚠️ Common Mistakes to Remember

- Forgetting that views modify the original array.
- Confusing argsort() with sort().
- Ignoring array dimensions before stacking.
- Splitting arrays into unequal sections.

---

# 📝 Revision Checklist

Before moving to Day 5, ensure you can:

✅ Explain Copy vs View

✅ Use sort() and argsort()

✅ Find unique values and frequencies

✅ Search arrays using where()

✅ Stack arrays correctly

✅ Split arrays correctly

---

# 🚀 Next Steps

Day 5:

- Advanced indexing
- Fancy indexing
- Structured arrays
- NumPy file handling
- Comprehensive NumPy revision