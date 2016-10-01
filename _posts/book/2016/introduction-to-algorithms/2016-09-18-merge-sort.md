---
categories: [introduction-to-algorithms-comparison-sort]
date: 2016-09-18 10:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /merge-sort/
title: "Merge Sort"
---

This is an efficient algorithm for sorting a large number of elements, using the __divide-and-conquer__ approach: break the problem into several subproblems that are similar to the original problem but smaller in size the subproblems recurseively, and then combine these solutions to create a solution to the original problem.

__Input__: A sequence of $n$ numbers $<a_1,a_2,\cdots,a_n>$

__Ouput__: A permutation (reordering) $<a'_1,a'_2,\cdots,a'n>$ of the input sequence such that $a'_1 \leq a'_2 \leq \cdots \leq a'_n$.

Involves the following three steps:

__Divide__: Divide the $n$-element sequence to be sorted into two subsequence of $\frac{n}{2}$ element each, $\Theta(1)$.

__Conquer__: Sort the two subsequences recurseively using merge sort, $\Theta(lg \\ n)$.

__Combine__: Merge the two sorted subsequences to produce the sorted answer,  $\Theta(n)$.

The key operation of this algorithm is the combine step, __MERGE(A, p, q, r)__, where $A$ is an array and $p$, $q$, and $r$ are indices into the array such that $p \leq q < r$. This procedure assumes that the subarrays $A[p..q]$ and $A[q+1..r]$ are in sorted order. It __merges__ them to form a single sorted subarray that replaces the current subarray $A[p..r]$.

__Description__: Suppose we have two piles of cards face up on a table. Each pile is sorted, with the smallest cards on top. We wish to merge the two piles into a single sorted output pile, which is to be face down on the table. Our basic step consists of choosing the smaller of the two cards on top of the face-up piles, removing it from its pile (which exposes a new top card), and placing this card face down onto the output file. We repeat this step until one input pile is empty, at which time we just take the remaining input pile and place it face down onto the output pile.

##### MERGE(A,p,q,r)

This _pseudocode_ uses __sentinel__ card at the bottom of each pile, this sentinel value helps check for when the pile is empty. In the code it is denoted as $\infty$, once a card with $\infty$ is exposed it cannot be the smaller card unless both piles have their sentinel cards exposed.

{% highlight java %}
  n_1 = q - p + 1
  n_2 = r - q
  let L[1..n_1 + 1] and R[1..n_2 + 1] be new arrays
  for i = 1 to n_1
    L[i] = A[p + i - 1]
  for j = 1 to n_2
    R[j] = A[q + j]
  L[n_1 + 1] = INFTY
  R[n_2 + 1] = INFTY
  i = 1
  j = 1
  for k = p to r
    if L[i] <= R[j]
      A[k] = L[i]
      i = i + 1
    else A[k] = R[j]
      j = j + 1
{% endhighlight %}

We created two arrays $L$ (left $A[p..q]$) and $R$ (right $A[q + 1..r]$), of length $n_1 + 1$ and $n_2 + 1$ (extra position holds the sentinel) respectively.

> Loop invariant: At the start of each iteration of the for loop, the subarray $A[p..k - 1]$ contains the $k - p$ smallest elements of $L[1..n_1 + 1]$ and $R[1..n_2 +1]$, in sorted order. Moreover, $L[i]$ and $R[j]$ are the smallest elements of their arrays that have not been copied back into A.

Now we can use the __MERGE__ procedure as a subroutine in the merge sort algorithm. The procedure __MERGE-SORT(A,p,r)__ sorts the elements in the subarray $A[p..r]$. If $p \geq r$, the subarray has at most one element and is therefore already sorted. Otherwise, the divide step simply computes an index $q$ that partitions $A[p..r]$ into two subarrays: $A[p..q]$, containing $[\frac{n}{2}]$ elements, and $A[q + 1..r]$, containing $[\frac{n}{2}]$ elements.

##### MERGE-SORT(A,p,r)

{% highlight java %}
  if p < r
    q = (p + r)/2
    MERGE-SORT(A,p,q)
    MERGE-SORT(A,q + 1,r)
    MERGE(A,p,q,r)
{% endhighlight %}

The worst-case running time is $\Theta(n \\ lg \\ n)$.

##### Java Implementation Using Figure 2.3 In Book

{% highlight java %}
  public class Main {
      public static void main(String args[])
      {
          int unsortedArray[] = {5, 2, 4, 7, 1, 3, 2, 6};
          mergeSort(unsortedArray,0,unsortedArray.length-1);
          printArray(unsortedArray);
          // returns 1 2 2 3 4 5 6 7
      }

      public static void mergeSort(int[] array, int startIndex, int endIndex)
      {
          int midpointIndex;
          if (startIndex<endIndex)
          {
              midpointIndex = (startIndex+endIndex)/2;
              mergeSort(array,startIndex,midpointIndex);
              mergeSort(array, midpointIndex+1, endIndex);
              merge(array,startIndex,midpointIndex,endIndex);
          }
      }

      public static void merge(int[] array, int startIndex, int midpointIndex, int endIndex)
      {
          int leftNumberOfElements = midpointIndex-startIndex+1;
          int rightNumberOfElements = endIndex-midpointIndex;

          int leftArray[] = new int[leftNumberOfElements+1];
          int rightArray[] = new int[rightNumberOfElements+1];
          int i,j,k;

          for(i=0; i< leftNumberOfElements; i++)
          {
              leftArray[i] = array[startIndex+i];
          }
          for(j=0; j< rightNumberOfElements; j++)
          {
              rightArray[j] = array[midpointIndex+j+1];
          }

          leftArray[leftNumberOfElements] = Integer.MAX_VALUE;
          rightArray[rightNumberOfElements] = Integer.MAX_VALUE;

          i = 0;
          j = 0;
          for(k = startIndex; k<= endIndex; k++)
          {

              if( leftArray[i]<=rightArray[j])
              {
                  array[k] = leftArray[i];
                  i = i+1;
              }
              else
              {
                  array[k] = rightArray[j];
                  j = j+1;

              }
          }
      }

      public static void printArray(int[] array) {
          for (int i = 0; i < array.length; i++) {
              System.out.print(array[i] + " ");
          }
      }
  }
{% endhighlight %}