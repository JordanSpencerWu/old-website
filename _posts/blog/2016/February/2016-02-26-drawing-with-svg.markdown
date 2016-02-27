---
layout: post
title:  "Drawing With SVG"
date:   2016-02-26 13:15:00
---
Scalable Vector Graphics (SVG) is a markup language for describing two-dimensional vector 
graphics. This allows you to draw images that has the same scaling 
in any screen size. This is great for creating images that will be used 
on a moblie, tablet, and desktop screens. This makes SVG very responsive and 
many images these days are replaced with svg. In this blog I will go over some of the 
basic shapes you can draw with svg.

#### SVG element
HTML5 introduced a new elment called `svg` which allows you to use svg inside your 
html. This element tells the browser that it is a svg and will act like a canvas for your
two-dimensional vectors graphics. This element has a few attributes that we can use, 
the commonly used attributes are `width` and `height`. Lets start off by creating our 
svg and defining a width and height for it.

{% highlight html %}
  <svg height="250" width="250">
  </svg>
{% endhighlight %}

Now we have a canvas for our vector graphics to live in, lets learn the SVG coordinate 
space. We know from math that any two-dimensional plane has a x and y coordinate. All 
the vector graphics has a `x` and `y` attribute that will determine the starting position 
of the element in the canvas. The top left of the canvas is (0, 0), the top right is (width, 0), 
the bottom left is (0, height), and the bottom right is (width, height).

<div>
  <svg height="65" width="300" style="display: block; margin:auto">
    <line x1="5" y1="5" x2="5" y2="50" stroke="gray" stroke-width="1"></line>
    <line x1="5" y1="50" x2="0" y2="45" stroke="gray" stroke-width="1"></line>
    <line x1="5" y1="50" x2="10" y2="45" stroke="gray" stroke-width="1"></line>
    <line x1="5" y1="5" x2="245" y2="5" stroke="gray" stroke-width="1"></line>
    <line x1="245" y1="5" x2="240" y2="0" stroke="gray" stroke-width="1"></line>
    <line x1="245" y1="5" x2="240" y2="10" stroke="gray" stroke-width="1"></line>
    <circle cx="5" cy="5" r="3" fill="#008"></circle>
    <text x="10" y="20">0,0</text>
    <circle cx="105" cy="25" r="3" fill="#008"></circle>
    <text x="110" y="40">100,20</text>
    <circle cx="205" cy="45" r="3" fill="#008"></circle>
    <text x="210" y="60">200,40</text>
  </svg>
</div>

As you can see the x coordinate increases from left to right while the 
y coordinate increases from top to bottom.

#### Draw a Line
There is a vector graphic for a `line` element. This `line` element needs to have the 
following attributes `x1`, `x2`, `y1`, and `y2`. You can probably see that these 
attributes represents points on the svg canvas. The starting point is (x1,y1) and the ending 
point is (x2, y2). Lets now draw a simple line.

{% highlight html %}
  <svg width="120" height="120">
    <line x1="20" y1="100" 
          x2="100" y2="20" 
          stroke="black" 
          stroke-width="2"/>
  </svg>
{% endhighlight %}

<div>
  <svg width="120" height="120" style="display: block; margin:auto">
    <line x1="20" y1="100" 
          x2="100" y2="20" 
          stroke="black" 
          stroke-width="2"/>
  </svg>
</div>

That was simple and easy!

#### Draw a Rectangle
Lets now draw a rectangle using the `rect` element! This `rect` element is 
based off the position of a corner and its width and height. The attributes you 
need to create a rectangle are `x`, `y`, `rx`, `ry`, `width`, and `height`. Lets 
now create this rectangle and add the color red to it.

{% highlight html %}
  <svg width="120" height="120">
  <rect x="10" y="10"
        width="100" height="100"
        rx="15" ry="15"
        style="fill: red;"/>
  </svg>
{% endhighlight %}

<div>
  <svg width="120" height="120" style="display: block; margin:auto">
  <rect x="10" y="10"
        width="100" height="100"
        rx="15" ry="15"
        style="fill: red;"/>
  </svg>
</div>

The following code creates a rectangle at (x,y) with the width of 100px 
and height of 100px. The `rx` and `ry` values defines the x-radius and 
y-radius, this give us a rounded corners. Lastly, we added some style to our 
rectangle with the property of fill and the color red.

#### Draw a Circle
Drawing a circle is simple with the `circle` element. All we have to do is add 
the `circle` element inside our `svg` and add the following attributes 
`cx`, `cy`, and `r`. We need to know where to put our circle in our canvas, 
the `cx` and `cy` attributes defines where the center coordinates of the circle 
should be placed and the `r` represents the radius. 

{% highlight html %}
  <svg width="120" height="120">
    <circle cx="60" cy="60" r="50" style="fill: crimson;"/>
  </svg>
{% endhighlight %}

<div>
  <svg width="120" height="120" style="display: block; margin:auto">
    <circle cx="60" cy="60" r="50" style="fill: crimson;"/>
  </svg>
</div>

Now we can draw a perfect circle!!

#### Conclusion
Many of the icons you see in the web today are svg, here is a popular 
icon library called <a href="https://fortawesome.github.io/Font-Awesome/" target="_blank">Font Awesome</a>.
<a href="https://inkscape.org/en/" target="_blank">Inkscape</a> and 
<a href="http://www.adobe.com/products/illustrator.html" target="_blank">Illustrator</a> are 
SVG-tools for converting images to svg. You can create amazing svg using those tools and 
apply animations to make them dynamic.

<svg version="1.1" width="320" height="320" viewBox="0 0 320 320" fill="none" stroke="#000" stroke-linecap="round"
     xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <path id="r1">
      <animate id="p1" attributeName="d" values="m160,160l0,0 0,0;m130,110l30,-17 30,17;m130,60l30,-17 30,17;m160,20l0,0 0,0" dur="6s" repeatCount="indefinite"/>
      <animate attributeName="stroke-width" values="0;4;4;4;0" dur="6s" repeatCount="indefinite" begin="p1.begin"/>
    </path>
    <path id="r2">
      <animate attributeName="d" values="m160,160l0,0 0,0;m130,110l30,-17 30,17;m130,60l30,-17 30,17;m160,20l0,0 0,0" dur="6s" repeatCount="indefinite" begin="p1.begin+1s"/>
      <animate attributeName="stroke-width" values="0;4;4;4;0" dur="6s" repeatCount="indefinite" begin="p1.begin+1s"/>
    </path>
    <path id="r3">
      <animate attributeName="d" values="m160,160l0,0 0,0;m130,110l30,-17 30,17;m130,60l30,-17 30,17;m160,20l0,0 0,0" dur="6s" repeatCount="indefinite" begin="p1.begin+2s"/>
      <animate attributeName="stroke-width" values="0;4;4;4;0" dur="6s" repeatCount="indefinite" begin="p1.begin+2s"/>
    </path>
    <path id="r4">
      <animate id="p1" attributeName="d" values="m160,160l0,0 0,0;m130,110l30,-17 30,17;m130,60l30,-17 30,17;m160,20l0,0 0,0" dur="6s" repeatCount="indefinite" begin="p1.begin+3s"/>
      <animate attributeName="stroke-width" values="0;4;4;4;0" dur="6s" repeatCount="indefinite" begin="p1.begin+3s"/>
    </path>
    <path id="r5">
      <animate attributeName="d" values="m160,160l0,0 0,0;m130,110l30,-17 30,17;m130,60l30,-17 30,17;m160,20l0,0 0,0" dur="6s" repeatCount="indefinite" begin="p1.begin+4s"/>
      <animate attributeName="stroke-width" values="0;4;4;4;0" dur="6s" repeatCount="indefinite" begin="p1.begin+4s"/>
    </path>
    <path id="r6">
      <animate attributeName="d" values="m160,160l0,0 0,0;m130,110l30,-17 30,17;m130,60l30,-17 30,17;m160,20l0,0 0,0" dur="6s" repeatCount="indefinite" begin="p1.begin+5s"/>
      <animate attributeName="stroke-width" values="0;4;4;4;0" dur="6s" repeatCount="indefinite" begin="p1.begin+5s"/>
    </path>
  </defs>
  <use xlink:href="#r1"/>
  <use xlink:href="#r1" transform="rotate(60 160 160)"/>
  <use xlink:href="#r1" transform="rotate(120 160 160)"/>
  <use xlink:href="#r1" transform="rotate(180 160 160)"/>
  <use xlink:href="#r1" transform="rotate(240 160 160)"/>
  <use xlink:href="#r1" transform="rotate(300 160 160)"/>
  <use xlink:href="#r2" transform="rotate(30 160 160)"/>
  <use xlink:href="#r2" transform="rotate(90 160 160)"/>
  <use xlink:href="#r2" transform="rotate(150 160 160)"/>
  <use xlink:href="#r2" transform="rotate(210 160 160)"/>
  <use xlink:href="#r2" transform="rotate(270 160 160)"/>
  <use xlink:href="#r2" transform="rotate(330 160 160)"/>
  <use xlink:href="#r3"/>
  <use xlink:href="#r3" transform="rotate(60 160 160)"/>
  <use xlink:href="#r3" transform="rotate(120 160 160)"/>
  <use xlink:href="#r3" transform="rotate(180 160 160)"/>
  <use xlink:href="#r3" transform="rotate(240 160 160)"/>
  <use xlink:href="#r3" transform="rotate(300 160 160)"/>
  <use xlink:href="#r4" transform="rotate(30 160 160)"/>
  <use xlink:href="#r4" transform="rotate(90 160 160)"/>
  <use xlink:href="#r4" transform="rotate(150 160 160)"/>
  <use xlink:href="#r4" transform="rotate(210 160 160)"/>
  <use xlink:href="#r4" transform="rotate(270 160 160)"/>
  <use xlink:href="#r4" transform="rotate(330 160 160)"/>
  <use xlink:href="#r5"/>
  <use xlink:href="#r5" transform="rotate(60 160 160)"/>
  <use xlink:href="#r5" transform="rotate(120 160 160)"/>
  <use xlink:href="#r5" transform="rotate(180 160 160)"/>
  <use xlink:href="#r5" transform="rotate(240 160 160)"/>
  <use xlink:href="#r5" transform="rotate(300 160 160)"/>
  <use xlink:href="#r6" transform="rotate(30 160 160)"/>
  <use xlink:href="#r6" transform="rotate(90 160 160)"/>
  <use xlink:href="#r6" transform="rotate(150 160 160)"/>
  <use xlink:href="#r6" transform="rotate(210 160 160)"/>
  <use xlink:href="#r6" transform="rotate(270 160 160)"/>
  <use xlink:href="#r6" transform="rotate(330 160 160)"/>
</svg>

SVG is amazing, learn more about svg <a href="https://developer.mozilla.org/en-US/docs/Web/SVG" target="_blank">here</a>. 
SVG is used in <a href="https://d3js.org/" target="_blank">D3 js</a> for creating scalable 
data visualization.