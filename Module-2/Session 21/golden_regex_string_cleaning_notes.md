# Python String Cleaning + Regex — Golden Notes

# 1. THE BIG PICTURE

This whole topic is about:

# “Making messy text reliable.”

Real-world data is NEVER clean.

Examples of messy data:
- extra spaces
- uppercase/lowercase inconsistency
- invalid emails
- mixed phone formats
- special characters
- random symbols
- inconsistent categories

Example:

```python
"Toronto"
"toronto"
" TORONTO "
```

Humans think:
- same city

Computer thinks:
- 3 completely different strings

WHY?

Because computers compare characters EXACTLY.

```python
"Toronto" == "toronto"
```

Output:

```python
False
```

This is WHY data cleaning exists.

---

# 2. HOW STRINGS WORK INTERNALLY

A string is basically:

# sequence of characters

Example:

```python
"HELLO"
```

Internally:

| Index | Character |
|---|---|
| 0 | H |
| 1 | E |
| 2 | L |
| 3 | L |
| 4 | O |

Even spaces are characters.

```python
" HI "
```

actually contains:

```python
[space] H I [space]
```

That is why spaces create problems.

---

# 3. WHY STRING CLEANING IS IMPORTANT

Without cleaning:
- joins fail
- groupby becomes wrong
- ML models learn wrong categories
- dashboards show duplicate categories
- reports become inaccurate

Example:

```python
Toronto
toronto
TORONTO
```

Without cleaning:
- 3 separate groups

With cleaning:
- 1 standardized group

---

# 4. VECTORIZED OPERATIONS IN PANDAS

Suppose:

```python
df["name"]
```

contains many rows.

Normal Python methods work on ONE string:

```python
"shiv".lower()
```

But DataFrame columns contain MANY strings.

So Pandas provides:

```python
.str
```

This allows string operations on the ENTIRE column.

---

# 5. WHY VECTORIZATION EXISTS

Beginner approach:

```python
clean = []

for i in names:
    clean.append(i.strip())
```

Pandas approach:

```python
df["name"].str.strip()
```

This is called:

# vectorized operation

Meaning:

# “Apply operation on full column internally.”

Why faster?
- avoids Python loop overhead
- uses optimized internal operations
- uses NumPy arrays underneath

Very important for:
- AI
- ML
- Data Engineering
- Big datasets

---

# 6. IMPORTANT STRING METHODS

---

## strip()

Removes:
- leading spaces
- trailing spaces

Example:

```python
"  Shiv Kumar  ".strip()
```

Output:

```python
"Shiv Kumar"
```

IMPORTANT:

It DOES NOT remove spaces between words.

```python
"Shiv   Kumar".strip()
```

Output:

```python
"Shiv   Kumar"
```

Only outer spaces removed.

---

## lower()

Converts everything to lowercase.

```python
"TORONTO".lower()
```

Output:

```python
"toronto"
```

Used for:
- grouping
- joins
- comparisons
- standardization

---

## upper()

Converts everything to uppercase.

```python
"hello".upper()
```

Output:

```python
"HELLO"
```

---

## title()

Capitalizes first letter of every word.

```python
"shiv kumar".title()
```

Output:

```python
"Shiv Kumar"
```

Useful for:
- names
- addresses
- reports

---

# 7. METHOD CHAINING

Example:

```python
df["city"] = df["city"].str.strip().str.lower()
```

Execution order:

Step 1:

```python
.str.strip()
```

Step 2:

```python
.str.lower()
```

This style is called:

# method chaining

Very common in:
- Pandas
- Spark
- Data Engineering
- AI pipelines

---

# 8. CLEANING ALL STRING COLUMNS AT ONCE

Sometimes we want to clean all string columns.

Correct approach:

```python
df = df.apply(
    lambda col: col.str.strip()
    if col.dtype == "object"
    else col
)
```

---

# UNDERSTAND THIS CAREFULLY

## df.apply()

Means:

# apply operation column-by-column

---

## lambda col

Current column stored inside variable `col`.

---

## col.dtype == "object"

String columns in pandas usually have dtype:

```python
object
```

We check this because:

```python
123.strip()
```

would crash.

So only string columns are cleaned.

---

# 9. REGEX (REGULAR EXPRESSIONS)

Regex means:

# pattern matching language

Purpose:
- find patterns
- validate patterns
- replace patterns
- split text intelligently

Regex is heavily used in:
- NLP
- AI preprocessing
- backend validation
- cybersecurity
- observability
- log parsing
- ETL pipelines

---

# 10. IMPORTING REGEX MODULE

```python
import re
```

`re` stands for:

# regular expression

---

# 11. RAW STRING IMPORTANT CONCEPT

Regex almost always uses:

```python
r"pattern"
```

Example:

```python
r"\d+"
```

WHY?

Because Python itself uses:

```python
\
```

for escaping.

Example:

```python
\n
```

means newline.

So raw string tells Python:

# “Do not interpret backslashes.”

Very important.

---

# 12. MOST IMPORTANT REGEX SYMBOLS

| Pattern | Meaning |
|---|---|
| \d | single digit |
| \d+ | complete number |
| \D | non-digit |
| \w | word character |
| \w+ | complete word |
| \s | whitespace |
| + | one or more |
| * | zero or more |
| ? | optional |
| ^ | starts with |
| $ | ends with |

These solve MOST real regex problems.

---

# 13. UNDERSTANDING \d vs \d+

---

## \d

Means:

# one digit

Example:

```python
re.findall(r"\d", "Age 25")
```

Output:

```python
['2', '5']
```

---

## \d+

Means:

# continuous digits together

Example:

```python
re.findall(r"\d+", "Age 25")
```

Output:

```python
['25']
```

IMPORTANT:

`+` means:

# “one or more continuously”

---

# 14. UNDERSTANDING \w

```python
\w
```

means:
- alphabets
- digits
- underscore

Example:

```python
re.findall(r"\w+", "hello_123 !!!")
```

Output:

```python
['hello_123']
```

Special characters removed.

---

# 15. UNDERSTANDING [ ]

Square brackets mean:

# allowed character set

Example:

```python
[a-z]
```

means:

# lowercase letters

---

## Examples

```python
[A-Z]
```

uppercase letters.

```python
[a-zA-Z]
```

all alphabets.

---

# 16. WHY THIS RETURNS SEPARATE WORDS

Example:

```python
re.findall(r"[a-zA-Z]+", "Shiv Kumar")
```

Output:

```python
['Shiv', 'Kumar']
```

WHY?

Because regex sees:

```python
Shiv[space]Kumar
```

Space breaks continuity.

Regex pattern only allowed alphabets.

Space is NOT alphabet.

---

# 17. HOW TO ALLOW SPACES

```python
re.findall(r"[a-zA-Z\s]+", "Shiv Kumar")
```

Output:

```python
['Shiv Kumar']
```

Because:

```python
\s
```

means whitespace.

---

# 18. IMPORTANT REGEX FUNCTIONS

---

## re.findall()

Returns ALL matches.

Most commonly used.

Example:

```python
re.findall(r"\d+", text)
```

---

## re.search()

Returns FIRST match only.

Useful for:
- checking existence
- getting first occurrence

---

## re.sub()

Replace/substitute text.

Example:

```python
re.sub(r"\d", "", text)
```

Removes digits.

---

## re.split()

Split text using regex.

Example:

```python
re.split(r"[,;\s]+", text)
```

---

# 19. findall vs split vs sub

---

## findall()

Thinking:

# “What should I KEEP?”

Extract patterns.

---

## split()

Thinking:

# “Where should I CUT?”

Separates text.

---

## sub()

Thinking:

# “What should I REPLACE?”

Transforms text.

---

# 20. UNDERSTANDING re.split()

Text:

```python
"apple,banana;orange mango"
```

Goal:
- split on commas
- semicolons
- spaces

Regex:

```python
r"[,;\s]+"
```

Meaning:

Split wherever you see:
- comma
- semicolon
- whitespace

Example:

```python
re.split(r"[,;\s]+", text)
```

Output:

```python
['apple', 'banana', 'orange', 'mango']
```

---

# 21. UNDERSTANDING re.sub()

Text:

```python
"hello@#$world!!!"
```

Goal:

```python
"helloworld"
```

Regex:

```python
r"[^a-zA-Z]"
```

IMPORTANT:

Inside square brackets:

```python
^
```

means:

# NOT

So:

```python
[^a-zA-Z]
```

means:

# anything NOT alphabet

Then:

```python
re.sub(pattern, "", text)
```

replaces those characters with nothing.

Output:

```python
helloworld
```

---

# 22. STARTS WITH AND ENDS WITH

---

## ^

Outside square brackets:

```python
^hello
```

means:

# starts with hello

---

## $

```python
world$
```

means:

# ends with world

---

# 23. WHY BACKSLASH SOMETIMES USED

Regex has special symbols:

| Symbol | Meaning |
|---|---|
| . | any character |
| + | one or more |
| * | repeat |
| ? | optional |

If we want ACTUAL symbol:

we escape using:

```python
\
```

Example:

```python
\.
```

means actual dot.

---

# 24. WHY HYPHEN SOMETIMES NO ESCAPE

Inside square brackets:

```python
[a-z]
```

hyphen creates range.

But if hyphen placed at end:

```python
[\d\s-]
```

regex understands literal hyphen.

Safer professional style:

```python
[\d\s\-]
```

---

# 25. IMPORTANT ENGINEER MINDSET

Regex is NOT about memorizing symbols.

Regex is about:

# writing rules for text patterns

Think like this:

| Problem | Regex Thinking |
|---|---|
| emails | what format valid? |
| phone | what structure allowed? |
| logs | what pattern extract? |
| NLP | what should be cleaned? |
| hashtags | what pattern identify? |

---

# 26. REAL INDUSTRY USAGE

Regex used heavily in:
- Datadog
- Splunk
- ELK
- SIEM tools
- NLP pipelines
- AI preprocessing
- backend APIs
- fraud detection
- cybersecurity

Example:

```python
ERROR 500 at 10:45
```

Regex extracts:
- error code
- timestamps
- IP addresses
- request IDs

This powers observability systems.

---

# 27. FINAL GOLDEN MEMORY

String cleaning + regex are actually about:

# “Helping computers understand messy human text.”

That is the REAL core idea.

Everything else is syntax.

