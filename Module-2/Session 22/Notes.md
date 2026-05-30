# Data Cleaning Master Notes (Golden Notes)

# The Biggest Lesson of This Entire Topic

Most beginners think:

```python
Machine Learning = Model Building
```

Reality:

```python
Machine Learning = Data Cleaning + Data Understanding
```

A senior data scientist spends far more time cleaning data than training models.

Why?

Because:

```text
Garbage In = Garbage Out
```

If your data is bad:

* Analysis will be wrong
* Dashboard will be wrong
* Machine Learning model will be wrong
* AI predictions will be wrong

Before touching any model, ask:

1. Is data missing?
2. Is data duplicated?
3. Are there impossible values?
4. Are there extreme values?
5. Does the data make business sense?

---

# Step 1: Missing Values (NaN)

Example:

```python
import numpy as np

age = [20, 30, np.nan, 40]
```

NaN means:

```text
Value is unknown
```

NOT:

```text
0
```

NOT:

```text
False
```

NOT:

```text
Empty
```

Just unknown.

---

# Why Missing Values Are Dangerous

Dataset:

```text
20
30
40
NaN
```

Question:

Can we calculate accurate statistics?

Not really.

Missing values reduce data quality.

---

# Count Missing Values

```python
df.isna().sum()
```

Example:

```python
name      1
salary    2
city      1
```

Meaning:

```text
name column has 1 missing value
salary column has 2 missing values
city column has 1 missing value
```

---

# Percentage Missing Values

```python
df.isna().mean() * 100
```

Example:

```python
salary    25
```

Meaning:

```text
25% values are missing
```

Very common interview question.

---

# Drop Missing Values

```python
df.dropna()
```

Example:

Before:

```text
20
30
NaN
40
```

After:

```text
20
30
40
```

Problem:

You lose information.

Use only when missing values are very small.

Example:

```text
10 missing rows
out of
1,000,000 rows
```

Then dropping is okay.

---

# Filling Missing Values

This is called Imputation.

---

# Numerical Columns

Examples:

```text
Age
Salary
Amount
Weight
Price
```

---

# Mean Imputation

```python
df["salary"] = df["salary"].fillna(
    df["salary"].mean()
)
```

Use when:

```text
No extreme values exist
```

Example:

```text
20
30
40
NaN
```

Mean:

```text
30
```

Fill:

```text
20
30
40
30
```

Distribution remains similar.

---

# Median Imputation

```python
df["salary"] = df["salary"].fillna(
    df["salary"].median()
)
```

Use when:

```text
Outliers exist
```

Example:

```text
100
200
300000
NaN
```

Mean:

```text
100100
```

Bad choice.

Median:

```text
200
```

Much better.

---

# Golden Rule

```text
No Outlier → Mean

Outlier Present → Median
```

---

# Categorical Columns

Examples:

```text
City
Department
Country
Name
Gender
```

---

# Why Mean Cannot Work

Can we do:

```python
(Toronto + Ottawa) / 2
```

No.

Categorical data has no mathematical meaning.

---

# Mode

Mode means:

```text
Most Frequent Value
```

Example:

```text
Toronto
Toronto
Ottawa
NaN
```

Mode:

```text
Toronto
```

---

# Syntax

```python
df["city"].mode()
```

Output:

```python
0    Toronto
dtype: object
```

Notice:

It returns a Series.

Not a string.

Therefore:

```python
df["city"].mode()[0]
```

returns:

```python
Toronto
```

---

# Why [0] ?

Because mode() returns a Series.

Example:

```python
0    Toronto
```

Index:

```python
0
```

Value:

```python
Toronto
```

So:

```python
mode()[0]
```

means:

```text
Give me first mode value
```

---

# Important Real World Insight

Mode is NOT always correct.

Example:

```text
Name
-----
John
Alice
NaN
```

Should we fill:

```text
John
```

No.

Better:

```python
fillna("Unknown")
```

---

# Unknown Category

Very common in industry.

```python
df["name"] = df["name"].fillna(
    "Unknown"
)
```

Use when:

```text
We genuinely do not know the value
```

---

# Duplicates

Example:

```text
Customer_ID
------------
100
100
100
101
```

Question:

How many customers?

Wrong:

```text
4
```

Correct:

```text
2
```

---

# Detect Duplicates

```python
df.duplicated()
```

Output:

```python
False
True
True
False
```

---

# Remove Duplicates

```python
df.drop_duplicates()
```

---

# Remove Duplicates and Reset Index

```python
df.drop_duplicates(
    ignore_index=True
)
```

---

# Outliers

Definition:

```text
Extreme Observations
```

Example:

```text
100
120
130
140
50000
```

50000 looks suspicious.

---

# Important Insight

Outlier ≠ Wrong

Example:

Age:

```text
20
21
22
90
```

90 is not wrong.

Depends on context.

Always think:

```text
Why is it extreme?
```

before removing it.

---

# Understanding Quartiles

Sorted Data:

```text
10
20
30
40
50
60
70
80
90
100
```

---

# Q1

25% position.

Approximately:

```text
30
```

---

# Q2

Median.

Approximately:

```text
50
```

---

# Q3

75% position.

Approximately:

```text
80
```

---

# What is IQR?

Formula:

IQR = Q3 - Q1

Example:

```text
Q1 = 30
Q3 = 80
```

Then:

```text
IQR = 50
```

Meaning:

```text
Middle 50% of data spans 50 units
```

Think:

```text
How wide is the normal middle region?
```

That is IQR.

---

# Why Not Use Max - Min?

Example:

```text
10
20
30
40
50
1000000
```

Max-Min becomes huge.

One extreme value destroys it.

IQR ignores extremes.

Therefore IQR is more robust.

---

# Lower Bound Formula

Formula:

Q1 - 1.5 × IQR

Purpose:

```text
Detect unusually small values
```

---

# Upper Bound Formula

Formula:

Q3 + 1.5 × IQR

Purpose:

```text
Detect unusually large values
```

---

# Do I Need To Memorize These?

Yes.

You should understand:

```text
Q1 and Q3 define normal region
```

Then memorize:

```text
Lower = Q1 - 1.5 × IQR
Upper = Q3 + 1.5 × IQR
```

This is a standard statistical rule.

---

# Calculate IQR In Pandas

```python
Q1 = df["amount"].quantile(0.25)

Q3 = df["amount"].quantile(0.75)

IQR = Q3 - Q1
```

---

# Calculate Bounds

```python
lower = Q1 - 1.5 * IQR

upper = Q3 + 1.5 * IQR
```

---

# Remove Outliers

```python
df = df[
    (df["amount"] >= lower)
    &
    (df["amount"] <= upper)
]
```

---

# Capping

Most Important Concept

Instead of removing:

```text
50000
```

Replace it with:

```text
Upper Bound
```

Why?

Because:

```text
Row survives
Information survives
Only extreme effect is reduced
```

---

# Capping Syntax

```python
import numpy as np

df["amount"] = np.clip(
    df["amount"],
    lower,
    upper
)
```

Meaning:

```text
Anything below lower
→ lower

Anything above upper
→ upper
```

---

# Binary Column Logic

Professor's Advanced Question

Example:

```text
is_fraud

1
0
1
0
NaN
```

This column only contains:

```text
0 and 1
```

---

# Why Check Binary Columns?

Because median can create nonsense.

Example:

```text
0
1
0
1
```

Median can become:

```text
0.5
```

But:

```text
is_fraud = 0.5
```

makes no sense.

Fraud is:

```text
0 or 1
```

Only.

---

# Understanding This Code

```python
unique_vals = (
    df[col]
    .dropna()
    .unique()
)
```

Suppose:

```text
1
0
1
NaN
0
```

After dropna():

```text
1
0
1
0
```

After unique():

```python
[1, 0]
```

Meaning:

```text
Distinct values only
```

---

# Understanding issubset()

```python
set(unique_vals).issubset({0,1})
```

Question:

```text
Do all values belong to {0,1} ?
```

Example:

```python
{0,1}
```

Answer:

```python
True
```

Example:

```python
{0,1,2}
```

Answer:

```python
False
```

---

# Complete Logic

```text
For each column

Is it numeric?
    Yes
        Is it binary?
            Yes → Skip
            No → Fill Median

Is it categorical?
    Yes → Fill Mode
```

This is exactly what the professor's automation question was testing.

---

# Golden Interview Questions

Q1. When should Mean be used?

Answer:

```text
When data has no major outliers.
```

---

Q2. When should Median be used?

Answer:

```text
When data contains extreme values.
```

---

Q3. Why use Mode?

Answer:

```text
Most frequent categorical value.
```

---

Q4. Why use Unknown?

Answer:

```text
When guessing is unsafe.
```

---

Q5. Why is IQR preferred over Max-Min?

Answer:

```text
IQR ignores extreme observations.
```

---

Q6. Why not always remove outliers?

Answer:

```text
Outliers may contain useful information
(Fraud, VIP customer, rare events)
```

---

# Final Senior-Level Workflow

Whenever you receive a dataset:

```python
df.info()

df.describe()

df.isna().sum()

df.duplicated().sum()
```

Then ask:

1. Missing Values?
2. Duplicates?
3. Outliers?
4. Wrong Data Types?
5. Business Logic Violations?

Only after this:

```text
Analysis
↓
Visualization
↓
Machine Learning
↓
AI Models
```

This is how real Data Analysts and Data Scientists think.
