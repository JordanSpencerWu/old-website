---
categories: [blog]
date: 2016-10-06 10:15:00
layout: post
title: "Redux With React"
---

Redux can be used with React to help manage all the states changes of the application. The Redux community has provided many useful libraries to integrate Redux with React. As I went through the todos example, I learned some of the libraries. In this blog I will go over what I learned after going through the examples.

Like most React project you will mount a React componenet at a root location, this is usually a `div` element with and unqiue id inside the HTML.

{% highlight javascript %}
  // index.html
  <div id="root"></div>  
{% endhighlight %}

Now to mount our React component!

{% highlight javascript %}
  // index.js
  import React from 'react'
  import { render } from 'react-dom'
  import { createStore } from 'redux'
  import { Provider } from 'react-redux'
  import App from './components/App'
  import reducer from './reducers'

  const store = createStore(reducer)

  render(
    <Provider store={store}>
      <App />
    </Provider>,
    document.getElementById('root')
  )
{% endhighlight %}

There's a few libraries we're importing, lets go over some of them. The _render_ variable from the `react-dom` library will help us mount our component into our div. 

Before we mount anything we should create our application __store__!! This __store__ will hold all the states of our application, the only way the states can change is when a __dispatch__ happens. This __dispatch__ takes in a __action__ that will tell the store how to change it's current states. Once a __dispatch__ happens, we call the __reducers__ which takes in the current state and __action__ then returns the new state. Redux provides a way to create the store using `createStore` which takes in all the __reducers__ (note this is the combined reducers using `combineReducers`).

In Redux there's only one source of truth! This is the store which is used in most of our react application. Redux provide a `Provider` react component that takes in `store` as props, this will allow all it's children access to the store. Since `App` component is a children of `Provider`, it has access to the store!

The `App` react component will be our entire application and it contains four  components.

{% highlight javascript %}
  // App.js
  import React from 'react'
  import Footer from './Footer'
  import AddTodo from '../containers/AddTodo'
  import VisibleTodoList from '../containers/VisibleTodoList'
  import UndoRedo from '../containers/UndoRedo'

  const App = () => (
    <div>
      <AddTodo />
      <VisibleTodoList />
      <Footer />
      <UndoRedo />
    </div>
  )

  export default App
{% endhighlight %}

In React the component can only return one element, that is why we have to put all the react components inside a `div`. The first component `AddTodo` allows us to add a todo into our application. It looks like the following:

{% highlight javascript %}
  // AddTodo.js
  import React from 'react'
  import { connect } from 'react-redux'
  import { addTodo } from '../actions'

  let AddTodo = ({ dispatch }) => {
    let input

    return (
      <div>
        <form onSubmit={e => {
          e.preventDefault()
          if (!input.value.trim()) {
            return
          }
          dispatch(addTodo(input.value))
          input.value = ''
        }}>
          <input ref={node => {
            input = node
          }} />
          <button type="submit">
            Add Todo
          </button>
        </form>
      </div>
    )
  }
  AddTodo = connect()(AddTodo)

  export default AddTodo
{% endhighlight %}

Let's look at the `connect` import from `react-redux` first. This will connect the React component to the Redux store. This component doesn't need to access the store. We can call `connect()` with a wrapped component `AddTodo`, this will allow the `AddTodo` component access to the `dispatch` props. This is called `containers`, they are connect to the Redux store and will rerender everytime the store's states changes. In other words the `connect()` helps synchronize this component with the redux store.

Now lets look at `VisibleTodoList`.

{% highlight javascript %}
  // VisibleTodoList.js
  import { connect } from 'react-redux'
  import { toggleTodo } from '../actions'
  import TodoList from '../components/TodoList'

  const getVisibleTodos = (todos, filter) => {
    switch (filter) {
      case 'SHOW_ALL':
        return todos
      case 'SHOW_COMPLETED':
        return todos.filter(t => t.completed)
      case 'SHOW_ACTIVE':
        return todos.filter(t => !t.completed)
      default:
        throw new Error('Unknown filter: ' + filter)
    }
  }

  const mapStateToProps = (state) => ({
    todos: getVisibleTodos(state.todos.present, state.visibilityFilter)
  })

  const mapDispatchToProps =  ({
    onTodoClick: toggleTodo
  })

  const VisibleTodoList = connect(
    mapStateToProps,
    mapDispatchToProps
  )(TodoList)

  export default VisibleTodoList
{% endhighlight %}

The `VisibleTodoList` component is a `container` that uses the `TodoList` component as the wrapped component. This wrapped component needs access to the store and dispatch. In this case the `connect()` will need to take in two parameters, one will pass in the store and the other will pass in the dispatch. This means that the `TodoList` component will be passed in store's states and dispatch as props.

{% highlight javascript %}
 // TodoList.js
  import React, { PropTypes } from 'react'
  import Todo from './Todo'

  const TodoList = ({ todos, onTodoClick }) => (
    <ul>
      {todos.map(todo =>
        <Todo
          key={todo.id}
          {...todo}
          onClick={() => onTodoClick(todo.id)}
        />
      )}
    </ul>
  )

  TodoList.propTypes = {
    todos: PropTypes.arrayOf(PropTypes.shape({
      id: PropTypes.number.isRequired,
      completed: PropTypes.bool.isRequired,
      text: PropTypes.string.isRequired
    }).isRequired).isRequired,
    onTodoClick: PropTypes.func.isRequired
  }

  export default TodoList
{% endhighlight %}

As you can see above this `TodoList` component is a presentational component that needs `todos` and `onTodoClick` props to work, this was provide when we passed in arguments to the `connect()`.

Now `Footer` is a bit different.

{% highlight javascript %}
 // Footer.js
  import React from 'react'
  import FilterLink from '../containers/FilterLink'

  const Footer = () => (
    <p>
      Show:
      {' '}
      <FilterLink filter="SHOW_ALL">
        All
      </FilterLink>
      {', '}
      <FilterLink filter="SHOW_ACTIVE">
        Active
      </FilterLink>
      {', '}
      <FilterLink filter="SHOW_COMPLETED">
        Completed
      </FilterLink>
    </p>
  )

  export default Footer
{% endhighlight %}

Now looking at the code above, notice that it's getting a `container` component called `FilterLink`. The reason why is some of our presentational components needs to rerender when the user clicks on a link. Only the `containers` components are connected to the store and will rerender when the store states changes!

{% highlight javascript %}
 // FilterLink.js
  import { connect } from 'react-redux'
  import { setVisibilityFilter } from '../actions'
  import Link from '../components/Link'

  const mapStateToProps = (state, ownProps) => ({
    active: ownProps.filter === state.visibilityFilter
  })

  const mapDispatchToProps = (dispatch, ownProps) => ({
    onClick: () => {
      dispatch(setVisibilityFilter(ownProps.filter))
    }
  })

  const FilterLink = connect(
    mapStateToProps,
    mapDispatchToProps
  )(Link)

  export default FilterLink
{% endhighlight %}

Looking above we can tell that this `container` component will pass in store states and dispatch into the wrapped component `Link`. The `Link` is a presentational component that need those props to work.

The last component of the `App` component is `UndoRedo`!

{% highlight javascript %}
 // UndoRedo.js
  import React from 'react'
  import { ActionCreators as UndoActionCreators } from 'redux-undo'
  import { connect } from 'react-redux'

  let UndoRedo = ({ canUndo, canRedo, onUndo, onRedo }) => (
    <p>
      <button onClick={onUndo} disabled={!canUndo}>
        Undo
      </button>
      <button onClick={onRedo} disabled={!canRedo}>
        Redo
      </button>
    </p>
  )

  const mapStateToProps = (state) => ({
    canUndo: state.todos.past.length > 0,
    canRedo: state.todos.future.length > 0
  })

  const mapDispatchToProps = ({
    onUndo: UndoActionCreators.undo,
    onRedo: UndoActionCreators.redo
  })

  UndoRedo = connect(
    mapStateToProps,
    mapDispatchToProps
  )(UndoRedo)

  export default UndoRedo
{% endhighlight %}

What makes this different from the others is it's using a library called `redux-undo`. This allows us access to the past, future, and present store object. This will help when we need to undo/redo a store change! When using this library remember to add it to your reducer!

{% highlight javascript %}
 // undoableTodos.js
  import undoable, { distinctState } from 'redux-undo'

  const todo = (state, action) => {
    switch (action.type) {
      case 'ADD_TODO':
        return {
          id: action.id,
          text: action.text,
          completed: false
        }
      case 'TOGGLE_TODO':
        if (state.id !== action.id) {
          return state
        }

        return Object.assign({}, state, {
          completed: !state.completed
        })
      default:
        return state
    }
  }

  const todos = (state = [], action) => {
    switch (action.type) {
      case 'ADD_TODO':
        return [
          ...state,
          todo(undefined, action)
        ]
      case 'TOGGLE_TODO':
        return state.map(t =>
          todo(t, action)
        )
      default:
        return state
    }
  }

  const undoableTodos = undoable(todos, {
    filter: distinctState()
  })

  export default undoableTodos
{% endhighlight %}

This will make the `todos` a undoable state!