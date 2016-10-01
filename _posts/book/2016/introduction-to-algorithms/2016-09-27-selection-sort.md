---
categories: [introduction-to-algorithms-additional-comparison-sort]
date: 2016-09-27 16:00:00
hidden: true
layout: book-notes
libraries: [mathjax]
permalink: /selection-sort/
title: "Selection Sort"
---

This sorting algorithm is a in-place comparison based algorithm in which the list is divided into two parts, sorted part at left end and unsorted part at right end. Initially sorted part is empty and unsorted part is entire list.

Smallest element is selected from the unsorted array and swapped with the leftmost element and that element becomes part of sorted array. This process continues moving unsorted array boundary by one element to the right.

This algorithm is not suitable for large data set as its average and worst case complexity are of $\Theta(n^2)$ where $n$ are number of items.

##### SELECTION-SORT(A)

{% highlight java %}
  for i = 1 to A.length
    smallest_index = i
    for j = i + 1 to A.length
      if A[j] < A[smallest_index]
        smallest_index = j
    exhange A[i] with A[smallest_index]
{% endhighlight %}

##### Java Implementation

{% highlight java %}
  public class Main {

      public static void main(String[] args) {
          int[] unsortedIntegerArray = {64, 25, 12, 22, 11};
          selectionSort(unsortedIntegerArray);
          printArray(unsortedIntegerArray);
          // return 11 12 22 25 64 
      }

      public static void selectionSort(int[] array) {
          for (int i = 0; i < array.length; i++) {
              int smallestIndex = i;
              for (int j = i + 1; j < array.length; j++) {
                  if (array[j] < array[smallestIndex]) {
                      smallestIndex = j;
                  }
              }
              int temp = array[smallestIndex];
              array[smallestIndex] = array[i];
              array[i] = temp;
          }
      }

      public static void printArray(int[] array) {
          for( int i = 0; i < array.length; i++) {
              System.out.print(array[i] + " ");
          }
      }
  }
{% endhighlight %}