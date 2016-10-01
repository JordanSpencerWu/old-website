---
categories: [introduction-to-algorithms-elementary-data-structures]
date: 2016-09-27 10:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /hash-tables/
title: "Hash Tables"
---

A __hash table__ is an effective data structure for implementing dictionaries. Although searching for an element in a hash table can take as long as searching for an element in a linked list, $\Theta(n)$ time in the worst case, in practice, hashing performs extremely well. The average time to search for an elment in a hash table is $\Theta(1)$.

##### Direct-Address Table

Direct addressing is a simple technique that works well when the universe $U$ of keys is reasonably small. Suppose that an application needs a dynamic set in which each element has a key drawn from the universe $U = \{0, 1,..., m - 1\}$, where $m$ is not too large. We shall assume that no two elements have the same key. (Use Figure 11.1 in the book for more visualization)

> The downside of direct addressing: if universe $U$ is large, storing a table $T$ of size $U$ may be impractical. Furthermore, the set $K$ of keys _actually stored_ may be so small relative to $U$ that most of the space allocated for $T$ would be wasted.

##### Hash Tables

When the set $K$ of keys stored in a dictionary is much smaller than the universe $U$ of all possible keys, a hash table requires much less storage than a direct-address table. With hashing, this element is stored in slot $h(k)$; this is, we use a __hash function__ $h$ to compute the slot from the key $k$. Here, $h$ maps the universe $U$ of keys into the slots of a __hash table__ $T$ $\{0,1,...,m - 1\}$:

$$h: U \to \{ 0,1,...,m - 1 \}$$

Where the size $m$ of the hash table is typically much less than $U$. We say that an element with key $k$ __hashes__ to slot $h(k)$; we also say that $h(k)$ is the __hash value__ of key $k$. (Use Figure 11.2 in the book for more visualization)

> The hash function reduces the range of array indices and hence the size of the array. There is one hitch: two key may hash to the same slot. We call this situation a __collision__.

##### Collision Resolution By Chaining

In __chaining__, we place all the elements that hash to the same slot into the same linked list. Slot $j$ contains a pointer to the head of the list of all stored elements that hash to $j$; if there are no such elements, slot $j$ contains $NIL$.

> Given a hash table $T$ with $m$ slots that stores $n$ elements, we defined the __load factor__ $\alpha$ for $T$ as $\frac{n}{m}$, that is, the average number of elements stored in a chain. (Use Figure 11.2 in the book for more visualization)

The worst-case behavior of hashing with chaining: all $n$ keys hash to the same slot, creating a list of length $n$.

The average-case performance of hashing depends on how well the hash function $h$ distributes the set of keys to be stored among the $m$ slots, on the average.

##### What Makes A Good Hash Function?

> A good hash function satisfies (approximately) the assumption of simple uniform hashing: each key is equally likely to hash to any of the $m$ slots, independently of where any other key has hashed to.

Two of the schemes, hashing by division and hashing by multiplication, are heuristic in nature, whereas the third scheme, universal hashing, uses randomization to provide provably good performance.