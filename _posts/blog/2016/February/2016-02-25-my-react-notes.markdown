---
layout: post
title:  "My React Notes"
date:   2016-02-25 13:15:00
categories: [blog]
---
React is a JavaScript library for building user interfaces (UI) by Facebook. 
Think of React like the View in the Model, View, Controller (MVC) web design 
pattern. The power of React is to create reusable components and dynamic UIs. 
This library allows you to create your own UI components using Javascript and 
allows you to reuse them anywhere in your web application. This blog will be 
my notes on React.

#### Why React?
The web is becoming more interactive. React makes it easy to display data and 
will automatically update when the data changes. After creating a 
UI component, you are able to reuse it in you web application. One of 
React's finest features is composability which allows you to use UI 
components together. React in my words is that it allows you to create custom 
web components that will change dynamically with user interactions. This makes 
DOM manipulation easy and fast by using a virtual DOM. With React you can create 
dynamic UI components that enhance user experience (UX).

#### Getting Started
To get started with React you need the libraries and tools. To get the react 
libraries you will need to have `npm` installed on your machine. `NPM` is a 
javascript package manager that allows distribution of javascript modules. The 
two modules you need will be `react` and `react-dom`. It is recommend that 
you use JSX, this makes it easier to write your 
react components. JSX syntax makes it more HTML-like, since you are creating 
a custom web components it should look more like HTML. 

Here is a example using pure JavaScript:

{% highlight javascript %}
  React.createElement('a', {href: 'https://facebook.github.io/react/'}, 'Hello!')
{% endhighlight %}

Here is the same example using JSX:

{% highlight markdown %}
  <a href="https://facebook.github.io/react/">Hello!</a>
{% endhighlight %}

For you to use JSX you need the tool that transform JSX to JS. Babel is a 
Javascript compiler that provides the tools you need to use JSX with React. 
The npm module you need is `babel-preset-react`, this will transform JSX files to JS files 
. If you want to learn more about Babel, click 
this <a href="http://babeljs.io/" target="_blank">link</a>.

#### Thinking in React
React uses one-way data flow by introducing `states` and `props`. You have to think 
differently when creating a react components. Here is the procedures I follow when 
creating a React component:

1. Look at the JSON API to see what data can be used to display in the UI component
2. Create a mock up of the React component
3. Break down the UI into a component hierarchy
4. Build a static version of React
5. Add in states and properties
6. Add in inverse data flow using event handling and callbacks

#### Understanding States and Properties
React thinks of UI as state machines. UI has various states and depending on thoses 
states it determines how the UI is rendered. The UI component will change only when a state 
is changed! The properties also known as `props` are the data that will be displayed. 
Think of `props` as a read-only variable or a constant, the only way to change the 
`props` is by changing the state. In React, an owner is the component that sets the `props` 
of the other components. The owner-ownee relationship is used in React where the owner 
components is the stateful component and the ownee is the stateless component. This means 
the owner component will control the `props` passed down to the ownee component. This is 
the one-way data binding where the stateful components passes down data as `props` to the 
ownee components and when the state in the owner components is changed the data changes and 
the `props` is updated in the ownee component. Understanding how to use `states` and `props` 
is essential when creating your own react component.

#### Conclusion
React is a powerful Javascript library that makes amazing UI components. Writing React components with JSX 
produce simple and easy to read code. There are many data fetching libraries that can be used with React like 
<a href="http://graphql.org/" target="_blank">GraphQL</a> and <a href="http://netflix.github.io/falcor/">Falcor</a>. You can 
start learning React by doing their getting started tutorial <a href="https://facebook.github.io/react/docs/tutorial.html">here</a>. 
Once you have a better understand of React, you can create your own React workflow 
using <a href="https://webpack.github.io/">Webpack</a>.

#### Useful Reference Links
* <a href="https://facebook.github.io/react/docs/top-level-api.html" target="_blank">Top-Level API</a>
* <a href="https://facebook.github.io/react/docs/component-api.html" target="_blank">Component API</a>
* <a href="https://facebook.github.io/react/docs/component-specs.html" target="_blank">Component Specs and Lifecycle</a>
* <a href="https://facebook.github.io/react/docs/tags-and-attributes.html" target="_blank">Supported Tags and Attributes</a>
* <a href="https://facebook.github.io/react/docs/glossary.html" target="_blank">React (Virtual) DOM Terminology</a>