---
categories: [blog]
date: 2016-09-04 12:15:00
layout: post
title: "Learning Vue.js"
---

Vue.js is a upcoming library for building interactive web interfaces. The goal is to create reactive data binding and composable view components with an API that is simple to use. Vue.js is similar to React, focusing on the view layer only, this makes it easy to integrate into existing projects. I heard many great feedbacks about this library in recent blogs and surveys. Vue.js seems like a promising library to learn, here are my notes on Vue.js.

#### Reactive Data Binding

Many frameworks those days focus on binding data to the DOM. Vue.js has a reactive data-binding system that keeps the data and the DOM in sync. This library provides you all the tools you need to create interactive web components. It works by connecting the View (DOM) with a Model (Plain JavaScript Object) through a ViewModel (Vue Instance). The Vue instance has a simple api for creating custom web components that interacts with data.

> Directive are prefixed with `v-` to indicate that they are special attributes provided by Vue.js, and as you may have guessed, they apply special reactive behavior to the rendered DOM.

#### Component System

Another important concept in Vue.js it's allows us to build small, self-contained, and reusable components. HTML5 introduces ways of creating your own custom html elements, Vue.js is library that builds custom html element called components which are supported on most browsers. Features like cross-component data flow, custom event communication and dynamic component switching with transition effects are available with Vue.js. When building a large-scale application it's important to decouple the system by using a component system.

#### The Vue Instance

A Vue instance is a __ViewModel__ as defined in the __MVVM__ pattern, handles most if not all of the view's display logic. Every Vue.js app is bootstrapped by creating a root Vue instance with the Vue constructor function. 

{% highlight javascript %}
  var vm = new Vue({
    // options
  })
{% endhighlight %}

All Vue.js components are extended Vue instances.

{% highlight javascript %}
  var MyComponent = Vue.extend({
    // extension options
  })
  // all instance of MyComponent are created with 
  // the pre-defined extension options
  var myComponentInstance = new MyComponent()
{% endhighlight %}

Each Vue instance proxies all the properties found in its `data` object, the proxied properties are __reactive__. Changes to the properties in the data object or in the ViewModel are in sync.

> Vue instance properties and methods are prefixed with `$` to differentiate from proxied data properties.

#### Instance Lifecycle

Each Vue instance is created in the following steps - it set up data observation, compile the template, and create the data binding. Along the way it will invoke some lifecyle hooks.

> All lifecycle hooks are called with their `this` context pointing to the Vue instance invoking it.

#### Data Binding Syntax

Text interpolation using the Mustache syntax: 

{% highlight html %}
  <span>Message: {{ "{{ msg " }}}}</span>
{% endhighlight %}

One-time interpolations:

{% highlight html %}
  <span>This will never change: {{ "{{* msg " }}}}</span>
{% endhighlight %}

To output real HTML, use triple mustaches:

{% highlight html %}
  <div>{{ "{{{ raw_html " }}}}}</div>
{% endhighlight %}

Mustache can be used inside HTML attributes:

{% highlight html %}
  <div id="item-{{ "{{ id " }}}}"></div>
{% endhighlight %}

> Note that attribute interpolations are disallowed in Vue.js directives and special attributes.

> text inside the mustache tags are called __binding expressions__. In Vue.js a binding expression consists of a single JavaScript expression optionally followed by one more filters.

Here are some of the JavaScript Expressions available:

{% highlight html %}
  {{ "{{ number + 1 " }}}}
  {{ "{{ ok ? 'Yes' : 'No' " }}}}
  {{ "{{ message.split('').reverse().join('') " }}}}
{% endhighlight %}

Vue.js allow you to append optional filters at the end of an expression using the pipe symbol:

{% highlight html %}
  {{ "{{ message | filterA | filterB " }}}}
  {{ "{{ message | filterA 'arg1' arg2 " }}}}
{% endhighlight %}

> Filters can also take arguments, quoted arguments are plain string. while un-quoted ones are expressions.

Directive attribute values are expected to be __binding expressions__, their job is to reactively apply special behavior to the DOM when the value of its expression changes.

{% highlight html %}
  <p v-if="greeting">Hello!</p>
{% endhighlight %}

Directive can take an argument, denoted by a colon after the directive name:

{% highlight html %}
  <a v-bind:href="url"></a>
{% endhighlight %}

Modifiers are special postfixes denoted by a dot, which tells that a directive should be cound in some special way:

{% highlight html %}
  <a v-bind:href.literal="/a/b/c"></a>
{% endhighlight %}

Here are some shorthands that Vue.js provides

{% highlight html %}
  <!-- full syntax -->
  <a v-bind:href="url"></a>
  <!-- shorthand -->
  <a :href="url"></a>
  or
  <!-- full syntax -->
  <a v-on:click="doSomething"></a>
  <!-- shorthand -->
  <a @click="doSomething"></a>
{% endhighlight %}

#### Computed Properties

Template are meant to describe the structure of your view, avoid putting too much logic. For any logic that requires more than one expression, use a __computed property__.

{% highlight javascript %}
  var vm = new Vue({
    el: '#example',
    data: {
      a: 1
    },
    computed: {
      // a computed getter
      b: function () {
        // `this` points to the vm instance
        return this.a + 1
      }
    }
  })
{% endhighlight %}

#### Class and Style Binding

It's common to change the element's class list and its inline styles. Both are html attributes, we can use the `v-bind` to handle them. We can pass an Object to `v-bind:class` to dynamically toggle classes:

{% highlight html %}
  <div v-bind:class="classObject"></div>
{% endhighlight %}

{% highlight javascript %}
  data: {
    classObject: {
      'class-a': true,
      'class-b': false
    }
  }
{% endhighlight %}

We can also pass in an Array to `v-bind:class` to apply a list of classes:

{% highlight html %}
  <div v-bind:class="[classA, classB]">
{% endhighlight %}

{% highlight javascript %}
  data: {
  classA: 'class-a',
  classB: 'class-b'
  }
{% endhighlight %}

Binding Inline Styles is similar to classes using `v-bind:style`:

{% highlight html %}
  <div v-bind:style="styleObject"></div>
{% endhighlight %}

{% highlight javascript %}
  data: {
    styleObject: {
      color: 'red',
      fontSize: '13px'
    }
  }
{% endhighlight %}

#### Conditional Rendering

The `v-if` and `v-show` are used for conditional rendering in Vue.js. The main difference is `v-if` is real conditional rendering because it ensures that event listeners and child components inside the conditional block are properly destory and re-created during toggles. `v-show` will always be rendered and remain in the DOM. The `v-else` is used with `v-if` as the catch all conditional. 

> So prefer `v-show` if you need to toggle something very often, and prefer `v-if` if the condition is unlikely to change at runtime.

#### List Rendering

We can use `v-for` to iterate through an Array, inside the `v-for` blocks we have full access to parent scope proerties, plus a special variable `$index` and `$key`:

{% highlight html %}
  <ul id="example-2">
    <li v-for="item in items">
      {{ parentMessage }} - {{ $index }} - {{ item.message }}
    </li>
  </ul>
{% endhighlight %}

{% highlight javascript %}
  var example2 = new Vue({
    el: '#example-2',
    data: {
      parentMessage: 'Parent',
      items: [
        { message: 'Foo' },
        { message: 'Bar' }
      ]
    }
  })
{% endhighlight %}

`v-for` can also take an integer Number:

{% highlight html %}
  <div>
    <span v-for="n in 10">{{ n }} </span>
  </div>
{% endhighlight %}

> You can also specify an alias for the index (or the key if `v-for` is used on an Object), you can also use `of` as the delimiter instead of `in`.

#### Methods and Event Handling

The `v-on` directive is used to listen to DOM events. We can bind a click event to a method named greet, by defining that method in our Vue instance. When we need to acces the original DOM event pass in `$event` as an argument into the method.

{% highlight html %}
  <button v-on:click="say('hello!', $event)">Submit</button>
{% endhighlight %}

{% highlight javascript %}
  // ...
  methods: {
    say: function (msg, event) {
      // now we have access to the native event
      event.preventDefault()
    }
  }
{% endhighlight %}

It is very common to call `event.preventDefault()` or `event.stopPropagation()` inside event handlers. Vue.js provides two event modifiers for `v-on` : `.prevent` and `.stop`:

{% highlight html %}
  <!-- the click event's propagation will be stopped -->
  <a v-on:click.stop="doThis"></a>
  <!-- the submit event will no longer reload the page -->
  <form v-on:submit.prevent="onSubmit"></form>
  <!-- modifiers can be chained -->
  <a v-on:click.stop.prevent="doThat">
  <!-- just the modifier -->
  <form v-on:submit.prevent></form>
  <!-- use capture mode when adding the event listener -->
  <div v-on:click.capture="doThis">...</div>
  <!-- only trigger handler if event.target is the element itself -->
  <!-- i.e. not from a child element -->
  <div v-on:click.self="doThat">...</div>
{% endhighlight %}

There are also Key Modifiers:

{% highlight html %}
  <!-- same as above -->
  <input v-on:keyup.enter="submit">
  <!-- also works for shorthand -->
  <input @keyup.enter="submit">
{% endhighlight %}

#### Form Input Bindings

The `v-model` directive is used to create two-way data binding on form input and textarea elements. This will sync the View and Model, for updating data on user input events. For radio, checkbox and select options, the `v-model` binding value are static strings (or booleans for checkbox). Use `v-bind` when you want to bind a value to a dynamic property on the Vue instance.

#### Components

Coming soon..