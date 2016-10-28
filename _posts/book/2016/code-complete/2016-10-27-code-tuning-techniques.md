---
categories: [code-complete]
date: 2016-10-27 11:00:00
hidden: true
layout: book-notes
permalink: /code-tuning-techniques/
title: "Code-Tuning Techniques"
---

Performance usually refers to both speed and size, but size reductions tend to come more from redesigning classes and data than from tuning code.

Some languages provide a form of expression evaluation known as "short-circuit evaluation," which means that the compiler generates code that automatically stops testing as soon as it knows the answer.

Arrange test so that the one that's fastest and most likely to be true is performed first.

In some circumstances, a table lookup might be quicker than traversing a complicated chain of logic.

If a program uses lazy evaluation, it avoids doing any work until the work is needed.

Switching refers to making a decision inside a loop every time it's executed. If the decision doesn't change while the loop is executing, you can unswitch the loop by making the decision outside the loop.

Jamming, or "fusion" is the result of combining two loops that operate no the same set of elements.

If the loop is a search loop, one way to simplify the test is to use a sentinel value, a value that you put just past the end of the search range and that's guaranteed to terminate the search.

The key to improving the loop is that the outer loop executes much more often than the inner loops, put the busiest loop on the inside.

Reducing strength means replacing an expensive operation such as multiplication with a cheaper operation such as addition.

Change in data types can be a powerful aid in reducing program size and improving execution speed.

Used named constants and literals that are the same type as the variables they're assigned to.

One of the most powerful tools in code tuning is a good routine decomposition. Small, well-defined routines saves space because they take the place of doing jobs separately in multiple places.

Code tuning invariably involves tradeoffs among complexity, readability, simplicity, and maintainability on the one hand and a desire to improve performance on the other.