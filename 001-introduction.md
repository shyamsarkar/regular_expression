# 001 - Introduction to Regular Expressions (Regex) in Ruby

> **Goal:** Understand what Regular Expressions are, why they exist, where they are used, and how Ruby supports them.

---

# Table of Contents

- What is a Regular Expression?
- Why do we need Regex?
- Where is Regex used?
- Regex in Ruby
- Your First Regex
- How Regex Works
- Common Terminology
- When NOT to Use Regex
- Summary
- Practice Questions

---

# What is a Regular Expression?

A **Regular Expression (Regex)** is a sequence of characters that defines a **search pattern**.

Instead of searching for exact text, Regex allows us to search for **patterns**.

Think of Regex as a language for describing text.

Examples:

- Find all numbers
- Find all email addresses
- Find phone numbers
- Validate passwords
- Extract dates
- Replace unwanted characters

---

# Why do we need Regex?

Imagine you have the following text:

```text
John - john@gmail.com
Alice - alice@yahoo.com
Bob - bob@hotmail.com
```

Suppose you want only the email addresses.

Without Regex, you would need to manually process every line.

With Regex:

```ruby
text.scan(/\S+@\S+/)
```

Output

```ruby
[
  "john@gmail.com",
  "alice@yahoo.com",
  "bob@hotmail.com"
]
```

Regex allows us to describe *what we want* instead of writing long parsing logic.

---

# Real World Uses

Regex is used almost everywhere.

## User Validation

- Email validation
- Phone number validation
- Username validation
- Password validation

Example

```ruby
email.match?(...)
```

---

## Data Extraction

Extract

- Names
- Emails
- Dates
- Prices
- URLs

Example

```text
Order Total: $450
```

Regex can extract

```text
450
```

---

## Text Replacement

Replace

```text
This    has     extra      spaces
```

with

```text
This has extra spaces
```

using

```ruby
gsub
```

---

## Log Parsing

Example

```text
ERROR 2025-12-30 User not found
```

Extract

- Log level
- Date
- Message

---

## Ruby on Rails

Regex is commonly used in

- Model validations
- Route constraints
- Importing CSV files
- Parsing logs
- Cleaning user input
- Background jobs
- API request validation

---

# Regex in Ruby

Ruby has built-in support for Regular Expressions.

A regex is written between two forward slashes.

```ruby
/ruby/
```

This creates a **Regexp** object.

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

# Your First Regex

Suppose we have

```ruby
text = "I love ruby"
```

Search for

```ruby
/ruby/
```

```ruby
puts text.match(/ruby/)
```

Output

```text
ruby
```

---

Another example

```ruby
puts "I love python".match(/ruby/)
```

Output

```ruby
nil
```

---

# How Regex Works

Imagine

```text
I love ruby programming
```

Regex starts scanning from the beginning.

```text
I love ruby programming
^
```

No match.

Move one character.

```text
I love ruby programming
 ^
```

Still no match.

Continue...

```text
I love ruby programming
       ^
```

Now

```text
ruby
```

matches.

Regex stops and returns the match.

---

# Common Terminology

## Pattern

The expression we write.

Example

```ruby
/\d+/
```

---

## Match

The text that satisfies the pattern.

Pattern

```ruby
/\d+/
```

Text

```text
Age: 25
```

Match

```text
25
```

---

## Search

Looking through text to find a match.

---

## Capture

Saving a matched value for later use.

Example

```ruby
/(\d+)/
```

captures

```text
123
```

---

## Replace

Changing matched text into something else.

Example

```ruby
gsub(/\d/, "")
```

---

# When NOT to Use Regex

Regex is powerful, but it is not always the best solution.

Avoid Regex when a simple Ruby method is easier to understand.

Instead of

```ruby
text =~ /^Hello/
```

prefer

```ruby
text.start_with?("Hello")
```

---

Instead of

```ruby
text =~ /world$/
```

prefer

```ruby
text.end_with?("world")
```

---

Instead of

```ruby
text =~ /ruby/
```

prefer

```ruby
text.include?("ruby")
```

---

Good developers know **when not to use Regex**.

---

# Summary

In this chapter, you learned

- What Regex is
- Why Regex exists
- Real-world applications
- How Ruby supports Regex
- Basic matching
- Important terminology
- When Regex should not be used

In the next chapter, we'll learn the building blocks of every Regular Expression.

---

# Practice Questions

## Question 1

What is a Regular Expression?

---

## Question 2

Name five real-world uses of Regex.

---

## Question 3

Which Ruby class represents a regular expression?

---

## Question 4

What does the following return?

```ruby
"hello".match(/world/)
```

---

## Question 5

When should you use `include?` instead of Regex?

---

# Next Chapter

➡ **002-ruby-regex-basics.md**