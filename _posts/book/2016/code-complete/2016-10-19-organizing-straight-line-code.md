---
categories: [code-complete]
date: 2016-10-19 08:00:00
hidden: true
layout: book-notes
permalink: /organizing-straight-line-code/
title: "Organizing Straight-Line Code"
---

Although organizing straight-line code is a relatively simple task, some organizational subtleties influence code quality, correctness, readability, and maintainability.

The easiest sequential statements to order are those in which the order counts. When statements have dependencies that require you to put them in a certain order, take steps to make the dependencies clear.

You might encounter cases in which one statement doesn't depend on, or logically follow, a statement. But ordering affects readability, performance, and maintainability. Use this guiding principle called Principle of Proximity: _keep related actions together_. They can be related because they operate on the same data, perform similar tasks, or depend on each other's being performed in order.