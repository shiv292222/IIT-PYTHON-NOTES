# 🏆 GOLDEN PANDAS TRANSFORMATION NOTES

# 🚀 BIG PICTURE

Pandas is not just for viewing tables.

Real-world pandas is mainly used for:
- cleaning data
- transforming data
- reshaping data
- handling dates
- handling missing values
- preparing data for ML/analytics

The MOST IMPORTANT pandas mindset:

# 👉 Think in COLUMNS, not ROWS.

Beginners think:
```python
for row in dataframe
```

Professionals think:
```python
df["salary"] * 2
```

This is called:
# 👉 vectorized thinking

---

# 🔥 MASTER DATASET

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "customer_id": [101, 102, 103, 104, 105],
    "name": ["Aman", "Riya", "Kabir", "Neha", "Simran"],
    "city": ["Toronto", "Delhi", "Mumbai", "Toronto", "Delhi"],
    "amount": [500, 200, 700, 300, 150],
    "order_date": [
        "2024-01-10",
        "2024-02-15",
        "2024-03-20",
        "2024-01-25",
        "2024-02-05"
    ]
})

print(df)
```

---

# 1️⃣ APPLY FUNCTION

# ❓ PURPOSE

Used for:
- custom logic
- if/else logic
- business rules
- row-wise transformation

---

# ✅ EXAMPLE

```python
def categorize(x):

    if x > 300:
        return "High"

    else:
        return "Low"


df["category"] = df["amount"].apply(categorize)
```

---

# 🧠 INTERNAL THINKING

Pandas internally behaves LIKE:

```python
categorize(500)
categorize(200)
categorize(700)
```

for every row.

---

# ✅ OUTPUT

| amount | category |
|---|---|
| 500 | High |
| 200 | Low |
| 700 | High |

---

# 🔥 WHEN TO USE APPLY?

Use apply when:
- custom rules exist
- if/else logic needed
- calculations are complicated
- normal math is not enough

---

# ❌ WHEN NOT TO USE APPLY?

Bad:

```python
df["new_amount"] = df["amount"].apply(lambda x: x * 100)
```

Good:

```python
df["new_amount"] = df["amount"] * 100
```

Because pandas is vectorized.

---

# 2️⃣ LAMBDA FUNCTION

# ❓ WHAT IS LAMBDA?

Lambda is:
# 👉 quick anonymous function

Anonymous means:
# 👉 function without name

---

# ✅ NORMAL FUNCTION

```python
def multiply(x):
    return x * 100
```

---

# ✅ SAME LAMBDA VERSION

```python
lambda x: x * 100
```

---

# 🧠 BREAKDOWN

```python
lambda x: x * 100
```

| Part | Meaning |
|---|---|
| lambda | create quick function |
| x | input value |
| : | return this |
| x * 100 | logic |

---

# ✅ EXAMPLE

```python
df["name_length"] = df["name"].apply(lambda x: len(x))
```

---

# 3️⃣ MAP FUNCTION

# ❓ PURPOSE

Used for:
# 👉 one-to-one mapping

---

# ✅ EXAMPLE

```python
city_map = {
    "Toronto": "TOR",
    "Delhi": "DEL",
    "Mumbai": "MUM"
}


df["city_code"] = df["city"].map(city_map)
```

---

# 🧠 INTERNAL THINKING

```python
Toronto → TOR
Delhi → DEL
Mumbai → MUM
```

using dictionary lookup.

---

# ❌ IMPORTANT

If mapping missing:

```python
NaN
```

comes.

---

# ✅ EXAMPLE

```python
city_map = {
    "Delhi": "DEL"
}
```

Toronto becomes:

```python
NaN
```

because mapping missing.

---

# 🧠 MEMORY TRICK

## map
Strict teacher 😈

"Mapping nahi mila? NaN."

---

# 4️⃣ REPLACE FUNCTION

# ❓ PURPOSE

Replace values.

Looks similar to map.

---

# ✅ EXAMPLE

```python
df["city_replace"] = df["city"].replace(city_map)
```

---

# 🔥 DIFFERENCE BETWEEN MAP & REPLACE

| Function | Missing Mapping |
|---|---|
| map | NaN |
| replace | original value |

---

# 🧠 MEMORY TRICK

## replace
Friendly teacher 😎

"Mapping nahi mila? Original rehne do."

---

# 5️⃣ DATETIME CONVERSION

# ❓ WHY IMPORTANT?

Dates are EXTREMELY important in:
- logs
- monitoring
- dashboards
- ML
- analytics
- business reporting

---

# ❓ PROBLEM

Initially:

```python
print(df.dtypes)
```

shows:

```python
object
```

Meaning:
# 👉 pandas thinks date is TEXT.

---

# ✅ SOLUTION

```python
df["order_date"] = pd.to_datetime(df["order_date"])
```

---

# 🧠 WHAT HAPPENS?

Pandas tries to PARSE date string.

Example:

```python
"2024-01-10"
```

Pandas recognizes:

```python
YYYY-MM-DD
```

and converts it into:

```python
datetime64[ns]
```

---

# 🔥 AFTER CONVERSION SUPERPOWERS UNLOCK

Now pandas can:
- compare dates
- subtract dates
- extract year/month/day
- sort dates
- filter dates
- timezone conversion

---

# 6️⃣ DATETIME EXTRACTION

---

# ✅ YEAR

```python
df["year"] = df["order_date"].dt.year
```

---

# ✅ MONTH NUMBER

```python
df["month"] = df["order_date"].dt.month
```

---

# ✅ DAY

```python
df["day"] = df["order_date"].dt.day
```

---

# ✅ MONTH NAME

```python
df["month_name"] = df["order_date"].dt.month_name()
```

---

# ✅ DAY NAME

```python
df["day_name"] = df["order_date"].dt.day_name()
```

---

# 🧠 REAL-WORLD USE

Companies ask:
- monthly sales?
- weekday traffic?
- quarterly revenue?
- yearly growth?
- weekend activity?

All require datetime extraction.

---

# 7️⃣ DATE DIFFERENCE

# ❓ PURPOSE

Calculate days between dates.

---

# ✅ EXAMPLE

```python
df["days_diff"] = (
    pd.Timestamp("2024-04-01")
    - df["order_date"]
).dt.days
```

---

# 🧠 INTERNAL THINKING

Pandas calculates:

```python
2024-04-01 - 2024-01-10
```

for every row.

---

# 🔥 REAL-WORLD USE

Used in:
- SLA tracking
- incident duration
- subscription age
- retention analysis
- days since signup

---

# 8️⃣ VECTORIZATION 🔥🔥🔥

# ❓ MOST IMPORTANT PANDAS CONCEPT

Pandas can operate on FULL columns directly.

---

# ✅ EXAMPLE

```python
df["new_amount"] = df["amount"] * 100
```

---

# 🧠 INTERNAL THINKING

Pandas internally behaves LIKE:

```python
500 * 100
200 * 100
700 * 100
```

for entire column.

---

# ❌ BAD STYLE

```python
for x in df["amount"]:
```

---

# ✅ GOOD STYLE

```python
df["amount"] * 100
```

---

# 🧠 GOLDEN RULE

Always prefer:

1. vectorized operations
2. built-in pandas functions
3. apply
4. loops last

---

# 9️⃣ PIVOT

# ❓ PURPOSE

Convert:
# 👉 rows into columns

---

# ✅ ORIGINAL DATA

| customer | month | sales |
|---|---|---|
| A | Jan | 100 |
| A | Feb | 200 |
| B | Jan | 300 |

---

# ✅ CODE

```python
sales_df = pd.DataFrame({
    "customer": ["A", "A", "B", "B"],
    "month": ["Jan", "Feb", "Jan", "Feb"],
    "sales": [100, 200, 300, 400]
})


pivot_df = sales_df.pivot(
    index="customer",
    columns="month",
    values="sales"
)
```

---

# ✅ OUTPUT

| customer | Jan | Feb |
|---|---|---|
| A | 100 | 200 |
| B | 300 | 400 |

---

# 🧠 WHAT HAPPENED?

Before:

```python
Jan / Feb were row values
```

After:

```python
Jan / Feb became column names
```

---

# 🔥 USE CASES

Used for:
- dashboards
- reports
- Excel-style summaries
- business analytics

---

# 🔟 MELT (UNPIVOT)

# ❓ PURPOSE

Convert:
# 👉 columns back into rows

Reverse of pivot.

---

# ✅ CODE

```python
melt_df = pd.melt(
    pivot_df.reset_index(),
    id_vars="customer",
    var_name="month",
    value_name="sales"
)
```

---

# ✅ OUTPUT

| customer | month | sales |
|---|---|---|
| A | Jan | 100 |
| A | Feb | 200 |
| B | Jan | 300 |
| B | Feb | 400 |

---

# 🧠 IMPORTANT PARAMETERS

| Parameter | Meaning |
|---|---|
| reset_index() | convert index back to column |
| id_vars | keep fixed column |
| var_name | name of new variable column |
| value_name | name of values column |

---

# 🧠 MEMORY TRICK

| Function | Think Like |
|---|---|
| pivot | rows → columns |
| melt | columns → rows |

---

# 1️⃣1️⃣ MISSING VALUES (NaN)

# ❓ WHY IMPORTANT?

Real-world data ALWAYS has missing values.

Examples:
- missing salary
- broken API data
- incomplete forms
- null timestamps
- failed logs

---

# ✅ DATASET

```python
import numpy as np


df = pd.DataFrame({
    "name": ["Aman", "Riya", "Kabir", None, "Simran"],
    "salary": [50000, np.nan, 70000, 40000, np.nan],
    "city": ["Toronto", "Delhi", None, "Mumbai", "Delhi"]
})
```

---

# 1️⃣2️⃣ isna()

# ❓ PURPOSE

Find missing values.

---

# ✅ EXAMPLE

```python
print(df.isna())
```

---

# 🧠 OUTPUT

| Value | Meaning |
|---|---|
| True | missing |
| False | exists |

---

# ✅ COUNT MISSING VALUES

```python
print(df.isna().sum())
```

---

# 🧠 INTERNAL THINKING

```python
True = 1
False = 0
```

So sum counts missing values.

---

# 1️⃣3️⃣ fillna()

# ❓ PURPOSE

Replace missing values.

---

# ✅ EXAMPLE

```python
df["salary"] = df["salary"].fillna(0)
```

---

# ✅ STRING EXAMPLE

```python
df["city"] = df["city"].fillna("Unknown")
```

---

# 🧠 REAL-WORLD USE

Companies often fill with:
- Unknown
- Missing
- Not Available
- 0

instead of deleting rows.

---

# 1️⃣4️⃣ dropna()

# ❓ PURPOSE

Remove rows with missing values.

---

# ✅ EXAMPLE

```python
print(df.dropna())
```

---

# 🧠 WHAT HAPPENS?

Rows containing:
- NaN
- None

are removed.

---

# ✅ REMOVE ROWS ONLY IF SPECIFIC COLUMN HAS NaN

```python
df.dropna(subset=["salary"])
```

---

# 🧠 WHEN TO USE?

| Function | Use Case |
|---|---|
| fillna | keep rows but repair missing |
| dropna | remove damaged rows |

---

# 🏆 FINAL GOLDEN UNDERSTANDING

| Function | Think Like |
|---|---|
| apply | custom logic |
| lambda | quick small function |
| map | strict dictionary mapping |
| replace | safer replacement |
| to_datetime | convert text → real date |
| dt.year/month/day | extract date info |
| Timestamp subtraction | date difference |
| vectorization | operate on whole column |
| pivot | rows → columns |
| melt | columns → rows |
| isna | find missing |
| fillna | repair missing |
| dropna | remove missing |

---

# 🚀 MOST IMPORTANT PANDAS RULE

# 👉 Think in columns, not loops.

That is the REAL pandas mindset.

---

# 🏆 YOUR CURRENT LEVEL

You now understand:
- dataframe transformations
- custom logic
- datetime engineering
- reshaping
- missing value handling
- vectorized thinking

This is a STRONG pandas foundation.

