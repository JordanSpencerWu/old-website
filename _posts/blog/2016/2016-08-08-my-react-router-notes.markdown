---
layout: post
title: "My React Router Notes"
date: 2016-08-08 12:15:00
categories: [blog]
---

React Router is a routing library for React.js! This library is similar to Sinatra and Express.js, both are used to response to HTTP requests. What makes React Router so powerful is it's ability to create a Single Page Application (SPA) using react components. React.js is a great library for dynamically updating the webpage, now it has a routing framework that makes it easy to change between react components! This will be my notes on React Router after doing the tutorial.

#### Router & Route

The goal of React Router is to match the URL of the HTTP request and display the correct react component! The `Router` component is the main React component from the library that does the job. This component takes in `Route` props as children to configure a URL and a react component. The other common props for this component is the `history` props to keep track of the current URLs and past URLs. The following code below creates a simple `Router` component.

{% highlight javascript %}
  import { Router, hashHistory } from 'react-router'

  render((
    <Router history={hashHistory}>
      // Route children goes here!!
    </Router>
  ), document.getElementById('app'));
{% endhighlight %}

The Router needs a configuration component called `Route` to setup the application's component hierarchy. This component takes in a `path` props that is used as the URL. Once we have the `path` props, we need the component which will be render once it hits this path URL. We can pass in `component` or `components` as props, depending if we want to pass in a singular or multiple components.

{% highlight javascript %}
  import { Router, Route, hashHistory } from 'react-router'
  import App from './modules/App'
  import Users from './modules/Users'
  import UsersGroup from './modules/UsersGroup'

  render((
    <Router history={hashHistory}>
      <Route path="/" component={App}/>
      <Route path="Users" components={ { main: Users, sidebar: UsersGroup } }/>
    </Router>
  ), document.getElementById('app'));
{% endhighlight %}

Let's think about the purpose of a Single Page Application. My definition of a SPA is that it is similar to a AJAX call which the webpage changes dynamically without a page reload. In this case we want the page to change to another react component when the URL is changed. It's important to organize the routes, we do this by nesting routes! We know that all website has a home/index page, when using react-router we want to have one main `Route` component. Our home/index route component will be used to store all the links and render all the children react components when the URL is changed.

{% highlight javascript %}
  import { Router, Route, hashHistory } from 'react-router'
  import App from './modules/App'

  render((
    <Router history={hashHistory}>
      <Route path="/" component={App}>
        // nested routes goes here!!
      </Route>
    </Router>
  ), document.getElementById('app'));
{% endhighlight %}

Now we know where the nested routes goes! Let's add in a Repos and About page like they did in the tutorial!

{% highlight javascript %}
  import { Router, Route, hashHistory } from 'react-router'
  import App from './modules/App'
  import About from './modules/About'
  import Repos from './modules/Repos'

  render((
    <Router history={hashHistory}>
      <Route path="/" component={App}>
        <Route path="/repos" component={Repos}/>
        <Route path="/about" component={About}/>
      </Route>
    </Router>
  ), document.getElementById('app'));
{% endhighlight %}

#### Links & Active Links

Our goal is to create a SPA, we need to have a navbar that holds all the URLs inside our `App` react component. This component will hold all its children `Route` components paths! The react-router library has a `Link` component that will bind the URL path with the `Link` and `Route` component. Here is the ES5 code example.

{% highlight javascript %}
  // modules/App.js
  import React from 'react'
  import { Link } from 'react-router'

  export default React.createClass({
    render() {
      return (
        <div>
          <h1>React Router Tutorial</h1>
          <ul role="nav">
            <li><Link to="/about">About</Link></li>
            <li><Link to="/repos">Repos</Link></li>
          </ul>
        </div>
      )
    }
  })
{% endhighlight %}

Now our Link's path are binded with our Route's path!! A problem with the following code is that we don't know which link is active. It's important to distinguish a active link with a inactive link, so that we know where we're at in the website. There are two ways of doing this with `activeStyle` or `activeClassName` props of the `Link` component.

{% highlight javascript %}
  // inline style
  <li><Link to="/about" activeStyle={{ color: 'red' }}>About</Link></li>
  // class name
  <li><Link to="/about" activeClassName="active">About</Link></li>
{% endhighlight %}

The tutorial recommend creating a `NavLink` component for your active Link components. The only links that you need to know if they are active or not is the primary links, the ones on the Navbar!

{% highlight javascript %}
  // modules/NavLink.js
  import React from 'react'
  import { Link } from 'react-router'

  export default React.createClass({
    render() {
      return <Link {...this.props} activeClassName="active"/>
    }
  })
{% endhighlight %}

#### URL Params

Like many web frameworks, the routing configuration must be able to take in parameters! Whenever I think about URL I think about the Model View Controller (MVC) web application design. In the ASP.NET MVC5 they have the routing params as `/:controller/:action/:id` which is similar to the Ruby on Rails. The react-router has something similar `/repos/:userName/:repoName`.

{% highlight javascript %}
  <Route path="/repos/:userName/:repoName" component={Repo}/>
{% endhighlight %}

Both params are available to the Repo component using `this.props.params` inside your react component file. This is a quick and easy way of passing in params to your URL!

#### Index Routes & Index Links

We need to have a default page for the home page, so whenever the user goes to the `/` path it will render a `Home` component. With the help of the `IndexRoute` component from the react-router library we are able to create a page for when the parent `Route` component path is requested.

{% highlight javascript %}
  import { Router, Route, hashHistory, IndexRoute } from 'react-router'
  import App from './modules/App'
  import About from './modules/About'
  import Repos from './modules/Repos'
  import Repo from './modules/Repo'
  import Home from './modules/Home'

  render((
    <Router history={hashHistory}>
      <Route path="/" component={App}>
        <IndexRoute component={Home}/>
        <Route path="/repos" component={Repos}>
          <Route path="/repos/:userName/:repoName" component={Repo}/>
        </Route>
        <Route path="/about" component={About}/>
      </Route>
    </Router>
  ), document.getElementById('app'));
{% endhighlight %}

Now we have a `IndexRoute` for our parent `Route` component's path. We need a way to get to this `IndexRoute`, that's where the `IndexLink` comes in! There are two ways to use this component.

{% highlight javascript %}
  // import the IndexLink component
  import { IndexLink } from 'react-router'
  <IndexLink to="/" activeClassName="active">HOme</IndexLink>
  // or Link using onlyActiveOnIndex props
  import { Link } from 'react-router'
  <Link to="/" activeClassName="active" onlyActiveOnIndex={true}>Home</Link>
{% endhighlight %}

The last thing I want to note is that the `this.props.children` will render the react component that was passed in to the `Route` component! Here is an example.

{% highlight javascript %}
  // modules/App.js
  import React from 'react'
  import NavLink from './NavLink'

  export default React.createClass({
    render() {
      return (
        <div>
          <h1>React Router Tutorial</h1>
          <ul role="nav">
            <li><NavLink to="/" onlyActiveOnIndex>Home</NavLink></li>
            <li><NavLink to="/about">About</NavLink></li>
            <li><NavLink to="/repos">Repos</NavLink></li>
          </ul>
          {this.props.children}
        </div>
      )
    }
  })
{% endhighlight %}

#### Conclusion

This is my quick notes on <a href="https://github.com/reactjs/react-router" target="_blank">React Router</a> after doing the <a href="https://github.com/reactjs/react-router-tutorial" target="_blank">tutorial</a>. This library provides you all the tools you need to make a single page application using <a href="https://facebook.github.io/react/" target="_blank">React.js<a/>! This will help reduce page reload and HTTP request to the server while providing the user with better user experience! React router is a routing library for creating a single page application with React.js, it's powerful and simple to use!