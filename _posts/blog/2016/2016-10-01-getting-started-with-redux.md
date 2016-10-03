---
categories: [blog]
date: 2016-10-01 10:15:00
layout: post
title: "Getting Started with Redux"
---

Creating a single-page applications is becoming increasingly complicated. We must keep track of all the states and data of the application, as the application grows, so does the data we must manage. That's where Redux comes in, it's an evolution of the ideas presented by Facebook's Flux. Redux is useful for React application, but React is not a requirement. This will be my notes on Redux after reading the documentation.

##### Three Principles

The first principle of Redux is that the state of your whole application is stored in an object tree within a single JavaScript object. Only one single immutable state tree that contains all the state of your application, this is known as the __single source of truth__.

The second principle of Redux is that the only way to change the state of the tree is by dispatching an __action__, an object describing what happened. This action is a plain JavaScript object that has a _type_ property and other properties that tells us what happened in our application.

The last principle is that we must write pure functions to specify how the state tree is transformed by actions. A pure function's return value must depend solely on the arguments passed into the function. There must be no side effects like querying the database and using other variables outside the pure function's scope or calling non-pure functions. The benefits of pure function is that it's predictable, passing in the same arguments will result in the same return value, an use case of using pure function is __memoization__. Lastly the return value must not modify any of the arguments passed into the pure function.

> __Reducers__ are just pure functions that take the previous state and an action, and returns the next state.

When writing a reducer functions remember to set a default intital state and have a catch all `action.type` that returns the current state.

{% highlight javascript %}
  const counter = (state = 0, action) => {
    switch (action.type) {
      case 'INCREMENT':
        return state + 1;
      case 'DECREMENT':
        return state - 1;
      default:
        return state;
    }
  }
{% endhighlight %}

##### Actions

__Actions__ are payload of information that send data from your application to your store. They are the _only_ source of information for the store, you send them to the store using `store.dispatch()`. Again actions are plain JavaScript object that must have a `type` property that indicates the type of action being performed. It best practice to store your actions types in a separate module: 

{% highlight javascript %}
  import { ADD_TODO, REMOVE_TODO } from '../actionTypes'
{% endhighlight %}

##### Action Creators

__Action creators__ are functions that create actions, they simply return an action.

{% highlight javascript %}
  function addTodo(text) {
    return {
      type: ADD_TODO,
      text
    }
  }
{% endhighlight %}

Then we can dispatch the action by passing in the action creator function to the dispatch function.

{% highlight javascript %}
  dispatch(addTodo(text))
{% endhighlight %}

Alternatively, we can create a __bound action creator__ that automatically dispatches:

{% highlight javascript %}
  const boundAddTodo = (text) => dispatch(addTodo(text))

  // then call them directly
  boundAddTodo(text)
{% endhighlight %}

##### Reducers

The __Reducers__ specify how the application's state tree changes in response to the __actions__. In Redux, all application state is stored as a single object, it's a good idea to think of it's shape before writing any code. What's the minimal representation of your app's state as an object? Once we decided on a state tree, we can create a reducer for our application, takes in previous state and an action, and returns the next state.

{% highlight javascript %}
  (previousState, action) => newState
{% endhighlight %}

> Avoid array mutations with `concat()`, `slice()`, and `...spread`!

{% highlight javascript %}
  const addCounter = (list) => {
    return [...list, 0];
  };

  const removeCounter = (list, index) => {
    return [
      ...list.slice(0, index),
      ...list.slice(index + 1)
    ];

    const incrementCounter = (list, index) => {
      return [
        ...list.slice(0, index),
        list[index] + 1,
        ...list.slice(index + 1)
      ];
    };
  };
{% endhighlight %}

> Avoid object mutations with `Object.assign()` and `...spread`!

{% highlight javascript %}
  // Object.assign() is ES6
  const toggleTodo = (todo) => {
    return Object.assign({}, todo, {
      completed: !todo.completed
    });
  };
{% endhighlight %}

Here is an example of the todoApp reducer function that can call another reducer function, this is called _reducer composition_, and it's the fundamental pattern of building Redux apps:

{% highlight javascript %}
  function todos(state = [], action) {
    switch (action.type) {
      case ADD_TODO:
        return [
          ...state,
          {
            text: action.text,
            completed: false
          }
        ]
      case TOGGLE_TODO:
        return state.map((todo, index) => {
          if (index === action.index) {
            return Object.assign({}, todo, {
              completed: !todo.completed
            })
          }
          return todo
        })
      default:
        return state
    }
  }

  function todoApp(state = initialState, action) {
    switch (action.type) {
      case SET_VISIBILITY_FILTER:
        return Object.assign({}, state, {
          visibilityFilter: action.filter
        })
      case ADD_TODO:
      case TOGGLE_TODO:
        return Object.assign({}, state, {
          todos: todos(state.todos, action)
        })
      default:
        return state
    }
  }
{% endhighlight %}

We now can extract the `SET_VISIBILITY_FILTER` action type and create a `visibilityFilter` reducer function to make it more modular.

{% highlight javascript %}
  function todos(state = [], action) {
    switch (action.type) {
      case ADD_TODO:
        return [
          ...state,
          {
            text: action.text,
            completed: false
          }
        ]
      case TOGGLE_TODO:
        return state.map((todo, index) => {
          if (index === action.index) {
            return Object.assign({}, todo, {
              completed: !todo.completed
            })
          }
          return todo
        })
      default:
        return state
    }
  }

  function visibilityFilter(state = SHOW_ALL, action) {
    switch (action.type) {
      case SET_VISIBILITY_FILTER:
        return action.filter
      default:
        return state
    }
  }
{% endhighlight %}

Now we can rewrite the main reducer as a function that calls the reducers managing parts of the state, and combine them into a single object. This reducer will be to specify how the application's state tree changes in response to the actions. Redux provides a utility called `combineReducers()` that combines all the reducers functions that makes up your application state tree.

{% highlight javascript %}
  import { combineReducers } from 'redux'

  const todoApp = combineReducers({
    visibilityFilter,
    todos
  })

  export default todoApp
{% endhighlight %}

##### Store

The __Store__ is the object that stores the application's state object, it has the following responsibilities:

1. Holds application state
2. Allows access to state via `getState()`
3. Allows state to be updated via `dispatch(action)`
4. Registers listeners via `subscribe(listener)`
5. Handles unregistering of listeners via the function returned by `subscribe(listener)`

{% highlight javascript %}
  import { createStore } from 'redux'
  import todoApp from './reducers'
  let store = createStore(todoApp)
{% endhighlight %}

##### Data Flow

Redux architecture revolves around a __strict unidirectional data flow__. This means that all data in the application follows the same lifecycle pattern, making the logic of your app more predictable and easier to understand. The data lifecycle in any Redux app follows these 4 steps:

1. You call `store.dispatch(action)`
2. The Redux store calls the reducer function you gave it
3. The root reducer may combine the output of multiple reducers into a single state tree.
4. The Redux store saves the complete state tree returned by the root reducer.

These are the information I need to know before I check the example <a href="http://redux.js.org/docs/introduction/Examples.html" target="_blank">source code</a> provided on the website. There are two great resources for learning redux by creating a todo react application. One of the resource is vidoes by Dan Abramov (creator of Redux), click <a href="https://egghead.io/courses/getting-started-with-redux" target="_blank">here</a> to watch the videos. The other resource is the source code for the todo list provided by the redux website, click <a href="http://redux.js.org/docs/basics/ExampleTodoList.html" target="_blank">here</a> to check it out.