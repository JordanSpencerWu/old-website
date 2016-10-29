---
author: Douglas Crockford
categories: [book]
class: 10
date: 2016-10-28 10:00:00
description: The authors talks about the good parts of JavaScript. He describes that every programming languages has good and bad parts. We can create amazing software using only the good parts and avoiding the bads ones. Using only the good parts will increase readability and maintainability!
hidden: true
img-path: /assets/images/books/javascript-the-good-parts.jpg
layout: book
permalink: /javascript-the-good-parts/
title: "JavaScript The Good Parts"
---

The very good ideas include functions, loose typing, dynamic objects, and an expressive object literal notation. The bad ideas include a programming model based on global variables.

The values produced by `typeof` are 'number', 'string', 'boolean', 'undefined',
'function', and 'object'.

The `&&` operator produces the value of its first operand if the first operand is falsy. Otherwise, it produces the value of the second operand.

The `||` operator produces the value of its first operand if the first operand is truthy. Otherwise, it produces the value of the second operand.

##### list of _falsy_ values:

1. false
2. null
3. undefined
4. The empty string ''
5. The number 0
6. The number NaN

__Note:__ All other values are truthy!

##### Objects

The simple types of JavaScript are numbers, strings, booleans (true and false), null, and undefined. All other values are objects.

The quotes around a property’s name in an object literal are optional if the name would be a legal JavaScript name and not a reserved word. Values can be retrieved from an object by wrapping a string expression in a [ ] suffix. If the string expression is a constant, and if it is a legal JavaScript name and not a reserved word, then the . notation can be used instead.

{% highlight javascript %}
  var object = {
    "first-name": "Jordan",
    last_name: "Wu"
  };

  object["first-name"]  // returns Jordan
  object.last_name      // returns Wu
{% endhighlight %}

Every object is linked to a prototype object from which it can inherit properties. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. Use `object.hasOwnProperty(variable)` to determine whether the property name is truly a member of the object or was found instead on the prototype chain and using `typeof` to exclude functions.

Objects produced from object literals are linked to Object.prototype. Function objects are linked to Function.prototype (which is itself linked to Object.prototype).

##### Functions

Objects produced from object literals are linked to Object.prototype. Function objects are linked to Function.prototype (which is itself linked to Object.prototype).

Functions can be defined inside of other functions. An inner function of course has access to its parameters and variables. An inner function also enjoys access to the parameters and variables of the functions it is nested within. The function object created by a function literal contains a link to that outer context. This is called _closure_.

In addition to the declared parameters, every function receives two additional parameters: _this_ and _arguments_. There is no runtime error when the number of arguments and the number of parameters do not match. If there are too many argument values, the extra argument values will be ignored. If there are too few argument values, the undefined value will be substituted for the missing values. There is no type checking on the argument values: any type of value can be passed to any parameter.

__The Method Invocation Pattern__ is when a function is stored as a property of an object, we call it a method. When a method is invoked, _this_ is bound to that object. A method can use _this_ to access the object so that it can retrieve values from the object or modify the object.

__The Function Invocation Pattern__ is when a function is not the property of an object, then it is invoked as a function. When a function is invoked with this pattern, _this_ is bound to the global object.

JavaScript is a prototypal inheritance language. __The Constructor Invocation Pattern__ is when a function is invoked with the _new_ prefix, then a new object will be created with a hidden link to the value of the function’s prototype member, and _this_ will be bound to that new object. Functions that are intended to be used with the _new_ prefix are called constructors. By convention, they are kept in variables with a capitalized name.

__The Apply Invocation Pattern__, Because JavaScript is a functional object-oriented language, functions can have methods. The _apply_ method lets us construct an array of arguments to use to invoke a function. It also lets us choose the value of _this_.

The _return_ statement can be used to cause the function to return early. When _return_ is executed, the function returns immediately without executing the remaining statements. A function always returns a value. If the return value is not specified, then _undefined_ is returned. If the function was invoked with the _new_ prefix and the _return_ value is not an object, then _this_ (the new object) is returned instead.

The _throw_ statement interrupts execution of the function. It should be given an exception object containing a _name_ property that identifies the type of the exception, and a descriptive _message_ property.

JavaScript allows the basic types of the language to be _augmented_, that adding a method to `Object.prototype` makes that method available to all objects.

_Scope_ in a programming language controls the visibility and lifetimes of variables and parameters. JavaScript does have function scope. That means that the parameters and variables defined in a function are not visible outside of the function, and that a variable defined anywhere within a function is visible everywhere within the function.

We can use functions and closure to make modules. A module is a function or object that presents an interface but that hides its state and implementation.

If we have those methods return _this_ instead of undefined, we can enable cascades.

Functions can use objects to remember the results of previous operations, making it possible to avoid unnecessary work. This optimization is called _memoization_. JavaScript’s objects and arrays are very convenient for this.

##### inheritance

JavaScript is a prototypal language, which means that objects inherit directly from other objects.

__Use Object Specifiers__ when a constructor is given a very large number of parameters.

Prototypal inheritance is conceptually simpler than classical inheritance: a new object can inherit the properties of an old object.

One weakness of the inheritance patterns we have seen so far is that we get no privacy. All properties of an object are visible.

##### Arrays

JavaScript provides an object that has some array-like characteristics. An
array literal is a pair of square brackets surrounding zero or more values separated by commas. An array literal can appear anywhere an expression can appear. The first value will get the property name '0', the second value will get the property name '1', and so on.

A common error in JavaScript programs is to use an object when an array is required or an array when an object is required. The rule is simple: when the property names are small sequential integers, you should use an array. Otherwise, use an object.

JavaScript does not have a good mechanism for distinguishing between arrays and objects. We can work around that deficiency by defining our own is_array function:

{% highlight javascript %}
  var is_array = function (value) {
    return value &&
      typeof value === 'object' &&
      typeof value.length === 'number' &&
      typeof value.splice === 'function' &&
      !(value.propertyIsEnumerable('length'));
  };
{% endhighlight %}

JavaScript provides a set of methods for acting on arrays. The methods are functions stored in Array.prototype. Learn more <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array" target="_blank">here</a>.

##### Regular Expression

Many of JavaScript’s features were borrowed from other languages. The syntax came from Java, functions came from Scheme, and prototypal inheritance came from Self. JavaScript’s Regular Expression feature was borrowed from Perl.

Regular expressions are used with methods to search, replace, and extract information from strings. The methods that work with regular expressions are `regexp.exec`, `regexp.test`, `string.match`, `string.replace`, `string.search`, and `string.split`. Click <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions" target="_blank">here</a> to learn more.

##### Methods

JavaScript includes a small set of standard methods that are available on the standard types. The best way to see all the methods is by looking at this <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript" target="_blank">website</a>.