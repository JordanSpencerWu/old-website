---
categories: [introduction-to-algorithms]
date: 2016-09-23 10:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /randomized-quick-sort/
title: "Randomized Quicksort"
---

Instead of always using $A[r]$ as the pivot, we will select a randomly chosen element from the subarray $A[p..r]$. We do so by first exchanging element $A[r]$ with an element chosen at random from $A[p..r]$. By randomly sampling the range $p,...,r$, we ensure that the pivot element $x = A[r]$ is equally likely to be any of the $r - p + 1$ elements in the subarray. Because we randomly choose the pivot element, we expect the split of the input array to be reasonably well balanced on average.

##### RANDOMIZED-PARTITION(A,p,r)

{% highlight java %}
  i = RANDOM(p,r)
  exchange A[r] with A[i]
  return PARTITION(A,p,r)
{% endhighlight %}

The new quicksort calls __RANDOMIZED-PARTITION__ in place of __PARTITION__, note that __PARTITION__ is inside <a href="{{ "/quick-sort/" | prepend: site.baseurl }}">__Quicksort__</a> notes.

##### RANDOMIZED-QUICKSORT(A,p,r)

{% highlight java %}
  if p < r
    q = RANDOMIZED-PARTITION(A,p,r)
    RANDOMIZED-QUICKSORT(A,p,q - 1)
    RANDOMIZED-QUICKSORT(A,q + 1,r)
{% endhighlight %}

The worst case running time happens on the worst partitioning case which produces $\Theta(n^2)$. The expected running time of this algorithm is $\Theta(n \\ lg \\ n)$.

{% highlight java %}
  public class Main {

      public static void main(String[] args) {
          int[] array = {13, 19, 9, 5, 12, 8, 7, 4, 21, 2, 6, 11};
          RandomizedQuickSort(array,0,array.length - 1);
          printArray(array);
          // return 2 4 5 6 7 8 9 11 12 13 19 21
      }

      public static void RandomizedQuickSort(int[] array, int startIndex, int endIndex) {
          if (startIndex < endIndex) {
              int pivot = randomizedPartition(array,startIndex,endIndex);
              RandomizedQuickSort(array,startIndex,pivot - 1);
              RandomizedQuickSort(array,pivot + 1,endIndex);
          }
      }

      public static int randomizedPartition(int[] array, int startIndex, int endIndex) {
          int randomEndIndex = randomNumberBetween(startIndex,endIndex);
          swap(array,endIndex,randomEndIndex);
          return partition(array,startIndex,endIndex);
      }

      public static int randomNumberBetween(int startNumber, int endNumber) {
          return (int)Math.floor(Math.random() * (endNumber - startNumber + 1) + startNumber);
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