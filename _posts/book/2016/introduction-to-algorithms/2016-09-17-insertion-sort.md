---
categories: [introduction-to-algorithms]
date: 2016-09-17 10:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /insertion-sort/
title: "Insertion Sort"
---

This is an efficient algorithm for sorting a small number of elements.

__Input__: A sequence of $n$ numbers $<a_1,a_2,\cdots,a_n>$

__Ouput__: A permutation (reordering) $<a'_1,a'_2,\cdots,a'n>$ of the input sequence such that $a'_1 \leq a'_2 \leq \cdots \leq a'_n$.

##### INSERTION-SORT

This _pseudocode_ takes as a parameter an array $A[1..n]$ containing a sequence of length $n$ that is to be sorted. The algorithm sorts the input numbers __in place__: it rearranges the numbers within the array.

{% highlight java %}
  for j = 2 to A.length
    key = A[j]
    // Insert A[j] into the sorted sequence A[1..j-1].
    i = j - 1
    while i > 0 and A[i] > key
      A[i + 1] = A[i]
      i = i - 1
    A[i + 1] = key
{% endhighlight %}

The index $j$ indicates the "current card" being inserted into the subarray consisting of elements $A[1..j - 1]$ (currently sorted array). The remaining subarray $A[j + 1..n]$ corresponds to the unordered array.

> Elements $A[1..j - 1]$ are the elements _originally_ in positions $1$ through $j - 1$, but now in sorted order, this is known as __loop invariant__

We use __loop invariants__ to help us understand why an algorithm is correct, must show three things about a __loop invariant__:

__Initialization__: It is true prior to the first iteration of the loop.

__Maintenance__: If it is true before an iteration of the loop, it remains true before the next iteration.

__Termination__: When the loop terminates, the invariant gives us a useful property that helps show that the algorithm is correct.

The best-case occurs if the array is already sorted and the best-case running time will be a __linear function__ of $n$.

The wrost-case occurs when the array is in reverse sorted order and the wrote-case running time is a __quadratic function__ of $n$.