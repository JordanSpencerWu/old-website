---
author: Thomas H. Cornmen, Charles E Leiserson, Ronald L. Riverest, & Clifford Stein
categories: [book]
class: 5
date: 2016-09-17 10:00:00
description: Currently Reading...
hidden: true
img-path: /assets/images/books/introduction-to-algorithms.jpeg
layout: book
libraries: [mathjax]
permalink: /introduction-to-algorithms/
title: "Introduction to Algorithms"
---

An __algorithm__ is a sequence of computational steps that transform the input into the output. __Analyzing__ an algorithm has come to mean predicting the resources that the algorithm requires. The time taken by an algorithm grows with the size of the input, so it is traditional to describe the running time of a program as a function of the size of its input. To do so, we need to define the terms "running time" and "size of input" more carefully.

__input size__ depends on the problem being studied. For many problems the _number of items in the input_, or it may be _total numbers of bits_ needed to represent the input in ordinary binary notation.

__running time__ of an algorithm on a particular input is the number of primitive operations or "steps" executed.

For the most part of the book, the focus will be on the __worst-case running time__, the longest running time for _any_ input of size $n$. The reason why is this running time gives us the upper bound on the running time for any input of size $n$ (guarantee that the algorithm will never take any longer).

__rate of growth__ or __order of growth__ of the running time, we consider only the leading term of the running time function and also ignore the leading term's constant coefficient.

We use __loop invariants__ to help us understand why an algorithm is correct, it must satisfy the following conditions:

__Initialization__: It is true prior to the first iteration of the loop.

__Maintenance__: If it is true before an iteration of the loop, it remains true before the next iteration.

__Termination__: When the loop terminates, the invariant gives us a useful property that helps show that the algorithm is correct.

Click <a href="http://clrs.skanev.com/" target="_blank">here</a> to see exercises answers in the book.

##### Comparison Sorts

> These algorithms share an interesting property: _the sorted order they determine is based only on comparison between the input elements. Any comparison sort must make $\Theta(n \\ lg \\ n)$ comparisons in the worst case to sort $n$ elements._

<div class="collection">
  {% for post in site.categories.introduction-to-algorithms-comparison-sort reversed %}
    <a href="{{ post.url | prepend: site.baseurl }}"  class="collection-item">{{ post.title }}</a>
  {% endfor %}
</div>

##### Sort Algorithm (Linear Time)

 <div class="collection">
  {% for post in site.categories.introduction-to-algorithms-sort-linear-time reversed %}
    <a href="{{ post.url | prepend: site.baseurl }}"  class="collection-item">{{ post.title }}</a>
  {% endfor %}
</div>