---
author: Andrew Hunt & David Thomas
categories: [book]
class: 4
date: 2016-09-07 10:00:00
description: The road to mastering your software craftsmanship is to constantly invest in your learning. This book shows you how a pragmatic programmer create clean, flexible, and adaptable code. Everything you need to know about working on a project and more! 
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

Requirement gathering rarely lie on the surface. Normally, they're buried deep beneath layers of assumptions, misconceptions, and politics.

> Work with a user to think like a user

##### Pragmatic Projects

The success of a project is measured by how well it meets the expectations of its users.

> The Golden Rule ("Do unto others as you would have them do unto you")

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

__Documenting Requirements__, you want to write likely scenarios that describe what the application need to do and publish a document that everyone can use as a basis for discussions - the developers, the end users, and the project sponsors.

__Use cases__: describe a particular use of the system - not in terms of user interface, but in a more abstract fashion.

__Requirements__ are not architecture. Requirements are not designs, nor are they the user interface. Requirements are need.

__Project glossary__ - one place that defines all the specific terms and vocabulary used in a project.

__Project specification__ is the process of taking a requirement and reducing it down to the point where a programmer's skill can take over.

__Seamless approach__: specification and implementation are simply different aspects of the same process - an attempt to capture and codify a requirement.

__Quality officer__ - someone to whom the team delegates the responsibility for the qualiy of the deliverable.

__Chief water tester__: this person check constantly for increased scope, decreased time scales, additional features, new environments - anything that wasn't in the original agreement.

__Project librarian__: responsible for coordinating documentation and code repositories.

__Tool Builders__: to construct and deploy the tools that automate the project drudgery.

A __build__ is a procedure that takes on empty directory and builds the project from scratch, producing whatever you hope to produce as a final deliverable.

__Final builds__: which you intend to ship as products, may have different requirement from the regular nightly build.

__Integration testing__ shows that the major subsystem that make up the project work and play well with each other.

__Real-world conidtions__, in the real world, your programs don't have limitless resources; they run out of things.

__Regression test__ compares the output of the current test with previous (or known) values.

__Test data__: there are only two kinds of data: real-world data and synthetic data.

__Coverage analysis__ tools watch your code during testing and keep track of which lines of code have been executed and which haven't.

__Internal documentation__ includes source code comments, design and test document, and so on.

__External documentation__ is anything shipped or published to the outside world, such as user manuals. 