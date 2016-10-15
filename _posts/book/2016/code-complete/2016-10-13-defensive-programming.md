---
categories: [code-complete]
date: 2016-10-13 12:00:00
hidden: true
layout: book-notes
permalink: /defensive-programming/
title: "Defensive Programming"
---

In defensive programming, the main idea is that if a routine is passed bad data, it won't be hurt, even if the bad data is another routine's fault. Protect yourself from the cold, cruel world of invalid data, events that can "never" happen, and other programmers' mistakes. A good program never puts out garbage, regardless of what it takes in.

An assertion is code that's used during development - usually a routine or macro - that allows a program to check itself as it runs. They enable programmers to more quickly flush out mismatched interface assumptions, errors that creep in when code is modified, and so on. An assertion usually takes two arguments: a Boolean expression that describes the assumption that's supposed to be true, and a message to display if it isn't.

> Use error-handling code for conditions you expect to occur; use assertions for conditions that should never occur.

Correctness means never returning an inaccurate result; returning non result is better than returning an inaccurate result. Robustness means always trying to do something that will allow the software to keep operating, even if that leads to results that are inaccurate sometimes. Safety-critical applications tend to favor correctness to robustness, while consumer applications tends to favor robustness to correctness.

Exception are a specific means by which code can pass along errors or exceptional events to the code that called it. Code that has no sense of the context of an error can return control to other parts of the system that might have a better ability to interpret the error and do something useful about it.

Barricades are damage-containment strategy. One way to barricade for defensive programming purposes is to designate certain interfaces as boundaries to "safe" areas. Check data crossing the boundaries of a safe area for validity, and respond sensibly if the data isn't valid. This can be used at class level, the public methods assume the data is unsafe, and they are responsible for checking the data and sanitizing it. Once the data has been accepted by the class's public methods, the class's private methods can assume the data is safe.

Another key aspect of defensive programming is the use of debugging aids, which can be a powerful ally in quickly detecting errors. Be willing to trade speed and resources usage during development in exchange for built-in tools that can make development go more smoothly. Plan to remove debugging aids before production!
