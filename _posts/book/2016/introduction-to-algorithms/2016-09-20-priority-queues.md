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

##### Java Implementation

{% highlight java %}
  public class Example {

      private static int heapSizeMaxIndex;

      public static void main(String[] args) {
          int[] maxHeapArray = {15, 13, 9, 5, 12, 8, 7, 4, 0, 6, 2, 1};
          heapSizeMaxIndex = maxHeapArray.length - 1;
          maximum(maxHeapArray);
          heapExtractMax(maxHeapArray);
          printHeap(maxHeapArray);
          heapIncreaseKey(maxHeapArray,8,15);
          printHeap(maxHeapArray);
          maxHeapInsert(maxHeapArray,16);
          printHeap(maxHeapArray);

          // returns 15
          // removes 15 from heap
          // 13 12 9 5 6 8 7 4 0 1 2 
          // 15 13 9 12 6 8 7 4 5 1 2 
          // 16 13 15 12 6 9 7 4 5 1 2 8 
      }

      public static void maximum(int[] array) {
          System.out.println("returns " + array[0]);
      }

      public static void heapExtractMax(int[] array) {
          if (heapSizeMaxIndex < 0) {
              System.out.println("heap underflow");
              System.exit(1);
          }
          int rootIndex = 0;
          int max = array[0];

          array[rootIndex] = array[heapSizeMaxIndex];
          heapSizeMaxIndex = heapSizeMaxIndex - 1;
          maxHeapify(array,rootIndex);
          System.out.println("removes " + max + " from heap");
      }

      public static void maxHeapify(int[] array, int parentIndex) {
          int leftChildIndex = (parentIndex * 2) + 1;
          int rightChildIndex = (parentIndex * 2) + 2;
          int indexOfLargestValue = parentIndex;

          if (leftChildIndex <= heapSizeMaxIndex && array[leftChildIndex] > array[indexOfLargestValue]) {
              indexOfLargestValue = leftChildIndex;
          }
          if (rightChildIndex <= heapSizeMaxIndex && array[rightChildIndex] > array[indexOfLargestValue]) {
              indexOfLargestValue = rightChildIndex;
          }
          if (indexOfLargestValue != parentIndex) {
              swap(array,parentIndex,indexOfLargestValue);
              maxHeapify(array, indexOfLargestValue);
          }
      }

      public static void swap(int[] array, int firstIndex, int secondIndex) {
          int temp = array[firstIndex];
          array[firstIndex] = array[secondIndex];
          array[secondIndex] = temp;
      }

      public static void heapIncreaseKey(int[] array, int currentKeyIndex, int newKeyIndex) {
          if (newKeyIndex < array[currentKeyIndex]) {
              System.out.println("new key is smaller than current key");
              System.exit(1);
          }
          int parentIndex = getParentIndex(currentKeyIndex);
          array[currentKeyIndex] = newKeyIndex;

          while(currentKeyIndex > 0 && array[parentIndex] < array[currentKeyIndex]) {
              swap(array,currentKeyIndex,parentIndex);
              currentKeyIndex = getParentIndex(currentKeyIndex);
              parentIndex = getParentIndex(currentKeyIndex);
          }
      }

      public static int getParentIndex(int index) {
          return (index - 1) / 2;
      }

      public static void maxHeapInsert(int[] array, int key) {
          heapSizeMaxIndex = heapSizeMaxIndex + 1;
          array[heapSizeMaxIndex] = Integer.MIN_VALUE;
          heapIncreaseKey(array,heapSizeMaxIndex,key);
      }

      public static void printHeap(int[] array) {
          for (int i = 0; i <= heapSizeMaxIndex; i++) {
              System.out.print(array[i] + " ");
          }
          System.out.println("");
      }
  }
{% endhighlight %}