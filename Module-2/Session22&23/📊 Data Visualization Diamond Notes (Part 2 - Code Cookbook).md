# 📊 Data Visualization Diamond Notes (Part 2 - Code Cookbook)

# 🚀 Standard Imports

Use this in almost every notebook.

```python
import pandas as pd
import numpy as np

import matplotlib.pyplot as plt
import seaborn as sns
```

---

# 🎨 Professional Visualization Template

Use this before most charts.

```python
plt.figure(figsize=(8,5))

sns.set_style("whitegrid")

# chart here

plt.title("Meaningful Title")
plt.xlabel("X Label")
plt.ylabel("Y Label")

plt.show()
```

---

# 📋 Universal Practice Dataset

Use this dataset for almost every chart.

```python
df = pd.DataFrame({
    "employee": [
        "A","B","C","D","E",
        "F","G","H","I","J"
    ],

    "department": [
        "IT","IT","HR","HR","Finance",
        "Finance","IT","HR","Finance","IT"
    ],

    "city": [
        "Toronto","Toronto","Ottawa","Ottawa","Toronto",
        "Ottawa","Toronto","Ottawa","Toronto","Ottawa"
    ],

    "salary": [
        50000,70000,60000,80000,120000,
        95000,85000,75000,110000,90000
    ],

    "experience": [
        1,3,2,5,10,
        8,6,4,9,7
    ],

    "age": [
        22,25,24,30,40,
        35,32,28,38,34
    ]
})
```

---

# 📈 Histogram

## Purpose

Distribution of one numerical column.

```python
plt.figure(figsize=(8,5))

sns.histplot(
    data=df,
    x="salary",
    bins=5,
    kde=True
)

plt.title("Salary Distribution")
plt.show()
```

---

## Important Parameters

```python
bins=10
```

Number of bars.

---

```python
kde=True
```

Adds smooth curve.

---

# 📦 Box Plot

## Purpose

Find outliers and spread.

```python
plt.figure(figsize=(8,5))

sns.boxplot(
    data=df,
    y="salary"
)

plt.title("Salary Box Plot")

plt.show()
```

---

## Compare Categories

```python
sns.boxplot(
    data=df,
    x="department",
    y="salary"
)
```

---

# 🎻 Violin Plot

## Purpose

Distribution Shape + Box Plot

```python
plt.figure(figsize=(8,5))

sns.violinplot(
    data=df,
    x="department",
    y="salary",
    palette="Set2",
    inner="box",
    cut=0
)

plt.title("Salary Distribution by Department")

plt.show()
```

---

## Important Parameters

```python
palette="Set2"
```

Color theme.

---

```python
inner="box"
```

Adds mini boxplot.

---

```python
inner="quartile"
```

Shows quartile lines.

---

```python
cut=0
```

Prevents violin extending beyond data.

---

# 🎯 Scatter Plot

## Purpose

Relationship between 2 numerical columns.

```python
plt.figure(figsize=(8,5))

sns.scatterplot(
    data=df,
    x="experience",
    y="salary"
)

plt.title("Experience vs Salary")

plt.show()
```

---

## With Groups (Most Useful)

```python
sns.scatterplot(
    data=df,
    x="experience",
    y="salary",
    hue="department"
)
```

---

# 🫧 Bubble Chart

## Purpose

Show 3 numerical variables.

```python
plt.figure(figsize=(8,5))

sns.scatterplot(
    data=df,
    x="experience",
    y="salary",
    size="age",
    hue="department"
)

plt.title("Bubble Chart")

plt.show()
```

---

## Important Parameters

```python
size="age"
```

Bubble size.

---

```python
hue="department"
```

Group colors.

---

# 📊 Bar Plot

## Purpose

Compare categories.

```python
plt.figure(figsize=(8,5))

sns.barplot(
    data=df,
    x="department",
    y="salary"
)

plt.title("Average Salary by Department")

plt.show()
```

---

## Hidden Magic

Internally similar to:

```python
df.groupby(
    "department"
)["salary"].mean()
```

---

# Bar Plot With Hue

```python
sns.barplot(
    data=df,
    x="department",
    y="salary",
    hue="city"
)
```

---

# Bar Plot With Max Salary

```python
sns.barplot(
    data=df,
    x="department",
    y="salary",
    hue="city",
    estimator=np.max
)
```

---

## Important Parameters

```python
estimator=np.mean
```

Average.

---

```python
estimator=np.max
```

Maximum.

---

```python
estimator=np.min
```

Minimum.

---

```python
estimator=np.median
```

Median.

---

# 🔢 Count Plot

## Purpose

Category Frequency

```python
plt.figure(figsize=(8,5))

sns.countplot(
    data=df,
    x="department"
)

plt.title("Department Count")

plt.show()
```

---

## With Hue

```python
sns.countplot(
    data=df,
    x="department",
    hue="city"
)
```

---

# 📉 Line Plot

## Purpose

Trend Over Time

```python
sales = pd.DataFrame({
    "month": [
        "Jan","Feb","Mar",
        "Apr","May","Jun"
    ],

    "sales": [
        100,120,140,
        180,160,210
    ]
})
```

```python
sns.lineplot(
    data=sales,
    x="month",
    y="sales",
    marker="o"
)

plt.title("Monthly Sales Trend")

plt.show()
```

---

## Important Parameters

```python
marker="o"
```

Show points.

---

```python
linewidth=3
```

Thicker line.

---

# 🔥 Heatmap

## Purpose

Correlation Matrix

```python
corr_matrix = df[
    ["salary","experience","age"]
].corr()
```

```python
plt.figure(figsize=(8,5))

sns.heatmap(
    corr_matrix,
    annot=True,
    cmap="coolwarm"
)

plt.title("Correlation Heatmap")

plt.show()
```

---

## Important Parameters

```python
annot=True
```

Show values.

---

```python
cmap="coolwarm"
```

Color theme.

---

# 🎨 Most Useful Seaborn Parameters

---

# hue

```python
hue="department"
```

Purpose:

```text
Split data into groups.
```

---

# size

```python
size="age"
```

Purpose:

```text
Add another numerical variable.
```

---

# estimator

```python
estimator=np.mean
```

Purpose:

```text
How categories should be summarized.
```

---

# palette

```python
palette="Set2"
```

Purpose:

```text
Chart color theme.
```

Recommended:

```python
Set2
deep
pastel
viridis
```

---

# legend

Move legend outside chart.

```python
plt.legend(
    bbox_to_anchor=(1.05,1),
    loc="upper left"
)
```

---

# 🏗️ Subplots

## Purpose

Multiple charts together.

```python
fig, axes = plt.subplots(
    2,
    2,
    figsize=(10,8)
)
```

---

## Example

```python
fig, axes = plt.subplots(
    2,
    2,
    figsize=(10,8)
)

sns.histplot(
    data=df,
    x="salary",
    ax=axes[0,0]
)

sns.boxplot(
    data=df,
    y="salary",
    ax=axes[0,1]
)

sns.scatterplot(
    data=df,
    x="experience",
    y="salary",
    ax=axes[1,0]
)

sns.countplot(
    data=df,
    x="department",
    ax=axes[1,1]
)

plt.tight_layout()

plt.show()
```

---

## Important Concepts

### fig

```text
Entire dashboard.
```

---

### axes

```text
Individual chart location.
```

---

### axes[0,0]

```text
Top Left
```

---

### axes[0,1]

```text
Top Right
```

---

### axes[1,0]

```text
Bottom Left
```

---

### axes[1,1]

```text
Bottom Right
```

---

### tight_layout()

```python
plt.tight_layout()
```

Fixes overlapping.

---

# 💎 Most Used Charts In Industry

Ranked by frequency:

### Tier 1

```text
Histogram
Box Plot
Scatter Plot
Bar Plot
Line Plot
Heatmap
```

---

### Tier 2

```text
Count Plot
Subplots
```

---

### Tier 3

```text
Violin Plot
Bubble Chart
```

---

# 🏆 My Default Workflow

```python
1. df.head()

2. df.info()

3. Histogram

4. Box Plot

5. Count Plot

6. Scatter Plot

7. Heatmap

8. Subplots Dashboard
```

If you master those steps, you'll handle most EDA tasks comfortably.
