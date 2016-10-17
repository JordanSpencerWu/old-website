---
categories: [code-complete]
date: 2016-10-17 11:00:00
hidden: true
layout: book-notes
permalink: /unusual-data-types/
title: "Unusual Data Types"
---

The term "structure" refers to data that's built up from other types. Deals with user-created structured data - _structs_ in C and C++ and _structures_ in Microsoft Visual Basic. Classes also sometimes perform as structures (when the class consists entirely of public data members with no public routines).

Conceptually, every pointer consists of two parts: a location in memory and a knowledge of how to interpret the contents of that location. The location in memory is an address, the pointer itself contains only this address. To use the data the pointer points to, you have to go to that address and interpret the contents of memory at that location.

Global variables are accessible anywhere in a program. Most experienced programmers have concluded that access to data from several routines is pretty useful. Anything you can do with global data, you can do better with access routines. The use of access routines is a core technique for implementing abstract data types and achieving information hiding.