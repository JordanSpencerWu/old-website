---
categories: [blog]
date: 2017-05-20 10:00:00
layout: post
title: "Learning Webpack 2"
---

As developers write more JavaScript to enhance user experience, they need a tool that will help manage their application's dependencies. [Webpack 2](https://webpack.js.org/) is a module bundler that helps import those dependencies into our html. In this blog, I will talk about what I learned from using Webpack 2.

Webpack is simple to use once you used it a few times. It starts with an entry point where you start importing modules that your application needs to run. It continues going into those modules to get their dependencies until it has all the dependencies that your app depends on. It will then output everything into a file or more files depending on how you configured your webpack output. Since webpack treats every file (.css, .html, .scss, .jpg, etc) as a module and that it only understands JavaScript. We would need to use loaders to transform those modules to JavaScript. Lastly, there are plugins for webpack for more powerful and customizable options. The two plugins I commonly use are _Extract Text Plugin_ (I use it to separate css and js files) and _HTML Webpack Plugin_ (used to create the html file and automatically imports the bundle output files in).

Webpack 2 uses _tree shaking_ which will eliminate any dead code that your project doesn't need. In other words, it will only import modules to your output bundle file if you need it. This will reduce the size of your output file which allows users to download it faster (important for mobile users).

Another feature is _Hot Module Replacement_ (HMR) which improves the development process. This allows the developer to make changes in their source code, then in real time once they've saved the file. The page will load the changes and the page will render the changes without a page reload, this speeds up development time and makes the developer more productive. There's a Webpack Dev Server available. You can use it by running the cli `webpack-dev-server`, this command will run the webpack config file and is used with the HMR.

Webpack makes building production code easier and faster. It provides a production cli command that optimize and minimize your output. Using this with it's code splitting option will greatly improve your web performance. The code splitting will allow you to utilize browser asset caching by splitting up your source code with your vendor libraries.

Webpack is commonly used in many open source projects and it's a useful tool to know and use. The documentation for it has greatly improved compared to Webpack 1. There's many guides that will help you learn the basics, click [here](https://webpack.js.org/guides/get-started/) to learn more.