---
layout: post
title:  "My Node.js Notes"
date:   2016-03-30 13:15:00
---
Node.js is a server side scripting language that uses Chrome's V8 JavaScript 
engine. This engine allows Node.js to be cross-platform, it doesn't matter if you're 
using a Windows, Mac, or Linux!! The best part of Node.js is it makes I/O operations 
asynchronous and will optimize the throughput in your web applications. Many web 
applications use Node.js for it's event driven architecture and non-blocking features. 
This blog post will be my notes on Node.js.

#### Getting Started

The first thing you need is to download Node.js on your machine. You can click this 
<a href="https://nodejs.org/en/download/" target="_blank">link</a> to go to the download 
page. By downloading Node.js on your machine you can start to use JavaScript in your terminal 
or command window. Remember that Node.js is a JavaScript runtime built on Chrome's V8 
JavaScript engine. Now you can use JavaScript not only on your browser but on your machine! Let's 
quickly test this out, in your terminal or command window type the following.

{% highlight shell %}
  $ node
  > console.log("Hello World!")
{% endhighlight %}

The `node` command is a CLI command that will run the JavaScript runtime in your terminal. This 
allows you to run JavaScript commands in your terminal, this is similar to a JavaScript sandbox. 
Another way to use Node.js is to create a JavaScript file and then run it using the `node` command. 
Here is a quick example, first create a file with a extension `.js`.

{% highlight javascript %}
  // helloWorld.js
  console.log("Hello World!");
{% endhighlight %}

Then run this command in your terminal

{% highlight shell %}
  $ node helloWorld.js
{% endhighlight %}

This will produce the same output as the example above.

#### NON-BLOCKING
What makes Node.js so great is that it supports non-blocking code. This will increase your 
throughput in your web application, in other words allows more work on a process. There are two 
ways of running your code in Node.js __synchronous__ or __asynchronous__. A __synchronous__ process 
is similar to doing something in a sequence and waiting for a task to finish before continuing 
to another task. An example will be reading a file then outputing before starting a new task. 

{% highlight javascript %}
  // BLOCKING EXAMPLE!!
  // import the node File System module (provides methods for reading and writing files)
  const fs = require('fs');
  
  var contents = fs.readFileSync('helloWorld.txt');
  console.log(contents.toString());
  console.log('new task');
  
  // terminal output:
  // Hello World!
  // new task
{% endhighlight %}

The following code will run in a sequence, this means one instruction at a time. The first thing 
is it will read the file called `helloWorld.txt` and saves all the content into the variable `contents`. 
Once it finished reading the file it will console log the content to the terminal, note: the __readFileSync__ 
returns a instance of the __Buffer__ class in node. Buffer are necessary to deal with purely binary streams of data. 
Remember everything can be represented in a binary form and there are many encoding and decoding 
techniques used with binary data. Lastly it will start a new task. You might notice that if the 
file is big it will take a few seconds to read the whole file before continuing. In programming we 
want to optimize time, that is where __asynchronous__ comes in. In a asynchronous process, we are 
able to do other tasks while waiting for a task to be done. This is called non-blocking process which is common 
in Node.js programs.

{% highlight javascript %}
  // NON-BLOCKING EXAMPLE!!
  // import the node File System module (provides methods for reading and writing files)
  const fs = require('fs');
  
  var contents = fs.readFile('helloWorld.txt', function(err, contents) {
    console.log(contents);  
  });
  console.log('new task');
  
  // terminal output:
  // new task
  // Hello World!
{% endhighlight %}

In the example above we are able to read the file asynchronously which allows the program to 
continue doing other tasks while it also reads the file at the same time. The __readFile__ takes 
in a few parameters like the file to read and a __callback__. A __callback__ function is called at the 
completion of a given task.

