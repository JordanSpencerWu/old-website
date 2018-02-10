---
author: Jim R. Wilson
categories: [book]
class: 63
date: 2018-02-10 10:00:00
description: A great book for getting started with Node.js. You learn by doing and this book provides you with projects to do, along with detailed explanation of each line of code written. I enjoyed reading this book and it's a great way to see what's being used in today's web services.
hidden: true
img-path: /assets/images/books/node-8-the-right-way.jpg
layout: book
permalink: /node-8-the-right-way/
title: "Node.js 8 the Right Way"
---

Node.js's philosophy is to give you low-level access to the event-loop and to system resources.

Node.js is a single-thread environment, or in other words "everything runs in parallel except your code."

Event Emitter provides a channel for events to be dispatched and listeners to be notified.

A Buffer is Nodejs's way of representing binary data. It points to a blob of memory allocated by Nodejs's native code, outside of the JavaScript engine.

Networked services exist to do two things: connect endpoints and transmit information between them.

TCP socket connections consist of two endpoints. One endpoint binds to a numbered port while the other endpoint connects to a port.

A protocol is a set of rules that defines how endpoints in a system communicate.

Strong convention in the Node community to put supporting code in the lib directory.

Regular dependencies are used at runtime by your code when you use require() to bring in modules. Dev dependences are programs that your project needs during development.

##### Semantic versioning convention:

1. If your code change does not introduce or remove any functionality (like a bug fix), then just increment the patch version.

2. If your code introduces functionality but doesn't remove or alter existing functionality, then increment the minor version and reset the patch version.

3. If your code in any way breaks existing functionality, then increment the major version and reset the minor version and reset the patch version.

publish/subscribe PUB/SUB EX. The server would publish information in this format, and any number of client programs could subscribe to it.

request/reply REQ/REP EX. a request comes in, then a reply goes out.

ROUTER Socket are like parallel REP socket, can handle many requests simultaneously.

DEALER Socket are like parallel REQ, can send multiple requests in parallel.

Clustering is a useful technique for scaling up your Node.js application when there's unused CPU capacity available.

forking creates a worker process running the same scripts as the original.

Spawning a Child Process works great for executing non-Node.js processes from your Node.js program.

PUSH and PULL Socket types are useful when you have a queue of jobs that you want to assign among a pool of available workers.

A message traveling from a PUSH socket to a PULL socket is one-way: the puller can't send a response back through the same socket.

The practice of compiling source code from one programming language into another (or from one language version to another version) is called transpiling.