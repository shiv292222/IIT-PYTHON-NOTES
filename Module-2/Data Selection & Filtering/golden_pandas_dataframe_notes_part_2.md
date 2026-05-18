# Pandas DataFrame — Golden Notes (Part 2)

## What We Covered

1. Index in Pandas
2. Custom Index
3. reset_index()
4. drop=True
5. inplace=True
6. set_index()
7. Sorting + ignore_index
8. iloc
9. loc
10. Filtering
11. AND / OR Conditions
12. Real Logic Behind loc and iloc

---

# 1. What is Index in Pandas?

Every DataFrame row has a label.

Example:

```python
import pandas as pd

df = pd.DataFrame({
    "name": ["shiv", "rahul", "aman"],
    "salary": [50000, 70000, 60000]
})

print(df)
```

Output:

```python
    name   salary
0   shiv   50000
1  rahul   70000
2   aman   60000
```

The values:

```python
0
1
2
```

are called:

# INDEX

Think of index as:
- row label
- row identity
- row reference

---

# VERY IMPORTANT

Index is NOT a column.

Check:

```python
print(df.columns)
```

Output:

```python
Index(['name', 'salary'], dtype='object')
```

Notice:
- name exists
- salary exists
- index does NOT exist

Because index is separate from actual data.

---

# 2. Custom Index

We can create our own index.

```python
import pandas as pd

df = pd.DataFrame({
    "name": ["shiv", "rahul", "aman"],
    "salary": [50000, 70000, 60000]
}, index=["emp101", "emp102", "emp103"])

print(df)
```

Output:

```python
         name   salary
emp101   shiv   50000
emp102  rahul   70000
emp103   aman   60000
```

This is called:

# CUSTOM INDEX

---

# Why Custom Index Exists?

Real companies use:
- employee IDs
- customer IDs
- order IDs
- transaction IDs

instead of random row numbers.

So Pandas supports custom labels.

---

# 3. reset_index()

Suppose you want normal index back.

```python
df.reset_index()
```

Output:

```python
    index    name   salary
0  emp101    shiv   50000
1  emp102   rahul   70000
2  emp103    aman   60000
```

---

# VERY IMPORTANT OBSERVATION

Two things happened:

## Observation 1
Old index became a NEW column.

## Observation 2
New default index created.

---

# 4. reset_index(drop=True)

Suppose you DO NOT want old index.

```python
df.reset_index(drop=True)
```

Output:

```python
    name   salary
0   shiv   50000
1  rahul   70000
2   aman   60000
```

Old index removed completely.

---

# 5. VERY IMPORTANT — Changes Are NOT Saved Automatically

This is one of the MOST IMPORTANT Pandas concepts.

```python
df.reset_index(drop=True)
```

This only TEMPORARILY shows output.

Original dataframe remains unchanged.

---

# How To Save Changes?

## Method 1

```python
df = df.reset_index(drop=True)
```

---

## Method 2 (Better)

```python
df.reset_index(drop=True, inplace=True)
```

---

# 6. inplace=True

# GOLDEN DEFINITION

```python
inplace=True
```

means:

# “Modify original dataframe directly.”

Without inplace=True:
- temporary result
- original dataframe unchanged

With inplace=True:
- original dataframe permanently modified

---

# 7. set_index()

Suppose you want a column to become index.

```python
df.set_index("name", inplace=True)
```

Output:

```python
        salary
name
shiv     50000
rahul    70000
aman     60000
```

Now:

```python
name
```

became index.

---

# Real Industry Use

Companies often make:
- employee_id
- order_id
- product_id

as index because searching becomes easier.

---

# 8. Sorting Data

```python
df.sort_values(by="salary")
```

Sorts dataframe using salary column.

---

# Descending Order

```python
df.sort_values(by="salary", ascending=False)
```

---

# Problem After Sorting

Indexes may become messy.

Example:

```python
3
1
4
0
```

because rows got rearranged.

---

# Solution

## Method 1

```python
df.sort_values(by="salary", ascending=False, ignore_index=True)
```

---

## Method 2

```python
df.sort_values(by="salary", ascending=False).reset_index(drop=True)
```

Both are correct.

---

# 9. Why df[0,0] Does NOT Work?

This is a VERY IMPORTANT CONCEPT.

Many beginners think:

```python
df[0,0]
```

should work.

But DataFrame is NOT a NumPy array.

---

# NumPy vs Pandas

## NumPy

Pure matrix/array structure.

```python
arr[0,0]
```

works because arrays only understand positions.

---

## Pandas

Pandas supports:
- row labels
- column labels
- mixed data types
- custom indexes
- named columns

So Pandas needed a clearer indexing system.

---

# BIG DESIGN REASON

Suppose:

```python
df = pd.DataFrame({
    "0": [10,20],
    "1": [30,40]
})
```

Now if:

```python
df[0]
```

What should Pandas do?

Should it:
- fetch column named 0?
OR
- fetch first row?

This creates ambiguity/confusion.

---

# Pandas Solution

Pandas created TWO separate systems:

## iloc
(integer location)

## loc
(label location)

This removed confusion completely.

---

# 10. iloc

# iloc = Integer Location

Used for:
- row numbers
- column numbers

Syntax:

```python
df.iloc[row, column]
```

---

# Example

```python
df.iloc[0,0]
```

Means:
- first row
- first column

---

# Example

```python
import pandas as pd

df = pd.DataFrame({
    "name": ["shiv", "rahul"],
    "salary": [50000, 70000]
})

print(df.iloc[1,1])
```

Output:

```python
70000
```

Because:
- row index 1 = rahul row
- column index 1 = salary column

---

# iloc Slicing

```python
df.iloc[0:2, 0:1]
```

Means:
- rows 0 and 1
- column 0 only

---

# 11. loc

# loc = Label Based Indexing

loc works using:
- names
- labels
- identities
- custom indexes

Syntax:

```python
df.loc[row_label, column_label]
```

---

# Example

```python
df.loc[0, "name"]
```

Output:

```python
shiv
```

---

# Example with Custom Index

```python
import pandas as pd

df = pd.DataFrame({
    "name": ["shiv", "rahul"],
    "salary": [50000, 70000]
}, index=["emp101", "emp102"])
```

Now:

```python
df.loc["emp102"]
```

Output:

```python
name      rahul
salary    70000
```

---

# GOLDEN UNDERSTANDING

## iloc

Think:

# “Position based”

---

## loc

Think:

# “Identity based”

---

# 12. Filtering Data

Filtering is REAL Data Analyst work.

Example:

```python
df[df["salary"] > 60000]
```

Returns rows where salary > 60000.

---

# Real Industry Examples

Filtering is used for:
- employees with high salary
- customers from Canada
- failed transactions
- fraud detection
- products under specific price

---

# 13. Multiple Conditions

## AND Condition

Use:

```python
&
```

Example:

```python
df[(df["city"] == "Toronto") & (df["salary"] > 65000)]
```

Both conditions must be TRUE.

---

# OR Condition

Use:

```python
|
```

Example:

```python
df[(df["city"] == "Toronto") | (df["salary"] > 65000)]
```

Any one condition can be TRUE.

---

# NOT Condition

```python
df[df["city"] != "Delhi"]
```

Means:
- all rows except Delhi

---

# MOST COMMON BEGINNER MISTAKE

Wrong:

```python
df[df["city"] == "Toronto" & df["salary"] > 65000]
```

Correct:

```python
df[(df["city"] == "Toronto") & (df["salary"] > 65000)]
```

---

# GOLDEN RULE

Whenever using:
- &
- |

Always wrap EACH condition in brackets.

---

# 14. Selecting Specific Columns After Filtering

Example:

```python
df[(df["city"] == "Toronto") & (df["salary"] > 65000)]["name"]
```

This means:
1. Filter rows
2. Select name column only

---

# Better Industry Method

```python
df.loc[
    (df["city"] == "Toronto") & (df["salary"] > 65000),
    "name"
]
```

---

# GOLDEN STRUCTURE OF loc

```python
df.loc[ rows , columns ]
```

Remember this forever.

---

# MOST IMPORTANT TAKEAWAYS

You MUST remember these forever:

✅ Index is NOT a column
✅ reset_index() restores normal index
✅ drop=True removes old index
✅ inplace=True permanently changes dataframe
✅ set_index() makes a column the index
✅ iloc works using positions
✅ loc works using labels/identities
✅ DataFrames are NOT NumPy arrays
✅ Use & for AND
✅ Use | for OR
✅ Use brackets around each condition
✅ Filtering is real analyst work

---

# Mini Revision Questions

1. Why does df[0,0] not work?
2. Difference between loc and iloc?
3. What does inplace=True do?
4. Why use drop=True?
5. Is index a column?
6. How does loc think?
7. How does iloc think?
8. Which operator used for AND?
9. Which operator used for OR?
10. How to make a column an index?
11. How to remove custom index?
12. Why are brackets important in filtering?

---

# Final Golden Line

# Pandas is NOT about memorizing syntax.

It is about:
- understanding tables
- understanding rows and columns
- understanding labels vs positions
- understanding filtering logic
- thinking like a data analyst

