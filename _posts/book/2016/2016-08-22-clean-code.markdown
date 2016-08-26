---
author: Robert C. Martin
categories: [book]
class: 4
date: 2016-08-22 14:00:00
description: Currently reading this book.
hidden: true
img-path: /assets/images/clean-code.jpg
layout: book
permalink: /clean-code/
title: "Clean Code"
---

<div class="fixed-action-btn horizontal" style="bottom:10px;right:20px;">
  <a onclick="scroll(0,0)" class="btn-floating btn-large red">
    <i class="large material-icons">library_books</i>
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

The most important rule of functions is that it should be small!! This implies that the function block using if statement, else statements, while statements, and so on should be a function call. This allows you to name a descriptive function name and reduces your function size. Use the Step=down rule, a top-down narrative where every function to be followed by those at the next level of abstraction.

The ideal number of arguments for a function is zero (niladic). The more arguments you have, the more complex your function gets. We want simple and short functions! You can create functions with parameters but think carefully! Give parameter meaningful names that goes with the descriptive function name.

Avoid side effects! Your functions should only do one thing, avoid doing other hidden things. If you do have a side effect, change the function name to include the side effect!

Function should either do something or answer something, but not both. Every function, and every block within a function, should have one entry and one exit. There should only be one return statement in a function, no break or continue statements in a loop.

Master programmers writes stories rather than programs. The art of programming is and has always been, the art of language design.

> FUNCTIONS SHOULD DO ONE THING, THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.

<span id="comments" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Comments

Comments are evil! They propagates lies and misinformation, code are always evolving and the comments don't always follow them. The older the comment is, the farther away it is from the code it describes. Truth can only be found in the code, only the code can truly tell you what it does. Comments can be avoided if you write clean code! You can still use comments, focus on intent and informative.

<span id="formatting" style="display:block;height:60px;margin-top:-60px;visibility:hidden;"></span>

#### Formatting

Code formatting is imporatant along with readability of you code! Remember readability comes before functionality, the functionality of the code will always change. Readability helps with modifying to the functionality, your style and discipline survives.

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

Currently reading...

