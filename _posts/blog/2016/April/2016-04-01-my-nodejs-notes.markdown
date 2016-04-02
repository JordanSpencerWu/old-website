---
layout: post
title:  "My Node.js Notes"
date:   2016-04-01 13:15:00
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
completion of a given task. Asynchronous process will optimize time complexity of your program by 
increasing throughput!

#### Global Variables
In Node there are global variables you can use in your program. We know that Node.js are best for 
I/O operations which involves files and directories. If you want to get the name of the current executing 
script's directory, you are able to use the variable ____dirname__ to accomplish this task. You can also 
use ____filename__ to get the filename of the code being executed. The commonly used globals are the 
exports and require methods for distributing JavaScript files! The __require()__ allows you to import a 
JavaScript object into your code, this is where modularized code comes in handy. Node makes it easy to 
share your modularized code using the __module.exports__, this allows you to define what codes you are 
exporting (Remember in JavaScript, functions are first-class objects). 
To see all the global variables and methods check out the documentation of the version of Node you are 
using and click on __Globals__.

#### HTTP
You are able to create servers in Node that listens to client's request and will response to them. In web 
development the clients will make request to the server then the server will response to the request according to 
the code you provide. In Node.js there is a module called __HTTP__ which allows you to create a server that will 
listen to http requests. Here is a simple example of creating a server in node.

{% highlight javascript %}
  const http = require('http');

  const hostname = '127.0.0.1';
  const port = 1337;

  http.createServer((req, res) => {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Hello World\n');
  }).listen(port, hostname, () => {
    console.log(`Server running at http://${hostname}:${port}/`);
  });
{% endhighlight %}

To import the __HTTP__ module into your script you have to use the __require('http')__ which allows you to 
any of the methods in module's library. The hostname __127.0.0.1__ is the domain name in the URL for example, 
you can type __http://127.0.0.1:1337/__ or __http://localhost:1337/__ in a web browser to make a http request 
to this server. The code above will create a server that is listening on port 1337 on the domain name 
localhost (this is a local server on your machine), once it receives this http request it will response with a 
status code of 200, with content-type of text/plain and will output a string 'Hello World' on the webpage.

#### Events
Remember that Node.js is event-driven!! A event is when a action in the DOM is triggered for example 
when you click on a button on a website. Many of the Node.js objects emit events for example the __readStream__ 
is a class of __EventEmitter__ which has a data event. Here is a example of how to create a event and how to emit it.

{% highlight javascript %}
  const EventEmitter = require('events').EventEmitter;
  const logger = new EventEmitter();

  logger.on('error', function(message) {
    console.log(`ERR: ${message}`); 
  });
  logger.emit('error', 'Spilled Milk');
  
  // output to console
  // ERR: Spilled Milk
{% endhighlight %}

We have to import the event module from the Node.js library. After we will create a new instance of the 
EventEmitter class, we can then create a new event call __error__. The __error__ event takes in a message 
parameter that will be used when this event is emitted. To trigger or call this event we would use the dot 
notation to invoke the __emit__ method, this will trigger/call the event. This was a simple example of how 
events are used in Node.js, there are many applications in using events in Node.js.

#### Node API
There are many modules in Node.js, the Node.js website provides documentations on all them. 
You can click <a href="https://nodejs.org/en/docs/" target="_blank">here</a> to see the document page. Remember 
to select the correct Node.js version which you are using, the newer version of Node.js at the time of 
writing this blog has ES6 features.

#### NPM
 
<a href="https://www.npmjs.com/" target="_blank">NPM.js</a> is known as Node Package Manager, is the package manager for JavaScript. This is where 
all the JavaScript code are shared between developers. There are tons of packages that can be imported 
into your program and npm is commonly used when finding these packages. When you downloaded Node.js it comes 
with __npm__. Note that npm usually have more updates then Node.js!
 
{% highlight shell %}
  $ node -v // check node version
  $ npm -v // check npm version
  $ npm install npm -g // install the lastest version on your machine
{% endhighlight %}
 
 A few things to know before using npm. NPM is similar to git, whenever you are going to use npm, you have 
 to create a file to use it. Run `npm init` in your terminal to create a __package.json__, this file will have all the 
 information about your project and packages you are using. The __package.json__ file is a JavaScript object that 
 has the following properties __name__, __version__, __main__, __scripts__, __keywords__, __author__, 
 __license__, __repository__, __bugs__, and __homepage__.
 
#### Dependencies
 
Node.js has a active community that works together on open source projects. Many of the JavaScript packages 
depends on other packages, this creates a dependencies to use a given package. Just remember that JavaScript packages 
might need other packages to work! There are two types of dependencies when creating your Node.js project, 
__dependencies__ and __devDependencies__. __Dependencies__ are packages required by your application in 
production, while __devDependencies__ are packages used for development and testing.
 
{% highlight shell %}
  $ npm install <package_name> --save // install package into your package.json as dependencies
  $ npm install <package_name> --save-dev // install package into your package.json as devDependencies
  $ npm install <package_name> -g // install package on your machine
  $ npm install // install all dependencies and devDependencies in your package.json file
  $ npm start // start project (look at task property in package.json)
{% endhighlight %}

It's easy to use npm when installing packages to your Node.js project. All the packages required for 
your project is in __package.json__ file!!

#### Version
Each JavaScript package on npm has a version number. This version number will keep track of when 
updates are made to the package. Version numbers are important, some projects need a specfic version 
of the package to work while other versions might break the application! There are three version numbers, 
they are __major__, __minor__, and __patch__. 

{% highlight javascript %}
  "express": "4.13.4" // major_number.minor_number.patch_number
  
  // Ranges
  "express": "~4" // >=4.0.0 <5.0.0 Dangerous
  "express": "~4.13" // >=4.13.0 <4.14.0 API could change
  "express": "~4.13.4" // >=4.13.4 <4.14.0 Considered safe
{% endhighlight %}

#### Conclusion

Node.js is used in many web application and for prototyping new JavaScript libraries. Node.js can be 
used to create a web application using only JavaScript! This is called the MEAN stack, which stands for 
__Mongodb__, __Express.js__, __Angular.js__, and __Node.js__. NPM is used to install many of the JavaScript 
libraries like __Webpack__, __React.js__, __Polymer.js__, and more. NPM is similar to __Bundler__, 
a manager for ruby gems used for Ruby projects.
