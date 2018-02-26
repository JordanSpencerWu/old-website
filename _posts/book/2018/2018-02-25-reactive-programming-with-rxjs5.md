---
author: Sergi Mansilla
categories: [book]
class: 65
date: 2018-02-25 10:00:00
description: Reactive Programming makes asynchronous programming clean, intuitive, and robust. It combines the Observer pattern with the Iterator pattern and functional programming with collections which allows us to transform the stream of data using operators like map, filter, reduce, every, etc. This book does a great job at explaining the core concepts like Observable, Observer, Subscription, Operators, Subject, and Schedulers.
hidden: true
img-path: /assets/images/books/reactive-programming-with-rxjs5.jpg
layout: book
permalink: /reactive-programming-with-rxjs5/
title: "Reactive Programming with RxJS 5"
---

An Observable represents a stream of data.

The Observable "pushes" values to consumers as they become available.

RxJS is push-based, so the source of events (the Observable) will push new values to the consumer (the Subscriber), without the consumer requesting the next value.

Subscribers have to implement the Observer interface. The Observer interface contains three methods: next, complete, and error.

In RxJS, methods that transform or query sequences are called operators.

Observables are immutable, and every operator applied to them creates a new Observable.

Observables are just streams of events that we transform, combine, and query.

An Observable pipeline is a group of operators chained together, where each one takes an Observable as input and returns an Observable as output.

A Subject is a type that implements both Observer and Observable types. As an Observer, it can subscribe to Observables, and as an Observable it can produce values and have Observers subscribe to it.

AsyncSubject emits the last value of a sequence only if the sequence completes.

When an Observer subscribes to a BehaviorSubject, it receives the last emitted value and then all the subsequent values. BehaviorSubject requires that we provide a starting value, so that all Observers will always receive a value when they subscribe to a BehaviorSubject.

A ReplaySubject caches its values and re-emits them to any Observer that subscribe late to it.

Hot Observables emit values regardless of having any subscribers. Any Subscriber subscribed to a hot Observable will receive values emitted only from the exact moment it subscribes to it.

Cold Observable emit the entire sequence of values from the start to every subscriber. A cold Observable emits values only when Subscriber subscribe to it.

We can turn a cold Observable into a hot one using publish.

A Scheduler is a mechanism to "Schedule" an action to happen in the future.

##### Links to Resources

<a href="http://reactivex.io/rxjs/manual/overview.html" target="_blank">RxJS</a>

<a href="http://rxmarbles.com/" target="_blank">RxJS Marbles</a>

<a href="https://rxviz.com/" target="_blank">Rx Visualizer</a>