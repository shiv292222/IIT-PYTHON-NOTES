# Python Regex & String Cleaning

# Golden Notes V2

### By Your Friend GPT 😎

---

# 1. Why Do We Need String Cleaning?

Real-world data is messy.

Examples:

```python
" Shiv Kumar "
"SHIV KUMAR"
"shiv kumar"
```

Humans see the same value.

Computers see:

```python
"Shiv Kumar" != "SHIV KUMAR"
```

Therefore we clean data before analysis.

---

# 2. Why Does Pandas Use `.str`?

Normal Python:

```python
"shiv".lower()
```

works on ONE string.

DataFrame column:

```python
df["name"]
```

contains MANY strings.

Therefore Pandas provides:

```python
df["name"].str.lower()
```

which applies the operation to every row.

---

# 3. What is Vectorization?

Instead of:

```python
for name in names:
    print(name.lower())
```

Pandas performs operations on the entire column:

```python
df["name"].str.lower()
```

Benefits:

* Faster
* Cleaner
* Production style

---

# 4. Common String Methods

## strip()

Removes leading and trailing spaces.

```python
"  Shiv Kumar  ".strip()
```

Output:

```python
"Shiv Kumar"
```

### Edge Case

```python
"Shiv   Kumar".strip()
```

Output:

```python
"Shiv   Kumar"
```

Middle spaces remain.

---

## lower()

```python
"TORONTO".lower()
```

↓

```python
"toronto"
```

---

## upper()

```python
"toronto".upper()
```

↓

```python
"TORONTO"
```

---

## title()

```python
"shiv kumar".title()
```

↓

```python
"Shiv Kumar"
```

---

# 5. Why Is This Unsafe?

```python
df = df.apply(
    lambda col:
    col.str.strip()
    if col.dtype == "object"
    else col
)
```

Because:

```python
dtype = object
```

does NOT mean string.

It can contain:

* strings
* lists
* dictionaries
* tuples

If a list column is encountered:

```python
['7821']
```

Pandas attempts:

```python
['7821'].strip()
```

which is invalid.

Result:

```python
NaN
```

---

# Safer Approach

```python
text_cols = [
    "customer_info",
    "email",
    "phone",
    "order_details"
]

df[text_cols] = (
    df[text_cols]
    .apply(lambda x: x.str.strip())
)
```

Why safer?

Because we explicitly select columns we KNOW contain strings.

---

# 6. What is Regex?

Regex = Pattern Matching Language

Used for:

* Email validation
* Phone numbers
* Dates
* IDs
* Log parsing
* NLP
* Data Cleaning

Think:

> Regex is a language for describing text patterns.

---

# 7. Why Use Raw Strings?

Always write:

```python
r"\d+"
```

instead of:

```python
"\d+"
```

Reason:

```python
\
```

has special meaning in Python.

Raw strings avoid escape problems.

---

# 8. Important Regex Symbols

| Pattern | Meaning            |
| ------- | ------------------ |
| \d      | One digit          |
| \d+     | Full number        |
| \D      | Not digit          |
| \w      | One word character |
| \w+     | Full word          |
| \s      | Whitespace         |
| +       | One or more        |
| *       | Zero or more       |
| ?       | Optional           |
| {n}     | Exactly n          |
| ^       | Start              |
| $       | End                |

---

# 9. Understanding Character Sets []

## What Does [] Mean?

Character Set.

Meaning:

> Match ONE character from these options.

Example:

```python
[a-z]
```

One lowercase letter.

Example:

```python
[ABC]
```

Matches:

```text
A
B
C
```

---

# BIG CONFUSION CLEARED

Many students think:

```python
[a-zA-Z]
```

means:

> return one letter only

Not exactly.

It means:

> THIS PATTERN can match ONE letter.

Then regex continues applying the pattern repeatedly.

Example:

```python
re.findall(r"[a-zA-Z]", "Shiv")
```

Output:

```python
['S','h','i','v']
```

Regex keeps finding one-letter matches.

---

# Why Does This Return Shiv?

```python
re.findall(r"[a-zA-Z]+", "Shiv")
```

Output:

```python
['Shiv']
```

Because:

```python
+
```

means:

> Keep taking matching characters continuously.

---

# Why Does This Return Shiv Kumar?

```python
re.findall(r"[a-zA-Z\s]+", "Shiv Kumar")
```

Output:

```python
['Shiv Kumar']
```

Because allowed characters are:

* letters
* spaces

and `+` keeps consuming characters continuously.

---

# Golden Memory

| Pattern     | Result     |
| ----------- | ---------- |
| [a-zA-Z]    | one letter |
| [a-zA-Z]+   | full word  |
| [a-zA-Z\s]+ | full name  |

---

# 10. Understanding Quantifiers

## +

One or more

```python
\d+
```

Examples:

```text
1
12
123
12345
```

---

## *

Zero or more

```python
\d*
```

Matches:

```text
(empty)
1
12
123
```

---

## ?

Optional

```python
\+?
```

Matches:

```text
+1
1
```

Both valid.

---

## {n}

Exactly n occurrences.

```python
\d{5}
```

Matches:

```text
12345
```

Only.

---

# Edge Case

```python
re.findall(r"\d{2}", "123456")
```

Output:

```python
['12','34','56']
```

NOT:

```python
['123456']
```

---

# 11. What Does \d Mean?

```python
re.findall(r"\d", "Age 25")
```

Output:

```python
['2','5']
```

One digit.

---

# 12. What Does \d+ Mean?

```python
re.findall(r"\d+", "Age 25")
```

Output:

```python
['25']
```

Full number.

---

# 13. What Does \w Mean?

Includes:

* letters
* digits
* underscore

Example:

```python
re.findall(r"\w", "VIP123")
```

Output:

```python
['V','I','P','1','2','3']
```

---

# 14. What Does \w+ Mean?

```python
re.findall(r"\w+", "VIP123")
```

Output:

```python
['VIP123']
```

---

# 15. What Does \D Mean?

NOT digit.

```python
re.findall(r"\D+", "VIP123")
```

Output:

```python
['VIP']
```

---

# 16. What Does \s Mean?

Whitespace.

Includes:

* space
* tab
* newline

---

# 17. Understanding ^

Outside brackets:

```python
^Order
```

means:

Starts with Order.

---

Example:

```python
Order ID: 7821
```

Match.

---

Example:

```python
Refund Order ID: 7821
```

No match.

---

# 18. Understanding $

```python
pending$
```

means:

Ends with pending.

---

Example:

```python
Order pending
```

Match.

---

Example:

```python
Order pending tomorrow
```

No match.

---

# 19. Understanding [^ ]

Inside brackets:

```python
[^a-z]
```

means:

NOT lowercase letters.

---

Example:

```python
Anjali@123
```

Matches:

```text
@
1
2
3
```

---

# IMPORTANT EDGE CASE

Outside brackets:

```python
^
```

means:

Start of string.

Inside brackets:

```python
[^a-z]
```

means:

NOT.

Completely different meaning.

---

# 20. search() vs findall()

## search()

Returns FIRST match only.

```python
re.search(r"\d+", "A123 B456")
```

Returns:

```python
123
```

only.

---

## findall()

Returns ALL matches.

```python
re.findall(r"\d+", "A123 B456")
```

Returns:

```python
['123','456']
```

---

# Golden Memory

search()

↓

One

findall()

↓

Many

---

# 21. What is a Match Object?

```python
m = re.search(r"\d+", "Age 25")
```

Output:

```python
<match object>
```

To get value:

```python
m.group()
```

Output:

```python
25
```

---

# 22. What is extract()?

Used when business expects ONE structured value.

Example:

```python
df["comment"].str.extract(r"(\d+)")
```

Output:

```python
7821
```

Not:

```python
['7821']
```

---

# 23. findall() vs extract()

## findall()

Returns:

```python
['7821']
```

Always list.

---

## extract()

Returns:

```python
7821
```

Scalar value.

---

# Production Rule

Use:

```python
extract()
```

for database columns.

Use:

```python
findall()
```

for exploration.

---

# 24. Capture Groups ()

Most Important Regex Concept

Without capture group:

```python
findall(r"Order ID:\s*\d+")
```

Output:

```python
['Order ID: 7821']
```

Whole pattern returned.

---

With capture group:

```python
findall(r"Order ID:\s*(\d+)")
```

Output:

```python
['7821']
```

Only captured part returned.

---

# Golden Rule

```python
()
```

means:

Capture this part.

---

# 25. What is re.sub()?

Replace matches.

Example:

```python
re.sub(r"\d", "", "VIP123")
```

Output:

```python
VIP
```

---

Example

```python
re.sub(r"_", " ", "John_Doe")
```

Output:

```python
John Doe
```

---

# 26. What is re.split()?

Split text using regex.

```python
re.split(
    r"[,;\s]+",
    "apple,banana;orange mango"
)
```

Output:

```python
['apple','banana','orange','mango']
```

---

# 27. Understanding This Phone Pattern

```python
r"\+?\d[\d\s\-]+"
```

Breakdown:

```python
\+?
```

optional plus sign

---

```python
\d
```

first digit

---

```python
[\d\s\-]+
```

allow:

* digits
* spaces
* hyphens

continuously

---

Matches:

```text
+1-437-555-1234
4375559999
+1 647 123 8888
```

---

# Why This Is Wrong?

```python
r"[\+?\d[\d\s\-]+"
```

Because:

```python
[]
```

creates ONE character set.

Inside brackets:

```python
?
```

loses its regex meaning and becomes a literal character.

---

# Golden Rule

Outside brackets:

```python
?
```

means optional.

Inside brackets:

```python
[?]
```

means actual question mark.

---

# 28. Real Production Examples

## Extract Ticket ID

```python
Ticket#A123 created
```

Regex:

```python
r"Ticket#([A-Z]\d+)"
```

Output:

```python
A123
```

---

## Extract Error Code

```python
ERROR500 occurred
```

Regex:

```python
r"ERROR(\d+)"
```

Output:

```python
500
```

---

## Extract VIP ID

```python
Shiv Kumar (VIP123)
```

Regex:

```python
r"(VIP\d+)"
```

Output:

```python
VIP123
```

---

## Extract Order ID

```python
Order ID: 7821
```

Regex:

```python
r"Order ID:\s*(\d+)"
```

Output:

```python
7821
```

---

# Final Golden Regex Framework

Whenever you see a regex problem ask:

1. What pattern am I looking for?
2. One value or many values?
3. Extract, Replace, Split, or Validate?
4. Which characters are allowed?
5. Which characters are forbidden?
6. Do I need a capture group?

If you can answer these questions, most regex problems become straightforward.
