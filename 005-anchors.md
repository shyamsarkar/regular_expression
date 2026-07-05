# 005 - Anchors in Ruby Regular Expressions

> **Goal:** Learn how Anchors work, why they are different from normal characters, and how to use them for accurate validations.

---

# Table of Contents

- What are Anchors?
- Why do we need Anchors?
- `^` — Start of Line
- `$` — End of Line
- `\A` — Absolute Start of String
- `\Z` — End of String (Before Final Newline)
- `\z` — Absolute End of String
- `\b` — Word Boundary
- `\B` — Non-Word Boundary
- `^` vs `\A`
- `$` vs `\Z` vs `\z`
- Real World Examples
- Common Mistakes
- Interview Tips
- Summary
- Practice Questions

---

# What are Anchors?

Unlike character classes or quantifiers, **Anchors do not match characters.**

They match **positions**.

Think of an anchor as pointing to a location inside the string.

For example

```ruby
/^Ruby/
```

does **not** match the character `^`.

Instead, it says

> Match **Ruby** only if it starts at the beginning.

---

# Why do we need Anchors?

Suppose we want to validate a 10-digit mobile number.

Without anchors

```ruby
/\d{10}/
```

This matches

```text
9876543210
```

but it also matches

```text
abc9876543210xyz
```

because Regex finds a valid 10-digit sequence inside the string.

To ensure the **entire string** is a mobile number

```ruby
/^\d{10}$/
```

or even better in Ruby

```ruby
/\A\d{10}\z/
```

---

# `^` — Start of Line

The `^` anchor matches the **start of a line**.

Example

```ruby
/^Ruby/
```

Matches

```text
Ruby on Rails
```

Does NOT match

```text
I love Ruby
```

---

Example

```ruby
puts "Ruby on Rails".match?(/^Ruby/)
```

Output

```text
true
```

---

Example

```ruby
puts "I love Ruby".match?(/^Ruby/)
```

Output

```text
false
```

---

# `$` — End of Line

The `$` anchor matches the **end of a line**.

Example

```ruby
/Developer$/
```

Matches

```text
Ruby Developer
```

Does NOT match

```text
Developer Ruby
```

---

Example

```ruby
puts "Ruby Developer".match?(/Developer$/)
```

Output

```text
true
```

---

# Matching the Entire String

Using both anchors

```ruby
/^Ruby$/
```

Matches only

```text
Ruby
```

Does NOT match

```text
Ruby on Rails
```

or

```text
I love Ruby
```

---

# `\A` — Absolute Start of String

Ruby provides

```ruby
\A
```

which means

> Beginning of the entire string.

Example

```ruby
/\ARuby/
```

Unlike `^`, it does **not** change behavior in multiline matching.

---

Example

```ruby
puts "Ruby".match?(/\ARuby/)
```

Output

```text
true
```

---

# `\Z` — End of String (Before Final Newline)

`\Z` matches the end of the string **or just before a trailing newline**.

Suppose

```ruby
text = "Ruby\n"
```

Regex

```ruby
/\ARuby\Z/
```

matches successfully.

---

# `\z` — Absolute End of String

`\z` is stricter.

It matches only the absolute end.

Example

```ruby
text = "Ruby\n"
```

Regex

```ruby
/\ARuby\z/
```

does **not** match because a newline exists after `Ruby`.

---

# Difference Between `\Z` and `\z`

String

```text
Ruby
```

Both match.

---

String

```text
Ruby\n
```

Pattern

```ruby
/\ARuby\Z/
```

Result

```text
Matches
```

Pattern

```ruby
/\ARuby\z/
```

Result

```text
Does NOT match
```

---

# `\b` — Word Boundary

`\b` matches the boundary between a word character and a non-word character.

It does **not** match a visible character.

Suppose

```text
cat dog scatter category
```

Regex

```ruby
/\bcat\b/
```

Matches

```text
cat
```

Does NOT match

```text
scatter
category
```

---

Example

```ruby
puts "cat dog".scan(/\bcat\b/).inspect
```

Output

```ruby
["cat"]
```

---

# Why Word Boundaries Matter

Without

```ruby
/cat/
```

matches

```text
cat
scatter
category
```

With

```ruby
/\bcat\b/
```

only

```text
cat
```

is matched.

---

# `\B` — Non-Word Boundary

`\B` is the opposite of `\b`.

It matches positions **inside** words.

Example

```ruby
/\Bcat\B/
```

Matches

```text
scatter
```

Does NOT match

```text
cat
```

---

Example

```ruby
puts "scatter".match(/\Bcat\B/)
```

Output

```text
cat
```

---

# `^` vs `\A`

This is a common Ruby interview question.

| Anchor | Meaning |
|---------|---------|
| `^` | Start of a line |
| `\A` | Absolute start of the string |

For most validations in Ruby, prefer

```ruby
\A
```

instead of

```ruby
^
```

---

# `$` vs `\Z` vs `\z`

| Anchor | Meaning |
|---------|---------|
| `$` | End of a line |
| `\Z` | End of string (before optional final newline) |
| `\z` | Absolute end of string |

---

# Why Ruby Developers Prefer `\A` and `\z`

Instead of

```ruby
/^\d{10}$/
```

most Ruby codebases use

```ruby
/\A\d{10}\z/
```

because it avoids unexpected multiline behavior.

This is considered the Ruby convention.

---

# Real World Examples

## Email Validation

```ruby
/\A[\w.+-]+@[a-z\d.-]+\.[a-z]{2,}\z/i
```

---

## Indian Mobile Number

```ruby
/\A[6-9]\d{9}\z/
```

---

## PIN Code

```ruby
/\A\d{6}\z/
```

---

## Username

```ruby
/\A[A-Za-z][A-Za-z0-9_]{4,15}\z/
```

---

## Find Whole Word

```ruby
/\bruby\b/i
```

Matches

```text
Ruby
ruby
RUBY
```

but not

```text
rubygems
```

---

# Common Mistakes

## Mistake 1

Using

```ruby
/\d{10}/
```

for validation.

Always use anchors.

Correct

```ruby
/\A\d{10}\z/
```

---

## Mistake 2

Using

```ruby
^
```

and

```ruby
$
```

for every validation.

In Ruby,

```ruby
\A
```

and

```ruby
\z
```

are usually better.

---

## Mistake 3

Thinking

```ruby
\b
```

means a backspace.

In Regex,

```ruby
\b
```

means **word boundary**.

---

## Mistake 4

Forgetting that anchors match positions, **not characters**.

---

# Interview Tips

A very common interview question is:

**Which is preferred in Ruby validations?**

```ruby
^\d+$
```

or

```ruby
\A\d+\z
```

The correct answer is

```ruby
\A\d+\z
```

because it validates against the entire string and avoids multiline issues.

Another common question:

What is the difference between

```ruby
cat
```

and

```ruby
\bcat\b
```

Always mention **whole-word matching**.

---

# Summary

In this chapter, you learned

- `^`
- `$`
- `\A`
- `\Z`
- `\z`
- `\b`
- `\B`
- Why anchors match positions instead of characters
- Ruby's preferred validation style
- Whole-word matching

Anchors are essential for writing accurate validations and are heavily used in Ruby on Rails applications.

---

# Practice Questions

## Question 1

What is the difference between

```ruby
^
```

and

```ruby
\A
```

---

## Question 2

What is the difference between

```ruby
$
```

and

```ruby
\z
```

---

## Question 3

Why is

```ruby
/\d{10}/
```

not suitable for validating a phone number?

---

## Question 4

Write a Regex that validates exactly six digits.

---

## Question 5

Write a Regex that matches the word

```text
Ruby
```

only when it appears as a complete word.

---

## Question 6

What does

```ruby
\b
```

represent?

---

## Question 7

What does

```ruby
\B
```

represent?

---

## Question 8

Which is preferred in Ruby validations?

```ruby
^\w+$
```

or

```ruby
\A\w+\z
```

Why?

---

## Question 9

Explain why

```ruby
/\bruby\b/
```

does not match

```text
rubygems
```

---

## Question 10

Write a Regex that validates an email address using `\A` and `\z`.

---

# Next Chapter

➡ **006-groups-and-capturing.md**