---
author: Robert C. Martin
categories: [book]
class: 4
date: 2016-08-22 14:00:00
description: There are two reason to read this book. One you are a programmer, second you want to become a better programmer. Many thought processes are introduced that will make you a professional programmer, where clarity is king. Creating clean code takes a lot of time and effort, always improving readability and design structure of the code. The key is "code-sense" being able to spot bad code and transform it into clean code.
hidden: true
img-path: /assets/images/books/clean-code.jpg
layout: book
permalink: /clean-code/
title: "Clean Code"
---

<div class="fixed-action-btn horizontal" style="bottom:10px;right:20px;">
  <a onclick="scroll(0,0)" class="btn-floating btn-large red">
    <i class="large material-icons">navigation</i>
  </a>
</div>

* <a href="#clean-code">Clean Code</a>
* <a href="#meaningful-names">Meaningful Names</a>
* <a href="#functions">Functions</a>
* <a href="#comments">Comments</a>
* <a href="#formatting">Formatting</a>
* <a href="#objects-and-data-structures">Objects and Data Structures</a>
* <a href="#error-handling">Error Handling</a>
* <a href="#boundaries">Boundaries</a>
* <a href="#unit-tests">Unit Tests</a>
* <a href="#classes">Classes</a>
* <a href="#systems">Systems</a>
* <a href="#emergence">Emergence</a>
* <a href="#smells-and-heuristics">Smells and Heuristics</a>

<span id="clean-code" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Clean Code

Bad code will bring the company down! It's obvious that messy code takes longer to understand. As the mess continues, productivity will continue to decrease to zero. The only way to increase productivity is to prevent good code from rotting to bad code by writing clean code. It's our job to defend the code and keep it clean. The key is "code-sense" being able to spot bad code and transform it into clean code.

> I could list all of the qualities that I notice in clean code, but there is one overarching quality that leads to all of them. Clean code always looks like it was written by someone who cares. There is nothing obvious that you can do to make it better. All of those things were thought about by the code's author, and if you try to imagine improvements, you're led back to where you are, sitting in appreciation of the code someone left for you - code left by someone who cares deeply about the craft.

> by Michael Feathers

Programmers are the authors of their code, it's their responsiblity for communicating well with their readers. Most of the time are spent reading code instead of writing, making it easy to read should be the main focus when creating clean code. Follow the boy scout rule, leave the campground cleaner than you found it. To develop "code sense" by practicing the tools, techniques, and thought processes used by good programmers.

<span id="meaningful-names" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Meaningful Names

Name is everywhere in software, it's important to pick a intention-revealing name. The name should tell you why it exists, what it does, and how it is used. Avoid disinformation, leaving false clues that obscure the meaning of code. Remember to make meaningful distinctions, be able to distinguish between variable names. Use pronounceable names so that everyone knows what you're are talking about. Classes and objects should have noun or noun phrase names while methods should have verb or verb phrase names. Pick one word per concept, that one word should be the same everywhere in the software. Avoid using the same word for two purposes. A professional programmer understands that clarity is king! You are the author of your story, use names that will help you tell your story to the reader.

<span id="functions" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Functions

The most important rule of functions is that it should be small!! This implies that the function block using if statement, else statements, while statements, and so on should be a function call. This allows you to name a descriptive function name and reduces your function size. Use the Step-down rule, a top-down narrative where every function to be followed by those at the next level of abstraction.

The ideal number of arguments for a function is zero (niladic). The more arguments you have, the more complex your function gets, we want simple and short functions! You can create functions with parameters but think carefully! Give parameter meaningful names that goes with the descriptive function name.

Avoid side effects! Your functions should only do one thing, avoid doing other hidden things. If you do have a side effect, include the side effect in the function name.

Function should either do something or answer something, but not both. Every function, and every block within a function, should have one entry and one exit. There should only be one return statement in a function, no break or continue statements in a loop.

Master programmers writes stories rather than programs. The art of programming is and has always been, the art of language design.

> FUNCTIONS SHOULD DO ONE THING, THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.

<span id="comments" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Comments

Comments are evil! They propagates lies and misinformation, code are always evolving and the comments don't always follow them. The older the comment is, the farther away it is from the code it describes. Truth can only be found in the code, only the code can truly tell you what it does. Comments can be avoided if you write clean code! You can still use comments, focus on intent and informative.

<span id="formatting" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Formatting

Code formatting is imporatant along with readability of you code! Remember readability comes before functionality, the functionality of the code will always change. Readability helps with modifying the functionality, your style and discipline survives.

The newspaper metaphor, think of a well-written newspaper article. The top is where to have your high-level abstraction, as you go down there's more details. The end is where you will find the lowest level functions.

Concepts that are closely related should be kept vertically close to each other. For example, instance variables should be declared at the top of the class. If one functions calls another, they should be vertically close, and the caller should be above the callee. This creates a nice flow down the source code module from high level to low level.

The horizonal formatting limit should be around 80 to 120 characters per line. We can use horizontal white space to associate things that are strongly related and disassociate things that are more weakly related. Every programmer has his own formatting rules, but if he works in a team, then the team rules. Keep to the formatting style that the teams agrees upon.

<span id="objects-and-data-structures" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Objects and Data Structures

Hiding implementation is not just a matter of putting a layer of functions between the variables, it's about abstractions. Abstract interfaces allows its users to manipulate the essence of the data, without having to know its implementation.

Objects hide their data behind abstractions and expose functions that operate on that data. Data structure expose their data and have no meaningful functions. Objects and data structure are virtual opposites!

##### Procedual Shape

{% highlight java %}
  public class Square {
    public Point topLeft;
    public double side;
  }

  public class Rectangle {
    public Point topLeft;
    public double height;
    public double width;
  }

  public class Circle {
    public Point center;
    public double radius;
  }

  public class Geometry {
    public final double PI = 3.14;

    public double area(Object shape) throws NoSuchShapeException
    {
      if (shape instanceof Square) {
        Square s = (Square) shape;
        return s.side * s.side;
      }
      else if (shape instanceof Rectangle) {
        Rectangle r = (Rectangle) shape;
        return r.height * r.width;
      }
      else if (shape instanceof Circle) {
        Circle c = (Circle) shape;
        return PI * c.radius * c.radius
      }
      throw new NoSuchShapeException();
    }
  }
{% endhighlight %}

##### Polymorphic Shapes

{% highlight java %}
  public class Square implements Shape {
    private Point topLeft;
    private double side;

    public double area() {
      return side*side;
    }
  }

  public class Rectangle implements Shape {
    private Point topLeft;
    private double height;
    private double width;

    public double area() {
      return height * width;
    }
  }

  public class Circle implements Shape {
    private Point center;
    private double radius;
    public final double PI = 3.14

    public double area() {
      return PI * radius * radius;
    }
  }
{% endhighlight %}

> Procedual code (code using data structure) makes it easy to add new functions without changing the existing data structure. OO code, on the other hand, makes it easy to add new classes without changing existing functions.

In other words:

> Procedural code makes it hard to add new data structure because all the functions must change. OO code makes it hard to add new functions because all the classes must change.

<span id="error-handling" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Error Handling

Error handling is important, but if it obscures logic, it's wrong. Write Try-Catch-Finally Statement first, when you run the code in the try portion, you are stating that execution can abort at any point and then resume at the catch. Create informative error message and pass them along with your exceptions. Don't return null and avoid passing null into methods!

<span id="boundaries" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Boundaries

We want to control all software in our systems. This includes cleanly integrating foreign code like third-party libraries with the help of design patterns. One way can be creating a wrapper class that implements a interface that is tailored and constrained to meet the needs of the application. It's recommend to use learning tests when exploring third-party API. Code at the boundaries needs clear separation and tests that define expectations.

> It's better to depend on something you control than on something you don't control, lest it end up controlling you.

<span id="unit-tests" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Unit Tests

Test Driven Development (TDD) asks us to write unit tests first, before writing any production code. The tests and the production code are written together, with the tests just a few seconds ahead of the production code. Consider the following three laws:

1. You may not write production code until you have written a failing unit test.
2. You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
3. You may not write more production code than is sufficient to pass the currently failing test.

Keeping tests clean will allow the production code to evolve. The unit tests gives the ability to make sure that changes to the code base worked as expected. Tests preserve and enhance the flexibility, maintainability, and reusability of the production code. Creating clean tests is the same as creating clean code, it follows the same practices, expect it's in a different environment.

Clean tests follow __F.I.R.S.T.__ acronym :

__Fast__: Tests should be fast.

__Independent__: Tests should not depend on each other.

__Repeatable__: Test should be repeatable in any environment.

__Self-Validating__: The tests should have a boolean output (pass or fail).

__Timely__: The tests need to be written in a timely fashion.

> Test code is just as important as production code.

<span id="classes" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Classes

The first rule of classes is that they should be small! With classes we count responsibilities. The name of the class should depend on the responsibility it has. The Single Responsibility Principle (SRP) states that classes should have one responsibility - one reason to change. We want our systems to be composed of many small classes, not a few large ones. Each small class encapsulates a single responsibility, has a single reason to change, and collaborates with a few others to achieve the desired system behaviors.

Classes should have a small number of instance variables. Each of the methods of a class should manipulate one or more of those variables. In general the more variables a method manipulates the more cohesive that method is to its class. When cohesion is high, it means that the methods and variables of the class are co-dependent and hang together as a logical whole. Maintaining cohesion results in many small classes.

<span id="systems" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Systems

The code base is similiar to cities, teams of people who manage particular parts of the city. Some of those people are responsible for the big picture, while others focus on the details. Remember that cities works with the help of levels of abstractions and modularity. Construction is a very different process from use. Create clean systems by applying design patterns, never forget to use the simplest thing that can possibly work.

<span id="emergence" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Emergence

Here are four simple rules that will help make applying principles such as Single Responsibility Principle (SRP) and Dependency Injection Principle (DIP) easier. A testable system is important, writing simple and easy tests will make us think about better designs. Following a simple and obvious rule that says we need to have tests and run them continuously impacts our system's adherence to the primary Object Oriented (OO) goals of low coupling and high cohesion. Once we have a testable system, refactor to clean code. The fact that we have these tests eliminates the fear that cleaning up the code will break it.

1. Runs All the Tests
2. Contains no duplication
3. Expresses the intent of the programmer
4. Minimizes the number of classes and methods

Following the practice of simple design can and does encourage and enable developers to adhere to good principles and patterns that otherwise takes years to learn.

<span id="smells-and-heuristics" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Smells and Heuristics

Here are a list of code smells!!

##### Comments

__C1: Inappropriate Comment__

__C2: Obsolete Comment__

__C3: Redundant Comment__

__C4: Poorly Written Comment__

__C5: Commented-Out Code__

##### Environment

__E1: Build Requires More Than One Step__

__E2: Tests Require More Than One Step__

##### Functions

__F1: Too Many Arguments__

__F2: Output Arguments__

__F3: Flag Arguments__

__F4: Dead Function__

##### General

__G1: Multiple Languages in One Source File__

__G2: Obvious Behavior Is Unimplemented__

__G3: Incorrect Behavior at the Boundaries__

__G4: Overridden Safeties__

__G5: Duplication__

__G6: Code at Wrong Level of Abstraction__

__G7: Base Classes Depending on Their Derivatives__

__G8: Too Much Information__

__G9: Dead Code__

__G10: Vertical Separation__

__G11: Inconsistency__

__G12: Clutter__

__G13: Artificial Coupling__

__G14: Feature Envy__

__G15: Selector Arguments__

__G16: Obscured Intent__

__G17: Misplaced Responsibility__

__G18: Inappropriate Static__

__G19: Use Explanatory Variables__

__G20: Function Names Should Say Whay They Do__

__G21: Understand the Algorithm__

__G22: Make Logical Dependencies Physical__

__G23: Prefer Polymorphism to If/Else or Switch/Case__

__G24: Follow Standard Conventions__

__G25: Replace Magic Number with Named Constants__

__G26: Be Precise__

__G27: Structure over Convention__

__G28: Encapsulate Conditionals__

__G29: Avoid Negative Conditionals__

__G30: Functions Should Do One Thing__

__G31: Hidden Temporal Couplings__

__G32: Don't Be Arbitrary__

__G33: Encapsulate Boundary Conditions__

__G34: Functions Should Descend Only One Level of Abstraction__

__G35: Keep Configurable Data at High Levels__

__G36: Avoid Transitive Navigation__

##### Java

__J1: Avoid Long Import Lists by Using Wildcards__

__J2: Don't Inherit Constants__

__J3: Contants versus Enums__

##### Names

__N1: Choose Descriptive Names__

__N2: Choose Names at the Appropriate Level of Abstraction__

__N3: Use Standard Nomenclature Where Possible__

__N4: Unambiguous Names__

__N5: Use Long Names for Long Scopes__

__N6: Avoid Encodings__

__N7: Names Should Describe Side-Effects__

##### Tests

__T1: Insufficient Tests__

__T2: Use a Coverage Tool!__

__T3: Don't Skip Trivial Tests__

__T4: An Ignored Test Is a Question about an Ambiguity__

__T5: Test Boundary Conditions__

__T6: Exhaustively Test Near Bugs__

__T7: Patterns of Failure Are Revealing__

__T8: Test Coverage Patterns Can be Revealing__

__T9: Tests Should be Fast__

> Clean code is not written by following a set of rules. Professionalism and craftmanship come from values that drive disciplines.