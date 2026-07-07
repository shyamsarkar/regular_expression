# 007 - Lookaheads and Lookbehinds in Ruby Regular Expressions

> **Goal:** Learn how to match text based on what comes before or after it without including that surrounding text in the match.

---

# Table of Contents

- What are Lookarounds?
- Why do we need Lookarounds?
- Positive Lookahead
- Negative Lookahead
- Positive Lookbehind
- Negative Lookbehind
- Combining Lookarounds
- Real World Examples
- Common Mistakes
- Interview Tips
- Summary
- Practice Questions

---

# What are Lookarounds?

Lookarounds are **zero-width assertions**.

This means they **check a condition** without consuming (matching) any characters.

Unlike normal patterns, lookarounds do not become part of the final match.

There are four types:

| Type | Syntax |
|------|--------|
| Positive Lookahead | `(?=...)` |
| Negative Lookahead | `(?!...)` |
| Positive Lookbehind | `(?<=...)` |
| Negative Lookbehind | `(?<!...)` |

---

# Why do we need Lookarounds?

Suppose we have

```text
Price: $250
```

We want only

```text
250
```

not

```text
$250
```

Instead of matching the dollar sign, we can simply check that it exists before the number.

---

# Positive Lookahead

Syntax

```ruby
pattern(?=another_pattern)
```

Meaning

> Match `pattern` only if it is immediately followed by `another_pattern`.

The second pattern is **not included** in the result.

---

## Example

```ruby
text = "100kg"

puts text.match(/\d+(?=kg)/)
```

Output

```text
100
```

Notice that

```text
kg
```

is not part of the match.

---

## Another Example

```ruby
puts "apple pie".match(/\w+(?=\spie)/)
```

Output

```text
apple
```

---

# Negative Lookahead

Syntax

```ruby
pattern(?!another_pattern)
```

Meaning

> Match only if the next characters are **not** the specified pattern.

---

## Example

```ruby
puts "cat dog".scan(/\w+(?!\sdog)/).inspect
```

Output

```ruby
["ca", "do", "g"]
```

The above result may surprise you.

Why?

Because Regex keeps searching after a failed match.

A better example is:

```ruby
puts "cat dog".match(/\bcat(?!\sdog)\b/)
```

Output

```ruby
nil
```

Since

```text
cat
```

is followed by

```text
 dog
```

the assertion fails.

---

# Positive Lookbehind

Syntax

```ruby
(?<=pattern)another_pattern
```

Meaning

> Match only if the previous characters match the specified pattern.

---

## Example

```ruby
text = "$250"

puts text.match(/(?<=\$)\d+/)
```

Output

```text
250
```

The dollar sign is checked but not included.

---

## Another Example

```ruby
text = "ID:12345"

puts text.match(/(?<=ID:)\d+/)
```

Output

```text
12345
```

---

# Negative Lookbehind

Syntax

```ruby
(?<!pattern)another_pattern
```

Meaning

> Match only if the previous characters are **not** the specified pattern.

---

## Example

```ruby
text = "A1 B2"

puts text.scan(/(?<!A)\d/).inspect
```

Output

```ruby
["2"]
```

The digit

```text
1
```

is ignored because it is preceded by

```text
A
```

---

# Combining Lookarounds

Lookarounds can be combined.

Example

```ruby
/(?<=\$)\d+(?=USD)/
```

Input

```text
$250USD
```

Output

```text
250
```

Both conditions must be true.

---

# Password Validation Example

Suppose a password must contain

- at least one uppercase letter
- at least one lowercase letter
- at least one digit

Regex

```ruby
/\A(?=.*[A-Z])(?=.*[a-z])(?=.*\d).+\z/
```

Example

```ruby
puts "Ruby123".match?(/\A(?=.*[A-Z])(?=.*[a-z])(?=.*\d).+\z/)
```

Output

```text
true
```

---

# Real World Examples

## Extract Price

```ruby
/(?<=\$)\d+/
```

Input

```text
Price: $500
```

Output

```text
500
```

---

## Extract Percentage

```ruby
/\d+(?=%)/
```

Input

```text
Success Rate: 98%
```

Output

```text
98
```

---

## Extract File Extension

```ruby
/(?<=\.)\w+/
```

Input

```text
report.pdf
```

Output

```text
pdf
```

---

## Match Usernames Ending with Numbers

```ruby
/[a-z]+(?=\d+)/
```

Input

```text
john123
```

Output

```text
john
```

---

# Common Mistakes

## Mistake 1

Thinking lookarounds consume characters.

They do not.

Example

```ruby
/(?<=\$)\d+/
```

matches only

```text
250
```

not

```text
$250
```

---

## Mistake 2

Confusing lookahead with lookbehind.

Remember

```
Lookahead → looks ahead

Lookbehind → looks behind
```

---

## Mistake 3

Using lookarounds when a simple capture group is easier.

Sometimes this

```ruby
/\$(\d+)/
```

is simpler than

```ruby
/(?<=\$)\d+/
```

Choose the most readable solution.

---

# Interview Tips

A common interview question:

What is the difference between

```ruby
\$(\d+)
```

and

```ruby
(?<=\$)\d+
```

Answer

The first captures the number after matching the dollar sign.

The second never matches the dollar sign at all.

---

Another common question:

Why are lookarounds called **zero-width assertions**?

Answer

Because they verify a condition without consuming any characters.

---

# Summary

In this chapter, you learned

- Positive Lookahead
- Negative Lookahead
- Positive Lookbehind
- Negative Lookbehind
- Zero-width assertions
- Password validation using lookaheads
- Practical extraction examples

Lookarounds are one of the most advanced and useful Regex features. They allow you to express conditions cleanly without including those conditions in the matched text.

---

# Practice Questions

## Question 1

Write a Regex that extracts the number from

```text
$999
```

using a lookbehind.

---

## Question 2

Write a Regex that extracts

```text
250
```

from

```text
250kg
```

using a lookahead.

---

## Question 3

What is the difference between

```ruby
(?<=\$)\d+
```

and

```ruby
\$(\d+)
```

---

## Question 4

What does the following Regex validate?

```ruby
/\A(?=.*[A-Z])(?=.*\d).+\z/
```

---

## Question 5

What are the four types of lookarounds?

---

## Question 6

Why are lookarounds called zero-width assertions?

---

## Question 7

Write a Regex that extracts the file extension from

```text
archive.zip
```

using a lookbehind.

---

## Question 8

Write a Regex that extracts the percentage value from

```text
85%
```

using a lookahead.

---

## Question 9

Can lookaheads and lookbehinds be combined in a single Regex? Explain with an example.

---

## Question 10

When would you choose a capture group instead of a lookaround?

---

# Next Chapter

➡ **008-ruby-regex-api.md**