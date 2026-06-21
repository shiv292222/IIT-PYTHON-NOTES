# 📊 Data Visualization Diamond Notes (Part 1 - Concepts & Thinking)

---

# 🎯 Golden Rule of Visualization

Most beginners think:

```text
Which chart should I use?
```

Professionals think:

```text
What question am I trying to answer?
```

The chart is just the tool.

Always start with the question.

---

# 🧠 Visualization Decision Tree

### One Numerical Column

Questions:

```text
How is data distributed?
Are there outliers?
```

Use:

* Histogram
* Box Plot

---

### Two Numerical Columns

Questions:

```text
Is there a relationship?
Do both variables move together?
```

Use:

* Scatter Plot
* Bubble Chart

---

### Category + Numerical

Questions:

```text
Which category performs better?
How do categories compare?
```

Use:

* Bar Plot
* Box Plot
* Violin Plot

---

### Category Only

Questions:

```text
How many records belong to each category?
```

Use:

* Count Plot

---

### Many Numerical Columns

Questions:

```text
Which variables are related?
```

Use:

* Heatmap

---

# 📈 Histogram

## Purpose

Shows how values are distributed.

---

## Answers Questions Like

```text
Are salaries concentrated?
Are marks normally distributed?
Where do most observations lie?
```

---

## Think Of It As

```text
Frequency Counter
```

---

## What It Shows

```text
How many values fall inside each range
```

Example:

```text
Salary Range     Employees

0-20k            ██

20-40k           ███████

40-60k           ███████████

60-80k           ████
```

---

## Use When

You have:

```text
One Numerical Column
```

Examples:

* Salary
* Age
* Marks
* Revenue

---

## Avoid When

Comparing categories.

---

# 📦 Box Plot

## Purpose

Shows summary statistics and outliers.

---

## Think Of It As

```text
Data Health Report
```

---

## Shows

* Minimum
* Q1
* Median
* Q3
* Maximum
* Outliers

---

## Answers Questions Like

```text
Are there unusual values?
Is salary data spread out?
```

---

## Best Use Case

Outlier detection.

---

## Real World

Usually the first chart analysts create.

---

# 🎻 Violin Plot

## Purpose

Shows summary + distribution shape.

---

## Problem It Solves

Box Plot shows:

```text
Min
Q1
Median
Q3
Max
```

But hides:

```text
Where most observations exist
```

---

## Think Of It As

```text
Box Plot +
Distribution
```

---

## Important Idea

### Wide Section

```text
Many observations exist here
```

---

### Thin Section

```text
Few observations exist here
```

---

## Use When

Comparing distributions across categories.

Example:

```text
Department vs Salary
```

---

## Real World

Useful.

But Box Plot is used more frequently.

---

# 🎯 Scatter Plot

## Purpose

Shows relationship between two numerical variables.

---

## Think Of It As

```text
Relationship Detector
```

---

## Questions It Answers

```text
Does experience increase salary?

Does study time increase marks?

Does advertisement increase sales?
```

---

## Interpretation

### Upward Trend

```text
Positive Correlation
```

---

### Downward Trend

```text
Negative Correlation
```

---

### Random Points

```text
No Relationship
```

---

# 🫧 Bubble Chart

## Purpose

Shows three variables simultaneously.

---

## Think Of It As

```text
Scatter Plot +
One Extra Numerical Variable
```

---

## Example

```text
X = Experience
Y = Salary
Bubble Size = Age
```

---

## Use When

Need to show:

```text
3 Numerical Variables
```

in one graph.

---

# 📊 Bar Plot

## Purpose

Compare categories.

---

## Think Of It As

```text
Category Comparison Tool
```

---

## Questions It Answers

```text
Which department earns highest?

Which city has highest sales?
```

---

## Important Hidden Secret

Bar Plot performs aggregation.

Usually:

```python
mean()
```

internally.

---

## Mental Model

```python
groupby() + aggregation + chart
```

---

# 🔢 Count Plot

## Purpose

Count category frequencies.

---

## Think Of It As

```python
value_counts() + chart
```

---

## Questions It Answers

```text
How many employees belong to IT?

How many customers belong to each city?
```

---

## Difference From Bar Plot

### Bar Plot

Needs:

```text
Category + Numerical
```

Example:

```text
Department + Salary
```

---

### Count Plot

Needs:

```text
Category Only
```

Example:

```text
Department
```

---

# 📉 Line Plot

## Purpose

Show trends over time.

---

## Think Of It As

```text
Trend Detector
```

---

## Questions It Answers

```text
How is revenue changing?

How are sales changing monthly?
```

---

## Use When

Order matters.

Examples:

* Days
* Months
* Years
* Time

---

# 🔥 Heatmap

## Purpose

Show relationships between many numerical columns.

---

## Think Of It As

```text
Correlation Dashboard
```

---

## Questions It Answers

```text
Which variables move together?
```

---

## Common Usage

```python
df.corr()
```

followed by:

```python
sns.heatmap()
```

---

## Interpretation

### Near +1

Strong Positive Correlation

---

### Near -1

Strong Negative Correlation

---

### Near 0

Little Relationship

---

# 🎨 Seaborn Superpowers

These are more important than many chart types.

---

# hue

## Real Meaning

NOT:

```text
Add colors
```

Actual Meaning:

```text
Split data into groups
for comparison
```

---

Example:

```python
hue="city"
```

Now every city gets separate color.

---

# size

## Purpose

Add one extra numerical variable.

Example:

```python
size="age"
```

---

# estimator

## Purpose

Tells Seaborn how to aggregate data.

---

Examples

```python
np.mean
```

Average

---

```python
np.max
```

Maximum

---

```python
np.min
```

Minimum

---

```python
np.median
```

Median

---

# palette

## Purpose

Controls chart color theme.

Common Choices:

```python
Set2
deep
pastel
viridis
```

---

# legend

## Purpose

Explains colors used by hue.

Example:

```text
Blue = Toronto
Orange = Ottawa
```

---

# 🏗️ Subplots

## Purpose

Show multiple charts together.

---

## Think Of It As

```text
Mini Dashboard
```

---

Instead Of

```text
Chart 1
Chart 2
Chart 3
Chart 4
```

You Get

```text
+---------+---------+
| Chart 1 | Chart 2 |
+---------+---------+
| Chart 3 | Chart 4 |
+---------+---------+
```

---

## Most Important Concepts

### fig

Entire dashboard.

---

### axes

Individual chart locations.

---

### plt.tight_layout()

Prevents overlapping.

---

# 💎 Final Interview Cheat Sheet

| Question                 | Chart        |
| ------------------------ | ------------ |
| Distribution             | Histogram    |
| Outliers                 | Box Plot     |
| Distribution Shape       | Violin Plot  |
| Relationship             | Scatter Plot |
| 3 Variables              | Bubble Plot  |
| Category Comparison      | Bar Plot     |
| Category Frequency       | Count Plot   |
| Trend Over Time          | Line Plot    |
| Correlation Matrix       | Heatmap      |
| Multiple Charts Together | Subplots     |

---

# 🏆 Golden Rule To Remember Forever

Never start with:

```text
Which chart should I use?
```

Always start with:

```text
What question am I trying to answer?
```

The chart choice becomes obvious after that.
