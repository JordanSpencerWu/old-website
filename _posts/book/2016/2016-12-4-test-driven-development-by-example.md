---
author: Kent Beck
categories: [book]
class: 14
date: 2016-12-04 10:00:00
description: Test-driven development is a way of managing fear during programming. TDD is a set of techniques that any software engineer can follow, which encourages simple designs and test suites that inspire confidence. First we'll solve the "that works" part of the problem. Then we'll solve the "clean code" part, removing duplication between test and code as a way to drive the design.
hidden: true
img-path: /assets/images/books/test-driven-development-by-example.jpg
layout: book
permalink: /test-driven-development-by-example/
title: "Test-Driven Development"
---

##### Two Simple Rules

1. Write new code only if an automated test has failed

2. Eliminate duplication

##### The TDD Mantra 

1. Red - Write a little test that doesn't work, and perhaps doesn't even compile at first.

2. Green - Make the test work quickly, committing whatever sins necessary in the process.

3. Refactor - Eliminate all of the duplication created in merely getting the test to work.

##### Three Techniques for Quickly Getting To Green

1. Fake it

2. Use Obvious Implementation

3. Triangulation

The first option is to __fake it__ which means to return a constant and gradually replace constants with variables until you have the real code. For __obvious implementation__ means to type in the real implementation. Lastly, __triangulation__ is used to get the code to compile quickly with a stub implementation and make the test work by typing in what seemed to be the right code.

##### 3A Pattern

1. Arrange - Create some objects

2. Act - Stimulate them

3. Assert - Check the results

##### TDD Patterns

Testing is a very important discipline in the software industry. Having test suites gives developers more confidence in making changes to the code base. This will reduce stress knowing that the changes made will not break the code base and reduces the number of errors. When writing or designing a test make sure the tests are independent from each other by decoupling them. By writing isolated tests, we can achieve high cohesion. Be sure to make a test list, write a list of all the tests you know you will have to write. Remember to test first, when we test first, we reduce the stress, which makes us more likely to test. Lastly, use data that makes the test easy to read and follow, you are writing tests for a reader.

##### Testing Patterns

When writing a test that is too big, try writing a smaller test case that represents the broken part of the bigger test case. When testing an object that relies on an expensive or complicated resource, create a mock object of the resource that answers constants. You may leave the last test broken when taking a break, this will allow you to think about what you wrote and help you continue finishing the test. Always make sure that all of the tests are running before you check in your code.


##### Examples

1. <a href="https://github.com/JordanSpencerWu/TDD-money-example-jUnit" target="_blank">Money Example</a>

2. <a href="https://github.com/JordanSpencerWu/TDD-xUnit-Example" target="_blank">xUnit Example</a>

