---
author: Ulisses Almeida
categories: [book]
class: 70
date: 2018-06-14 10:00:00
description: This is a good introduction book to the programming language Elixir. I recommend this book to those who like to learn a programming language using code examples and walkthrough.
hidden: true
img-path: /assets/images/books/learn-functional-programming-with-elixir.jpg
layout: book
permalink: /learn-functional-programming-with-elixir/
title: "Learn Functional Programming with Elixir"
---

A programming paradigm consists of the rules and design principles of building software.

In the functional programming paradigm, funcitons are the basic building blocks, all values are immutable, and the code is declarative.

A closure has access to variable values both inside and outside of the code block.

The lexical scope is related to the visibility of the variables in the code where they were defined.

A function arity is the number of arguments a function receivies, commonly expressed as `name_of_the_function/arity`.

The & operator to capture a reference to the function, it's a short way of binding named functions to variables or functions' arguments. We can also use the & operator to create anonymous functions with arity greater than zero.

Elixir pattern matching is useful for assigning variables, unpacking values, and making decisions such as which function to invoke.

We can bind new values for existing variables, this is called rebinding.

We can avoid the rebinding by using the pin operator: `^`.

Pattern matching is also useful for extracting parts of values to variables in a process called destructuring.

A keyword list is a list of two-element tuples: it allows duplicated keys but they must be atoms, are useful for function options.

Sigils are shortcuts to create values with a simplified text representation.

In Elixir we call these multiple function definitions function clauses.

We can apply a default value to named function arguments using the `||` operator.

Guard clauses permit us to add Boolean expresssions in our functions, adding more power to our function clauses.

Create macro functions to be used in guard clauses with the defgaurd directive.

Case is useful when we want to check an expression with multiple pattern-matching clauses.

The cond control flow is useful when you want to check different variables and values in logical expressions.

A bounded recursion is a type of recursive function in which the successive calls to itself have an end. The boundary clause is very important; it should always be defined before the clauses that can be repeated.

Decrease and conquer is a technique for reducing a problem to its simplest form and starting to solve it incrementally.

The divide-and-conquer technique is about separating the problem into two or more parts that can be processed independently and can be combined in the end.

Tail-call optimization is when the compiler reduces functions in memory without allocating more memory. To use it, we need to ensure that the last expression of our function is a function call.

Unbounded recurrsion is when we can't predict the number of repetition for a recursive function.

Higher-order functions are those that have functions in their arguments and/or can return functions.

The pipe operator is useful for combining functions to achieve a greater goal.

A behavior is a contract between a module and the client code that's using it.

You need both pure and impure functions to write useful software. In order to build maintainable software, you should produce more pure functions while isolating the impure parts with proper handling.