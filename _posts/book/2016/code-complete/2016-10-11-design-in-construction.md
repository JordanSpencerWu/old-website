---
categories: [code-complete]
date: 2016-10-11 14:00:00
hidden: true
layout: book-notes
permalink: /design-in-construction/
title: "Design in Construction"
---

The phrase "software design" means the conception, invention, or contrivance of a scheme for turning a specification for computer software into operational software. Design is the activity that links requirements to coding and debugging.

A "wicked" problem as one that could be clearly defined only by solving it, or by solving part of it. This paradox implies that you have to "solve" the problem once in order to clearly define it and then solve it again to create a solution that works.

Good design depends on understanding the importance of managing complexity by dividing the system into subsystems. The more independent the subsystem are, the more you make it safe to focus on one bit of complexity at a time. There's a list of desirable characteristics of a Design: Minimal complexity, Ease of maintenance, Loose coupling, Extensibility, Reusability, High fan-in, Low-to-medium fan-out, portability, Leanness, and Stratification.

It's important to decouple subsystem by only allowing "need to know" communication. A program shouldn't contain any circular relationships in which Class A uses Class B, Class B uses Class C, and Class C uses Class A. Here are the level of Design: level 1: Software System, Level 2: Division into Subsystems or Packages, Level 3: Division into Classes, Level 4: Division into Routines, and Level 5: Internal Routine Design.

Abstraction is the ability to engage with a concept while safely ignoring some of its details. From the complexity point of view, the principal benefit of abstraction is that it allows you to ignore irrelevant details. Good programmers create abstractions at many levels of design. A base class are abstractions that allow you to focus on common attributes of a set of derived classes and ignore the details of the specific classes while you're working on the base class.

Encapsulation picks up where abastraction leaves off, encapsulation helps to manage complexity by forbidding you to look at the complexity. In designing a software system, you'll often find objects that are much like other objects, except for a few differences. Defining similarities and differences among such objects is called "inheritance".