# Python String Cleaning + Regex

# Golden Questions & Answers Notes

# By Your Friend GPT 😎

---

# Q1. Why do we need String Cleaning?

## Answer

Real-world data is messy.

Examples:

```python
" Shiv Kumar "
"SHIV KUMAR"
"shiv kumar"
```

Humans see the same person.

Computers see different strings.

```python
"Shiv Kumar" != "SHIV KUMAR"
```

Therefore we clean data before analysis.

---

# Q2. Why does Pandas provide `.str`?

## Answer

Normal Python:

```python
"shiv".lower()
```

works on ONE string.

DataFrame:

```python
df["name"]
```

contains MANY strings.

Therefore Pandas provides:

```python
df["name"].str.lower()
```

which applies operation on every row.

---

# Q3. What is Vectorization?

## Answer

Instead of:

```python
for name in names:
    print(name.lower())
```

Pandas does:

```python
df["name"].str.lower()
```

Benefits:

* cleaner code
* faster execution
* production style

---

# Q4. What does strip() do?

## Answer

Removes leading and trailing spaces.

Example:

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

Only outer spaces removed.

---

# Q5. What does lower() do?

## Answer

Converts text to lowercase.

Example:

```python
"TORONTO".lower()
```

Output:

```python
"toronto"
```

Useful for:

* joins
* grouping
* comparisons

---

# Q6. What does upper() do?

## Answer

Converts text to uppercase.

```python
"toronto".upper()
```

↓

```python
"TORONTO"
```

---

# Q7. What does title() do?

## Answer

Capitalizes first letter of every word.

```python
"shiv kumar".title()
```

↓

```python
"Shiv Kumar"
```

---

# Q8. What is Regex?

## Answer

Regex = Pattern Matching Language.

Used for:

* emails
* phone numbers
* dates
* IDs
* log parsing
* NLP

Think:

> Regex is a language for describing text patterns.

---

# Q9. Why do we use r""?

## Answer

Always write:

```python
r"\d+"
```

because:

```python
\
```

has special meaning in Python.

Raw strings prevent escape confusion.

---

# Q10. What does \d mean?

## Answer

One digit.

Example:

```python
re.findall(r"\d", "Age 25")
```

Output:

```python
['2', '5']
```

---

# Q11. What does \d+ mean?

## Answer

Continuous digits.

Example:

```python
re.findall(r"\d+", "Age 25")
```

Output:

```python
['25']
```

---

# Q12. Difference between \d and \d+?

## Answer

```python
\d
```

means one digit.

```python
\d+
```

means full number.

Example:

```python
Age 25
```

Results:

```python
\d   → ['2','5']
\d+  → ['25']
```

---

# Q13. What does \w mean?

## Answer

One word character.

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

# Q14. What does \w+ mean?

## Answer

Continuous word characters.

Example:

```python
re.findall(r"\w+", "VIP123")
```

Output:

```python
['VIP123']
```

---

# Q15. What does \D mean?

## Answer

NOT digit.

Example:

```python
re.findall(r"\D+", "VIP123")
```

Output:

```python
['VIP']
```

---

# Q16. What does \s mean?

## Answer

Whitespace.

Includes:

* space
* tab
* newline

---

# Q17. What do [] mean?

## Answer

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

```python
A
B
C
```

---

# Q18. Why does [a-zA-Z] return one letter at a time?

## Answer

Pattern:

```python
[a-zA-Z]
```

means:

ONE alphabet.

Example:

```python
re.findall(r"[a-zA-Z]", "Shiv")
```

Output:

```python
['S','h','i','v']
```

Regex matches one character at a time.

---

# Q19. Why does [a-zA-Z]+ return Shiv?

## Answer

Because:

```python
+
```

means:

one or more continuously.

Example:

```python
re.findall(r"[a-zA-Z]+", "Shiv")
```

Output:

```python
['Shiv']
```

Regex keeps taking letters until pattern breaks.

---

# Q20. Why does [a-zA-Z\s]+ return Shiv Kumar?

## Answer

Allowed characters:

* letters
* spaces

And:

```python
+
```

means continuous matching.

Therefore:

```python
Shiv Kumar
```

becomes ONE match.

Output:

```python
['Shiv Kumar']
```

---

# Q21. What does [^a-zA-Z] mean?

## Answer

NOT alphabet.

Example:

```python
Anjali@123
```

Matches:

```python
@
1
2
3
```

---

# Q22. Why does ^ mean two different things?

## Answer

Outside brackets:

```python
^Order
```

means:

Starts with Order.

Inside brackets:

```python
[^a-z]
```

means:

NOT lowercase letters.

Very important edge case.

---

# Q23. What does $ mean?

## Answer

End of string.

Example:

```python
pending$
```

means:

Must end with pending.

---

# Q24. What is findall()?

## Answer

Returns ALL matches.

Example:

```python
re.findall(r"\d+", "Order 7821 Refund 9981")
```

Output:

```python
['7821','9981']
```

---

# Q25. Why does findall() return a list?

## Answer

Because multiple matches may exist.

Even one match returns:

```python
['7821']
```

instead of:

```python
7821
```

---

# Q26. What is extract()?

## Answer

Extracts ONE structured value.

Example:

```python
df["comment"].str.extract(r"(\d+)")
```

Output:

```python
7821
```

not

```python
['7821']
```

---

# Q27. When should I use findall()?

## Answer

When multiple values may exist.

Example:

```python
Order 7821 Refund 9981
```

Output:

```python
['7821','9981']
```

---

# Q28. When should I use extract()?

## Answer

When business expects ONE value.

Example:

```python
Order ID: 7821
```

Output:

```python
7821
```

---

# Q29. What is a Capture Group?

## Answer

Parentheses:

```python
()
```

create capture groups.

Example:

```python
r"Order ID:\s*(\d+)"
```

captures:

```python
7821
```

only.

Without parentheses:

```python
Order ID: 7821
```

entire match returned.

---

# Q30. What is re.sub()?

## Answer

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

# Q31. What is re.split()?

## Answer

Split text using regex.

Example:

```python
re.split(r"[,;\s]+",
         "apple,banana;orange mango")
```

Output:

```python
['apple','banana','orange','mango']
```

---

# Q32. What does {5} mean?

## Answer

Exactly 5 occurrences.

Example:

```python
\d{5}
```

means:

Exactly 5 digits.

---

# Q33. Difference between + and {5}?

## Answer

```python
\d+
```

Any length.

```python
\d{5}
```

Exactly 5 digits.

---

# Q34. Why did .str.strip() create NaN on my regex column?

## Answer

Because:

```python
findall()
```

created lists:

```python
['7821']
```

Lists do not support:

```python
strip()
```

Pandas converted invalid operations to NaN.

---

# ADVANCED REAL-WORLD QUESTIONS

## Extract Ticket Code

Text:

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

Text:

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

## Extract Email Domain

Text:

```python
support@company.com
```

Regex idea:

Extract everything after:

```python
@
```

Output:

```python
company.com
```

---

## Extract IP Address

Text:

```python
192.168.1.1
```

Common in:

* Datadog
* Splunk
* Logs
* Monitoring

---

# FINAL GOLDEN RULE

Regex is not about memorizing symbols.

Regex is about answering:

1. What pattern am I looking for?
2. One value or many values?
3. Extract, Replace, Split, or Validate?
4. Which characters are allowed?
5. Which characters are forbidden?

If you can answer those 5 questions, regex becomes easy.
