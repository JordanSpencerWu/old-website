---
categories: [introduction-to-algorithms-sort-linear-time]
date: 2016-09-24 10:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /counting-sort/
title: "Counting Sort"
---

__Counting sort__ assumes that each of the $n$ input elements is an integer in the range $0$ to $k$, for some integer $k$. When $k = O(n)$, the sort runs in $\Theta(n)$ time. This algorithm determines, for each input element $x$, the number of elements less than $x$. It uses this information to place element $x$ directly into its position in the output array. We must modify this scheme slightly to handle the situation in which several elements have the same value, since we do not want to put them all in the same position.

We assume that the input is an array $A[1..n]$ and thus $A.length = n $. We require two other arrays: the array $B[1..n]$ holds the sorted output, and the array $C[0..k]$ provides temporary working storage.

##### COUNTING-SORT(A, B, k)

{% highlight java %}
  let C[0..k] be a new array
  for i = 0 to k
    C[i] = 0
  for j = 1 to A.length
    C[A[j]] = C[A[j]] + 1
  // C[i] now contains the number of elements equal to i.
  for i = 1 to k
    C[i] = C[i] + C[i - 1]
  // C[i] now contains the number of elements less than or equal to i.
  for j = A.length downto 1
    B[C[A[j]]] = A[j]
    C[A[j]] = C[A[j]] - 1
{% endhighlight %}

The overall time it takes is $\Theta(k + n)$, in practice, we usually use counting sort when we have $k = O(n)$, in which case the running time is $\Theta(n)$.

> An important property of counting sort is that it is __stable__: numbers with the same value appear in the output array in the same order as they do in the input array. Counting sort is often used as a subroutine in radix sort.

##### Java Implementation Using Figure 8.2 In Book

{% highlight java %}
  public class Example {

      public static void main(String[] args) {
          int[] unsortedIntegerArray = {2, 5, 3, 0, 2, 3, 0, 3};
          int[] sortedArray = new int[unsortedIntegerArray.length];
          int maxInteger = getMaxIntegerInArray(unsortedIntegerArray);
          countingSort(unsortedIntegerArray,sortedArray,maxInteger);
          // return 0 0 2 2 3 3 3 5
      }

      public static int getMaxIntegerInArray(int[] array) {
          int max = array[0];

          for (int i = 0; i < array.length; i++) {
              if (array[i] > max) {
                  max = array[i];
              }
          }

          return max;
      }

      public static void countingSort(int[] unsortedArray, int[] sortedOuput, int maxInteger) {
          int[] tempArray = new int[maxInteger + 1];

          for (int i = 0; i <= maxInteger; i++) {
              tempArray[i] = 0;
          }

          for (int j = 0; j < unsortedArray.length; j++) {
              tempArray[unsortedArray[j]] = tempArray[unsortedArray[j]] + 1;
          }

          for (int i = 1; i <= maxInteger; i++) {
              tempArray[i] = tempArray[i] + tempArray[i - 1];
          }

          for (int j = unsortedArray.length - 1; j >= 0; j--) {
              sortedOuput[tempArray[unsortedArray[j]] - 1] = unsortedArray[j];
              tempArray[unsortedArray[j]] = tempArray[unsortedArray[j]] - 1;
          }

          printArray(sortedOuput);
      }

      public static void printArray(int[] array) {
          for( int i = 0; i < array.length; i++) {
              System.out.print(array[i] + " ");
          }
      }
  }
{% endhighlight %}