---
author: Steve McConnell
categories: [book]
class: 7
date: 2016-10-11 10:00:00
description: Currently Reading...
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