---
categories: [blog]
date: 2016-11-27 10:00:00
layout: post
title: "So You Think You Know Javascript?"
---

JavaScript is used intensively in web development and is starting to branch out to other industries like virtual reality and native application. This language is different from the other languages that uses the classical inheritance, instead it uses prototypal inheritance. When I was learning JavaScript there were many features that caused unexpected results for example scoping and type conversions. This blog will be my notes on JavaScript.

##### Scopes, Callbacks and Closures

In JavaScript functions are the first class citizen and are the only way to create a scope. Whenever you declare a `var` variable, it is scope to the closest function scope, otherwise it will be scope to the global scope. Additional the arguments passed into the functions are scope to the function. There are a few ways to create functions in JavaScript:

{% highlight javascript %}
  // function declaration
  function example1() {
    console.log("example1");
  }

  // function expression
  var example2 = function() {
    console.log("example2");
  };

  // named function expression
  var example3 = function example() {
    console.log("example3");
  };
{% endhighlight %}

Notice that the function expressions requires the semi-colon at the end while the function delaration don't. The following functions are scope to the global scope which will pollute the global scope. To create a namespace in JavaScript we use immediately-invoked function expression (IIFE), it’s important that this function cannot be invoked again and executes once. It’s used for creating a namespace that doesn't affect the global scope and encapsulate public/private members.

{% highlight javascript %}
  (function(global) {
    console.log("THIS IS IN AN IIFE);

    function privateFunction() {
      console.log("I am private");
    }

    global.public1 = function() {
      privateFunction();
      console.log("IN PUBLIC 1");
    };
  })(jQuery);
{% endhighlight %}

An important topic in JavaScript is hoisting, JavaScript is compiled and executed by the browser. During the compile time the left hand side `var` variable are hoisted to the closest function scope while the right hand side expression stays. The hoisting will assign the hoisted `var` variable the value of `undefined` until it is assigned a value. Function declaration are also hoisted to the closest function scope while the function expression acts like the hoisting of the `var` variable. JavaScript uses Static/Lexical scope which will bind values to a variable during compile time.

A Closure is a function that uses variables from its parent scope. Remember that functions creates a new scope and can be used to store variables for other functions to use, this allows us to use higher order functions. We are able to pass in function as arguments to a function and also return a function in JavaScript. The power of Closures is being able to reuse functions that have different closure scopes.

The example below is a common issue that appears in JavaScript and understanding the languages will help you debug your programs. 

{% highlight javascript %}
  var people = ["Foo", "Bar", "Baz"];
  var list = document.getElementById("people-list");

  // -------------------------
  // BAD Solution

  for (var i = 0; i < people.length; i++) {
    var person = people[i];
    var element = document.createElement("li");
    element.innerText = person;

    element.addEventListener("click", function() {
    alert("you clicked on " + person + ", at index " + i);
    });
  }

  list.appendChild(element);

  // -------------------------
  // Solution 1

  for (var i = 0; i < people.length; i++) {
    var person = people[i];
    var element = document.createElement("li");
    prepareElementForPerson(person, element);
    list.appendChild(element);
  }

  function prepareElementForPerson(person, element) {
    element.innerText = person;
    element.addEventListener("click", function() {
      alert("You clicked on " + person);
    });
  }

  // -------------------------
  // Solution 2

  for (var i = 0; i < people.length; i++) {
    var person = people[i];
    var element = document.createElement("li");
    (function() {
      var person2 = person;
      element.innerText = person2;
      element.addEventListener("click", function() {
        alert("You clicked on " + person2);
      });
    })();

    list.appendChild(element);
  }

  // -------------------------
  // Solution 3

  people.forEach(function(person) {
    var element = document.createElement("li");
    element.innerText = person;
    element.addEventListener("click", function() {
      alert("You clicked on " + person);
    });

    list.appendChild(element);
  });

  // -------------------------
  // Solution 4
  for (let i = 0; i < people.length; i++) {
    let person = people[i];
    let element = document.createElement("li");
    element.innerText = person;

    element.addEventListener("click", function() {
      alert("You clicked on " + person);
    });

    list.appendChild(element);
  }
{% endhighlight %}

##### What Is This?

The `this` keyword is binded at runtime and depends on how it is invoked. When an object invokes a function with the keyword `this`, the `this` will be the object that invoked the function. It is common to use `call`, `apply` and `bind` to bind the `this` variable to the correct scope. The `call` and `apply` are similar, the only difference is that one takes in arguments parameter list and the other takes in an array of arguments, they can be used to borrow functions. The `bind` function can be used to currying or part application which allows constructing functions that allows partial application of a function's arguments. In ES6 the arrow function feature will lexical scope the `this` keyword for you.

{% highlight javascript %}
  // -----------------------
  // ES arrow function
  var person = {
    firstName: "Jordan",
    printNameDelayed: function() {
      window.setTimeout(() => {
        console.log(this.firstName);
      }, 1000);
    }
  };

  person.printNameDelayed();

  // --------------------------
  // Converts to ES5
  var person = {
    firstName: "Jordan",
    printNameDelayed: function() {
      var _this = this;
      window.setTimeout(function() {
        console.log(_this.firstName);
      }, 1000);
    }
  }
{% endhighlight %}

##### Prototypes

JavaScript uses the prototypal inheritance and that everything in JavaScript is an object. Each object has its own property, you can use `hasOwnProperty()` to check if that object has a specific property. If that object doesn't have that specific property, you can check to see if it's prototype has that property using `object.__proto__.hasOwnProperty("someProperty")`, don't forget to use the `call` method to bind `this` to the function call if you want to invoked a function that is in the prototype chain. You can create objects using functions, this is called function prototype. To do this you use the `new` keyword on a function constructor, a function constructor uses the `this` keyword to define properties and should not return anything. In ES6 the `class` feature makes creating object inheritance a lot easier.

{% highlight javascript %}
  // --------------------------
  // ES5 object inheritance
  function Person(name, rank) {
    this.name = name;
    this.rank = rank;
  }

  Person.prototype = {
    sayName: function() {
      console.log("Hello, I am " + this.name);
    },
    firePerson: function(person) {
      return false;
    },
    giveRaises: function() {
      return false;
    }
  }

  function Manager(name, rank) {
    Person.call(this, name, rank);
  }

  Manager.prototype = Object.create(Person.prototype);
  Manager.prototype.firePerson = function(person) {
    return this.rank > person.rank;
  };

  function Ceo(name, rank) {
    Manager.call(this, name, rank);
  }

  Ceo.prototype = Object.create(Manager.prototype);
  Ceo.prototype.giveRaises = function() {
    return true;
  };

  // --------------------------
  // ES6 object inheritance
  class Person (
    constructor(name, rank) {
      this.name = name;
      this.rank = rank;
    }

    sayName() {
      console.log("Hello, I am " + this.name);
    }

    firePerson(person) {
      return false;
    }

    giveRaises() {
      return false;
    }
  )

  class Manager extends Person {
    constructor(name, rank) {
      super(name, rank);
    }

    firePerson(person) {
      return this.rank > person.rank;
    }
  }

  class Ceo extends Manager {
    constructor(name, rank) {
      super(name, rank);
    }

    giveRaises() {
      return true;
    }
  }
{% endhighlight %}

Babel provides a read-eval-print loop (REPL) that allows you to see what JavaScript compiles to, this is a great tool to understanding the JavaScript language. Click <a href="https://babeljs.io/repl/" target="_blank">here</a> to check it out.