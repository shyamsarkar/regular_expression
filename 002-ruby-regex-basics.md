# 002 - Ruby Regex Basics

> **Goal:** Learn the fundamental building blocks of every Regular Expression in Ruby.

---

# Table of Contents

- What is a Regex Pattern?
- Creating a Regex
- The Regexp Class
- Searching Text
- The `=~` Operator
- The `match` Method
- The `match?` Method
- Regex Literals vs `Regexp.new`
- Escaping Special Characters
- Summary
- Practice Questions

---

# What is a Regex Pattern?

A **Regex Pattern** is a sequence of characters that describes what we want to search for.

Examples

```ruby
/ruby/
/hello/
/123/
/cat/
```

Each of these patterns searches for the exact text inside the forward slashes.

---

# Creating a Regex

Ruby represents Regular Expressions using the `Regexp` class.

The most common way to create one is with forward slashes.

```ruby
/ruby/
```

This is called a **Regex Literal**.

Example

```ruby
pattern = /ruby/

puts pattern.class
```

Output

```text
Regexp
```

---

# The Regexp Class

Every Regex in Ruby is an object of the `Regexp` class.

```ruby
pattern = /rails/

puts pattern.class
```

Output

```text
Regexp
```

You can also inspect it.

```ruby
pattern = /ruby/

puts pattern.inspect
```

Output

```text
/ruby/
```

---

# Searching Text

Suppose we have

```ruby
text = "I love Ruby and Rails"
```

Search for the word "Ruby".

```ruby
puts text.match(/Ruby/)
```

Output

```text
Ruby
```

If the pattern is not found

```ruby
puts text.match(/Python/)
```

Output

```ruby
nil
```

---

# The `=~` Operator

The `=~` operator searches for a pattern and returns the **index of the first match**.

Example

```ruby
text = "I love Ruby"

puts text =~ /Ruby/
```

Output

```text
7
```

If nothing matches

```ruby
puts text =~ /Python/
```

Output

```ruby
nil
```

---

## Why is the result 7?

```text
I love Ruby
01234567890
       ^
```

The letter **R** starts at index **7**.

---

# The `match` Method

The `match` method returns a **MatchData** object.

Example

```ruby
text = "Ruby on Rails"

result = text.match(/Ruby/)

puts result.class
```

Output

```text
MatchData
```

To get the matched text

```ruby
puts result[0]
```

Output

```text
Ruby
```

---

# The `match?` Method

Sometimes we only need to know whether a pattern exists.

Instead of returning a `MatchData` object, `match?` returns `true` or `false`.

Example

```ruby
text = "Ruby"

puts text.match?(/Ruby/)
```

Output

```text
true
```

Example

```ruby
puts text.match?(/Python/)
```

Output

```text
false
```

### Why use `match?`

It is faster than `match` because it does **not** create a `MatchData` object.

Use `match?` when you only need a boolean result.

Example

```ruby
if email.match?(EMAIL_REGEX)
  puts "Valid Email"
end
```

---

# Comparing `=~`, `match`, and `match?`

| Method | Returns | Best Used For |
|---------|----------|---------------|
| `=~` | Index or `nil` | Finding the first match position |
| `match` | `MatchData` or `nil` | Extracting matched values |
| `match?` | `true` or `false` | Validation |

---

# Regex Literals vs `Regexp.new`

Most Ruby developers write Regex like this

```ruby
/ruby/
```

However, Regex can also be created dynamically.

```ruby
Regexp.new("ruby")
```

Both create the same object.

```ruby
puts /ruby/.class

puts Regexp.new("ruby").class
```

Output

```text
Regexp
Regexp
```

Use `Regexp.new` only when the pattern needs to be built dynamically.

Example

```ruby
word = "rails"

pattern = Regexp.new(word)

puts "I love rails".match?(pattern)
```

Output

```text
true
```

---

# Escaping Special Characters

Some characters have special meanings in Regex.

Examples

```text
.
+
*
?
(
)
[
]
{
}
|
\
^
$
```

If you want to match them literally, you must escape them with a backslash (`\`).

Example

```ruby
puts "3.14".match?(/\./)
```

Output

```text
true
```

Without escaping

```ruby
/.
/
```

the dot means **any single character**, not a literal period.

---

# Common Mistakes

## Mistake 1

Searching with

```ruby
/ruby/
```

does **not** ignore case.

```ruby
"Ruby".match?(/ruby/)
```

Output

```text
false
```

To ignore case

```ruby
"Ruby".match?(/ruby/i)
```

Output

```text
true
```

---

## Mistake 2

Confusing `match` with `match?`

```ruby
text.match(...)
```

returns a `MatchData` object.

```ruby
text.match?(...)
```

returns only `true` or `false`.

---

## Mistake 3

Assuming `=~` returns `true`

```ruby
puts "Ruby" =~ /Ruby/
```

Output

```text
0
```

It returns the starting **index**, not a boolean.

---

# Interview Tips

✅ Know the difference between:

- `=~`
- `match`
- `match?`

Interviewers ask this surprisingly often.

Also remember that `match?` is preferred for validations because it avoids creating unnecessary objects.

---

# Summary

In this chapter, you learned

- What a Regex pattern is
- The `Regexp` class
- Regex literals
- `Regexp.new`
- The `=~` operator
- `match`
- `match?`
- Escaping special characters
- Common beginner mistakes

In the next chapter, we'll learn **Character Classes**, one of the most important concepts in Regular Expressions.

---

# Practice Questions

## Question 1

What is the class of `/ruby/`?

---

## Question 2

What does the following code return?

```ruby
"Ruby".match(/Ruby/)
```

---

## Question 3

What does the following return?

```ruby
"Ruby" =~ /Ruby/
```

---

## Question 4

Which method is better for validation?

- `match`
- `match?`

Why?

---

## Question 5

Create a Regex that matches the word

```text
Rails
```

---

# Next Chapter

➡ **003-character-classes.md**