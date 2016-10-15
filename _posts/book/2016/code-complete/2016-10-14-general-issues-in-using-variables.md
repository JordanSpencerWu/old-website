---
categories: [code-complete]
date: 2016-10-14 11:00:00
hidden: true
layout: book-notes
permalink: /general-issues-in-using-variables/
title: "General Issues In Using Variables"
---

Implicit declaration is one of the most hazardous features available in any language. Languages that require you to declare data explicitly are, in essence, requiring you to use data more carefully, which is one of their primary advantages.

> Improper data initialization is one of the most fertile sources of error in computer programming.

Scope, or visibility, refers to the extent to which your variables are known and can be referenced throughout a program. It's always a good idea to localize references to variables by keeping them close together. A variable's life begins at the first statement in which it's referenced; it's life ends at the last statement in which it's referenced. A short live time makes your code more readable, fewer lines of code a reader has to keep in mind at once.

> "Persistence" is another word for the life span of a piece of data.

> "Binding time": the time at which the variable and its value are bound together.

Sequential data consists of clusters of data used together in a certain order. Selective data is a collection in which one of several pieces of data is used at any particular time. Iterative data is the same type of data repeated several times. Your real data can be combination of all three types of data above.