# R Basics Tutorial

Welcome to the R basics tutorial. In this guide, you'll learn the fundamental concepts of R programming.

## Table of Contents

- [R Basics Tutorial](#r-basics-tutorial)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Variables and Data Types](#variables-and-data-types)
    - [Variables](#variables)
    - [Data Types](#data-types)
  - [Control Structures](#control-structures)
    - [If Statement](#if-statement)
    - [For Loop](#for-loop)
    - [While Loop](#while-loop)
  - [Functions](#functions)
  - [Input and Output](#input-and-output)
    - [Input](#input)
    - [Output](#output)
  - [Conclusion](#conclusion)

## Introduction

R is a powerful and widely-used programming language for statistical computing and graphics. This tutorial covers the basics that every R programmer should know.

## Variables and Data Types

### Variables

In R, a variable is a container for storing data values.

```r
x <- 5
y <- "Hello, World!"
```

### Data Types

R supports various data types including vectors, lists, matrices, arrays, factors, data frames, and others. Here are some basic examples:

```r
# Numeric
numeric_vector <- c(1, 2, 5.5, 6.6)

# Character
character_vector <- c("Hello", "World")

# Boolean (Logical)
logical_vector <- c(TRUE, FALSE, T, F)
```

## Control Structures

### If Statement

The `if` statement in R is used to execute a block of code only if a specified condition is true.

```r
x <- 10
if (x > 5) {
  print("x is greater than 5")
}
```

### For Loop

The `for` loop in R is used to iterate over a sequence (vector, list).

```r
fruits <- c("apple", "banana", "cherry")
for (fruit in fruits) {
  print(fruit)
}
```

### While Loop

The `while` loop allows you to execute a block of code as long as a condition is true.

```r
i <- 1
while (i < 6) {
  print(i)
  i <- i + 1
}
```

## Functions

A function is a block of code that only runs when it is called. You can pass data, known as arguments, into a function.

```r
greet <- function(name) {
  print(paste("Hello,", name, "!"))
}

greet("Alice")
```

## Input and Output

### Input

To get input from the user in R, you can use the `readline()` function.

```r
name <- readline(prompt="Enter your name: ")
print(paste("Hello,", name))
```

### Output

Use the `print()` function to output data to the standard output device.

```r
print("Hello, R!")
```

## Conclusion

Congratulations! You've covered the basics of R programming. Continue practicing to enhance your understanding and skills.