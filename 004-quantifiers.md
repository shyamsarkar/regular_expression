# 004 - Quantifiers in Ruby Regular Expressions

> **Goal:** Learn how to control **how many times** a character or pattern should appear using Regex quantifiers.

---

# Table of Contents

- What are Quantifiers?
- Why are Quantifiers Needed?
- `*` (Zero or More)
- `+` (One or More)
- `?` (Zero or One)
- `{n}` (Exactly n Times)
- `{n,}` (At Least n Times)
- `{n,m}` (Between n and m Times)
- Greedy Quantifiers
- Lazy Quantifiers
- Quantifiers with Groups
- Common Mistakes
- Interview Tips
- Summary
- Practice Questions

---

# What are Quantifiers?

A **Quantifier** tells Regex **how many times** a character, character class, or group should appear.

Without a quantifier

```ruby
/a/
```

matches exactly one `a`.

With a quantifier

```ruby
/a+/
```

it can match

```text
a
aa
aaa
aaaa
```

---

# Why are Quantifiers Needed?

Suppose we want to match

```text
1
12
123
123456
```

Writing

```ruby
/\d/
```

only matches one digit.

Instead

```ruby
/\d+/
```

matches one or more digits.

---

# `*` — Zero or More

Syntax

```ruby
pattern*
```

Meaning

> Match the previous character **zero or more times**.

Example

```ruby
/ab*/
```

Matches

```text
a
ab
abb
abbb
abbbb
```

Notice that even

```text
a
```

matches because `b` is allowed to appear **zero times**.

---

Example

```ruby
puts "abbbb".match(/ab*/)
```

Output

```text
abbbb
```

---

Example

```ruby
puts "a".match(/ab*/)
```

Output

```text
a
```

---

# `+` — One or More

Syntax

```ruby
pattern+
```

Meaning

> Match the previous character **one or more times**.

Example

```ruby
/ab+/
```

Matches

```text
ab
abb
abbb
abbbb
```

Does NOT match

```text
a
```

---

Example

```ruby
puts "abbb".match(/ab+/)
```

Output

```text
abbb
```

---

Example

```ruby
puts "a".match(/ab+/)
```

Output

```ruby
nil
```

---

# Difference Between `*` and `+`

Pattern

```ruby
ab*
```

Matches

```text
a
ab
abb
abbb
```

Pattern

```ruby
ab+
```

Matches

```text
ab
abb
abbb
```

---

Rule to remember

| Quantifier | Minimum Matches |
|------------|----------------:|
| `*` | 0 |
| `+` | 1 |

---

# `?` — Zero or One

Syntax

```ruby
pattern?
```

Meaning

> Match the previous character **zero or one time**.

Example

```ruby
/colou?r/
```

Matches

```text
color
colour
```

Does NOT match

```text
colouur
```

---

Example

```ruby
puts "color".match(/colou?r/)
```

Output

```text
color
```

---

Example

```ruby
puts "colour".match(/colou?r/)
```

Output

```text
colour
```

---

# `{n}` — Exactly n Times

Syntax

```ruby
pattern{n}
```

Example

```ruby
/\d{5}/
```

Matches

```text
12345
```

Does NOT match

```text
1234
```

or

```text
123456
```

---

Example

```ruby
puts "12345".match(/\d{5}/)
```

Output

```text
12345
```

---

# `{n,}` — At Least n Times

Syntax

```ruby
pattern{n,}
```

Example

```ruby
/\d{3,}/
```

Matches

```text
123
1234
12345
123456
```

---

Example

```ruby
puts "123456".match(/\d{3,}/)
```

Output

```text
123456
```

---

# `{n,m}` — Between n and m Times

Syntax

```ruby
pattern{n,m}
```

Example

```ruby
/^\d{2,4}$/
```

Matches

```text
12
123
1234
```

Does NOT match

```text
1
12345
```

---

Example

```ruby
puts "123".match(/^\d{2,4}$/)
```

Output

```text
123
```

---

# Combining Quantifiers

Example

```ruby
/[A-Za-z]{3,8}/
```

Matches

```text
Tom
Alice
Michael
```

Does NOT fully match

```text
Jo
```

because it has fewer than 3 letters.

---

Example

```ruby
/\d{2}-\d{2}-\d{4}/
```

Matches

```text
12-05-2025
```

---

# Quantifiers with Groups

Quantifiers can also be applied to **groups**.

Example

```ruby
/(ab)+/
```

Matches

```text
ab
abab
ababab
```

Example

```ruby
puts "ababab".match(/(ab)+/)
```

Output

```text
ababab
```

---

Another example

```ruby
/(ha){3}/
```

Matches

```text
hahaha
```

Does NOT match

```text
haha
```

---

# Greedy Quantifiers

By default, quantifiers are **greedy**.

They match as much text as possible.

Example

```ruby
text = "<div>one</div><div>two</div>"
```

Regex

```ruby
/<div>.*<\/div>/
```

Output

```text
<div>one</div><div>two</div>
```

The `.*` consumes everything until the last `</div>`.

---

# Lazy Quantifiers

Add `?` after a quantifier to make it lazy.

Example

```ruby
/<div>.*?<\/div>/
```

Output

```text
<div>one</div>
```

Now it stops at the first possible match.

---

Comparison

| Pattern | Behavior |
|---------|----------|
| `.*` | Greedy |
| `.*?` | Lazy |
| `.+` | Greedy |
| `.+?` | Lazy |

---

# Real World Examples

## Indian Mobile Number

```ruby
/\A[6-9]\d{9}\z/
```

Exactly ten digits.

---

## PIN Code

```ruby
/\A\d{6}\z/
```

Exactly six digits.

---

## Username

```ruby
/\A[A-Za-z][A-Za-z0-9_]{4,15}\z/
```

Starts with a letter.

Minimum 5 characters.

Maximum 16 characters.

---

## Password Length

```ruby
/.{8,}/
```

Minimum 8 characters.

---

# Common Mistakes

## Mistake 1

Confusing

```ruby
*
```

with

```ruby
+
```

Remember

```text
* → Zero or More

+ → One or More
```

---

## Mistake 2

Using

```ruby
.*
```

without anchors.

Example

```ruby
/.*/
```

matches almost everything.

Be careful.

---

## Mistake 3

Forgetting that quantifiers apply only to the previous token.

Example

```ruby
ab+
```

means

```text
a
followed by

one or more b
```

NOT

```text
one or more "ab"
```

To repeat the whole word

```ruby
(ab)+
```

---

# Interview Tips

Interviewers often ask

What is the difference between

```ruby
ab*
```

and

```ruby
(ab)*
```

Answer

```ruby
ab*
```

means

```text
a
followed by

zero or more b
```

Whereas

```ruby
(ab)*
```

means

```text
zero or more occurrences of

ab
```

Examples

```text
Pattern: ab*

Matches

a
ab
abb
abbb
```

Examples

```text
Pattern: (ab)*

Matches

(empty string)
ab
abab
ababab
```

---

# Summary

In this chapter, you learned

- `*`
- `+`
- `?`
- `{n}`
- `{n,}`
- `{n,m}`
- Greedy matching
- Lazy matching
- Quantifiers with groups
- Real-world validation patterns

Quantifiers are among the most frequently used Regex features and appear in almost every real-world Regular Expression.

---

# Practice Questions

## Question 1

What is the difference between

```ruby
a*
```

and

```ruby
a+
```

---

## Question 2

Write a Regex that matches exactly 8 digits.

---

## Question 3

Write a Regex that matches between 5 and 10 lowercase letters.

---

## Question 4

Why does

```ruby
.*
```

often match more text than expected?

---

## Question 5

What is the difference between

```ruby
ab+
```

and

```ruby
(ab)+
```

---

## Question 6

Write a Regex that matches an Indian PIN code.

---

## Question 7

Which quantifier would you use for an optional character?

---

## Question 8

Convert this greedy Regex into a lazy one.

```ruby
/<p>.*<\/p>/
```

---

## Question 9

Will this Regex match `"a"`?

```ruby
ab*
```

Explain why.

---

## Question 10

Write a Regex that matches usernames between **5 and 16 characters**, starting with a letter and containing only letters, digits, and underscores.

---

# Next Chapter

➡ **005-anchors.md**