---
categories: [code-complete]
date: 2016-10-27 10:00:00
hidden: true
layout: book-notes
permalink: /code-tuning-strategies/
title: "Code-Tuning Strategies"
---

Strategic performance issues: what performance is, how important it is, and the general approach to achieving it. Code tuning is one way of improving a program's performance.

> Users are more interested in tangible program characteristics than they are in code quality.

Code tuning is the practice of modifying correct code in ways that make it run more efficiently. "Tuning" refers to small-scale changes that affect a single class, a single routine, or, more commonly, a few lines of code.

Use a high-quality design. Make the program right. Make it modular and easily modifiable so that it's easy to work on later. When it's complete and correct, check the performance.

When shopping for a compiler, compare the performance of each compiler on your program. Each compiler has different strengths and weaknesses, and some will be better suited to your program than others.

You always have to profile the program to know with any confidence which parts are slow and fat.