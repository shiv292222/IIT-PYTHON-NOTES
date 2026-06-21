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

# 📊 EDA Golden Notes Part 2 (Bar Chart, Pie Chart, Bubble Chart, Heatmap)

---

# 1. BAR CHART

## Definition

A Bar Chart compares values across categories.

Think:

```text
Category + Number
```

Example:

| City     | Sales |
| -------- | ----- |
| Toronto  | 300   |
| Ottawa   | 400   |
| Montreal | 700   |

Question:

```text
Which city generated the highest sales?
```

Bar Chart is the answer.

---

## What Data Goes In?

### X-Axis

Usually categories:

```text
City
Department
Product
Country
```

### Y-Axis

Usually numbers:

```text
Sales
Revenue
Count
Salary
Profit
```

---

## Most Common Workflow

Raw Data:

| city    | sales |
| ------- | ----- |
| Toronto | 100   |
| Toronto | 200   |
| Ottawa  | 150   |
| Ottawa  | 250   |

---

### Step 1: Aggregate

```python
sales_per_city = (
    df.groupby("city")["sales"]
      .sum()
      .reset_index()
)
```

Output:

| city    | sales |
| ------- | ----- |
| Ottawa  | 400   |
| Toronto | 300   |

---

### Step 2: Plot

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(8,5))

plt.bar(
    sales_per_city["city"],
    sales_per_city["sales"]
)

plt.title("Sales By City")
plt.xlabel("City")
plt.ylabel("Sales")

plt.show()
```

---

# IMPORTANT BUSINESS THINKING

Always ask:

```text
What question is the business asking?
```

---

### Question

```text
Which city generated most sales?
```

Use:

```python
.sum()
```

---

### Question

```text
Which city has highest average transaction?
```

Use:

```python
.mean()
```

---

### Question

```text
How many transactions happened?
```

Use:

```python
.count()
```

---

# Sorting Before Plotting

Bad:

```text
Toronto   300
Ottawa    400
Montreal  700
```

Better:

```python
sales_per_city = (
    sales_per_city
    .sort_values(
        "sales",
        ascending=False
    )
)
```

Result:

```text
Montreal 700
Ottawa   400
Toronto  300
```

Much easier to understand.

---

# Horizontal Bar Chart

When category names are long:

```python
plt.barh(
    sales_per_city["city"],
    sales_per_city["sales"]
)
```

Remember:

```text
bar()
=
Vertical

barh()
=
Horizontal
```

---

# Value Labels

Shows values on bars.

Example:

```python
bars = plt.bar(
    sales_per_city["city"],
    sales_per_city["sales"]
)

for bar in bars:

    plt.text(
        bar.get_x() + bar.get_width()/2,
        bar.get_height(),
        str(bar.get_height()),
        ha="center"
    )

plt.show()
```

---

## Understanding plt.text()

Syntax:

```python
plt.text(
    x_position,
    y_position,
    text_to_write,
    formatting
)
```

Example:

```python
plt.text(
    2,
    100,
    "Toronto"
)
```

Means:

```text
Go to coordinate (2,100)

Write:
Toronto
```

---

# Bar Chart Summary

Use when:

```text
Comparing categories.
```

Examples:

```text
Sales by City

Revenue by Product

Employees by Department

Profit by Country
```

---

# 2. PIE CHART

## Definition

A Pie Chart shows how a whole is divided into parts.

Think:

```text
Part of Total
```

---

Example

| Department | Employees |
| ---------- | --------- |
| IT         | 40        |
| HR         | 20        |
| Finance    | 40        |

Total:

```text
100 Employees
```

Question:

```text
What percentage belongs
to each department?
```

---

## Pie Chart Code

```python
import matplotlib.pyplot as plt

plt.figure(figsize=(6,6))

plt.pie(
    [40,20,40],
    labels=["IT","HR","Finance"],
    autopct="%1.1f%%"
)

plt.title("Employee Share")

plt.show()
```

---

## Understanding Each Part

### Slice Size

```python
[40,20,40]
```

Means:

```text
IT = 40

HR = 20

Finance = 40
```

---

### Labels

```python
labels=["IT","HR","Finance"]
```

Names of slices.

---

### autopct

```python
autopct="%1.1f%%"
```

Shows:

```text
40.0%
20.0%
40.0%
```

inside pie slices.

---

# When To Use Pie Chart?

Question:

```text
What percentage of the total
belongs to each category?
```

Examples:

```text
Market Share

Department Share

Budget Allocation

Sales Contribution
```

---

# Bar Chart vs Pie Chart

Bar Chart:

```text
Compare values
```

Pie Chart:

```text
Show percentage of total
```

---

# Reality

Most analysts prefer:

```text
Bar Chart > Pie Chart
```

Because humans compare heights better than slices.

---

# 3. BUBBLE CHART

## Definition

Bubble Chart = Scatter Plot + One More Variable

Think:

```text
X
Y
Size
```

---

Scatter Plot:

```text
Experience
Salary
```

Bubble Chart:

```text
Experience
Salary
Age
```

---

Example Dataset

| Experience | Salary | Age |
| ---------- | ------ | --- |
| 2          | 50000  | 22  |
| 5          | 70000  | 35  |
| 10         | 120000 | 55  |

---

Question

```text
Show relationship between
Experience and Salary

AND ALSO

show Age
```

---

# Bubble Chart Logic

```text
X = Experience

Y = Salary

Bubble Size = Age
```

---

## Code

```python
plt.scatter(
    df["experience"],
    df["salary"],
    s=df["age"] * 20
)

plt.show()
```

---

# Understanding s=

```python
s=
```

means:

```text
Size of bubble
```

---

Example:

```python
age = 22
```

Bubble size:

```python
22 * 20
=
440
```

---

Question:

```text
Why multiply by 20?
```

Answer:

Because age itself creates tiny bubbles.

Scaling makes size differences visible.

---

Important:

```python
s=df["age"] * 20
```

DOES NOT change age.

It only changes visual size.

---

# When To Use Bubble Chart?

Question:

```text
Can I show a third variable
inside a scatter plot?
```

Answer:

```text
Bubble Chart
```

---

# Reality

Rarely used.

Good to know.

Not as important as:

```text
Scatter
Bar
Heatmap
```

---

# 4. HEATMAP

## Definition

A Heatmap is a visual representation of a correlation matrix.

Think:

```text
Relationship between
ALL numerical columns
```

---

# Before Heatmap

Suppose:

| Age | Salary | Experience |
| --- | ------ | ---------- |
| 22  | 45000  | 1          |
| 25  | 50000  | 2          |
| 30  | 65000  | 5          |

Question:

```text
Which columns are related?
```

---

# Correlation

Correlation measures relationship strength.

---

### Positive Correlation

```text
Age ↑

Salary ↑
```

Result:

```text
+1
```

---

### Negative Correlation

```text
Age ↑

Work Hours ↓
```

Result:

```text
-1
```

---

### No Correlation

```text
Random Pattern
```

Result:

```text
0
```

---

# Correlation Scale

```text
+1
=
Perfect Positive

0
=
No Relationship

-1
=
Perfect Negative
```

---

# Correlation Matrix

```python
corr_matrix = df.corr()
```

Think:

```text
Age vs Salary

Age vs Experience

Salary vs Experience

...
```

all at once.

---

# What Is Happening Behind The Scenes?

Pandas asks:

```text
As Age increases,

does Salary increase?
```

If yes:

```text
High Positive Correlation
```

---

Then asks:

```text
As Experience increases,

does Salary increase?
```

And keeps repeating for every column pair.

---

Result:

```python
corr_matrix
```

---

# Heatmap Code

```python
import seaborn as sns
import matplotlib.pyplot as plt

numeric_df = df.select_dtypes(
    include="number"
)

corr_matrix = numeric_df.corr()

plt.figure(figsize=(10,6))

sns.heatmap(
    corr_matrix,
    annot=True,
    fmt=".2f",
    cmap="coolwarm",
    linewidths=0.5,
    vmin=-1,
    vmax=1,
    center=0
)

plt.title(
    "Correlation Heatmap"
)

plt.show()
```

---

# Understanding Important Parameters

### annot=True

Show numbers inside boxes.

Example:

```text
0.95
0.82
-0.70
```

---

### fmt=".2f"

Show:

```text
0.95
```

instead of:

```text
0.954321987
```

---

### cmap="coolwarm"

Color theme.

---

### vmin=-1

Minimum correlation.

---

### vmax=1

Maximum correlation.

---

### center=0

Zero becomes neutral color.

---

# Heatmap Purpose

Question:

```text
Which numerical columns
are related?
```

Answer:

```text
Heatmap
```

---

# Scatter vs Heatmap

Scatter:

```text
Relationship between
TWO columns
```

Example:

```text
Experience vs Salary
```

---

Heatmap:

```text
Relationship between
ALL numerical columns
```

Example:

```text
Age vs Salary

Age vs Experience

Salary vs Bonus

Bonus vs Performance

...
```

all together.

---

# FINAL GOLDEN TABLE

| Chart        | Input                      | Main Purpose       |
| ------------ | -------------------------- | ------------------ |
| Histogram    | 1 Numerical Column         | Distribution       |
| Box Plot     | 1 Numerical Column         | Outliers & Summary |
| Scatter Plot | 2 Numerical Columns        | Relationship       |
| Line Chart   | Time + Number              | Trend              |
| Bar Chart    | Category + Number          | Comparison         |
| Pie Chart    | Categories as % of Total   | Composition        |
| Bubble Chart | X + Y + Size               | Show 3rd Variable  |
| Heatmap      | Multiple Numerical Columns | Correlation        |
|              |                            |                    |

---

# Interview One-Liners

Histogram

```text
Shows distribution of a numerical variable.
```

Box Plot

```text
Shows spread, median and outliers.
```

Scatter Plot

```text
Shows relationship between two numerical variables.
```

Line Chart

```text
Shows trends over time.
```

Bar Chart

```text
Compares values across categories.
```

Pie Chart

```text
Shows parts of a whole.
```

Bubble Chart

```text
Scatter Plot with a third variable represented by size.
```

Heatmap

```text
Visualizes correlation between numerical variables.
```

