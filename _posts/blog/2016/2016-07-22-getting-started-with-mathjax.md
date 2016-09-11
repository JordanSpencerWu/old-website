---
categories: [blog]
date: 2016-07-22 12:15:00
layout: post
libraries: [mathjax]
title: "Getting Started With MathJax"
---

The other day I was on the Mozilla Developer Network (MDN) website and saw something interesting on the page, it was MathML. This is a Markup Language for displaying mathematical equations on the browser. I took a quick tour of the MathML webpage in MDN and saw that most browsers don't support this language. I thought about writing mathematical equations on my blogsite, I wanted to create my own mathematical notes. That's where MathJax comes in! This JavaScript library will display beautiful math equation on all browsers! In this blog I will quickly go over how to use MathJax.

#### Getting MathJax!!

Like most JavaScript librarys there are two main ways of implementing this into any web application. One of the ways is to use the Content Delivery Network (CDN) which requires internet access to use this library. The other way of getting this library is by downlowning MathJax locally then linking it to your web application. I will be using the CDN, to use the CDN all you have to do is add the following code into your `<head>` html element.

{% highlight html %}
  <script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js">
</script>
{% endhighlight %}

MathJax comes with a few pre-defined and pre-compiled configuration files, click <a href="http://docs.mathjax.org/en/latest/config-files.html" target="_blank">here</a> to learn more! These combined configuration give you ready to use config for MathJax, for example one of the configuration allows you to use Tex, MathML, or AsciiMath input processors. These input processors can produce HTML+CSS, SVG or MathML outputs. I won't be using the combined configuration files since I only plan on using TeX as the input processor.

#### Configuring TeX and LaTeX input

We first need to get the `tex2jax` preprocessor, and the `TeX` input processor. The `tex2jax` preprocessor looks for the mathematical equation within the webpage by locating the delimiter, while the TeX processor converts the TeX notation into MathJaX's internal format then uses a MathJax output processor to display it on the page. I will be adding the following configuration above the MathJax CDN `script` element.

{% highlight html %}
  <script type="text/x-mathjax-config">
    MathJax.Hub.Config({
      extensions: ["tex2jax.js"],
      jax: ["input/TeX", "output/HTML-CSS"],
      tex2jax: {
        inlineMath: [ ['$','$'], ["\\(","\\)"] ],
        displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
        processEscapes: true
      },
      "HTML-CSS": { availableFonts: ["TeX"] }
    });
  </script>
{% endhighlight %}

#### Displaying Beautiful Mathematical Equations!

Note that there are two types of equations you can create using the TeX/LaTeX syntax: ones occur within a paragraph (in-line) and the other for displaying the equation in a larger format. Now that we have everything we need let's write a simple inline and display equation!

{% highlight html %}
  When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are
  $$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$
{% endhighlight %}

When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are

<div class="center">
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$
</div>

That's the quadratic formula from Algebra!!

#### Conclusion

<a href="https://www.mathjax.org/" target="_blank">MathJax</a> is a powerful library that makes displaying mathematical equations on any browser simple and beautiful. It only takes a few lines of code to get MathJax into your webpage! I will be using this library in the future to create my own mathematical notes.  