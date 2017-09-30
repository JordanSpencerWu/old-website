---
author: Eric Freeman And Elisabeth Robson with Kathy Sierra And Bert Bates
categories: [book]
class: 51
date: 2017-08-27 10:00:00
description: A great book that describes popular design patterns that is used in software development. Learning design pattern can be hard, but this book provides many coding examples and diagrams explaining each pattern step by step. I recommend this book to anyone who wants to learn design patterns.
hidden: true
img-path: /assets/images/books/head-first-design-patterns.jpg
layout: book
permalink: /head-first-design-patterns/
title: "Head First Design Patterns"
---

##### The Strategy Pattern

<blockquote>
  Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.
</blockquote>

__Design Principle:__

Identify the aspects of your application that vary and separate them from what stays the same. In other words, take the parts that vary and encapsulate them, so that later you can alter or extend the parts that vary without affecting those that don't.

Program to an interface, not an implementation.

Favor composition over inheritance.

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/strategy" target="_blank">link to example</a>

##### The Observer Pattern

<blockquote>
  Defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.
</blockquote>

Publishers + Subscribers = Observer Pattern

If you understand newspaper subscriptions, you pretty much understand that Observer Patter, only we call the publisher the __SUBJECT__ and the subscribers the __OBSERVERS__.

The Observer Pattern provides an object design where subjects and observers are loosely coupled. When two objects are loosely coupled, they can interact, but have very little knowledge of each other.

Design Principle: Strive for loosely coupled designs between objects that interact.

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/observer" target="_blank">link to example</a>

##### The Decorator Pattern

<blockquote>
  Attaches additional responsibilities to an object dynamically. Decorators provide a flexible alternative to sub classing for extending functionality. 
</blockquote>

Open-Closed Principle: Classes should be open for extension, but closed for modification.

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/decorator" target="_blank">link to example</a>

##### The Factory Pattern

<blockquote>
  Defines an interface for creating an object, but let’s subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.
</blockquote>

The Dependency Inversion Principle: Depend upon abstractions. Do not depend upon concrete classes.

The Abstract Factory Pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes.

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/factory" target="_blank">link to example</a>

##### The Singleton Pattern

<blockquote>
  Ensures a class has only one instance and provides a global point of access to it.
</blockquote>

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/singleton" target="_blank">link to example</a>

##### The Command Pattern

<blockquote>
  Encapsulates a request as an object, thereby letting you parameterize other objects with different requests, queue or log requests, and support undoable operations.
</blockquote>

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/command" target="_blank">link to example</a>

##### The Adapter Pattern

<blockquote>
  Converts the interface of a class into another interface the clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.
</blockquote>

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/adapter" target="_blank">link to example</a>

##### The Facade Pattern

<blockquote>
  Provides a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.
</blockquote>

Principle of Least knowledge: talk only to your immediate friends.

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/facade" target="_blank">link to example</a>

##### The Template Pattern

<blockquote>
  Defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.
</blockquote>

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/template" target="_blank">link to example</a>

##### The Iterator Pattern

<blockquote>
  Provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
</blockquote>

Design Principle: A class should have only one reason to change.

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/iterator" target="_blank">link to example</a>

##### The Composite Pattern

<blockquote>
  Allows you to compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of object uniformly.
</blockquote>

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/composite" target="_blank">link to example</a>

##### The State Pattern

<blockquote>
  Allows an object to alter its behavior when its internal state changes. The object will appear to change its class.
</blockquote>

<a href="https://github.com/JordanSpencerWu/head-first-design-patterns/tree/master/src/design/pattern/state" target="_blank">link to example</a>

##### The Proxy Pattern

<blockquote>
  Provides a surrogate or placeholder for another object to control access to it.
</blockquote>

A __Pattern__ is a solution to a problem in a context.

An __Anti-Pattern__ tells you how to go from a problem to a BAD solution.

__Creational Patterns__ involve object instantiation and all provide a way to decouple a client from the objects it needs to instantiate.

Any pattern that is a __Behavioral Pattern__ is concerned with how classes and objects interact and distribute responsibility.

__Structural Patterns__ let you compose classes or objects into larger structures.

__Class Patterns__ describe how relationships between classes are defined via inheritance. Relationships in class patterns are established at compile time.

__Object Patterns__ describe relationships between objects and are primarily defined by composition. Relationships in object patterns are typically created at runtime and are more dynamic and flexible.