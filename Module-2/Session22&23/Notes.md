# 📊 EDA & Matplotlib Diamond Notes

> These notes are written for complete beginners and cover:
>
> * What is EDA?
> * Why Visualization?
> * Histogram
> * Box Plot
> * Scatter Plot
> * Line Chart
> * Common Interview Questions
> * Common Confusions
> * Real Analyst Thinking

---

# 1. What is EDA?

EDA = Exploratory Data Analysis

EDA means:

```text
Understand the data
before making decisions.
```

Think:

```text
Raw Data
    ↓
Cleaning
    ↓
EDA
    ↓
Insights
    ↓
Machine Learning / Reporting
```

---

# Why Do We Need EDA?

Suppose someone gives you:

```text
100,000 rows
20 columns
```

You cannot understand this by looking at numbers.

EDA helps us answer:

* What patterns exist?
* Any missing values?
* Any outliers?
* Any relationships?
* Any trends?

---

# Types of EDA

## Univariate Analysis

Study of ONE variable.

Example:

```python
df["salary"]
```

Questions:

```text
How are salaries distributed?
Any outliers?
```

Charts:

* Histogram
* Box Plot

---

## Bivariate Analysis

Study of TWO variables.

Example:

```python
experience
salary
```

Question:

```text
Does experience affect salary?
```

Charts:

* Scatter Plot
* Line Chart

---

## Multivariate Analysis

Study of 3+ variables.

Example:

```text
salary
experience
age
department
```

Charts:

* Heatmap
* Bubble Chart

---

# Matplotlib

Main Python visualization library.

Import:

```python
import matplotlib.pyplot as plt
```

Think:

```text
plt = drawing tool
```

---

# Common Chart Structure

Most charts follow:

```python
plt.figure(figsize=(8,5))

plt.some_chart(...)

plt.title("Title")
plt.xlabel("X Axis")
plt.ylabel("Y Axis")

plt.show()
```

---

# HISTOGRAM

## Purpose

Shows:

```text
Distribution
Frequency
Spread
```

---

## Example Dataset

```python
salary = [
    45000,
    50000,
    52000,
    55000,
    60000,
    62000,
    65000,
    70000,
    72000,
    150000
]
```

---

## Code

```python
plt.hist(salary)

plt.title("Salary Distribution")

plt.xlabel("Salary")
plt.ylabel("Frequency")

plt.show()
```

---

## What Does Histogram Show?

It groups data into buckets.

Example:

```text
45000-60000 → 4 employees

60000-75000 → 5 employees

75000+ → 1 employee
```

---

## What are Bins?

```python
plt.hist(salary, bins=5)
```

Means:

```text
Create 5 buckets
```

Not:

```text
Show 5 salaries
```

---

## Interview Question

Histogram vs Bar Chart?

Histogram:

```text
Numerical Data
Continuous Data
Frequency
```

Bar Chart:

```text
Categorical Data
Comparison
```

---

# BOX PLOT

## Purpose

Shows:

```text
Median
Q1
Q3
IQR
Outliers
```

---

## Code

```python
plt.boxplot(salary)

plt.show()
```

---

## Outliers

Small circles:

```text
○
```

usually indicate potential outliers.

Example:

```python
salary = [
45,
46,
47,
48,
49,
50,
500
]
```

Box Plot highlights:

```text
500
```

as unusual.

---

## Why Use Box Plot?

Question:

```text
Any abnormal values?
```

Answer:

```text
Box Plot
```

---

# SCATTER PLOT

## Purpose

Shows:

```text
Relationship between
two numerical variables
```

---

## Example Dataset

```python
df = pd.DataFrame({
    "experience":[1,2,3,4,5],
    "salary":[45000,50000,55000,60000,65000]
})
```

---

## Code

```python
plt.scatter(
    df["experience"],
    df["salary"]
)

plt.show()
```

---

## MOST IMPORTANT RULE

Each row becomes ONE DOT.

Example:

```text
experience salary

1          45000
```

becomes:

```text
(1,45000)
```

---

## What are Coordinates?

A scatter plot uses:

```text
(x,y)
```

Example:

```text
(1,45000)

(2,50000)

(3,55000)
```

---

## Why Order Does NOT Matter?

Dataset:

```python
experience = [4,1,5,2,3]
salary = [60000,45000,65000,50000,55000]
```

Scatter Plot creates:

```text
(4,60000)

(1,45000)

(5,65000)

(2,50000)

(3,55000)
```

Dots are placed according to coordinates.

Scatter Plot does NOT connect dots.

Therefore:

```text
Row order does not matter.
```

---

## Analyst Question

```text
As experience increases,
does salary increase?
```

Scatter Plot answers this.

---

# LINE CHART

## Purpose

Shows:

```text
Trend
Change over time
```

---

## Example Dataset

```python
df = pd.DataFrame({
    "month":[
        "Jan",
        "Feb",
        "Mar",
        "Apr"
    ],

    "sales":[
        10000,
        12000,
        15000,
        18000
    ]
})
```

---

## Code

```python
plt.plot(
    df["month"],
    df["sales"]
)

plt.show()
```

---

## Why Order Matters?

Line chart:

```text
Connects points
```

Example:

```text
Jan → Feb → Mar → Apr
```

If order becomes:

```text
Mar → Jan → Apr → Feb
```

The chart becomes misleading.

---

## Scatter vs Line

| Scatter Plot         | Line Chart      |
| -------------------- | --------------- |
| Relationship         | Trend           |
| Dots only            | Dots + lines    |
| Order not important  | Order important |
| Experience vs Salary | Month vs Sales  |

---

# LABELS AND LEGENDS

## Label

Example:

```python
plt.plot(
    df["month"],
    df["sales"],
    label="Sales"
)
```

Means:

```text
Give this line a name:
Sales
```

---

## Legend

```python
plt.legend()
```

Means:

```text
Display line names
on chart
```

Example:

```text
Sales
Profit
Revenue
```

shown in a small box.

---

## Multiple Lines Example

```python
plt.plot(
    df["month"],
    df["sales"],
    label="Sales"
)

plt.plot(
    df["month"],
    df["profit"],
    label="Profit"
)

plt.legend()

plt.show()
```

---

# MONTH SORTING PROBLEM

After:

```python
monthly_sales = (
    df.groupby("month")["sales"]
      .sum()
      .reset_index()
)
```

Output might become:

```text
Feb
Jan
Mar
```

---

## Why?

Because months are strings.

Pandas sorts alphabetically.

---

## Fix

```python
month_order = [
    "Jan","Feb","Mar",
    "Apr","May","Jun",
    "Jul","Aug","Sep",
    "Oct","Nov","Dec"
]
```

---

## Step 1

```python
monthly_sales["month"] = pd.Categorical(
    monthly_sales["month"],
    categories=month_order,
    ordered=True
)
```

Meaning:

```text
Teach Pandas
the correct month order.
```

---

## Step 2

```python
monthly_sales = (
    monthly_sales
    .sort_values("month")
)
```

Meaning:

```text
Now apply that order.
```

---

## Easy Memory Trick

```python
pd.Categorical(...)
```

means:

```text
Define rules
```

```python
sort_values(...)
```

means:

```text
Apply rules
```

---

# ANALYST MINDSET

Wrong:

```text
Which chart should I use?
```

Correct:

```text
What question
am I trying to answer?
```

Then choose chart.

---

# Chart Selection Cheat Sheet

| Question           | Chart        |
| ------------------ | ------------ |
| Distribution       | Histogram    |
| Outliers           | Box Plot     |
| Relationship       | Scatter Plot |
| Trend Over Time    | Line Chart   |
| Compare Categories | Bar Chart    |

---

# Golden Interview Questions

## Q1

When do you use a Histogram?

Answer:

```text
To understand distribution and frequency of numerical data.
```

---

## Q2

When do you use a Scatter Plot?

Answer:

```text
To analyze relationship between two numerical variables.
```

---

## Q3

Why does order matter in Line Chart?

Answer:

```text
Because points are connected in sequence.
```

---

## Q4

Why does order not matter in Scatter Plot?

Answer:

```text
Because dots are placed only by coordinates and are not connected.
```

---

# Final Summary

Remember:

```text
Histogram
=
Distribution

Box Plot
=
Outliers

Scatter Plot
=
Relationship

Line Chart
=
Trend
```

If you understand those four sentences, you understand the foundation of EDA.
