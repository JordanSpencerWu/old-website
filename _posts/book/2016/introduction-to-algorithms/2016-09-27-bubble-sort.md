---
categories: [introduction-to-algorithms-additional-comparison-sort]
date: 2016-09-27 15:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /bubble-sort/
title: "Bubble Sort"
---

__Bubble sort__ is a simple sorting algorithm. This sorting algorithm is comparison based algorithm in which each pair of adjacent elements is compared and elements are swapped if they are not in order. This algorithm is not suitable for large data sets as its average and worst case complexity are of $\Theta(n^2)$ where $n$ are the number of items.

##### BUBBLE-SORT(A)

{% highlight java %}
  for i = 1 to A.length
    for j = 1 to A.length - i
      if A[j] > A[j + 1]
        exchange A[j] with A[j + 1]
{% endhighlight %}

##### Java Implementation

{% highlight java %}
  public class Main {

      public static void main(String[] args) {
          int[] unsortedIntegerArray = {64, 25, 12, 22, 11};
          bubbleSort(unsortedIntegerArray);
          printArray(unsortedIntegerArray);
          // return 11 12 22 25 64
      }

      public static void bubbleSort(int[] array) {
          for (int i = 0; i < array.length; i++) {
              for (int j = 0; j < array.length - 1; j++) {
                  if (array[j] > array[j + 1]) {
                      int temp = array[j];
                      array[j] = array[j + 1];
                      array[j + 1] = temp;
                  }
              }
          }
      }

      public static void printArray(int[] array) {
          for( int i = 0; i < array.length; i++) {
              System.out.print(array[i] + " ");
          }
      }
  }
{% endhighlight %}