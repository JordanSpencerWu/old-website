---
categories: [introduction-to-algorithms-elementary-data-structures]
date: 2016-09-26 12:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /linked-lists/
title: "Linked Lists"
---

A __linked list__ is a data structure in which the objects are arranged in a linear order, the order in a linked list is determined by a pointer in each object.

A __doubly linked list__ $L$ is an object with an attribute $key$ and two other pointer attribute: __next__ and __prev__. Given an element $x$ in the list, $x.next$ points to its __successor__ in the linked list, and $x.prev$ points to its __predecessor__. If $x.prev = NIL$, the element $x$ has no predecessor and is therefore the first element, or __head__, of the list. If $x.next = NIL$, the element $x$ has no successor and is therefore the last element, or __tail__, of the list. An attribute $L.head$ points to the first element of the list. If $L.head = NIL$, the list is empty.

> A list may have one of several forms. It may be either singly linked or doubly linked, it may be sorted or not, and it may be circular or not.

__Singly linked__, we omit the _prev_ pointer in each element.

A __sorted__ list, the linear order of the list corresponds to the linear order of keys stored in elements of the list; the minimum element is then the head of the list, and the maximum element is the tail.

A __unsorted__ list, the elements can appear in any order.

In a __circular__ list, the _prev_ pointer of the head of the list points to the tail, and the _next_ pointer of the tail of the list points to the head.

##### Searching a linked list

The procedure __LIST-SEARCH(L,k)__ finds the first element with key $k$ in list $L$ by a simple linear search, returning a pointer to this element. If no object with key $k$ appears in the list, then the procedure return $NIL$.

##### LIST=SEARCH(L,k)

{% highlight java %}
  x = L.head
  whilte x != NIL and x.key != k
    x = x.next
  return x
{% endhighlight %}

To search a list of $n$ objects, the __LIST-SEARCH__ procedure takes $\Theta(n)$ time in the worst case, since it may have to search the entire list.

##### Inserting into a linked list

Given an element $x$ whose $key$ attribute has already been set, __LIST-INSERT__ procedure "splices" $x$ onto the front of the linked list.

##### LIST-INSERT(L,x)

{% highlight java %}
  x.next = L.head
  if L.head != NIL
    L.head.prev = x
  L.head = x
  x.prev = NIL
{% endhighlight %}

The running time for __LIST-INSERT__ on a list of $n$ elements is $\Theta(1)$.

##### Deleting from a linked list

The procedure __LIST-DELETE__ removes an element $x$ from a linked list $L$. It must be given a pointer to $x$, and it then "splices" x out of list by updating pointers. If we wish to delete an element with a given key, we must first call __LIST-SEARCH__ to retrieve a pointer to the element.

##### LIST-DELETE(L,x)

{% highlight java %}
  if x.prev != NIL
    x.prev.next = x.next
  else L.head = x.next
  if x.next != NIL
    x.next.prev = x.prev
{% endhighlight %}

LIST-DELETE runs in $\Theta(1)$, but if we wish to delete an element with a given key, $\Theta(n)$ time is required in the worst case because we must first call __LIST-SEARCH__ to find the element.