---
categories: [blog]
date: 2016-09-16 10:15:00
layout: post
title: "Object-oriented Programming Notes"
---

__Object-oriented programming__ (OOP) involves programming using object, the object represents an entity in the real world. A class is a template, blue-print, or _contract_ that defines the _properties_ and _behaviors_ for objects. An object has a unique identity, state, and behavior. The _state_ of an object is defined as the _properties_ or _attributes_ of the class template, while the _behavior_ also known as its _actions_ is defined by methods.

> Classes are definitions of objects and objects are created from classes.

A _constructor_ is invoked to create an object using the __new__ operator, remember that a _constructor_ must have the same name as the class itself and do not have a return type. The _constructor_ may have optional parameters, if a class is defined without _constructors_ then a _default constrctuor_ is provided.

The class is a _reference type_ and objects are accessed via the object's _reference variables_.

{% highlight java %}
  Circle myCircle = new Circle();
{% endhighlight %}

The following variable myCircle holds a reference to a Circle object.

After a object is created, its data and methods can be invoked using the _dot operator_: `objectRefVar.dataField` and `objectRefVar.method(arugments)`. The data field is referred to as an _instance variable_, because it is dependent on a specific instance, the same goes for method is referred to as an _instance method_.

A _static variable_ is shared by all objects of the class, also known as _class variables_. A _static method_ cannot access instance members of the class and can be called without creating an instance of the class.

_Visiblity modifiers_ can be used to specify the visibility of a class and its members.

* __private__: accessible only from within its own class
* __default__: accessible by any class in the same package
* __protected__: accessible by subclasses
* __public__: accessible by any other classes

It's common to do data field encapsulation, making data fields private. This protects the data and allows the data to be change only through the object's behavior. The _getter_ and _setter_ methods are sometime used to modify the private data fields.

Normally, you create an object and allow its contents to be changed later. However, there will be times when you want a object whose content cannot changed once the object is created. This is called _immutable object_ and its class an _immutable class_. The requirements are all data fields must be private, there can't be any mutator methods for data fields, and no accessor methods can return a reference to a data field that is mutable.

> Accessor method returns a class's variable or its value (getter) and a Mutator method sets a class's variable or its value.

The keyword __this__ refers to the object itself, is the name of a reference that an object can use to refer to itself. It's common to use _this_ to invoke another constructor of the same class or to reference hidden data fields (private data fields).

An object can contain another object. The relationship between the two is called _composition_. Aggregation models _has-a_ relationships and represents an ownership relationship between two objects. The owner object is called an _aggregating object_ and its class an _aggregating class_. The subject object is called an _aggregated object_ and its class an _aggregated class_.

_Inheritance_ enables you to define a general class (superclass, parent class, or base class) and later extend it to more specialized classes (subclass, child class, or extended class). The keyword __super__ refers to the superclass and can be used to invoke the superclass's methods and constructors. To override a method, the method must be defined in the subclass using the same signature and the same return type as in its superclass.

> Overloading means to define multiple methods with same name but different signatures. Overriding means to provide a new implementation for a method in the subclass.

_Polymorphism_ means that a variable of a _supertype_ can refer to a _subtype_ object. A class defines a type. A type defined by a subclass is called a _subtype_, and a type defined by its superclass is called a _supertype_. A subclass is a specialization of its superclass; every instance of a subclass is also a instance of its superclass, but not vice versa.

The type that declares a variable is called the variable's _declared type_. The _actual type_ of the variable is the actual class for the object referenced by the variable. Here is an example:

{% highlight java %}
  Object o = new GeometricObject();
  System.out.println(o.toString());
{% endhighlight %}

The __declared type__ is Object, while the __actual type__ is GeometricObject, the `toString()` method invoked by `o` is determined by `o`'s actual type.

A method can be implemented in several classes along the inheritance chain, this is known as _dynamic binding_. _Dynamic binding_ works by checking the _actual type_ for the method then checking all proceeding superclass til the `Object` class. Once an implementation is found, the search stops and the first-found implementation is invoked.

One object reference can be typecast into another reference, this is called _casting object_.

{% highlight java %}
  Object o = new Student(); // Implicit casting
  Student b = (Student)o; // Explicit casting
{% endhighlight %}

> It is always possible to cast an instance of a subclass to a variable of a superclass (known as _upcasting_), because an instance of a subclass is _always_ an instance of its superclass. When casting an instance of a superclass to a variable of its subclass (known as _downcasting_), explicit casting must be used to confirm your intention to the compiler with the `(SubclassName) cast notation.

> Use `instanceof` operator to check if the object is an instance of another object.

A _final class_ cannot be extended and a _final method_ cannot be overridden by its subclasses. A final data field is a constant.

An _abstract class_ cannot be used to create objects. An _abstract class_ can contain _abstract methods_, which are implemented in concrete subclasses. _Abstract classes_ are like regular classes, but you cannot create instances of _abstract classes_ using the __new__ operator. An _abstract method_ is defined without implementation, its implementation is provided by the subclasses. A class that contains _abstract methods_ must be defined as _abstract_.

> The constructor in the abstract class is defined as protected, because it is used only by subclasses. When you create a instance of a concrete subclass, its superclass's constructor is invoked to initialize data fields defined in the superclass.

An _interface_ can be used to define common behavior for classes (including unrelated classes). A class-like construct that contains only constants and abstract methods. You can use _interface_ to specify common behavior for objects of related classes or unrelated classes. This is accomplished by letting the class for the object implement this _interface_ using the `implements` keyword. The relationship between the class and the interface is known as _interface inheritance_. Note, _interface_ doesn't have any constructors.

> A class can implement multiple interfaces, but it can only extend one superclass.

> An interface can inherit other interfaces using the `entends` keyword, such an _interface_ is called a _subinterface_.