---
categories: [introduction-to-algorithms-comparison-sort]
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

The quicksort algorithm has a worst-case running time of $\Theta(n^2)$, this occurs when the partitioning produces subproblem with $n - 1$ elements and one with 0 elements. The best-case running time is when the partitioning produces two subproblem, each of size no more than $\frac{n}{2}$ which is $\Theta(n \\ lg \\ n)$. The average-case running time of quicksort is much closer to the best case than to the worst case.

##### Java Implementation Using Figure 7.1 In Book

{% highlight java %}
  public class Main {

      public static void main(String[] args) {
          int[] array = {13, 19, 9, 5, 12, 8, 7, 4, 21, 2, 6, 11};
          quickSort(array,0,array.length - 1);
          printArray(array);
          // returns 2 4 5 6 7 8 9 11 12 13 19 21
      }

      public static void quickSort(int[] array, int startIndex, int endIndex) {
          if (startIndex < endIndex) {
              int pivot = partition(array,startIndex,endIndex);
              quickSort(array,startIndex,pivot - 1);
              quickSort(array,pivot + 1,endIndex);
          }
      }

      public static int partition(int[] array,int startIndex,int endIndex) {
          int pivotValue = array[endIndex];
          int pivotIndex = startIndex;

          for (int j = startIndex; j < endIndex; j++) {
              if (array[j] <= pivotValue) {
                  swap(array,pivotIndex,j);
                  pivotIndex = pivotIndex + 1;
              }
          }
          swap(array,pivotIndex,endIndex);
          return pivotIndex;
      }

      public static void swap(int[] array, int firstIndex, int secondIndex) {
          int temp = array[firstIndex];
          array[firstIndex] = array[secondIndex];
          array[secondIndex] = temp;
      }

      public static void printArray(int[] array) {
          for( int i = 0; i < array.length; i++) {
              System.out.print(array[i] + " ");
          }
      }
  }
{% endhighlight %}