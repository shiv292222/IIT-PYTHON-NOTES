# Pandas GroupBy & Pivot Table — Golden Notes 🔥

# WHY DO WE EVEN NEED AGGREGATION?

Imagine a company has:
- 10 lakh sales rows
- 5 lakh customers
- 1000 servers
- millions of logs

Can humans directly read all rows and understand insights?

NO.

We need a way to:
- summarize data
- reduce huge data into meaningful numbers
- detect patterns
- compare categories
- make decisions

This process is called:

# Aggregation

Aggregation means:

> Combining many rows into summarized information.

Examples:
- average salary
- total sales
- maximum CPU
- minimum latency
- count of users

---

# DESCRIPTIVE STATISTICS

Pandas gives quick summary statistics using:

```python
df.describe()
```

This gives:
- count
- mean
- std
- min
- max
- quartiles

Meaning:

> Quick statistical overview of the dataset.

---

# COLUMN-WISE DESCRIBE

```python
df["salary"].describe()
```

This gives statistics only for salary column.

---

# QUICK AGGREGATIONS

You can directly calculate:

```python
df["salary"].mean()
df["salary"].max()
df["salary"].min()
df["salary"].median()
df["salary"].sum()
df["salary"].count()
```

---

# THE BIG PROBLEM 🔥

Suppose:

```python
df["salary"].mean()
```

This gives:

> ONE overall average.

But companies usually ask:

- average salary per department
- total sales per city
- maximum CPU per server
- average latency per API
- total revenue per product

Now we need:

# Aggregation INSIDE categories.

This is why GroupBy exists.

---

# GROUPBY — CORE IDEA 🔥

# GroupBy = Split → Apply → Combine

This is the MOST IMPORTANT mental model.

---

# STEP 1 — Split

Split rows into groups.

Example:

```python
df.groupby("department")
```

creates groups like:

```text
IT → rows
HR → rows
Finance → rows
```

---

# STEP 2 — Apply

Apply calculations on each group.

Example:

```python
df.groupby("department")["salary"].mean()
```

For each department:
- take salary column
- calculate mean

---

# STEP 3 — Combine

Pandas combines results into summarized output.

---

# SIMPLE EXAMPLE

Suppose:

| name | department | salary |
|---|---|---|
| A | IT | 80000 |
| B | IT | 60000 |
| C | HR | 40000 |
| D | HR | 50000 |

---

# NORMAL AGGREGATION

```python
df["salary"].mean()
```

Calculation:

```python
(80000 + 60000 + 40000 + 50000) / 4
```

Overall average.

---

# GROUPBY AGGREGATION

```python
df.groupby("department")["salary"].mean()
```

Now:

IT group:
- 80000
- 60000

HR group:
- 40000
- 50000

Then average calculated separately.

Output:

| department | salary |
|---|---|
| HR | 45000 |
| IT | 70000 |

---

# MOST IMPORTANT SYNTAX 🔥

```python
df.groupby("group_column")["target_column"].aggregation()
```

Example:

```python
df.groupby("city")["salary"].mean()
```

Read like English:

> Group rows by city and calculate average salary.

---

# IMPORTANT UNDERSTANDING 🔥

This:

```python
df.groupby("department")
```

ONLY creates groups.

No calculation happens yet.

Calculation starts here:

```python
["salary"].mean()
```

---

# WHY ["salary"] AFTER GROUPBY?

This is VERY important.

```python
df.groupby("department")
```

groups the WHOLE dataframe.

Then:

```python
["salary"]
```

says:

> “Now calculate only on salary column.”

---

# COMMON AGGREGATIONS

```python
.mean()
.sum()
.max()
.min()
.median()
.count()
.std()
```

---

# EXAMPLES

## Average salary per city

```python
df.groupby("city")["salary"].mean()
```

---

## Maximum salary per department

```python
df.groupby("department")["salary"].max()
```

---

## Total sales per product

```python
df.groupby("product")["sales"].sum()
```

---

# MULTIPLE AGGREGATIONS 🔥

Companies usually need multiple summaries together.

Example:

```python
df.groupby("department")["salary"].agg(["mean", "max", "min"])
```

Output:
- average salary
- highest salary
- lowest salary

for each department.

---

# WHY .agg() EXISTS?

Because:

```python
.mean()
```

can do only ONE calculation.

But:

```python
.agg()
```

can perform MANY calculations together.

---

# MULTI-COLUMN GROUPBY 🔥

```python
df.groupby(["department", "city"])["salary"].mean()
```

Now grouping happens using COMBINATIONS.

Example groups:

```text
IT + Toronto
IT + Delhi
HR + Toronto
HR + Delhi
```

NOT separately.

---

# MULTIINDEX / HIERARCHICAL INDEX 🔥

When multiple group columns are used:

```python
df.groupby(["department", "city"])
```

Pandas creates nested indexes.

Example:

```text
department   city
IT           Delhi
             Toronto
HR           Delhi
```

This is called:
- MultiIndex
- Hierarchical Index

---

# RESET_INDEX 🔥

To convert grouped result back into normal dataframe:

```python
.reset_index()
```

Example:

```python
df.groupby(["department", "city"])["salary"].mean().reset_index()
```

VERY commonly used in industry.

---

# DIFFERENT AGGREGATIONS FOR DIFFERENT COLUMNS 🔥

```python
df.groupby("city").agg({
    "salary": "mean",
    "experience": "max"
})
```

Meaning:

For each city:
- calculate average salary
- calculate maximum experience

---

# REAL-WORLD INDUSTRY EXAMPLES 🔥

## SRE / Monitoring

```python
df.groupby("server")["cpu"].max()
```

Peak CPU per server.

---

## Datadog Style Metrics

```python
df.groupby("service")["latency"].mean()
```

Average latency per service.

---

## E-Commerce

```python
df.groupby("product")["sales"].sum()
```

Total sales per product.

---

## Machine Learning Feature Engineering

```python
df.groupby("customer")["orders"].count()
```

Total orders per customer.

Used as ML feature.

---

# PIVOT TABLE 🔥

Pivot table is ALSO used for:
- grouping
- aggregation
- summarization

BUT...

Pivot table additionally reshapes data into MATRIX format.

---

# BIGGEST DIFFERENCE 🔥

# GroupBy

Focus:
- aggregation

Output:
- long/list style

---

# Pivot Table

Focus:
- aggregation
- reshaping

Output:
- matrix/cross-tab style

---

# SIMPLE GROUPBY OUTPUT

```python
df.groupby("department")["salary"].mean()
```

Output:

| department | salary |
|---|---|
| HR | 45000 |
| IT | 70000 |

---

# SIMPLE PIVOT OUTPUT

```python
pd.pivot_table(
    df,
    values="salary",
    index="department",
    columns="city",
    aggfunc="mean"
)
```

Output:

| department | Delhi | Toronto |
|---|---|---|
| HR | 40000 | 50000 |
| IT | 60000 | 80000 |

---

# MOST IMPORTANT UNDERSTANDING 🔥

Pivot table ALSO does grouping internally.

But instead of writing:

```python
groupby("department")
```

pivot table uses:

```python
index="department"
```

Meaning:

> “Group rows by department.”

---

# PIVOT TABLE COMPONENTS 🔥

## values

```python
values="salary"
```

Means:

> Which column should calculations happen on?

---

## index

```python
index="department"
```

Means:

> Which column should become ROWS?

This is basically the GROUPBY part.

---

## columns

```python
columns="city"
```

Means:

> Which column should spread horizontally?

This creates matrix-style output.

---

## aggfunc

```python
aggfunc="mean"
```

Means:

> Which calculation should happen?

---

# PIVOT TABLE INTERNAL LOGIC 🔥

Pivot table internally performs:

```text
Grouping
+
Aggregation
+
Reshaping
```

---

# WHY PIVOT TABLE LOOKS CONFUSING?

Because it mixes:
- grouping
- aggregation
- reshaping

all together.

GroupBy looks easier because syntax is direct.

---

# LONG FORMAT VS WIDE FORMAT 🔥

# GroupBy → Long Format

| city | sales |
|---|---|
| Toronto | 100 |
| Delhi | 200 |

---

# Pivot Table → Wide Format

| Toronto | Delhi |
|---|---|
| 100 | 200 |

---

# WHEN TO USE WHAT?

# Use GroupBy when:
- doing analysis
- preprocessing data
- coding pipelines
- machine learning
- transformations

---

# Use Pivot Table when:
- creating reports
- dashboards
- Excel-style summaries
- cross-tab comparisons

---

# IMPORTANT REALITY 🔥

In real industry:

- GroupBy is MUCH more common
- Pivot tables are used mostly for reporting

This is because GroupBy is:
- simpler
- cleaner
- easier to program
- easier to chain with other operations

---

# FINAL GOLDEN MEMORY 🔥

# GroupBy

```text
Summarize data.
```

---

# Pivot Table

```text
Summarize AND rotate data into matrix form.
```

THAT is the real difference.

