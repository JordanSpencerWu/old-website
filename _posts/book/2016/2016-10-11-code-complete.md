---
author: Steve McConnell
categories: [book]
class: 7
date: 2016-10-11 10:00:00
description: This book contains many useful tips about software construction and best practices on creating clean code. A list of issues that can happen during software construction and how to avoid them by testing your code before writing them. The best part is the checklist at the end of every section containing useful items to check for during software construction.
hidden: true
img-path: /assets/images/books/code-complete.jpg
layout: book
permalink: /code-compete/
title: "Code Complete"
---

<div class="collection">
  {% for post in site.categories.code-complete reversed %}
    <a href="{{ post.url | prepend: site.baseurl }}"  class="collection-item">Chapter {{forloop.index}} : {{ post.title }}</a>
  {% endfor %}
</div>