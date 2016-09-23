---
categories: [introduction-to-algorithms]
date: 2016-09-21 10:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /quick-sort/
title: "Quicksort"
---

__Quicksort__, like merge sort, applies the _divide-and-conquer_ principle. Here is the three-step divide-and-conquer process for sorting a subarray $A[p..r]$:

__Divide__: Partition (rearrange) the array $A[p..r]$ into two (possible empty) subarrays $A[p..q - 1]$ and $A[q + 1..r]$ such that each element of $A[p..q - 1]$ is less than or equal to $A[q]$, which is, in turn, less than or equal to each element of $A[q + 1..r]$. Compute the index q as part of this partitioning procedure.

__Conquer__: Sort the two subarrays $A[p..q - 1]$ and $A[q + 1..r]$ by recursive calls to quicksort.

__Combine__: Because the subarrays are already sorted, no work is needed to combine them: the entire array $A[p..r]$ is now sorted.

##### QUICKSORT(A,p,r)

{% highlight java %}
  if p < r
    q = PARTITION(A,p,r)
    QUICKSORT(A,p,q - 1)
    QUICKSORT(A,q + 1,r)
{% endhighlight %}

__NOTE__: To sort an entire array $A$, the initial call is __QUICKSORT(A,1,A.length)__.

The key to the algorithm is the __PARTITION__ procedure, which rearranges the subarray $A[p..r]$ in place.

##### PARTITION(A,p,r)

{% highlight java %}
  x = A[r]
  i = p - 1
  for j = p to r - 1
    if A[j] <= x
      i = i + 1
      exchange A[i] with A[j]
  exchange A[i + 1] with A[r]
  return i + 1
{% endhighlight %}

__PARTITION__ always selects an element $x = A[r]$ as a __pivot__ element around which to partition the subarray $A[p..r]$

> Loop invariant: At the beginning of each iteration of the loop, for any array index k

> 1. If $p \leq k \leq, then A[k] \leq x$.
> 2. If $i + 1 \leq k \leq j - 1, then A[k] > x$.
> 3. If $k = r, then A[k] = x$.

The quicksort algorithm has a worst-case running time of $\Theta(n^2)$. Despite this slow worst-case running time, it is remarkably efficient on the average: its expected running time is $\Theta(n \\ lg \\ n)$.