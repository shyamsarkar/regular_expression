# 003 - Character Classes in Ruby Regular Expressions

> **Goal:** Learn how Character Classes work and how to match specific sets of characters using Regular Expressions in Ruby.

---

# Table of Contents

- What are Character Classes?
- Basic Character Classes
- Character Ranges
- Negated Character Classes
- Escape Sequences
- The Dot (`.`) Character
- Combining Character Classes
- Common Mistakes
- Interview Tips
- Summary
- Practice Questions

---

# What are Character Classes?

A **Character Class** tells Regex to match **exactly one character** from a given set.

Character classes are enclosed inside square brackets.

```ruby
[abc]
```

This means

> Match **either** `a`, `b`, or `c`.

---

# Basic Character Classes

## Match Any One Character

```ruby
/[abc]/
```

Matches

```text
a
b
c
```

Does NOT match

```text
d
x
1
```

Example

```ruby
puts "apple".match(/[abc]/)
```

Output

```text
a
```

---

## Multiple Matches using `scan`

```ruby
text = "banana"

puts text.scan(/[ab]/).inspect
```

Output

```ruby
["b", "a", "a", "a"]
```

---

# Character Ranges

Instead of listing every character individually, use ranges.

---

## Lowercase Letters

```ruby
/[a-z]/
```

Matches

```text
a
b
c
...
z
```

Example

```ruby
puts "Ruby".scan(/[a-z]/).inspect
```

Output

```ruby
["u", "b", "y"]
```

---

## Uppercase Letters

```ruby
/[A-Z]/
```

Example

```ruby
puts "Ruby".scan(/[A-Z]/).inspect
```

Output

```ruby
["R"]
```

---

## Digits

```ruby
/[0-9]/
```

Example

```ruby
puts "Age: 25".scan(/[0-9]/).inspect
```

Output

```ruby
["2", "5"]
```

---

## Hexadecimal Characters

```ruby
/[A-Fa-f0-9]/
```

Example

```ruby
puts "FF00AA".match?(/[A-Fa-f0-9]+/)
```

Output

```text
true
```

---

# Combining Character Classes

You can combine multiple ranges.

```ruby
/[A-Za-z]/
```

Matches

- Uppercase letters
- Lowercase letters

Example

```ruby
puts "Ruby123".scan(/[A-Za-z]/).inspect
```

Output

```ruby
["R", "u", "b", "y"]
```

---

Another example

```ruby
/[A-Za-z0-9]/
```

Matches

- Letters
- Numbers

Example

```ruby
puts "Ruby123".scan(/[A-Za-z0-9]/).inspect
```

Output

```ruby
["R", "u", "b", "y", "1", "2", "3"]
```

---

# Negated Character Classes

Sometimes we want the opposite.

Use

```ruby
[^...]
```

The `^` inside square brackets means

> Match any character **except** these.

---

## Not a Digit

```ruby
/[^0-9]/
```

Example

```ruby
puts "abc123".scan(/[^0-9]/).inspect
```

Output

```ruby
["a", "b", "c"]
```

---

## Not a Letter

```ruby
/[^A-Za-z]/
```

Example

```ruby
puts "Ruby123!".scan(/[^A-Za-z]/).inspect
```

Output

```ruby
["1", "2", "3", "!"]
```

---

# Escape Sequences

Ruby provides shorthand versions for common character classes.

---

## `\d`

Digit

Equivalent to

```ruby
[0-9]
```

Example

```ruby
puts "Age: 25".scan(/\d/).inspect
```

Output

```ruby
["2", "5"]
```

---

## `\D`

Non-digit

Equivalent to

```ruby
[^0-9]
```

Example

```ruby
puts "Age: 25".scan(/\D/).inspect
```

Output

```ruby
["A", "g", "e", ":", " "]
```

---

## `\w`

Word character

Equivalent to

```text
[A-Za-z0-9_]
```

Example

```ruby
puts "hello_world".scan(/\w/).inspect
```

Output

```ruby
["h","e","l","l","o","_","w","o","r","l","d"]
```

Notice that `_` is included.

---

## `\W`

Non-word character

Example

```ruby
puts "hello-world!".scan(/\W/).inspect
```

Output

```ruby
["-", "!"]
```

---

## `\s`

Whitespace

Matches

- Space
- Tab
- Newline

Example

```ruby
puts "Hello World".scan(/\s/).inspect
```

Output

```ruby
[" "]
```

---

## `\S`

Non-whitespace

Example

```ruby
puts "A B".scan(/\S/).inspect
```

Output

```ruby
["A", "B"]
```

---

# Character Class Comparison

| Pattern | Meaning |
|----------|---------|
| `[0-9]` | Digit |
| `\d` | Digit |
| `[^0-9]` | Not a digit |
| `\D` | Not a digit |
| `[A-Za-z]` | Letter |
| `\w` | Letter, digit or underscore |
| `\W` | Not a word character |
| `\s` | Whitespace |
| `\S` | Non-whitespace |

---

# The Dot (`.`) Character

The dot is **not** a character class.

It is a special metacharacter.

```ruby
/.
/
```

It matches **any single character** (except newline by default).

Example

```ruby
puts "cat".match(/c.t/)
```

Output

```text
cat
```

Also matches

```text
cot
cut
c9t
c_t
```

---

# Difference Between `.` and `[.]`

This is a very common interview question.

```ruby
/.
/
```

means

> Match any character.

Whereas

```ruby
/[.]/
```

means

> Match only a literal period (`.`).

Example

```ruby
puts "3.14".match(/[.]/)
```

Output

```text
.
```

---

# Common Mistakes

## Mistake 1

Thinking

```ruby
\w
```

means only letters.

Actually

```text
A-Z
a-z
0-9
_
```

are all included.

---

## Mistake 2

Confusing

```ruby
\d
```

with

```ruby
\D
```

Remember

Uppercase means the opposite.

| Lowercase | Uppercase |
|------------|-----------|
| `\d` | `\D` |
| `\w` | `\W` |
| `\s` | `\S` |

---

## Mistake 3

Using

```ruby
.
```

when you want a literal period.

Wrong

```ruby
/3.14/
```

Correct

```ruby
/3\.14/
```

or

```ruby
/3[.]14/
```

---

# Interview Tips

Interviewers frequently ask:

> What is the difference between

```ruby
[A-Za-z]
```

and

```ruby
\w
```

Answer

```text
[A-Za-z]
```

matches only letters.

```text
\w
```

matches

- letters
- digits
- underscore

---

# Summary

In this chapter, you learned

- Character classes
- Character ranges
- Negated character classes
- Escape sequences
- `\d`
- `\D`
- `\w`
- `\W`
- `\s`
- `\S`
- The difference between `.` and `[.]`

Character classes are one of the most frequently used features in Regular Expressions.

---

# Practice Questions

## Question 1

Write a Regex that matches any lowercase letter.

---

## Question 2

Write a Regex that matches any uppercase letter.

---

## Question 3

Write a Regex that matches any digit.

---

## Question 4

What is the difference between

```ruby
[A-Za-z]
```

and

```ruby
\w
```

---

## Question 5

What is the difference between

```ruby
.
```

and

```ruby
[.]
```

---

## Question 6

Which of the following are matched by `\w`?

```text
A
7
_
#
@
```

---

## Question 7

Write a Regex that matches any character except digits.

---

## Question 8

Write a Regex that extracts all digits from

```text
Order #12345 Amount $999
```

---

## Question 9

Why does

```ruby
/3.14/
```

also match

```text
3a14
```

---

## Question 10

Write a Regex that matches only hexadecimal characters.

---

# Next Chapter

➡ **004-quantifiers.md**