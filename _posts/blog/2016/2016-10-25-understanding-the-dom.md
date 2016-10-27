---
categories: [blog]
date: 2016-10-25 10:15:00
layout: post
title: "Understanding the DOM"
---

The Document Object Model (DOM) is a model of an HTML page and how JavaScript can access and update the content of the web page. When the browser loads a web page, it creates a model of the page in memory. The DOM is called an object model because the model (the DOM tree) is made of objects. It consists of four main types of nodes.

At the top of the DOM tree is a __document node__, it represents the entire page and corresponds to the document object. The __element nodes__ describes the structure of an HTML page, you find an element you want, and then you can access its text and attribute nodes if you want to. Note that __attribute nodes__ and __text nodes__ are part of an element, they are not children of the element. Each node is an object with methods and properties.

A __object model__ is a group of objects, each of which represent related things from the real world. There are three groups of built-in objects which offers a different range of tools that help you write scripts for web pages. The __browser object model__ creates a model of the browser used. The __document object model__ (DOM) creates a model of the current web page. Lastly the __global JavaScript objects__ a group of individual objects that relate to different parts of the JavaScript language.

When I think of JavaScript, it’s the behavior of HTML elements which allows users to interact with the webpage. With JavaScript we are able to modify the element nodes on the web page, by changing the object's properties and text/attribute object. Many JavaScript libraries today assist in making these changes by providing you with tools that makes it easier.