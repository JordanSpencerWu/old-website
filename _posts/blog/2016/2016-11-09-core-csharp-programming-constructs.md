---
categories: [blog]
date: 2016-11-09 10:00:00
layout: post
title: "Core C# Programming Constructs Notes"
---

The .NET Platform is made up of three key building blocks. The __Common Language Runtime (CLR)__ primary role is to locate, load, and manage .NET objects. The __Common Type System (CTS)__ specification fully describes all possible data types and all programming constructs supported by the runtime. Lastly, the __Common Language Specification (CLS)__ is related specification that defines a subset common types and programming constructs that all .NET programming languages can agree on.

Understand that C# is __not__ the only language that can be used to build .NET applications. This allows the use of other programming languages and that all .NET-aware compilers emit __Intermediate Language (IL)__ instructions and metadata, a binary blob or assembly (*.dll or *.exe). A __manifest__ contains information about the assemblies for example a list of externally referenced assemblies that are required for proper execution. The benefits of compiling into _CIL_ is that all .NET aware compiler produces nearly identical _CIL_ instructions, therefore all languages are able to interact within a well-defined binary arena. The _CIL_ code must be compiled into meaningful CPU instructions known as machine code using __Just In Time (JIT or Jitter)__ compiler.

> Note: __Intermediate Language (IL)__, __Microsoft Intermediate Language (MSIL)__, and __Common Intermediate Language (CIL)__ are describing the same concept.

A given assembly may contain any number of distinct _types_ {class, interface, structure, enumeration, delegate} that comes from the __Common Type System (CTS)__. Each of these _types_ take any number of _members_ given in this set {constructor, finalizer, static constructor, nested type, operator, method, property, indexer, field, read-only field, constant, event}. The _CTS_ defines various _adornments_ that may be associated with a given member. For example visibility trait (public, private, protected), abstract, virtual, and static or instance.

> The _CTS_ establishes a well-defined set of fundamental data types defined in an assembly named __mscorlib.dll__. These intrinsic data types are byte, sbyte, short, int, long , ushort, uint, ulong, float, double, object, char, string, decimal, and bool. Intrinsic data types support default constructors.

C# demands that all programming logic within a type definition {class, interface, structure, enumeration, delegate}. This programming language is case-sensitive and all _keywords_ are lowercase. Namespaces types and member name begin with an initial capital letter and have capitalized the first letter of any embedded words. The `main()` method is the entry point of the application and the class that contains this method is called the _application object_. The `main` method can have one parameter of an array of strings called _args_ and may have a return value of `int` otherwise `void`.

The primitive .NET data types are arranged in a _class hierarchy_ where all types are derived from `System.Object`. This means that all types has the set of methods (`toString()`, `Equals()`, `GetHashCode()`). Also note that many numerical data types derive from `System.ValueType`, descendants of this class are automatically allocated on the stack, therefore, have a very predictable lifetime. On the other hand types that do not have `System.ValueType` in their inheritance chain (such as `System.Type`, `System.String`, `System.Array`, `System.Exception`, and `System.Delegate`) are allocated on the garbage-collected heap.

Strings are _immutable_ meaning that whenever you manipulate a string, it returns a new copy of the modified string. A _verbatim_ string disables the processing of the escape character and print out a string as it is, to use it prefix a string literal with the `@` symbol (useful for directory/file paths). Remember to use a parse method when converting a string to a numerical type or use a convert method to convert a string to a data type. Strings are reference type but when comparing strings, the equality operators have been redefined to compare the _values_ of string object, not the object in memory to which they refer. Lastly, use a `StringBuilder` when you want a mutable string.

_Widening_ data type conversion is when you _upward cast_ that does not result in a loss of data, an example would be changing a `short` to an `int`. _Narrowing_ is the logical opposite of widening, in that a larger value is stored within a smaller data type variable, this may cause loss of data from overflow or underflow. We can use explicit cast to allow narrowing if you don't mind loss of data. You may use `checked` keyword to keep for loss of data by enabling project-wide overflow/underflow data checking (used for development and disable during production).

C# allows implicitly typed local variables using the keyword `var`. This only applies in a method or property scope. It is illegal to use `var` to define return value, parameters, or field data of custom type. The `var` keyword must be assigned an initial value of the exact time of declaration and cannot be assigned null. Also note that `var` is a strongly type data (cannot change to different data type once it is defined an initial data type). This is used with __LINQ__ where you don't know the data types from the _query expression_.

Methods can be implemented within the scope of classes or structures (as well as prototyped within interface type). Static members are scoped to the class level and can be invoked without creating a class instance. Method has _parameter modifier_ which allows extra functionality to a given parameter {none, out, ref, params}. Additionally methods has optional/default parameter, you can invoke methods using named parameters, and methods overloading.

> If a reference type is passed by reference, the callee may change the values of the object's state data, as well as the object it is referencing.

> If a reference type is passed by value, the callee may change the values of the object's state data, but _not_ the object it is referencing.

Value types can never be assigned the value `null`, as that is used to establish an empty object reference. It can be a nullable data type, by adding a suffixed question mark symbol (?), is only applicable to value types. Another feature is the `??` Operator which assigns a value to a nullable type if the retrieved value is in fact `null`.