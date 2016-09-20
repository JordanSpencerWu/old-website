---
categories: [introduction-to-algorithms]
date: 2016-09-20 10:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /priority-queues/
title: "Priority Queues"
---

One of the most popular applications of a heap: as an efficient _priority queue_. Priority queues come in two forms: _max-priority queues_ and _min-priority queues_. In a given application, such as job scheduling or event-driven simulation, element of a priority queue correspond to objects in the application.

A __priority queue__ is a data structure for maintaining a set $S$ of elements, each with an associated value called a __key__. A __max-priority queue__ supports the following operations:

$INSERT(S,x)$ inserts the element $x$ into the set $S$, which is equivalent to the operation $S = S \cup {x}$.

$MAXIMUM(S)$ removes and returns the element of $S$ with the largest key.

$EXTRACT-MAX(S)$ removes and returns the element of $S$ with the largest key.

$INCREASE-KEY(S,x,k)$ increases the value of element $x's$ key to the new value $k$, which is assumed to be at least as large as $x's$ current key value.

When we use a heap to implement a priority queue, we often need to store a __handle__ to the corresponding application object in each heap element. The exact makeup of the handle (such as a pointer or an integer) depends on the application.

##### HEAP-MAXIMUM(A)

The procedure $HEAP-MAXIMUM$ implements the __MAXIMUM__ operation in $\Theta(1)$.

{% highlight java %}
    return A[1]
{% endhighlight %}

##### HEAP-EXTRACT-MAX(A)

The procedure __HEAP-EXTRACT-MAX__ implements the __EXTRACT-MAX__ operation, the running time of __HEAP-EXTRACT-MAX__ is $\Theta(lg \\ n)$.

{% highlight java %}
  if A.heap-size < 1
    error "heap underflow"
  max = A[1]
  A[1] = A[A.heap-size]
  A.heap-size = A.heap-size - 1
  MAX-HEAPIFY(A,1)
  return max
{% endhighlight %}

##### HEAP-INCREASE-KEY(A,i,key)

The procedure __HEAP-INCREASE-KEY__ implements the __INCREASE-KEY__ operation. An index $i$ into the array identifies the priority-queue element whose key we wish to increase. The procedure first updates the key of element $A[i]$ to its new value. Because increasing the key of $A[i]$ might violate the max-heap property, the procedure then, traverses a simple path from this node toward the root to find a proper place for the newly increased key. As __HEAP-INCREASE-KEY__ traverses this path, it repeatedly compares an element to its parent, exchanging their keys and continuing if the element's key is larger,, and terminating if the element's key is smaller, since the max-heap property now holds. The running time is $\Theta(lg \\ n)$.

{% highlight java %}
  if key < A[i]
    error "new key is smaller than current key"
  A[i] = key
  while i > 1 and A[PARENT(i) < A[i]]
    exchange A[i] with A[PARENT(i)]
    i = PARENT(i)
{% endhighlight %}

##### MAX-HEAP-INSERT(A,key)

This procedure is an _insert_ operation, it takes as an input the key of the new element to be inserted into max-heap $A$, The procedure first expands the max-heap by adding to the tree a new leaf whose key is $- \infty$. Then it calls __HEAP-INCREASE-KEY__ to set the key of this new node to its correct value and maintain the max-heap property. The running time is $\Theta(lg \\ n)$.

{% highlight java %}
  A.heap-size = A.heap-size + 1
  A[A.heap-size] = -INFTY
  HEAP-INCREASE-KEY(A,A.heap-size,key)
{% endhighlight %}