---
author: Alvin Alexander
categories: [book]
class: 67
date: 2018-03-17 10:00:00
description: A great to learn about functional programming using the language Scala. The book goes in depth about FP using Scala examples, it would be better if you know Scala before reading. I didn't know Scala but got a general idea of the syntax. I skim through the book to understand the basic of FP.
hidden: true
img-path: /assets/images/books/functional-programming-simplified.jpg
layout: book
permalink: /functional-programming-simplified/
title: "FUNCTIONAL PROGRAMMING SIMPLIFIED"
---

Functional Programming (FP) applications consist of only immutable values and pure functions.

Pure function means that (a) a function's output depends only on its input parameters, and (b) functions have no side effects, such as reading user input or writing output to a screen, disk, web service, etc.

"In FP we don't tell the computer how to do things, we just tell it what we want."

#### FP Rules

1. There will be no null values.
2. Only pure functions will be used.
3. Only use immutable values for all fields.
4. Whenever you use an if, you must always also use an else.
5. We won't create "classes" that encapsulate data and behaviors. Instead we'll create data structures and write pure functions that operate on those data structures.

Higher-Order Function (HOF) means that (a) you can treat a function as a value and (b) you can pass that value into other functions.

"Functional code is characterized by one thing: the absence of side effects."

In modern functional programming, lambda means "anonymous function."

Lambda calculus refers to "a formal way to think about functions."

"Things that can be mapped over shall be called Functor."

Combinator: "a style of organizing libraries centered around the idea of combining things."

A mantra for writing pure functions: Output depends only on input.

Signs of impure functions. They don't have any input parameters and/or they don't return anything.

"Memorization is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls and returning the cached result when the same inputs occur again.

"Expression-Oriented Programming" or EOP means every line of code returns a result (evaluates to a result), and therefore an expression rather than a statement. Statements do not return results and are executes solely for their side effects.

#### Benefits of Pure Functions:

1. They're easier to reason about
2. They're easier to combine
3. They're easier to test
4. They're easier to debug
5. They're easier to parallelize
6. They are idempotent
7. They offer referential transparency
8. They are memoizable
9. They can be lazy

All that the theory of currying means is that a function that takes multiple arguments can be translated into a series of function calls that each take a single argument.

Partially-applied function (PAF) is a function that takes a function with multiple parameters and return a function with fewer parameters. The general benefit it's a way to create specialized methods from more general methods.

A recursive function is a function that calls itself.

#### The general recursive thought process:

1. What is the function signature?
2. What is the end condition for this algorithm?
3. What is the actual algorithm?

A tail-recursive function is a function whose very last action is a call to itself.

In FP you don't modify (mutate) existing objects, you create new objects with updated fields based on existing objects.

List comprehensions are a way to filter, transform, and combine lists.

Pure function never throws exceptions.

"Composition is a fancy term which means 'combining'... Function composition is the process of combining two or more functions to produce a new function. Composing functions together is like snapping together a series of pipes for our data to flow through."

A domain is "a sphere of activity or knowledge."

A domain model refers to the way we model the objects in a given domain as software engineers.