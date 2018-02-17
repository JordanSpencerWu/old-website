---
author: Robert C. Martin
categories: [book]
class: 64
date: 2018-02-17 10:00:00
description: A great book on learning about how software is designed and structured. Robert does an amazing job at providing real world examples of the many different ways of building software and things to think about. Software architect should focus on the business rules and use cases before thinking about the details like database, frameworks, and client. I will recommend this book for any developer who wants to expand their knowledge on software architecture.
hidden: true
img-path: /assets/images/books/clean-architecture.jpg
layout: book
permalink: /clean-architecture/
title: "Clean Architecture - A Craftsman's Guide to Software Structure and Design"
---

When software is done right, it requires a fraction of the human resources to create and maintain. Changes are simple and rapid.

The goal of software architecture is to minimize the human resources required to build and maintain the required system.

Making messes is always slower than staying clean.

Every software system provides two different values to the stakeholders: behavior and structure.

The first value of software is its behavior. Programmers are hired to make machines behave in a way that makes or saves money for the stakeholders.

The second value of software is, it must be easy to change. When the stakeholders change their minds about a feature, that change should be simple and easy to make.

Just remember: If architecture comes last, then the system will become ever more costly to develop, and eventually change will become practically impossible for part or all of the system.

Paradigms are ways of programming, relatively unrelated to languages. A paradigm tells you which programming structures to use, and when to use them.

Structured programming imposes discipline on direct transfer of control.

Object-oriented programming imposes discipline on indirect transfer of control.

Functional programming imposes discipline upon assignment.

Each of the paradigms removes capabilities from the programmer.

We use polymorphism as the mechanism to cross architectural boundaries; we use functional programming to impose discipline on the location of and access to data; and we use structured programming as the algorithmic foundation of our modules. Notice how well those three align with the three big concerns of architecture: function, separation of components, and data management.

Structured programming allows modules to be recursively decomposed into provable units, which in turn means that modules can be functionally decomposed.

"Testing shows the presence, not the absence, of bugs"

Structured programming forces us to recursively decompose a program into a set of small provable functions. We can then use test to try to prove those small provable function incorrect. If such test fails to prove incorrectness, then we deem the functions to be correct enough for our purposes.

The fact that OO languages provide safe and convenient polymorphism means that any source code dependency, no matter where it is, can be inverted. Any source code dependencies can be turned around by inserting an interface between them. (Dependency Inversion)

Software architects working in system written in OO languages have absolute control over the direction of all source code dependencies in the system.

All race conditions, deadlock conditions, and concurrent condition or a concurrent update problem are due to mutable variables.

##### Single Responsibility Principle (SRP)

Software systems are changed to satisfy a group of one or more people, we'll refer to them as an actor and are the "reason to change."

A module should be responsible to one, and only one, actor.

##### Open-Closed Principle (OCP)

A software artifact should be open for extension but closed for modification.

If component __A__ should be protected from changes in component __B__, then component __B__ should depend on component __A__.

##### Liskov Substitution Principle (LSP)

If for each object __o1__ of type __S__ there is an object __o2__ of type __T__ such that for all programs __P__ defined in terms of __T__, the behavior of __P__ is unchanged when __o1__ is substituted for __o2__ then __S__ is a subtype of __T__.

##### Interface Segregation Principle (ISP)

It is harmful to depend on modules that contain more than you need.

##### Dependency Inversion Principle (DIP)

The most flexible system are those in which source code dependencies refer only to abstraction, not to concretions.

It is the volatile concrete element of our system that we want to avoid depending on, therefore interfaces are less volatile than implementations.

Components are the units of deployment, they are the smallest entities that can be deployed as part of a system.

A directed acyclic graph (DAG): Regardless of which component you begin at, it is impossible to follow the dependency relationships and wind up back at that component.

Stability is related to the amount of work required to make a change.

One way to determine the stability of a component is to count the number of dependencies that enter and leaves that component.

Fan-in: Incoming dependencies

Fan-out: Outgoing dependencies

Instability (__I__): __I__ = Fan-out ÷ (Fan-in + Fan-out)

__I__ = 0 indicates a maximally stable component. __I__ = 1 indicates a maximally unstable component.

The changeable component are on top and depend on the stable component at the bottom. The __I__ metrics should decrease in the direction of dependency.

Stable Abstraction Principle (SAP): A stable component should also be abstract so that its stability does not prevent it from being extended. An unstable component should be concrete since its instability allows the concrete code within it to be easily changed.

Good architecture makes the system easy to understand, easy to develop, easy to maintain, and easy to deploy.

Arranging our systems into a plugin architecture creates firewalls across which changes cannot propagate.

Dependency arrows are arranged to point from lower-level details to higher-level abstractions.

Business rules are rules or procedures that make or save the business money.

An Entity is an object within our computer system that embodies a small set of critical business rules operating on Critical Business Data.

A use case is a description of the way that an automated system is used. It specifies the input to be provided by the user, the output to be returned to the user, and the processing steps involved in producing that output.

Good architectures are centered on use cases so that architects can safely describe the structures that support those use cases without committing to frameworks, tools, and environments.

Dependency Rule: Source code dependencies must point only inward, toward higher-level policies.

The Humble Object pattern is a design pattern that was originally identified as a way to help unit testers to separate behaviors that are hard to test from behaviors that are easy to test.

Database gateways are polymorphic interfaces that contain methods for every create, read, update, or delete operation that can be performed by the application on the database.

Data mapper load data into data structures from relational database tables.

Think of Main as a plugin to the application - a plugin that sets up the initial conditions and configurations, gathers all the outside resources, and then hands control over to high-level policy of the application.

Test are the most isolated system component, nothing within the system depends on tests, and the tests always depend inward on the components of the system.

First make it work, then make it right, then make it fast.