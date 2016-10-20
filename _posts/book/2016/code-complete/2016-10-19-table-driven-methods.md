---
categories: [code-complete]
date: 2016-10-19 12:00:00
hidden: true
layout: book-notes
permalink: /table-driven-methods/
title: "Table-Driven Methods"
---

A table-driven methods is a scheme that allows you to loop up information in a table rather than using logic statements (if and case) to figure it out. Used in appropriate circumstances, table-driven code is simpler than complicated logic, easier to modify, and more efficient.

When you use table-driven methods, you have to address two issues. First you have to address the question of how to look up entries in the table. Then second issue you have to address is what you should store in the table.

_Direct-access_ table replace more complicated logical control structure, they are "direct access" because you don't have to jump through any complicated hoops to find the information you want in the table.

When you use _indexed access_ scheme, you use the primary data to look up a key in a index table and then you use the value from the index table to look up the main data you're interested in.

The general idea of _stair-step access_ table, is that entries in a table are valid for ranges of data rather for distinct points.