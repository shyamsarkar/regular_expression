# 006 - Groups and Capturing in Ruby Regular Expressions

> **Goal:** Learn how to group patterns, capture matched values, use named captures, and understand backreferences in Ruby.

---

# Table of Contents

- What are Groups?
- Why do we need Groups?
- Capturing Groups
- Accessing Captured Values
- Multiple Groups
- Non-Capturing Groups
- Named Capture Groups
- `captures`
- `named_captures`
- Backreferences
- Groups with Quantifiers
- Real World Examples
- Common Mistakes
- Interview Tips
- Summary
- Practice Questions

---

# What are Groups?

Groups are created using parentheses.

```ruby
(pattern)
```

A group allows us to:

- Capture matched values
- Apply quantifiers to multiple characters
- Reuse matched text with backreferences
- Organize complex regex patterns

---

# Why do we need Groups?

Suppose we want to match a date:

```text
2025-12-28
```

Without groups, we can match the date:

```ruby
/\d{4}-\d{2}-\d{2}/
```

But we cannot easily extract:

- Year
- Month
- Day

With groups:

```ruby
/(\d{4})-(\d{2})-(\d{2})/
```

Now each part is captured separately.

---

# Capturing Groups

```ruby
date = "2025-12-28"

match = date.match(/(\d{4})-(\d{2})-(\d{2})/)
```

---

# Accessing Captured Values

```ruby
puts match[0]
```

Output

```text
2025-12-28
```

`match[0]` always contains the **entire match**.

---

```ruby
puts match[1]
```

Output

```text
2025
```

---

```ruby
puts match[2]
```

Output

```text
12
```

---

```ruby
puts match[3]
```

Output

```text
28
```

---

# Multiple Groups

```ruby
text = "John Doe"

match = text.match(/(\w+)\s(\w+)/)
```

| Index | Value |
|-------:|-------|
| 0 | John Doe |
| 1 | John |
| 2 | Doe |

---

# The `captures` Method

Instead of reading each group individually:

```ruby
match.captures
```

Example

```ruby
date = "2025-12-28"

match = date.match(/(\d{4})-(\d{2})-(\d{2})/)

puts match.captures.inspect
```

Output

```ruby
["2025", "12", "28"]
```

---

# Non-Capturing Groups

Sometimes we want grouping but do **not** need to capture the result.

Syntax

```ruby
(?:pattern)
```

Example

```ruby
/colou(?:r)?/
```

Matches

```text
color
colour
```

without creating an additional capture group.

---

# Why Use Non-Capturing Groups?

Compare

```ruby
/(ab)+/
```

with

```ruby
/(?:ab)+/
```

Both match

```text
ab
abab
ababab
```

The second version groups the pattern but does not store it.

---

# Named Capture Groups

Ruby supports named capture groups.

Syntax

```ruby
/(?<name>pattern)/
```

Example

```ruby
date = "2025-12-28"

match = date.match(
  /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/
)

puts match[:year]
puts match[:month]
puts match[:day]
```

Output

```text
2025
12
28
```

---

# The `named_captures` Method

```ruby
puts match.named_captures.inspect
```

Output

```ruby
{
  "year"=>"2025",
  "month"=>"12",
  "day"=>"28"
}
```

---

# Backreferences

A backreference allows us to reuse a previously captured value.

Syntax

```ruby
\1
\2
\3
```

---

# Example: Repeated Word Detection

```ruby
text = "the the cat"

match = text.match(/\b(\w+)\s+\1\b/)
```

Explanation

- `(\w+)` captures `"the"`
- `\1` requires the exact same word again

Result

```text
the the
```

---

Example

```ruby
puts "hello hello".match?(/\b(\w+)\s+\1\b/)
```

Output

```text
true
```

---

# Groups with Quantifiers

Quantifiers can be applied to an entire group.

Example

```ruby
/(ha){3}/
```

Matches

```text
hahaha
```

---

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

---

# Real World Examples

## Email Parsing

```ruby
email = "john.doe@gmail.com"

match = email.match(
  /(?<user>[\w.]+)@(?<domain>[\w.]+\.\w+)/
)

puts match[:user]
puts match[:domain]
```

Output

```text
john.doe
gmail.com
```

---

## Order Parsing

```ruby
text = "Order ID=12345 Amount=999"

match = text.match(
  /ID=(?<id>\d+)\s+Amount=(?<amount>\d+)/
)

puts match[:id]
puts match[:amount]
```

Output

```text
12345
999
```

---

## Name Extraction

```ruby
text = "Alice Johnson"

match = text.match(
  /(?<first>\w+)\s(?<last>\w+)/
)

puts match[:first]
puts match[:last]
```

Output

```text
Alice
Johnson
```

---

# Common Mistakes

## Mistake 1

Forgetting that

```ruby
match[0]
```

contains the entire match.

Captured groups begin at

```ruby
match[1]
```

---

## Mistake 2

Using a capturing group when a non-capturing group is sufficient.

```ruby
(?:...)
```

is often the better choice.

---

## Mistake 3

Using a backreference without creating a capture group.

Incorrect

```ruby
/\w+\s+\1/
```

Correct

```ruby
/(\w+)\s+\1/
```

---

## Mistake 4

Confusing named capture groups with hash syntax.

Correct

```ruby
/(?<year>\d{4})/
```

Incorrect

```ruby
/{year:\d{4}}/
```

---

# Interview Tips

### Difference between

```ruby
(ab)+
```

and

```ruby
(?:ab)+
```

Answer

- `(ab)+` captures the group.
- `(?:ab)+` groups the pattern without capturing it.

---

### What does `match[0]` contain?

Always answer:

> The complete matched string.

---

# Summary

In this chapter, you learned

- Capturing groups
- Accessing captured values
- `captures`
- Non-capturing groups
- Named capture groups
- `named_captures`
- Backreferences
- Groups with quantifiers
- Practical parsing examples

Groups are one of the most powerful Regex features and are heavily used for extracting structured data.

---

# Practice Questions

## Question 1

Write a Regex that captures:

- Year
- Month
- Day

from

```text
2026-07-03
```

---

## Question 2

What is the difference between

```ruby
(ab)+
```

and

```ruby
(?:ab)+
```

---

## Question 3

What does

```ruby
match[0]
```

return?

---

## Question 4

Write a named capture group for a phone number.

---

## Question 5

How would you access the named group `:year`?

---

## Question 6

Write a Regex that detects repeated words such as

```text
hello hello
```

---

## Question 7

What does

```ruby
captures
```

return?

---

## Question 8

What does

```ruby
named_captures
```

return?

---

## Question 9

Write a Regex that extracts the username and domain from

```text
alice@example.com
```

using named capture groups.

---

## Question 10

Why might a non-capturing group be preferred over a capturing group?

---

# Next Chapter

➡ **007-lookarounds.md**