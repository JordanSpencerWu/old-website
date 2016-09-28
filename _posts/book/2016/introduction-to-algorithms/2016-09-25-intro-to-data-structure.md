---
categories: [introduction-to-algorithms-elementary-data-structures]
date: 2016-09-25 12:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /introduction-to-data-structures/
title: "Introduction To Data Structures"
---

Sets are __dynamic__, the sets can be manipulated by algorithms can grow, shrink, or change over time. A __dictionary__ are dynamic set that supports the following operations: insert elements into, delete elements from, and test membership in a set.

In a typical implementation of a dynamic set, each element is represented by an object whose attributes can be examined and manipulated if we have a pointer to the object. Some kinds of dynamic sets assume that one of the object's attributes is an identifying __key__. The object may contain __satellite data__, which are carried around in other object attributes but are otherwise unused by the set implementation.

##### Operations on dynamic sets

> Operations on a dynamic set can be grouped into two categories: __queries__, which simply return information about the set, and __modifying operations__, which change the set.

##### SEARCH(S,k)

A query that, given a set $S$ and a key value $k$, return a pointer $x$ to an element in $S$ such that $x.key = k$, or $NIL$ if no such element belongs to $S$.

##### INSERT(S,x)

A modifying operation that augments the set $S$ with the element pointed to by $x$. We usually assume that any attributes in element $x$ needed by the set implementation have already been initialized.

##### DELETE(S,x)

A modifying operation that, given a pointer $x$ to an element in the set $S$, removes $x$ from $S$. (Note that this operation takes a pointer to an element $x$, not a key value.)

##### MINIMUM(S)

A query on a totally ordered set $S$ that returns a pointer to the element of $S$ with the smallest key.

##### MAXIMUM(S)

A query on a totally ordered set $S$ that returns a pointer to the element of $S$ with the largest key.

##### SUCCESSOR(S,x)

A query that, given an element $x$ whose key is from a totally ordered set $S$, return a pointer to the next larger element in $S$, or $NIL$ if $x$ is the maximum element.

##### PREDECESSOR(S,x)

A query that, given an element $x$ whose key is from a totally ordered set $S$, return a pointer to the next smaller element in $S$, or $NIL$ if $x$ is the minimum element.