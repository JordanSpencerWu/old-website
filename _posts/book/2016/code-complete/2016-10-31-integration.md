---
categories: [code-complete]
date: 2016-10-31 12:00:00
hidden: true
layout: book-notes
permalink: /integration/
title: "Integration"
---

The term "integration" refers to the software development activity in which you combine separate software components into a single system. The order in which you build class or components affects the order in which you can integrate them, you can't integrate something that hasn't been built yet. If you construct and integrate software in the wrong order, it's harder to code, harder to test, and harder to debug.

__Phased integration__, follow these well-defined steps:

1. Design, code, test, and debug each class. This step is called "unit development."

2. Combine the classes into one whopping-big system ("system integration").

3. Test and debug the whole system. This is called "system dis-integration."

One problem with phased integration is that when the classes in a system are put together for the first time, new problems inevitably surface and the causes of the problem could be anywhere.

In __incremental integration__, you write and test a program in small pieces and then combine the pieces one at a time, it follow these steps:

1. Develop a small, functional part of the system. Thoroughly test and debug it.

2. Design, code, test, and debug a class.

3. Integrate the new class with the small functional part of the system then test and debug. Make sure they work before adding new classes.

Planning for integration affects planning for construction, the order in which components are constructed has to support the order in which they will be integrated.

Whatever integration strategy you select, a good approach to integrating the software is the "daily build and smoke test." Every file is compiled, linked, and combined into an executable program every day, and the program is then put through a "smoke test", a relatively simple check to see whether the product "smokes" when it runs.