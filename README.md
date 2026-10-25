# NumPy — Practical Notes & Interview Preparation

A hands-on NumPy guide that explains **what a feature does, why it is useful, what problem it solves, and how to explain it in an interview**. Each section includes runnable Python examples and practical context rather than just a list of functions.

**Author:** [Nandan Sharma](https://github.com/nandan91531)

---

## Contents

- [About NumPy](#about-numpy)
- [Installation and import](#installation-and-import)
- [Creating arrays](#creating-arrays)
- [Array attributes](#array-attributes)
- [Data types](#data-types)
- [Indexing and slicing](#indexing-and-slicing)
- [Arithmetic and universal functions](#arithmetic-and-universal-functions)
- [Shape and reshaping](#shape-and-reshaping)
- [Joining and splitting](#joining-and-splitting)
- [Filtering and Boolean indexing](#filtering-and-boolean-indexing)
- [Sorting and searching](#sorting-and-searching)
- [Aggregations and axis](#aggregations-and-axis)
- [Random numbers](#random-numbers)
- [Copies and views](#copies-and-views)
- [Broadcasting](#broadcasting)
- [Linear algebra](#linear-algebra)
- [Missing and invalid values](#missing-and-invalid-values)
- [Quick reference](#quick-reference)
- [Interview questions and answers](#interview-questions-and-answers)
- [Practice exercises](#practice-exercises)
- [Useful links](#useful-links)

---

## About NumPy

> **Why this matters:** NumPy is built for numerical data. It gives us a consistent way to store numbers in one or more dimensions and apply calculations to many values at once.

NumPy stands for **Numerical Python**. It is a Python library for working with numerical data and multidimensional arrays. It is widely used in data analysis, scientific computing, engineering, and machine learning.

Its main data structure is the **`ndarray`**. NumPy supports vectorized operations, so calculations can often be performed on whole arrays without writing a Python loop for every element.

## Installation and import

> **Why this matters:** Installing the library makes its functions available in your Python environment. The `np` alias is a widely used convention, so examples and documentation are easier to read.

Install NumPy with pip:

```bash
python -m pip install numpy
```

Import it using the convention used in most Python projects:

```python
import numpy as np

print(np.__version__)
```

## Creating arrays

> **Why this matters:** Most numerical work starts by turning values into an array or creating a predictable array for testing. Constructors save you from manually building large datasets and matrices.

### From lists

```python
import numpy as np

one_d = np.array([10, 20, 30, 40])
two_d = np.array([
    [18, 85, 78],
    [19, 92, 88],
    [17, 76, 69]
])

print(one_d)
print(two_d)
```

### Common array constructors

```python
np.zeros((2, 3))       # 2 rows, 3 columns of zeros
np.ones((3, 2))        # 3 rows, 2 columns of ones
np.full((2, 2), 7)     # Fill an array with 7
np.eye(3)              # 3 x 3 identity matrix
np.arange(0, 10, 2)    # [0, 2, 4, 6, 8]
np.linspace(0, 1, 5)    # 5 evenly spaced values from 0 to 1
```

`np.arange(start, stop, step)` excludes the stop value. `np.linspace(start, stop, count)` produces the requested number of evenly spaced values and includes the endpoints by default.

`np.empty(shape)` allocates an array without initializing its elements to zero. Set its values before using them.

## Array attributes

> **Why this matters:** Before calculating anything, you often need to confirm the data has the expected structure. These attributes help catch shape mistakes early.

```python
data = np.array([[1, 2, 3], [4, 5, 6]])

print(data.ndim)       # Number of dimensions: 2
print(data.shape)      # Shape: (2, 3)
print(data.size)       # Total elements: 6
print(data.dtype)      # Element data type
print(data.itemsize)   # Bytes used by each element
```

| Attribute | What it tells you |
| --- | --- |
| `ndim` | Number of dimensions (axes) |
| `shape` | Length along each dimension |
| `size` | Total number of elements |
| `dtype` | Data type of the elements |
| `itemsize` | Bytes used by one element |

**Keep in mind:** `shape` describes the layout, while `size` counts all elements. For example, an array with shape `(3, 4)` contains 12 elements.

## Data types

> **Why this matters:** The data type affects what values can be represented, how much memory is used, and how calculations behave. Checking it is important when data comes from files or other libraries.

NumPy arrays generally hold elements of one data type. Common types include integers, floating-point values, Booleans, and strings.

```python
integers = np.array([1, 2, 3], dtype=np.int64)
decimals = np.array([1, 2, 3], dtype=np.float32)
flags = np.array([True, False, True])

values = np.array([1.8, 2.4, 3.9])
print(values.astype(int))  # [1 2 3]
```

`astype()` converts an array to another type. Converting floats to integers truncates the fractional part; it does not round to the nearest integer.

## Indexing and slicing

> **Why this matters:** Datasets commonly store one record per row and one feature per column. Indexing lets you extract exactly the records or features you need without writing loops.

Python and NumPy use zero-based indexing.

### One-dimensional arrays

```python
a = np.array([10, 20, 30, 40, 50])

print(a[0])       # 10: first element
print(a[-1])      # 50: last element
print(a[1:4])     # [20, 30, 40] (stop index is excluded)
print(a[::2])     # [10, 30, 50]
print(a[::-1])    # Reversed order
```

### Two-dimensional arrays

```python
data = np.array([
    [18, 85, 78],
    [19, 92, 88],
    [17, 76, 69]
])

print(data[0, 1])    # 85: row 0, column 1
print(data[1])       # Second row
print(data[:, 0])    # First column from every row
print(data[:, 2])    # Third column from every row
print(data[0:2, 1:3])
```

In `data[row, column]`, the first index selects the row and the second selects the column. A colon (`:`) means the full range along that axis.

## Arithmetic and universal functions

> **Why this matters:** A common numerical task is applying the same calculation to every element. Vectorized arithmetic and NumPy functions make this concise and can use optimized low-level implementations.

Most arithmetic operators work element by element when array shapes are compatible.

```python
a = np.array([10, 20, 30])
b = np.array([1, 2, 3])

print(a + b)    # [11 22 33]
print(a - b)    # [ 9 18 27]
print(a * b)    # [10 40 90]
print(a / b)    # [10. 10. 10.]
print(a ** 2)   # [100 400 900]
```

Useful numerical functions include:

```python
values = np.array([1, 4, 9, 16])

print(np.sqrt(values))
print(np.sum(values))
print(np.mean(values))
print(np.min(values))
print(np.max(values))
print(np.abs(np.array([-2, -5, 3])))
```

`*` performs element-wise multiplication. For matrix multiplication, use `@` or an appropriate function from `numpy.linalg`.

## Shape and reshaping

> **Why this matters:** The same values may need a different layout for a calculation, image, batch, or model input. Reshaping changes the arrangement, not the number of elements.

`reshape()` changes an array's dimensions without changing the order of its elements. The new shape must contain the same total number of elements.

```python
a = np.arange(1, 7)
print(a.reshape(2, 3))
# [[1 2 3]
#  [4 5 6]]

b = np.arange(12)
print(b.reshape(3, -1).shape)  # (3, 4); NumPy infers the dimension
```

Other useful operations:

```python
a = np.arange(6).reshape(2, 3)

print(a.T)          # Transpose for a 2D array
print(a.flatten())  # Flattened copy
print(a.ravel())    # Flattened view when possible
```

## Joining and splitting

> **Why this matters:** Real data often arrives in separate batches or needs to be divided into smaller parts. Joining and splitting let you organize these arrays while keeping dimensions consistent.

### Joining

```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

print(np.concatenate((a, b)))
print(np.vstack((a, b)))  # Stack as rows
print(np.hstack((a, b)))  # Stack along columns for 2D arrays
```

For arrays with more than one dimension, dimensions other than the joining axis generally need to match.

### Splitting

```python
a = np.array([10, 20, 30, 40, 50, 60])
print(np.split(a, 3))
```

`np.split()` requires equal-sized sections when given an integer number of sections. Use `np.array_split()` if section sizes can differ.

## Filtering and Boolean indexing

> **Why this matters:** Real datasets often contain rows that do not meet the condition you need. Boolean indexing selects or updates matching data without a manual loop.

A comparison on an array creates a Boolean array. Use it to select or update matching values.

```python
marks = np.array([85, 62, 91, 70, 48])
print(marks[marks >= 70])  # [85 91 70]
```

### Example: work with rows and columns

Assume the columns are **Age, Math marks, Science marks**:

```python
data = np.array([
    [18, 85, 78],
    [19, 92, 88],
    [17, 76, 69],
    [18, 60, 72]
])

print(data[:, 2])                    # Every Science mark
print(data[data[:, 2] < 75])         # Rows with Science < 75

data[data[:, 2] < 75, 2] = 0         # Replace those Science marks with 0
print(data)
```

How `data[data[:, 2] < 75, 2] = 0` works:

1. `data[:, 2]` selects the third column from every row.
2. `data[:, 2] < 75` produces a Boolean condition for those values.
3. `data[condition, 2]` selects the third-column entries in rows where the condition is true.
4. `= 0` replaces the selected entries with zero.

### Combining conditions

```python
a = np.array([10, 20, 30, 40, 50])

print(a[(a >= 20) & (a <= 40)])  # AND condition
print(a[(a < 20) | (a > 40)])    # OR condition
print(a[~(a > 30)])             # NOT condition
```

Use `&` for element-wise AND, `|` for OR, and `~` for NOT. Put each comparison in parentheses. Python's `and` and `or` are not suitable for element-wise array conditions.

Other useful functions:

```python
print(np.where(a > 30, "large", "small"))
print(np.any(a > 40))  # True if at least one element matches
print(np.all(a > 0))   # True if every element matches
```

## Sorting and searching

> **Why this matters:** Sorting helps order values, while search and index functions help locate important values or the positions that would order the data.

```python
a = np.array([40, 10, 30, 20])

print(np.sort(a))        # Sorted copy
print(np.argsort(a))     # Indices that would sort the array
print(np.argmax(a))      # Index of maximum value
print(np.argmin(a))      # Index of minimum value
print(np.where(a == 30)) # Matching index
```

For a 2D array, `np.sort(data, axis=0)` sorts each column, while `np.sort(data, axis=1)` sorts each row.

## Aggregations and axis

> **Why this matters:** Sums, averages, and other summaries turn raw data into useful information. The `axis` argument lets you summarize rows or columns independently.

Aggregations summarize an array's values.

```python
marks = np.array([85, 92, 76, 88, 69])

print(np.sum(marks))
print(np.mean(marks))
print(np.median(marks))
print(np.min(marks))
print(np.max(marks))
print(np.std(marks))
print(np.var(marks))
```

- `mean`: arithmetic average.
- `median`: middle value after sorting.
- `std`: standard deviation.
- `var`: variance.

By default, `std()` and `var()` use the population calculation (`ddof=0`). Use `ddof=1` for the sample versions.

### Understanding `axis`

```python
data = np.array([
    [10, 20, 30],
    [40, 50, 60]
])

print(np.sum(data, axis=0))  # [50 70 90]: one sum per column
print(np.sum(data, axis=1))  # [60 150]: one sum per row
```

For a 2D array, `axis=0` reduces the rows and leaves one result per column. `axis=1` reduces the columns and leaves one result per row.

## Random numbers

> **Why this matters:** Random data is useful for simulations, sampling, tests, and reproducible experiments. A generator with a fixed seed makes debugging and demonstrations repeatable.

Use NumPy's random number generator for simulations, sampling, and experiments.

```python
rng = np.random.default_rng(seed=42)

print(rng.integers(1, 10, size=5))  # Integers from 1 to 9
print(rng.random(3))                # Floats between 0 and 1
print(rng.normal(0, 1, size=4))     # Normal distribution
```

A fixed seed makes a sequence reproducible. The upper bound in `integers(1, 10)` is excluded.

```python
rng = np.random.default_rng(42)
a = np.array([1, 2, 3, 4, 5])
rng.shuffle(a)  # Shuffles a in place
print(a)
```

## Copies and views

> **Why this matters:** NumPy can expose the same underlying memory through a view. Understanding this avoids accidental changes to the original dataset and unnecessary copies.

A **view** shares the underlying data with another array when possible. A **copy** has independent data.

```python
a = np.array([10, 20, 30, 40])

view = a[1:3]
view[0] = 99
print(a)  # [10 99 30 40]: the original changed

copy = a[1:3].copy()
copy[0] = 55
print(a)  # [10 99 30 40]: the original did not change again
```

Basic slices commonly return views, while advanced indexing commonly returns copies. Use `.copy()` when you need an independent array.

## Broadcasting

> **Why this matters:** Sometimes you need to apply one value or a smaller array across a larger array. Broadcasting performs compatible operations without manually repeating the smaller array.

Broadcasting lets NumPy perform operations on arrays with compatible shapes without manually repeating values.

```python
a = np.array([10, 20, 30])
print(a + 5)  # [15 25 35]

matrix = np.array([
    [1, 2, 3],
    [4, 5, 6]
])
offset = np.array([10, 20, 30])
print(matrix + offset)
# [[11 22 33]
#  [14 25 36]]
```

When comparing shapes from the right, dimensions are compatible if they are equal or one of them is `1`. Incompatible shapes raise a broadcasting error.

## Linear algebra

> **Why this matters:** Many engineering, scientific, and machine-learning tasks use vectors and matrices. NumPy provides standard operations for multiplying matrices and solving systems of equations.

NumPy provides matrix and vector operations through `numpy.linalg`.

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

print(a @ b)               # Matrix multiplication
print(np.linalg.det(a))    # Determinant
print(np.linalg.inv(a))    # Inverse, if it exists
print(np.linalg.eig(a))    # Eigenvalues and eigenvectors
```

To solve a system of linear equations `Ax = b`, use `solve()`:

```python
A = np.array([[3, 1], [1, 2]])
b = np.array([9, 8])

solution = np.linalg.solve(A, b)
print(solution)
```

Using `solve()` is generally preferable to calculating an inverse just to solve a system of equations.

## Missing and invalid values

> **Why this matters:** Missing values and infinities can distort statistics or break later calculations. Detecting them early makes data cleaning more reliable.

Missing floating-point values are often represented by `np.nan`.

```python
a = np.array([10.0, 20.0, np.nan, 40.0])

print(np.isnan(a))
print(np.nanmean(a))  # Mean ignoring NaN values
print(np.nanmax(a))   # Maximum ignoring NaN values
```

Check for finite values (not NaN and not positive/negative infinity):

```python
a = np.array([1.0, np.inf, -np.inf, np.nan])
print(np.isfinite(a))
```

`np.nanmean()` ignores NaNs, but it does not automatically ignore positive or negative infinity.

## Quick reference

> **Why this matters:** Use this table when you remember the task but need to quickly recall the relevant NumPy function.

| Task | NumPy example |
| --- | --- |
| Create an array | `np.array([1, 2, 3])` |
| Create a range | `np.arange(start, stop, step)` |
| Create evenly spaced values | `np.linspace(start, stop, count)` |
| Check dimensions | `a.ndim` |
| Check shape | `a.shape` |
| Count elements | `a.size` |
| Select a row | `a[row_index]` |
| Select a column | `a[:, column_index]` |
| Reshape | `a.reshape(rows, cols)` |
| Flatten to a copy | `a.flatten()` |
| Calculate an average | `np.mean(a)` |
| Sum values | `np.sum(a)` |
| Sort values | `np.sort(a)` |
| Find matching indices | `np.where(condition)` |
| Select matching values | `a[condition]` |
| Matrix multiplication | `a @ b` |
| Make an independent copy | `a.copy()` |

## Interview questions and answers

These are common beginner-to-intermediate questions. Try answering each one aloud before reading the answer; interviewers often ask follow-up questions, so make sure you understand the example too.

### 1. What is NumPy, and where is it used?
NumPy is a Python library for numerical computing. Its main object is the N-dimensional `ndarray`, used in data analysis, scientific computing, engineering, and machine-learning preprocessing.

### 2. Why use NumPy instead of a Python list?
NumPy supports vectorized arithmetic, multidimensional arrays, and optimized numerical routines. Lists are more flexible for mixed objects, but NumPy is often more convenient and faster for substantial numerical workloads. It is not guaranteed to be faster for every tiny operation.

### 3. What is an `ndarray`?
It is NumPy's N-dimensional array object. It has a shape and a data type, and supports element-wise calculations and array operations.

### 4. What is the difference between `shape`, `size`, and `ndim`?
`shape` gives the length of each dimension, `size` gives the total number of elements, and `ndim` gives the number of dimensions. For a `(3,  4)` array, `ndim` is 2 and `size` is 12.

### 5. What is the difference between `arange()` and `linspace()`?
`arange()` creates values using a step size and excludes the stop value. `linspace()` creates a specified number of evenly spaced values and includes the endpoint by default.

### 6. What does vectorization mean?
Vectorization means applying an operation to an entire array instead of writing a Python loop for each element. NumPy can execute many such operations in optimized low-level code.

### 7. Explain `axis=0` and `axis=1`.
For a 2D array, `axis=0` reduces down the rows and returns one result per column. `axis=1` reduces across columns and returns one result per row. Example: `np.sum(data, axis=0)` calculates each column's sum.

### 8. What is broadcasting?
Broadcasting lets arrays of compatible shapes work together without manually repeating values. Dimensions are compatible when they are equal or one of them is 1.

### 9. What is the difference between a view and a copy?
A view shares underlying data with the original array when possible, so changing it may change the original. A copy owns independent data. Use `.copy()` when you need to edit a selection safely.

### 10. What is Boolean indexing?
It selects or updates array elements using a condition. For example, `marks[marks >= 70]` returns the marks that are at least 70.

### 11. What is the difference between `*` and `@`?
`*` performs element-wise multiplication. `@` performs matrix multiplication, provided the dimensions are compatible.

### 12. What is the difference between `flatten()` and `ravel()`?
`flatten()` always returns a copy. `ravel()` returns a view when possible and a copy when necessary.

### 13. What is the difference between `max()` and `argmax()`?
`max()` returns the maximum value. `argmax()` returns the index of the maximum value along the chosen axis.

### 14. How do you filter values in a range?
Use Boolean indexing and combine conditions with `&`:

```python
a[(a >= 20) & (a <= 40)]
```

Put each comparison in parentheses. For element-wise conditions, use `&` and `|`, not Python's `and` and `or`.

### 15. How do you replace values below 75 in the third column with zero?

```python
data[data[:, 2] < 75, 2] = 0
```

`data[:, 2]` selects the third column, the comparison creates a Boolean mask, and the assignment updates the selected rows in that column.

### 16. How do you handle NaN values when calculating an average?
Use `np.nanmean(data)` to ignore NaN values. Check for positive and negative infinity separately if they should also be treated as invalid.

### 17. How do you solve a system of linear equations `Ax = b`?
Use `np.linalg.solve(A, b)` when the system has a suitable square, nonsingular coefficient matrix. It is preferable to calculating an inverse just to solve the system.

### 18. How do you generate repeatable random numbers?
Use a seeded generator, such as `rng = np.random.default_rng(42)`. With the same seed and same sequence of calls, the generated sequence is reproducible.

### 19. Does NumPy always run faster than lists?
No. NumPy often performs well for larger numerical workloads, but creating arrays and calling functions has overhead. The best choice depends on data size and the operation.

### 20. Name some common NumPy mistakes.
Confusing `shape` with `size`, using `and` instead of `&` for array conditions, confusing element-wise multiplication with matrix multiplication, ignoring broadcasting rules, and accidentally changing source data through a view.

---

## Practice exercises

> **Why this matters:** Reading examples is not enough to build fluency. Solve these tasks yourself, then compare your result with the notes and test edge cases.

Try these without looking at the examples first:

1. Create an array from 1 to 20 and print only the even values.
2. Create a `3 × 3` matrix and print its shape, dimensions, and element count.
3. Given a marks array, calculate its mean and select marks greater than the mean.
4. Given a table with age, Math marks, and Science marks, replace Science marks below 75 with zero.
5. Reshape 12 elements into a `3 × 4` matrix.
6. Generate 100 random integers and calculate their mean, minimum, and maximum.
7. Create two matrices and multiply them using `@`.
8. Compare a slice with its copy by modifying an element in each.

## Useful links

> **Why this matters:** The official documentation is the best place to confirm exact behaviour, available arguments, and version-specific details.

- [NumPy documentation](https://numpy.org/doc/)
- [NumPy quickstart tutorial](https://numpy.org/doc/stable/user/quickstart.html)
- [NumPy API reference](https://numpy.org/doc/stable/reference/index.html)

---

**Author:** [Nandan Sharma](https://github.com/nandan91531)
