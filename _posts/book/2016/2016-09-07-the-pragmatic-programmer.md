---
author: Andrew Hunt & David Thomas
categories: [book]
class: 5
date: 2016-09-07 10:00:00
description: Currently Reading..
hidden: true
img-path: /assets/images/books/the-pragmatic-programmer.jpg
layout: book
permalink: /the-pragmatic-programmer/
title: "The Pragmatic Programmer"
---

##### A Pragmatic Philosophy

Invest in your knowledge portfolio, your knowledge and experience are your most important professional assets.

> An investment in knowledge always pays the best interest.

> Benjamin Franklin

##### A Pragmatic Approach

During development focus on orthogonality by reducing duplication in the system, remember to use Tracer Code or Prototyping when implementing new features.

##### The Basic Tools

Every craftsman starts his or her journey with tools, spend time learning to use these tools, and at some point you'll be surprised to discover your fingers moving over the keyboard, manipluating text without conscious thought. The tools well have become extensions of your hands.

##### Pragmatic Paranoia

Perfect software doesn't exist, use this to your advantage by applying techniques that test for the correctness of your code.

> You can't write perfect software.

##### Bend, or Break

The world is constantly changing, so does your code, focus on producing flexible and adaptable software.

##### While You Are Coding

Developers who don't actively think about their code or programming by coincidence - the code might work, but there's no particular reason why.

> Avoid programming by coincidence - relying on luck and accidental successes - in favoring of programming deliberately.


##### Before the Project

To be continued...

#### Terms

__Entropy__ is a term from physics that refers to the amount of "disorder" in a system. When disorder increases in software, programmers call it "software rot".

__Don't Repeat Yourself (DRY)__, every piece of knowledge must have a single, unambiguous, authoritative representation within a system.

__Orthogonality__, two or more things are orthogonal if changes in one do not affect any of the others.

__Cohesion__, components that are self-contained: independent, and with a single, well-defined purpose.

__Reversibility__ means producing flexible and adaptable software.

__Tracer code__ is not disposable: you write it for keeps. It contains all the error checking, structuring, documentation, and self-checking that any piece of production code has.

__Prototyping__ generates disposable code.

__Tracing statements__ are used to watch the state of a program or a data structure over time.

__Rubber Ducking__ a useful technique for finding the cause of a problem is simply to explain it to someone else.

__Code Generators__ are code that writes code, task of producing the same code over and over again.

__Design by Contract (DBC)__ a powerful technique that focuses on documenting (and agreeing to) the rights and responsibilities of software modules to ensure program correctness.

__Lazy code__: be strict in what you will accept before you begin, and promise as little as possible in return. 

__Coupling__, the dependencies among modules of code.

__Shy code__: don't reveal yourself to others, and don't interact with too many people.

__Decoupling__, reducing the dependencies among modules of code.

__Law of Demeter for functions__ attempts to minimize coupling between modules in any given program.

__Metadata__ is any data that describes the application - how it should run, what resources it should use, and so on.

__Temporal coupling__ is about time dependencies.

__Concurrency__ are things happening at the same time.

__Model-View-Controller (MVC)__: separating the model from both the GUI that represents it and the controls that manage the view.

__Big O Notation__: estimating the resources that algorithms use - time, processor, memory, and so on.

1. Access Array => __O(1)__
2. Simple loops => __O(n)__
3. Nested loops => __O(m x n)__
4. Binary chop => __O(lg(n))__
5. Divide and Conquer => __(n lg(n))__

__Premature optimization__: a good idea to make sure an algorithm really is a bottleneck before investing your precious time trying to improve it.

__Refactoring__: rewriting, reworking, and re-architecting code.

__Unit Testing__: testing done on each module, in isolation, to verify its behavior.

__Testing against contract__ tells us two things: whether the code meets the contract, and whether the contracts means what we think it means.