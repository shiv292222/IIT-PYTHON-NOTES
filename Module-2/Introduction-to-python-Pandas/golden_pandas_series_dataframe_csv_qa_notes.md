# 🏆 GOLDEN PANDAS QUESTIONS & ANSWERS
## Series + DataFrames + CSV (Foundation Mastery)

---

# 🐼 SECTION 1 — PANDAS SERIES

---

# ❓ QUESTION 1
# What is a Pandas Series?

## ✅ Answer

A Pandas Series is:

# A single column of data.

Example:

| Index | Value |
|---|---|
| 0 | 10 |
| 1 | 20 |
| 2 | 30 |

Series internally stores:
- indexes
- values

A Series is built on top of:
# NumPy arrays.

---

# ❓ QUESTION 2
# Create a Series containing 10,20,30,40.

## ✅ Answer

```python
import pandas as pd

s = pd.Series([10,20,30,40])

print(s)
```

---

# ❓ QUESTION 3
# What are automatic indexes in Series?

## ✅ Answer

When we do NOT provide custom indexes:

```python
s = pd.Series([10,20,30])
```

Pandas automatically creates:

```python
0
1
2
```

These are called:
# automatic indexes.

---

# ❓ QUESTION 4
# How to access first value in Series?

## ✅ Answer

```python
s[0]
```

Explanation:
- Pandas searches for label/index 0.
- Then returns corresponding value.

---

# ❓ QUESTION 5
# Create Series with custom indexes.

## ✅ Answer

```python
s = pd.Series(
    [95,88,76],
    index=["shiv","rahul","aman"]
)

print(s)
```

Output:

```python
shiv     95
rahul    88
aman     76
```

---

# ❓ QUESTION 6
# How to access value using custom label?

## ✅ Answer

```python
print(s["rahul"])
```

Output:

```python
88
```

---

# ❓ QUESTION 7
# Why does s[-1] sometimes give error?

## ✅ Answer

Example:

```python
s = pd.Series(
    [10,20,30],
    index=["a","b","c"]
)
```

Now:

```python
s[-1]
```

❌ Gives error.

Why?

Because Pandas thinks:
# “Find label -1.”

But label -1 does not exist.

---

# ❓ QUESTION 8
# How to access last element by position?

## ✅ Answer

```python
s.iloc[-1]
```

Explanation:

```python
iloc
```
means:
# integer-location indexing.

It accesses positions instead of labels.

---

# ❓ QUESTION 9
# Reverse a Series.

## ✅ Answer

```python
print(s[::-1])
```

Explanation:
- Uses slicing.
- Works similar to Python lists.
- Both indexes and values reverse.

---

# ❓ QUESTION 10
# Multiply all values in Series by 10.

## ✅ Answer

```python
s * 10
```

Explanation:
- Operation happens on complete column.
- No manual loops required.
- This is called:
# vectorized operation.

---

# ❓ QUESTION 11
# Create boolean mask for values > 50.

## ✅ Answer

```python
marks = pd.Series([45,90,78,20,99])

print(marks > 50)
```

Output:

```python
0    False
1    True
2    True
3    False
4    True
```

This is called:
# Boolean mask.

---

# ❓ QUESTION 12
# Filter values greater than 50.

## ✅ Answer

```python
print(marks[marks > 50])
```

Explanation:

Step 1:

```python
marks > 50
```

creates:

```python
True / False
```

Step 2:

```python
marks[mask]
```

keeps only True rows.

---

# ❓ QUESTION 13
# Sort Series ascending and descending.

## ✅ Answer

### Ascending

```python
s.sort_values()
```

### Descending

```python
s.sort_values(ascending=False)
```

---

# ❓ QUESTION 14
# Find sum, mean, max and min of Series.

## ✅ Answer

```python
print(s.sum())
print(s.mean())
print(s.max())
print(s.min())
```

---

# 🐼 SECTION 2 — PANDAS DATAFRAMES

---

# ❓ QUESTION 15
# What is a DataFrame?

## ✅ Answer

A DataFrame is:
# Multiple Series together.

OR

# Complete Excel-like table inside Python.

Example:

| Name | Age |
|---|---|
| Shiv | 22 |
| Rahul | 25 |

---

# ❓ QUESTION 16
# Create a DataFrame.

## ✅ Answer

```python
import pandas as pd

df = pd.DataFrame({
    "name": ["shiv","rahul","aman"],
    "age": [22,25,21],
    "salary": [5000,7000,4000]
})

print(df)
```

---

# ❓ QUESTION 17
# What is the internal structure of DataFrame?

## ✅ Answer

```text
DataFrame
   ↓
Multiple Series
   ↓
NumPy arrays
```

Every column inside DataFrame is internally a Series.

---

# ❓ QUESTION 18
# Show first and last rows of DataFrame.

## ✅ Answer

### First rows

```python
print(df.head())
```

### Last rows

```python
print(df.tail())
```

---

# ❓ QUESTION 19
# Find shape of DataFrame.

## ✅ Answer

```python
print(df.shape)
```

Example output:

```python
(5,4)
```

Meaning:
- 5 rows
- 4 columns

---

# ❓ QUESTION 20
# Print column names.

## ✅ Answer

```python
print(df.columns)
```

---

# ❓ QUESTION 21
# Print datatypes of all columns.

## ✅ Answer

```python
print(df.dtypes)
```

---

# ❓ QUESTION 22
# Why does df.info not work?

## ✅ Answer

❌ Wrong:

```python
df.info
```

✅ Correct:

```python
df.info()
```

Reason:

```python
info()
```
is a function.

Functions require:

```python
()
```

---

# ❓ QUESTION 23
# What is the difference between attribute and function?

## ✅ Answer

| Type | Example |
|---|---|
| Attribute | df.shape |
| Function | df.head() |

Attributes:
- stored properties
- no brackets

Functions:
- execute operations
- require ()

---

# ❓ QUESTION 24
# What does describe() do?

## ✅ Answer

```python
print(df.describe())
```

describe() gives statistical summary:
- mean
- min
- max
- count
- std

Mostly works on:
# numerical columns.

---

# ❓ QUESTION 25
# Why are string columns usually missing from describe()?

## ✅ Answer

Because statistics like:

```text
mean of "shiv"
```

make no sense.

So describe() mostly analyzes:
- int
- float

columns.

---

# ❓ QUESTION 26
# Select single column from DataFrame.

## ✅ Answer

```python
df["salary"]
```

Returns:
# Series

Because one column = Series.

---

# ❓ QUESTION 27
# Select multiple columns from DataFrame.

## ✅ Answer

```python
df[["name","salary"]]
```

Returns:
# DataFrame

Because multiple columns form table.

---

# ❓ QUESTION 28
# Difference between df["age"] and df[["age"]].

## ✅ Answer

| Syntax | Returns |
|---|---|
| df["age"] | Series |
| df[["age"]] | DataFrame |

Reason:
- single brackets → one column
- double brackets → list of columns

---

# ❓ QUESTION 29
# Create new column in DataFrame.

## ✅ Answer

```python
df["new_salary"] = df["salary"] + 1000
```

Explanation:
- Entire salary column updated.
- New column created.
- Vectorized operation.

---

# ❓ QUESTION 30
# Filter rows where salary > 5000.

## ✅ Answer

```python
print(df[df["salary"] > 5000])
```

Explanation:

Step 1:

```python
df["salary"] > 5000
```

creates boolean mask.

Step 2:

```python
df[mask]
```

returns matching rows.

---

# ❓ QUESTION 31
# Filter DataFrame using multiple conditions.

## ✅ Answer

```python
print(
    df[
        (df["salary"] > 5000) &
        (df["age"] > 22)
    ]
)
```

---

# ❓ QUESTION 32
# Why do we use & instead of and?

## ✅ Answer

Because Pandas works:
# element-wise.

```python
&
```
works element-wise for Series/DataFrames.

```python
and
```
does not.

---

# ❓ QUESTION 33
# Sort DataFrame ascending and descending.

## ✅ Answer

### Ascending

```python
df.sort_values(by="salary")
```

### Descending

```python
df.sort_values(by="salary", ascending=False)
```

---

# ❓ QUESTION 34
# Does sort_values permanently change DataFrame?

## ✅ Answer

No.

By default:

```python
df.sort_values()
```

returns temporary sorted result.

Original DataFrame remains unchanged.

---

# ❓ QUESTION 35
# How to permanently save sorting?

## ✅ Answer

### Method 1

```python
df = df.sort_values(by="salary")
```

### Method 2

```python
df.sort_values(by="salary", inplace=True)
```

---

# ❓ QUESTION 36
# Why do indexes become shuffled after sorting?

## ✅ Answer

Because original row labels remain attached.

Example:

```python
3
1
4
0
```

Indexes are original row labels.

---

# ❓ QUESTION 37
# Fix shuffled indexes after sorting.

## ✅ Answer

```python
df.reset_index(drop=True)
```

---

# ❓ QUESTION 38
# Why use drop=True in reset_index()?

## ✅ Answer

Without:

```python
drop=True
```

old indexes become new column.

With:

```python
drop=True
```

old indexes are removed completely.

---

# 🐼 SECTION 3 — CSV FILE HANDLING

---

# ❓ QUESTION 39
# What is CSV?

## ✅ Answer

CSV means:
# Comma Separated Values.

Example:

```csv
name,age,salary
shiv,22,5000
rahul,25,7000
```

CSV is lightweight tabular data format.

---

# ❓ QUESTION 40
# Why CSV files are important?

## ✅ Answer

CSV files are widely used because:
- lightweight
- easy to transfer
- easy to store
- database exports
- analytics datasets
- ML datasets

Used everywhere in industry.

---

# ❓ QUESTION 41
# Read CSV file using Pandas.

## ✅ Answer

```python
import pandas as pd

df = pd.read_csv("employees.csv")

print(df)
```

---

# ❓ QUESTION 42
# What does read_csv() do internally?

## ✅ Answer

Pandas:
1. opens file
2. reads rows
3. separates commas
4. creates columns
5. converts data into DataFrame

---

# ❓ QUESTION 43
# Save DataFrame as CSV.

## ✅ Answer

```python
df.to_csv("employees.csv", index=False)
```

---

# ❓ QUESTION 44
# Why use index=False in to_csv()?

## ✅ Answer

Without:

```python
index=False
```

Pandas also saves indexes:

```csv
0,shiv,22
1,rahul,25
```

Usually unwanted.

So:

```python
index=False
```

prevents saving indexes.

---

# ❓ QUESTION 45
# Real industry flow of CSV handling.

## ✅ Answer

```text
CSV file
   ↓
pd.read_csv()
   ↓
DataFrame
   ↓
Filtering / Analysis / Cleaning
   ↓
Save using to_csv()
```

---

# 🏆 FINAL GOLDEN UNDERSTANDING

| Structure | Purpose |
|---|---|
| List | General Python storage |
| Dictionary | Key-value storage |
| NumPy Array | Fast numerical operations |
| Series | One analytical column |
| DataFrame | Complete analytical table |
| CSV | Real-world data storage format |

---

# 🚀 MOST IMPORTANT MINDSET SHIFT

# Old Python Thinking

```python
for item in data:
```

# Pandas Thinking

```python
df["salary"] * 2
```

Operate on complete column/table at once.

This is called:
# vectorized thinking.

