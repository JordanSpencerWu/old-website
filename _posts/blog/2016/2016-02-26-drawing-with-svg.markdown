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

#### SVG Elements

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

#### Draw a Path

Now that we know how to draw a line, lets draw a path. There is a graphical 
element called `path` that allows us to draw on the canvas. This `path` element 
has an attribute `d` which contains a series of path description. The path description 
has a few instructions Moveto, Lineto, Curveto, Arcto, and ClosePath. 
Click <a href="https://developer.mozilla.org/en-US/docs/Web/SVG/Attribute/d" target="_blank">here</a> 
for more details on the `d` attribute. Lets draw a simple path!

{% highlight html %}
  <svg width="300" height="300">
    <path d="M 50 50 L 200 50 L 125 200 z"
          fill="orange" stroke="black" stroke-width="3" />
  </svg>
{% endhighlight %}

<div>
  <svg width="250" height="250" style="display: block; margin:auto">
    <path d="M 50 50 L 200 50 L 125 200 z"
          fill="orange" stroke="black" stroke-width="3" />
  </svg>
</div>

We are able to draw a triangle with this `path` element. The `d` attribute are instructions 
that will you how to draw the path. The first instruction `M 50 50` states to Moveto that location (50,50), 
then `L 200 50` states to write a Lineto that location (200,50), then `L 125 200` draws 
another Lineto (125,200), lastly we finish by ClosePath. We then add some styles like 
color, stroke color, and stroke width. 

#### Draw a Polyline

A `polyline` element is used to create a series of straight lines connecting several points. 
This element can be used to draw a line graph or any drawing that only uses straight lines. 
The `path` element needs the `points` attributes which specifies all the points. 

{% highlight html %}
  <svg width="120" height="120">
    <polyline fill="none" stroke="black" stroke-width="3"
              points="20,100 40,60 70,80 100,20"/>
  </svg>
{% endhighlight %}

<div>
  <svg width="120" height="120" style="display: block; margin:auto">
    <polyline fill="none" stroke="black" stroke-width="3" 
            points="20,100 40,60 70,80 100,20"/>
  </svg>
</div>

It's easy to use `polyline` when creating a line graph! All it requires are the 
points you want to connect.

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

#### Draw a Text

There will be times when you want to have text inside your `svg`. There is a `text` 
element that allows you to write text in your canvas.

{% highlight html %}
  <svg width="150" height="50">
    <text x="10" y="20">SVG Text Example</text>
  </svg>
{% endhighlight %}

<div>
  <svg width="150" height="50" style="display: block; margin:auto">
    <text x="10" y="20">SVG Text Example</text>
  </svg>
</div>

#### Draw a Polygon

There is a graphical element called `polygon` that defines a closed shape consisting of a set 
of connected straight lines segments. The last point is connected to the first point. This element 
is similar to `polyline` where you only need the `points` attributes.

{% highlight html %}
  <svg width="120" height="120">
    <polygon points="60,20 100,40 100,80 60,100 20,80 20,40" style="fill:red;"/>
  </svg>
{% endhighlight %}

<div>
  <svg width="120" height="120" style="display: block; margin:auto">
    <polygon points="60,20 100,40 100,80 60,100 20,80 20,40" style="fill:red;"/>
  </svg>
</div>

Use `polygon` whenever you need to create a closed shape with straight lines.

#### Draw a Circle

Drawing a circle is simple with the `circle` element. All we have to do is add 
the `circle` element inside our `svg` and add the following attributes 
`cx`, `cy`, and `r`. We need to know where to put our circle in our canvas, 
the `cx` and `cy` attributes defines where the center coordinates of the circle 
should be placed and the `r` represents the radius. 

{% highlight html %}
  <svg width="120" height="120">
    <circle cx="60" cy="60" r="50" style="fill:crimson;"/>
  </svg>
{% endhighlight %}

<div>
  <svg width="120" height="120" style="display: block; margin:auto">
    <circle cx="60" cy="60" r="50" style="fill:crimson;"/>
  </svg>
</div>

Now we can draw a perfect circle!!

#### Draw a Ellipse

The `ellipse` element is similar to the `circle` element with some additional attributes like 
`rx` and `ry`. Those attributes will control the radius with their corresponding x and y axis.

{% highlight html %}
  <svg width="120" height="120">
    <ellipse cx="60" cy="60" rx="50" ry="25" style="fill:steelblue"/>
  </svg>
{% endhighlight %}

<div>
  <svg width="120" height="120" style="display: block; margin:auto">
    <ellipse cx="60" cy="60" rx="50" ry="25" style="fill:steelblue"/>
  </svg>
</div>

Drawing two-dimensional vector graphics with `svg` elements is very easy! All these elements are 
commonly used when creating svg icons and logos. 

#### Container Elements

SVG has a few container elements that are used to groups your svg `elements` so that you can 
apply the same styles to a group of elements, reuse svg elements, or creating svg sprites.

#### Defs

SVG allows graphical objects to be defined for later reuse. It is recommended that, wherever possible, 
referenced elements be defined inside of a `defs` element. Its is commonly used for animations and adding 
adding gradients to svg elements.

{% highlight html %}
  <svg width="300" height="300">
      <!-- Item For Reuse -->
      <defs>
          <g id="itemForReuse">
              <circle cx="50" cy="50" r="50" />
          </g>
      </defs>
      
      <!-- Item Use #1 -->
      <use xlink:href="#itemForReuse" x="0" y="0" fill="#FF742B" />

      <!-- Item Use #2 -->
      <use xlink:href="#itemForReuse" x="120" y="120" fill="#A2CE5D" />
  </svg>
{% endhighlight %}

<div>
  <svg width="300" height="300" style="display: block; margin:auto">
      <defs>
          <g id="itemForReuse">
              <circle cx="50" cy="50" r="50" />
          </g>
      </defs>
      <use xlink:href="#itemForReuse" x="0" y="0" fill="#FF742B" />
      <use xlink:href="#itemForReuse" x="120" y="120" fill="#A2CE5D" />
  </svg>
</div>

#### G

The `g` element is a container used to group other SVG elements. Transformations 
applied to the g element are performed on all of its child elements, and 
any of its attributes are inherited by its child elements. A good example is applying 
the same styles to a group of elements.

{% highlight html %}
  <svg width="300" height="300">
      <style>
          .group { fill: red; }
      </style>
      <g class="group">
          <circle cx="50" cy="50" r="50" />
          <circle cx="170" cy="170" r="50" />
      </g>
  </svg>
{% endhighlight %}

<div>
  <svg width="300" height="300" style="display: block; margin:auto">
    <style>
        .group { fill: red; }
    </style>
    <g class="group">
        <circle cx="50" cy="50" r="50" />
        <circle cx="170" cy="170" r="50" />
    </g>
  </svg>
</div>

#### Symbol

The symbol element is used to define graphical template objects which can 
be instantiated by a <use> element. The use of symbol elements for graphics 
that are used multiple times in the same document adds structure and semantics.

{% highlight html %}
  <svg width="300" height="300">
    <!-- Symbol For Reuse -->
    <symbol id="symbolForReuse">
        <circle cx="50" cy="50" r="50" />
    </symbol>
    
    <!-- Symbol Use #1 -->
    <use xlink:href="#symbolForReuse" x="0" y="0" fill="#FF742B" />

    <!-- Symbol Use #2 -->
    <use xlink:href="#symbolForReuse" x="120" y="120" fill="#A2CE5D" />
  </svg>
{% endhighlight %}

<div>
  <svg width="300" height="300" style="display: block; margin:auto">
    <!-- Symbol For Reuse -->
    <symbol id="symbolForReuse">
        <circle cx="50" cy="50" r="50" />
    </symbol>
    
    <!-- Symbol Use #1 -->
    <use xlink:href="#symbolForReuse" x="0" y="0" fill="#FF742B" />

    <!-- Symbol Use #2 -->
    <use xlink:href="#symbolForReuse" x="120" y="120" fill="#A2CE5D" />
  </svg>
</div>

#### Adding Gradient

You can add two different gradients to your svg elements to add more visual 
effect to your shapes. The `linearGradient` element define linear 
gradients to fill or stroke graphical elements and `radialGradient` 
define radial gradients to fill or stroke graphical elements.

#### linearGradient

{% highlight html %}
  <svg width="300" height="250">
    <defs>
        <linearGradient id="gradient" x1="0" x2="0" y1="0" y2="1">
            <stop offset="0%" stop-color="#FCC1A7" />
            <stop offset="100%" stop-color="#F16823" />
        </linearGradient>
    </defs>
    
    <!-- Rectangle with gradient fill  -->
    <rect fill="url(#gradient)" x="0" y="0" width="300" height="200" />
  </svg>
{% endhighlight %}

<div>
  <svg width="300" height="250" style="display: block; margin:auto">
    <!-- Gradient -->
    <defs>
        <linearGradient id="gradient" x1="0" x2="0" y1="0" y2="1">
            <stop offset="0%" stop-color="#FCC1A7" />
            <stop offset="100%" stop-color="#F16823" />
        </linearGradient>
    </defs>
    
    <!-- Rectangle with gradient fill  -->
    <rect fill="url(#gradient)" x="0" y="0" width="300" height="200" />
  </svg>
</div>

#### radialGradient

{% highlight html %}
  <svg width="300" height="250">
    <!-- Gradient -->
    <defs>
        <radialGradient id="gradient" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
            <stop offset="0%" stop-color="#FCC1A7" />
            <stop offset="95%" stop-color="#F16823" />
        </radialGradient>
    </defs>
    
    <!-- Rectangle with gradient fill -->
    <rect fill="url(#gradient)" x="0" y="0" width="300" height="200" />
  </svg>
{% endhighlight %}

<div>
  <svg width="300" height="250" style="display: block; margin:auto">
    <defs>
        <radialGradient id="gradient" cx="50%" cy="50%" r="50%" fx="50%" fy="50%">
            <stop offset="0%" stop-color="#FCC1A7" />
            <stop offset="95%" stop-color="#F16823" />
        </radialGradient>
    </defs>
    
    <!-- Rectangle with gradient fill -->
    <rect fill="url(#gradient)" x="0" y="0" width="300" height="200" />
  </svg>
</div>

#### Animation Elements

You make your svg elements come to life by adding animations. Here a few examples 
of animation in svg.

#### Animate

{% highlight html %}
  <svg width="300" height="250">
    <rect x="0" y="0" width="300" height="200">
        <animate attributeName="x" from="-300" to="300" dur="5s" repeatCount="indefinite" />
    </rect>
  </svg>
{% endhighlight %}

<div>
  <svg width="300" height="250" style="display: block; margin:auto">
    <rect x="0" y="0" width="300" height="200">
        <animate attributeName="x" from="-300" to="300" dur="5s" repeatCount="indefinite" />
    </rect>
  </svg>
</div>

#### AnimateMotion

{% highlight html %}
  <svg width="300" height="250">
    <!-- Motion Path -->
    <path id="motionPath" 
          d="M-141.333,218C-60,138.667,20,39.333,74.667,45.333s244.667,200,244.667,200" 
          stroke="#ccc" stroke-width="3" fill="none" />

    <!-- Animated Item -->
    <circle cx="" cy="" r="40">
        <animateMotion dur="3s" repeatCount="indefinite">
            <mpath xlink:href="#motionPath" />
        </animateMotion>
    </circle>
  </svg>
{% endhighlight %}

<div>
  <svg width="300" height="250" style="display: block; margin:auto">
    <!-- Motion Path -->
    <path id="motionPath" 
          d="M-141.333,218C-60,138.667,20,39.333,74.667,45.333s244.667,200,244.667,200" 
          stroke="#ccc" stroke-width="3" fill="none" />

    <!-- Animated Item -->
    <circle cx="" cy="" r="40">
        <animateMotion dur="3s" repeatCount="indefinite">
            <mpath xlink:href="#motionPath" />
        </animateMotion>
    </circle>
  </svg>
</div>

#### AnimateTransform

{% highlight html %}
  <svg width="300" height="300">
    <rect x="75" y="75" width="150" height="150">
        <animateTransform attributeName="transform"
                          type="rotate"
                          from="0 150 150"
                          to="360 150 150"
                          dur="5s"
                          repeatCount="indefinite" />
    </rect>
  </svg>
{% endhighlight %}

<div>
  <svg width="300" height="300" style="display: block; margin:auto">
    <rect x="75" y="75" width="150" height="150">
        <animateTransform attributeName="transform"
                          type="rotate"
                          from="0 150 150"
                          to="360 150 150"
                          dur="5s"
                          repeatCount="indefinite" />
    </rect>
  </svg>
</div>

#### Tools

There are programs that can create svg for you like <a href="https://inkscape.org/en/" target="_blank">Inkscape</a> and 
<a href="http://www.adobe.com/products/illustrator.html" target="_blank">Illustrator</a>. These programs will create your 
svg by converting your drawing to svg elements like the ones mentioned above. These tools are great for creating your 
own custom icons and logos! If you are looking for great svg icons, you should check 
out <a href="https://fortawesome.github.io/Font-Awesome/" target="_blank">Font Awesome</a>.

#### Libraries

There are many good libraries for creating awesome svg available online. If you want to add more animation to your svg elements, you should 
take a look at <a href="http://snapsvg.io/" target="_blank">Snap.svg</a>. Snap.svg has a large library of animation you can 
use to make your svg come to life. If you want your svg to look like it's being drawn then you should use 
<a href="https://maxwellito.github.io/vivus/" target="_blank">Vivus.js</a>. Lastly, a popular svg library is 
<a href="https://d3js.org/" target="_blank">D3.js</a> which makes data visualization which helps you 
create graphs based on your data. You can do anything with svg!!

<div>
  <svg version="1.1" width="320" height="320" viewBox="0 0 320 320" fill="none" stroke="#000" stroke-linecap="round"
      xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" style="display: block; margin:auto">
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
</div>

SVG is amazing, learn more about 
svg <a href="https://developer.mozilla.org/en-US/docs/Web/SVG" target="_blank">here</a>.