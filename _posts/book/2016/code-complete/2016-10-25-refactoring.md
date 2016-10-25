---
categories: [code-complete]
date: 2016-10-25 10:00:00
hidden: true
layout: book-notes
permalink: /refactoring/
title: "Refactoring"
---

Software evolution is like biological evolution in that some mutations are beneficial evolution and many mutation are not. The key distinction between kinds of software evolution is whether the program's quality improves or degrades under modification. A second distinction is the one between changes made during construction and those made during maintenance.

The Cardinal Rule of Software Evolution is that evolution should improve the internal quality of the program. When you have to make change, strive to improve the code so that future changes are easier. The key strategy is refactoring, "a change made to the internal structure of the software to make it easier to understand and cheaper to modify without changing its observable behavior."