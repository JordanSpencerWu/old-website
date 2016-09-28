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

##### Direct-address table

Direct addressing is a simple technique that works well when the universe $U$ of keys is reasonably small. Suppose that an application needs a dynamic set in which each element has a key drawn from the universe $U = {0, 1,..., m - 1}$, where $m$ is not too large. We shall assume that no two elements have the same key. (Use Figure 11.1 in the book for more visualization)

> The downside of direct addressing: if universe $U$ is large, storing a table $T$ of size $|U|$ may be impractical. Furthermore, the set $K$ of keys _actually stored_ may be so small relative to $U$ that most of the space allocated for $T$ would be wasted.

To be continued...