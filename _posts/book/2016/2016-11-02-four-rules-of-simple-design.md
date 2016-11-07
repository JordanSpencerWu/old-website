---
author: Corey Haines
categories: [book]
class: 12
date: 2016-11-02 10:00:00
description: This book talks about simple design we should think about when constructing code. It talks about TDD and how it can influence the design of the code. All of the design principles are given in an example using Conway's Game of Life using Ruby.
hidden: true
img-path: /assets/images/books/understanding-the-four-rules-of-simple-design.png
layout: book
permalink: /understanding-the-four-rules-of-simple-design/
title: "Understanding The 4 Rules of Simple Design"
---

Rather than planning for change points, we build systems, by applying simple design principles, that can change easily at ANY point.

##### 4 Rules of Simple Design

1. Tests Pass
2. Expresses Intent
3. No Duplication (DRY)
4. Small

##### Test Names Should Influence Object's API

The idea of naming, and how it relates to the intent of your code can seen when looking at the symmetry between test names and the test code. When we write our tests, we should be spending time on our test names.

{% highlight ruby %}
  def test_a_new_world_is_empty
    world = World.new
    assert_true world.empty?
  end

  def test_a_cell_can_be_added_to_the_world
    world = World.new
    world.set_living_at(1, 1)
    assert_true world.alive_at?(1, 1)
  end

  def test_after_adding_a_cell_the_world_is_not_empty
    world = World.new
    world.set_living_at(1, 1)
    assert_false world.empty?
  end
{% endhighlight %}

Focusing on the symmetry between a good test name and the code
under tests is a subtle design technique.

##### Duplication of Knowledge about Topology

A good way to detect knowledge duplication is to ask what happens if we want to change something. What effort is required? How many places will we need to look at and change? A good example from the Conway's Game of Life is to extract the data that represents the location into its own class. This way if you change from two dimensions to three dimensions, you just have to change the `Location` class.

{% highlight ruby %}
  class Location
    attr_reader :x, :y
  end

  class World
    def set_living_at(location)
      #...
    end
    def alive_at?(location)
      #...
    end
  end

  class LivingCell
    attr_reader :location
    end

  class DeadCell
    attr_reader :location
  end
{% endhighlight %}

This makes the code more adaptable and readable.

#### Behavoir Attractors

Whenever we have a new method, a new behavoir, an important question is "where do we put it?" What type does this belong to? Imageine we find ourselves in need of asking for the neighbor locations for a given x, y.

{% highlight ruby %}
  def neighbors_of(x, y)
    # calculate the coordinates of neighbors
  end
{% endhighlight %}

We can add this method in several places, but the most logical place is in the `Location` class. This class focus on the topology, our behavior is asking for what locations constitute the neighborhood around a given location.

> By aggressively eliminating knowledge duplication through reification, we often find that we have built classes that naturally accept new behaviors that arise. They not only accept, but attract them; by the time we are looking to implement a new behavior, there is already a type that is an obvious place to put it.

##### Testing State vs Testing Behavoir

An alternate way to develop a system is to focus on the behavoir rather than the state of the objects. Think about what behaviors you expect and have our tests center around those. Building our system in a behavior-focused way is about only building the things that are absolutely needed and only at the time they are needed.

Here's an example from the book:

{% highlight ruby %}
  def test_a_new_world_is_empty
    assert_true World.new.empty?
  end

  # this behavior test will help create other tests (above test)
  def test_an_empty_world_stays_empty_after_a_tick
    world = World.new
    next_world = world.tick
    assert_true next_world.empty?
  end
{% endhighlight %}

##### Don't Have Tests Depend on Previous Tests

Looking above at the test case test_an_empty_world_stays_empty_after_a_tick, the test name indicates we are starting with an empty world, but the test code does not specify this explicitly. There is an assumption here that new worlds are empty, what if we don't start with an empty world?

The idea of letting the test name influence the test code and use that to make the test code a bit more explicit, let's explicitly ask for an empty world.

{% highlight ruby %}
  def test_an_empty_world_stays_empty_after_a_tick
    world = World.empty
      next_world = world.tick
    assert_true next_world.empty?
  end
{% endhighlight %}

> The outside world can’t use new to instantiate an object with an expectation of a specific state. Instead, there must be an explicitly named builder method on the class to create an object in a specific, valid state.

##### Breaking Abstraction Level

In a earlier example, we looked at:

{% highlight ruby %}
  def test_world_is_not_empty_after_adding_a_cell
    world = World.empty
    world.set_living_at(Location.new(1,1))
    assert_false world.empty?
  end
{% endhighlight %}

We can see that we are testing for a empty world then adding a cell into the empty world. However, looking at the test code, we can see details about the topology: the (1,1). In this case, the test code is implying that the `empty` method is somehow dependent on the coordinates, themselves. To improve this, we hide the details of the topology from the world object.

{% highlight ruby %}
  def test_world_is_not_empty_after_adding_a_cell
    world = World.empty
    world.set_living_at(Location.random)
    assert_false world.empty?
  end
{% endhighlight %}

By isolating ourselves from changes to the topology, the internals of the Location, we help ensure that this test won’t break if we change something about the underlying coordinate system. You can also use test double.

##### Naive Duplication

{% highlight ruby %}
  class Cell
    attr_reader :alive # true | false

    def alive_in_next_generation?
      if alive
        number_of_neighbors == 2 || number_of_neighbors == 3
      else
        number_of_neighbors == 3
    end
    end
  end
{% endhighlight %}

These 3's are not the same. In our alive case, the 3 is more closely linked to the 2 in the concept of a “stable neighborhood,” while in the dead case, it is linked to something like a “genetically fertile neighborhood.” A good technique is to refactor the conditions into methods.

{% highlight ruby %}
  class Cell
    # ...
    def alive_in_next_generation?
      if alive
        stable_neighborhood?
      else
        genetically_fertile_neighborhood?
      end
    end
  end
{% endhighlight %}

##### Procedural Polymorphism

Looking at the code above, the `alive` condition isn't a very good choice. Resolving this requires us to talk a bit about polymorphism in general. Polymorphism is about being able to call a method/send a message to an object and have more than one possible behavior. A seemingly quick solution would be to make it something like state and raise it to types: `LivingCell` and `DeadCell`.

{% highlight ruby %}
  class LivingCell
    def stays_alive?
      neighbor_count == 2 || neighbor_count == 3
    end
  end
  class DeadCell
    def comes_to_life?
      neighbor_count == 3
    end
  end
{% endhighlight %}

A great benefit is that we can add a new state, by adding a new class. We _extend_ our system, rather than modify it.

{% highlight ruby %}
  class ZombieCell
    def alive_in_next_generation?
      # new, possibly more complex rules
    end
  end
{% endhighlight %}

##### Making Assumption About Usage

Let's look at the Cell classes.

{% highlight ruby %}
  class LivingCell
    def stays_alive?(number_of_neighbors)
      number_of_neighbors == 2 || number_of_neighbors == 3
     end
  end
  class DeadCell
    def comes_to_life?(number_of_neighbors)
      number_of_neighbors == 3
    end
  end
{% endhighlight %}

Notice we talking about classes here. A class tend to encapsulate and provide behavoir around state. Methods on them are generally involved in working with that state. In this state the methods are not accessing internal state. Why don’t we reify the idea of a rule? One of the key parts of being easier to change (i.e. a better design) is being able to more easily find where the changes need to occur; this is what good naming contributes to.

{% highlight ruby %}
  class LivingCellRules
    def stays_alive?(number_of_neighbors)
      number_of_neighbors == 2 || number_of_neighbors == 3
    end
  end
  class DeadCellRules
    def comes_to_life?(number_of_neighbors)
      number_of_neighbors == 3
    end
  end
{% endhighlight %}

##### Unwrapping an Object

An example, imagine we have the following two location objects.

{% highlight ruby %}
  class Location
    attr_reader :x, :y
  end

  location1 = Location.new(1, 1)
  location2 = Location.new(1, 2)

  if location1.equals?(location2)
    # Do something interesting
  end

  class Location
    attr_reader :x, :y
    def equals?(other_location)
      self.x == other_location.x && self.y == other_location.y
    end
  end
{% endhighlight %}

This `equals?` method doesn’t conform to our constraint: it is asking other_location to return its x and y. This isn’t allowed. A technique that call unwrapping, follows alternate form of equals.

{% highlight ruby %}
  class Location
    attr_reader :x, :y
    def equals?(other_location)
      other_location.equals_coordinate?(self.x,self.y)
    end
    def equals_coordinate?(other_x, other_y)
      self.x == other_x && self.y == other_y
    end
  end
{% endhighlight %}

This new form of equals only allows the object access to it's own states. The section goes deeper into a constraints in coderetreat is writing your code with “no return values.”

##### Inverted Composition as a Replacement for Inheritance

Inheritance is often used as way of creating “reuse” rather than eliminating duplication.