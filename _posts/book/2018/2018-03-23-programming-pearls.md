---
author: Jon Bentley
categories: [book]
class: 68
date: 2018-03-23 10:00:00
description: Programming Pearls is about thinking like a software engineer. There's many things we have to consider like space and time of the software. We should spend more time thinking about the problem definition, algorithm design, and data structure selection. Remember that simple programs most often yields functionality, robustness, speed, and space.
hidden: true
img-path: /assets/images/books/programming-pearls.jpg
layout: book
permalink: /programming-pearls/
title: "Programming Pearls"
---

Careful analysis of a small problem can sometimes yield tremendous practical benefits.

The Bitmap Data Structure: This data structure represents a dense set over a finite domain when each element occurs at most once and no other data is associated with the element. Even if these conditions aren't satisfied (when there are multiple elements or extra data, for instance), a key from a finite domain can be used as an index into a table with more complicated entries.

Multiple-Pass Algorithms: algorithms make several passes over their input data, accomplishing a little more each time.

Less data to process means less time to process it, that reducing a program's space requirements also reduces its run time.

Signature: When an equivalence relation defines classes, it is helpful to define a signature and no other item does.

A proper view of data does indeed structure programs.

Don't write a big program when a little one will do.

Data structure can reduce big programs to small programs.

Writing correct programs involves: problem definition, algorithm design, and data structure selection.

Loop invariant: This assertion about the program state an invariant because it is true at the beginning and end of each iteration of the loop.

Program verification: Programmers have a deeper understanding of programs, if they execute the program by hand on one input.

Wise programmers instead build scaffolding to give them easy access to the function.

Everything should be made as simple as possible, but no simpler.

Divide-and-conquer: To solve a problem of size n, recursively solve two subproblems of size approximately n/2, and combine their solutions to yield a solution to the complete problem.

Reducing space often has desirable side-effects on run time: smaller programs are faster to load and fit more easily into a cache, and less data to manipulate usually means less time to manipulate it.

Simplicity can yield functionality, robustness, speed, and space.

"Code tuning" locates the expensive parts of an existing program and then makes little changes to improve its speed.

Premature optimization is the root of much programming evil.

"If it ain't broke, don't fix it."

#### RULES FOR CODE TUNING

##### Space-For-Time Rules

__Data Structure Augmentation__. The time required for common operation on data can often be reduced by augmenting the structure with extra information or by changing the information within the structure so that it can be accessed more easily.

__Store Precomputed Results__. The cost of recomputing an expensive function can be reduced by computing the function only once and storing the results. Subsequent requests for the function are then handled by table lookup rather than by computing the function.

__Caching__. Data that is accessed most often should be the cheapest to access.

__Lazy Evaluation__. The strategy of never evaluating an item until it is needed avoids evaluations of unnecessary items.

##### Time-For-Space Rules

__Packing__. Dense storage representations can decrease storage costs by increasing the time required to store and retrieve data.

__Interpreters__. The space required to represent a program can often be decreased by the use of interpreters in which common sequences of operations are represented compactly.

##### Loop Rules

__Code Motion Out of Loops__. Instead of performing a certain computation in each iteration of a loop, it is better to perform it only once, outside the loop.

__Combining Tests__. An efficient inner loop should contain as few tests as possible, and preferably only one. The programmer should therefore try to simulate some of the exit conditions of the loop by other exit conditions.

__Loop Unrolling__. Unrolling a loop can remove the cost of modifying loop indices, and also help to avoid pipeline stalls, to reduce branches, and to increase instruction-level parallelism.

__Transfer-Driven Loop Unrolling__. If a large cost of an inner loop is devoted to trivial assignments, then those assignments can often be removed by repeating the code and changing the use of variables. Specifically, to remove the assignment i = j, the subsequent code must treat j as though it were i.

__Unconditional Branch Removal__. A fast loop should contain no unconditional branches. An unconditional branch at the end of a loop can be removed by "rotating" the loop to have a conditional branch at the bottom.

__Loop Fusion__. If two nearby loops operate on the same set of elements, then combine their operational parts and use only one set of loop control operations.

##### Logic Rules

__Exploit Algebraic Identities__. If the evaluation of a logical expression is costly, replace it by an algebraically equivalent expression that is cheaper to evaluate.

__Short-Circuiting Monotone Functions__. If we wish to test whether some monotone nondecreasing function of several variables is over a certain threshold, then we need not evaluate any of the variables once the threshold has been reached.

__Reordering Tests__. Logical tests should be arranged such that inexpensive and often successful tests precede expensive and rarely successful tests.

__Precompute Logical Functions__. A logical function over a small finite domain can be replaced by a lookup in a table that represents the domain.

__Boolean Variable Elimination__. We can remove Boolean variables from a program by replacing the assignment to a Boolean variable v by an if - else statement in which one branch represents the case that v is true and the other represents the case that v is false.

##### Procedure Rules

__Collapsing Function Hierarchies__. The run times of the elements of a set of functions that (nonrecursively) call themselves can often be reduced by rewriting functions in line and binding the passed variables.

__Exploit Common Cases__. Functions should be organized to handle all cases correctly and common cases efficiently.

__Coroutines__. A multiple-pass algorithm can often be turned into a single-pass algorithm by use of coroutines.

__Transformations on Recursive Functions__. The run time of recursive functions can often be reduced by rewriting recursion to iteration.

__Parallelism__. A program should be structured to exploit as much of the parallelism as possible in the underlying hardware.

##### Expression Rules

__Compile-Time Initialization__. As many variables as possible should be initialized before program execution.

__Exploit Algebraic Identities__. If the evaluation of an expression is costly, replace it by an algebraically equivalent expression that is cheaper to evaluate.

__Common Subexpression Elimination__. If the same expression is evaluated twice with none of its variables altered between evaluations, then the second evaluation can be avoided by storing the result of the first and using that in place of the second.

__Pairing Computation__. If two similar expressions are frequently evaluated together, then we should make a new procedure that evaluates them as a pair.

__Exploit Word Parallelism__. Use the full data-path width of the underlying computer architecture to evaluate expensive expressions.