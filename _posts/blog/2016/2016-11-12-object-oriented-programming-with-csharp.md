---
categories: [blog]
date: 2016-11-12 10:00:00
layout: post
title: "Object-Oriented Programming With C# Notes"
---

A _class type_ is a user-defined type that is composed of field data (often called _member variables_) and members that operate on this data (such as constructors, properties, methods, events, and so forth). Object must be allocated into memory using the _new_ keyword. Constructors allows the state of an object to be established at the time of creation. Never have a return value and always name identically to the class they are constructing. The _this_ keyword provides access to the current class instance and can be used for _constructor chaining_.

A C# class may define any number of _static members_ using the _static_ keyword. When you do so, the member in question must be invoked directly from the class level. When you defined a static field data, the memory is shared by all objects of that class. When defining static methods, you can invoked this methods without creating any instance of the class. Static constructors can be used to assign values to the static data fields, a given class can only have one static constructor that don't have any parameters, it executes exactly one time before any instance of the class or before the first static member invoked by the caller. A static class cannot be created using the _new_ keyword and can only have static members.

##### Encapsulation

Whenever I think of _encapsulation_, the first thing that comes to my mind is data hiding. The ability to hide unnecessary implementation details from the object user. C# provides access modifiers to limit access to the class and nested types, they are `public`, `private`, `protected`, `internal`, and `protected internal`. By default, type members are _implicitly private_ while types are _implicitly internal_. 

The concept of encapsulation revolves around the notion that an object's internal data should not be directly accessible from an object instance. To do this we set the data field to `private` and create `public` accessor (get) and mutator (set) methods. The traditional way is to create a getter and setter public methods for a given data field. The .NET languages prefer to enforce data encapsulation state data using _properties_ (accessor and mutator methods).

Use _properties_ when setting class data in the constructors, this will reduce duplication. Also note that you can create read-only and write only _properties_ by excluding the method. Static properties can be used for static data field. Use _automatic properties_ when you need to get and set a value without any business logic, it must support both read and write functionality. When using _automatic properties_ be sure to assign value to them inside the constructors.

C# offers the _const_ keyword to define constant data. Always remember that the initial value assigned to the constant must be specified at the time you define the constant, value known at compile time. A _read-only_ field data is similar to the _const_ except for the value assigned to a read-only field can be determined at runtime. The read-only field can be static and the value can be assign inside the static constructor.

##### Inheritance

Inheritance helps with code reuse and it comes in two flavors: inheritance (the "is-a" relationship) and the containment/delegation model (the "has-a" relationship). 

The "is-a" relationship, formally termed _classical inheritance_ allows you to build new class definitions that extend the functionality of an existing class. An example is a MiniVan "is-a" type of Car and the MiniVan can inherit all the functionality of its base class Car. Derived classes have access to each public/protected member defined within the parent class, use the `base` keyword when you want to access members from the base class. When a base class defines protected data or protected members, it establishes a set of items that can be accessed directly by any descendent.

The "has-a" relationship is known as the containment/delegation model or aggregation. An example is each Employee "has-a" BenefitPackage, this means that the Employee class has a data field of BenefitPackage type. To expose the functionality of the contained object BenefitPackage to the outside world requires delegation. _Delegation_ is simply the act of adding public members to the containing class to make use of the contained object's functionality. It's possible to define a type (enum, class, interface, struct, or delegate) directly within the scope of a class or structure, this is called _nesting type_.

In C# a class can extend only one direct base class. Note you can use the `seal` keyword on a class to prevent inheritance from occurring. On the related note, sometime you might not wish to seal an entire class, but simply want to prevent derived types from overriding particular virtual methods. It is possible to override method from the parent class using `override` and `virtual` keywords. The `virtual` keyword allows the base class to define a method that _may be_ overridden by a subclass.

##### Abstract

There might be times when you want to make a base class that cannot be instantiate and only contains the common data and functionality for derived classes to inherit from, that's where the keyword `abstract` comes in. An `abstract` class may define any number of _abstract members_, abstract members are used when you wish to define a member that does not supply a default implementation, but must be accounted for by each derived class. This provides _polymorphic interface_ on each descendent, leaving them to contend with the task of providing the details behind your abstract methods. 

C# provides a facility that is the logical opposite of method overriding, termed _shadowing_. This might be used when inheriting from a third party .NET software package which you don't have any control over. You may use the `new` keyword on the method to explicitly state that the derived type's implementation is intentionally designed to effectively ignore the parent's version. There are _casting operations_ that are used to change the type of an object, to explicit cast using `(ClassIWantToCastTo)referenceIHave`.

C# language provides the `is` (returns false) and `as` (return null) keywords to determine whether two items are compatible.

##### Exception Handling

The .NET base class identifies numerous exceptions, provides standard techniques to send and trap runtime errors called _structured exception handling_ (SEH). You may throw an exception object, the object contains a human-readable description of the problem. The .NET base class libraries define many classes that derive from `System.Exception` that provides many useful properties you can use. Exceptions that are thrown by the .NET platform are called _system exceptions_. Sometime it's advantageous to build a _strongly typed exception_ that represents the unique details of your current problem. For all application-level exceptions, you may create a custom exception by inheriting from `System.ApplicationException`.

##### Interface

A _interface_ is nothing more than a named set of abstract members. The specific members defined by an interface depends on the exact behavior it is modeling, in other words expresses a _behavior_ that a given class or structure may choose to support. The main difference between a interface and abstract class is that the abstract class does define a set of abstract members, it is also free to define any number of constructors, field data, non-abstract members (with implementation), and so on. Interface only contains abstract member definition. You create an interface using the `interface` keyword, all interface members are implicitly public and abstract. It is possible to pass in an interface type into a method and return an interface type, this makes it highly polymorphic.