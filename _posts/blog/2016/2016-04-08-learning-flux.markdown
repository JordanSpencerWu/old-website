---
layout: post
title:  "Learning Flux"
date:   2016-04-08 13:15:00
---
Flux is an application architecture developed by Facebook for creating 
client-side web application. The main focus of this architecture is 
to utilize the unidirectional data flow. Unidirectional data flow will 
allow more control on how states changes when using React.js. You can 
implement this architecture into your web application without introducing 
a lot of new code. The Flux application has three major parts: the 
__dispatcher__, the __stores__, and the __views__. In this blog I explain each of these 
parts in my own words.

#### Why Use Flux?

In a large web application that utilize React components, 
it's hard to keep track of states and properties of every React component. 
With the Flux architecture we are able to predict the data of each react component using 
unidirectional data flow. The goal of Flux is to organize your application so that you can 
keep track of the data flow in your application. Flux is used by Facebook 
in their client-side web application, Facebook created Flux to eliminate dependencies 
and cascading updates that leads to unpredictable results. This architecture allows 
more control of data flow which lead to predictable results.

#### Dispatcher

The __dispatcher__ is where you manages all the data flow in the web application. The goal 
of the __dispatcher__ is to pass data into a store. The data is called __actions__ which will be 
used in the __store__ to change the state of the data. Each __store__ will register a 
__dispatcher__ and depending on the __actions__ type will update the data. The __dispatcher__ 
only has one task of providing stores with __actions__ for the data in the store to change. Flux provides a __dispatcher__ 
module that you can use with Node.js. Click 
<a href="https://facebook.github.io/flux/docs/dispatcher.html#content" target="_blank">here</a> to 
see the API.

{% highlight javascript %}
  import Flux from 'flux';

  var AppDispatcher = new Flux.Dispatcher();

  export default AppDispatcher;
{% endhighlight %}

The following code above will import the __flux__ module once you run `npm install --save-dev flux` or when 
you have the __flux__ module inside the __node_modules__ folder. This code will create a 
new __dispatcher__ instance that you will use in your web application. Remember to import this 
__dispatcher__ into your application using the relative path, you will use this dispatcher in your __stores__ 
and when you create __actions__.

#### Stores

The __stores__ contains all the states and logic! In React.js the components updates when the 
state changes, the goal of the __store__ is to keep track of the states. A __store__ is 
registered to a __dispatcher__, you provide a callback function to the __dispather__ to call 
when the __dispatcher__ is dispatched. This means that when a __action__ is maded in a React component that 
will change the state of the component, the __dispatcher__ is called using the __dispatch__ method. The __store__ 
holds all the data and logic in your application, this is where all your data lives and the 
__store__ controls how the data are changed!! Remember to import your __store__ into your react stateful components 
to allow the component to update by adding a listener to a event that will run `setState` function with the new data.

#### Views / Controller-Views

Remember that React.js is just the View in the MVC web design pattern. A React component is 
how your data will interact with the view. This is also known as a controller-view because it will 
get the data from the stores and pass data down it's descendants components as properties. React component 
allow us to create events and listeners to specific events like on click, on keydown, on change, and more. 
Whenever a user interact with a component there are events that we need to listen to, these events might 
change the state of our component. We call this __actions__ that will change the state of the 
component. The only way to change the state of our data is in our __stores__, we have use a __dispatcher__ 
to pass the data to the callback function in the __store__ then update our React component. This is where we have to use the __dispatcher__ with the 
__dispatch__ method to notify our __stores__ that a __action__ was made. The most important part of this 
is that the controller-view doesn't modify the data. this decouples the logic from the view.

#### Actions

We now know that __actions__ are created when the user interacts with the component that will change 
the state of our component. Actions are passed into the __dispatcher__ to be used in the __stores__. For our 
store to know what to do we need a create __actionType__ property that will tell the __store__ which 
logics to run, the other arguments pass is the data that we will be modified. It's best practice to 
create a module that holds all the actions that can be made in your React component. Remember to create a 
constant that holds all the __actionType__ in a separate module.

#### Conclusion

This is my notes on Flux after recreating the to-do list tutorial on the Flux website. You can 
do the tutorial <a href="https://facebook.github.io/flux/docs/todo-list.html#content" target="_blank">here</a>, 
it might be better if you look through the github example <a href="https://github.com/facebook/flux/tree/master/examples/flux-todomvc/" target="_blank">here</a>. 
What I learned while doing this tutorial is how to use ES6 `class` feature to create my React component 
instead of using `React.createClass` function. <a href="http://egorsmirnov.me/2015/05/22/react-and-es6-part1.html" target="_blank">Here</a> 
is a blog post on how to use ES6 with React. The Flux architecture is used when creating 
data-driven react application, as React.js is becoming more popular. Click <a href="https://facebook.github.io/flux/docs/overview.html#content" target="_blank">here</a>
for the offical overview of Flux. 