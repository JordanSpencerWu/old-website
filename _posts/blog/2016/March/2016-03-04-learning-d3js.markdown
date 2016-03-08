---
layout: post
title:  "Learning D3.js"
date:   2016-03-04 13:15:00
---
Data-Driven Documents also known as D3.js is a powerful JavaScript library for 
adding data visualization to a webpage. D3.js is a data-driven approach to DOM 
manipulation, this allows you to add svg elements to the DOM that is binded to 
data. Data visualization help us understand the data by creating graphical 
representation of data like graphs and charts. Data is everywhere and having 
these visualization helps us analyze the data. A common data visualization is a 
bar graph, in this blog I will go over some of the basic of D3.js while creating 
a bar graph.

#### Getting Started
The first thing you need to create cool data visualization is the D3.js JavaScript 
library. You can download the zip file <a href="https://d3js.org/" target="_blank">here</a>. 
This library gives you all the built-in methods you need to create svg elements in the 
DOM using only JavaScript! After downloading this zip file, all you have to unzip and add it to your project. Then 
add this JavaScript into your html.

{% highlight html %}
  <script src="/relative/path/goes/here/d3.min.js" charset="utf-8"></script>
{% endhighlight %}

#### Selecting an Element
The first thing to understand is how to select an element in the DOM. D3.js is similar to 
<a href="https://jquery.com/" target="_blank">jQuery</a> when selecting element using selectors. 
If there is a class on the DOM element you would use a prefix of `.` then the class attribute 
value to select it with a selector. Let's see a example of selecting a element with a class selector.

{% highlight html %}
  <div class="example">
  </div>
  
  <script src="/relative/path/goes/here/d3.min.js" charset="utf-8"></script>
  <script>
    d3.select(".example")
      .append("svg")
      .append("rect")
        .attr("width", 50)
        .attr("height", 100)
        .style("fill", "steelblue");
  </script>
{% endhighlight %}

Result:
<div class="example1">
</div>

The following code will insert elements into our div. With D3.js 
we are able to add svg into our html with a few lines of code. The following was added 
into our DOM.

{% highlight html %}
  <div class="example">
    <svg>
      <rect width="50" height="100" style="fill: steelblue;"></rect>
    </svg>
  </div>
{% endhighlight %}

#### Let's Make a Bar Graph
Making a `rect` svg element is easy, but it doesn't tell us anything! For 
the `rect` to be meaningful it has to represent some data or number. Lets learn how to 
bind data to our `rect` elements. The easiest way to store our data is in an `Array` 
in JavaScript. Let's bind our `rect` elements to data from an array.

{% highlight html %}
  <div class="example">
  </div>
  
  <script src="/relative/path/goes/here/d3.min.js" charset="utf-8"></script>
  <script>
    var data = [5, 10, 15, 20, 25],
        width = 200,
        height = 150;
    d3.select(".example")
      .append("svg")
        .attr("width", width)
        .attr("height", height)
      .selectAll("rect")
        .data(data)
        .enter()
        .append("rect")
          .attr("x", function(d, i) { return i * (width / data.length); })
          .attr("y", function(d) { return height - (d*4); })
          .attr("width", width / data.length - 1)
          .attr("height", function(d) { return d*4 })
          .style("fill", "steelblue");
  </script>
{% endhighlight %}

Result:
<div class="example2">
</div>

Now that looks like a bar graph! Lets break down the code:

1. The first things we did was create a few variables that will be used in our svg elements. The data variable is a array of 
numbers that represents the data we want to bind to our svg element. 
2. Everytime you use D3.js you need to select a element in your DOM as the starting point. After selecting a element using D3.js 
`select` method we can `append` a `svg` element to that selected element. This will create a canvas for our data visualization 
for our svg elements. 
3. We then added our `width` and `height` attributes to our `svg` element. 
4. The `selectAll` method is a bit tricky to understand. This method is used to select all `rect` elements inside our `svg` 
element. Since we created a new `svg` element with nothing in it, the `selectAll` will know that there isn't any `rect` element yet. 
5. The next step is to bind our data to the `rect` elements that we used `selectAll` method to select.
6. A very important method is `enter` which will append the `rect` into our canvas and will continue appending `rect` elements 
until every data in the array is binded to a `rect` element. 
7. Each `rect` element has the following attributes `x`, `y`, `width`, `height` and `style`. The `x` and `y` attributes are for the position of each `rect` element, 
we don't want all the `rect` to have the same position. Another thing is that we don't want the height of 
the `rect` to be the same. That's where `function (d,i)` comes in. This function is a built-in function parameter 
in D3.js. This function allows us to create different svg elements using data information! The following parameters 
for this function are `d` (data) and `i` (index).

What makes data binding amazing is that you can dynamically change the data and the bar graph will 
also change with it. Let's make some changes to our data array.

{% highlight javascript %}
  data = [23, 30, 11, 1, 4, 15];
{% endhighlight %} 

Result:
<div class="example3">
</div>

That's cool!! No matter how many data or how little data you have your bar graph will change 
depending on our data.

#### Adding Text
This bar graph is missing some number representation! We can see that each `rect` has different 
height, but we don't know the value of the rect. That's where the `text` svg comes in, we can bind 
our data to the `text` svg like we did to our `rect`. We have to change some of our code, we need 
a reference variable to the svg element. We do this by saving the selected element into a 
variable.

{% highlight html %}
  <div class="example">
  </div>
  
  <script src="/relative/path/goes/here/d3.min.js" charset="utf-8"></script>
  <script>
    var data = [23, 30, 11, 4, 8, 15];
        width = 200,
        height = 150;
    var svg = d3.select(".example")
                .append("svg")
                .attr("width", width)
                .attr("height", height);
                
    // bind data to rect
    svg.selectAll("rect")
      .data(data)
      .enter()
      .append("rect")
      .attr({
        x: function(d, i) {return i * (width / data.length);},
        y: function(d) {return height - (d*4);},
        width: width / data.length - 1,
        height: function(d) {return d*4;}
      })
      .style("fill", "steelblue");

    // bind data to text
    svg.selectAll("text")
      .data(data)
      .enter()
      .append("text")
      .text(function (d) { return d; })
      .attr({
        "text-anchor": "middle",
        x: function(d, i) {return i * (width / data.length)+(width / data.length - 1) / 2;},
        y: function(d) { return height - (d*4)+14; },
        "font-family": "sans-serif",
        "font-size": 12,
        "fill": "#ffffff"
      });  
  </script>
{% endhighlight %}

Result:
<div class="example4">
</div>

That looks better, this bar graph is starting to make more sense!

#### Add Scaling
A problem with our current bar graph is that if we have a data value that is higher than the 
height of our svg element it will not fit in our canvas. That's why we need some scaling factor 
that will scale our bar graph that has a dependency on the data value. D3.js has a few scaling 
methods that help us create scalable data visualization, the one we are going to use is the linear 
scale. We all remember learning about domain and range in math class, scale are function that 
map from an input domain to an output range. The domain in a function usually refers to the independent 
variable which is the x-axis on a graph. A function needs this independent variable say `x` to determine 
the dependent variable `y`. The domain is usually the min and max value of your data you will pass 
into the function and the range is the max and min of the x or y axis of the canvas. We are basically 
trying to normalize our data value with the given output range. Let's create a linear scale for our 
height of the `rect` element.

{% highlight javascript %}
  <div class="example">
  </div>
  
  <script src="/relative/path/goes/here/d3.min.js" charset="utf-8"></script>
  <script>
    var data = [23, 30, 11, 4, 8, 15];
        width = 200,
        height = 150;
    var svg = d3.select(".example")
                .append("svg")
                .attr("width", width)
                .attr("height", height);

    var y = d3.scale.linear()
                .domain([d3.max(data),0])
                .range([height,0]);
                
    // bind data to rect
    svg.selectAll("rect")
      .data(data)
      .enter()
      .append("rect")
      .attr({
        x: function(d, i) {return i * (width / data.length);},
        y: function(d) {return height - y(d);},
        width: width / data.length - 1,
        height: function(d) {return y(d);}
      })
      .style("fill", "steelblue");

    // bind data to text
    svg.selectAll("text")
      .data(data)
      .enter()
      .append("text")
      .text(function (d) { return d; })
      .attr({
        "text-anchor": "middle",
        x: function(d, i) {return i * (width / data.length)+(width / data.length - 1) / 2;},
        y: function(d) { return height - y(d)+14; },
        "font-family": "sans-serif",
        "font-size": 12,
        "fill": "#ffffff"
      });       
{% endhighlight %}

Result:
<div class="example5">
</div>

We added a scale to our y-axis since we are dealing with height. This is a linear scale with 
the domain of [d3.max(data), 0], this means that it will scale with our data. The domain of our 
data is the maximum value in the data array and 0. That means the function is expecting us to 
pass a number between zero and the max number and will normalize it depending on our range. The 
range is the output, this output we want should depend on the height of our canvas. In our case 
the range is [height,0], remember that the y-axis in the svg coordinate system start from zero at the 
top and increases at we go down. We are basically doing this.

<div>
  <svg height="115" width="250" style="display: block; margin:auto">
    <text x="125" y="15" font-style="italic" text-anchor="middle">Input domain</text>
    <line x1="5" y1="30" x2="245" y2="30" stroke="gray" stroke-width="1"></line>
    <circle cx="2" cy="30" r="3" fill="#008"></circle>
    <text x="10" y="48" text-anchor="middle">30</text>
    <circle cx="125" cy="30" r="3" fill="#008"></circle>
    <text x="125" y="48" text-anchor="middle">15</text>
    <circle cx="245" cy="30" r="3" fill="#008"></circle>
    <text x="245" y="48" text-anchor="middle">0</text>
    <line x1="5" y1="90" x2="245" y2="90" stroke="gray" stroke-width="1"></line>
    <circle cx="5" cy="90" r="3" fill="#008"></circle>
    <text x="15" y="84" text-anchor="middle">150</text>
    <circle cx="125" cy="90" r="3" fill="#008"></circle>
    <text x="125" y="84" text-anchor="middle">75</text>
    <circle cx="245" cy="90" r="3" fill="#008"></circle>
    <text x="245" y="84" text-anchor="middle">0</text>
    <text x="125" y="110" font-style="italic" text-anchor="middle">Output range</text>
  </svg>
</div>

As you can see if we pass in a value of 30 to the function we will get the value 150. If we 
pass in a value of 15 to our scale function we will get a value of 75. It's easy to understand 
this linear scale. Now you can see how scaling works in D3.js and how we use it when scaling our 
data visualization. Let's now change our data and our height of the canvas to demonstrate the 
power of scaling!

{% highlight javascript %}
  <div class="example">
  </div>
  
  <script src="/relative/path/goes/here/d3.min.js" charset="utf-8"></script>
    data = [10,38,34,56,79,100,57,88];
    width = 200,
    height = 250;
    var svg = d3.select(".example6")
                .append("svg")
                .attr("width", width)
                .attr("height", height);
                
    var y = d3.scale.linear()
                .domain([d3.max(data),0])
                .range([height,0]);
                
    // bind data to rect
    svg.selectAll("rect")
      .data(data)
      .enter()
      .append("rect")
      .attr({
        x: function(d, i) {return i * (width / data.length);},
        y: function(d) {return height - y(d);},
        width: width / data.length - 1,
        height: function(d) {return y(d);}
      })
      .style("fill", "steelblue"); 
  </script>
{% endhighlight %}

Result:
<div class="example6">
</div>

As you can see the maximum value of the array of 100 takes up all the space of the height of 
the canvas of 250. This is the power of the scale function in D3.js. 

#### Adding Axis
This bar graph is almost done, we have numbers without any description of what the number 
represents. If we add a x-axis to our graph, we can analyze the bar graph. Let's say we 
want to create a bar graph for the number of customers coming in to our store for this week. 
Now our data need to include two information, the day of the week and the number of customers. 
We can use an array of objects as our data which allows us to store more information in one entry. Let's 
now create this graph with x-axis and y-axis.

{% highlight javascript %}
  <div class="example">
  </div>
  <script src="/relative/path/goes/here/d3.min.js" charset="utf-8"></script>
  var data = [
    {"weekday":"Mon", "customers":156},
    {"weekday":"Tue", "customers":125},
    {"weekday":"Wed", "customers":186},
    {"weekday":"Thu", "customers":148},
    {"weekday":"Fri", "customers":99},
    {"weekday":"Sat", "customers":85},
    {"weekday":"Sun", "customers":53}
  ];
  var margin = {top: 0, right: 0, bottom: 30, left: 40};
  var width = 250 - margin.left - margin.right;
  var height = 300 - margin.top - margin.bottom;
              
  // y scale for the bar graph
  var yScale = d3.scale.linear()
              .domain([d3.max(data, function(data) { return data.customers; }),0])
              .range([height,0]);
              
  // y scale for the y-axis
  var y = d3.scale.linear()
          .domain([d3.max(data, function(data) { return data.customers; }),0])
          .range([0,height]);
  
  // x scale for the x-axis
  var xScale = d3.scale.ordinal()
              .domain(data.map(function(d) { return d.weekday }))
              .rangeBands([0, width]);
  
  // create x-axis
  var xAxis = d3.svg.axis()
        .scale(xScale)
        .orient("bottom");
  
  // create y-axis
  var yAxis = d3.svg.axis()
        .scale(y)
        .orient("left");
 
  // reference variable for svg element
  var svg = d3.select(".example")
          .append("svg")
          .attr("width", width + margin.left + margin.right)
          .attr("height", height + margin.bottom + margin.top)
          .style("display", "block")
          .style("margin", "0 auto")
          .append("g")
            .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
  
  // add x-axis
  svg.append("g")
    .attr("class", "x-axis")
    .attr("transform", "translate(0," + height + ")")
    .call(xAxis);
    
  // add y-axis
  svg.append("g")
    .attr("class", "y-axis")
    .call(yAxis);
    
  // bind data to rect
  svg.selectAll("rect")
    .data(data)
    .enter()
    .append("rect")
    .attr({
      x: function(d, i) {return i * (width / data.length);},
      y: function(d) {return height - yScale(d.customers);},
      width: width / data.length - 1,
      height: function(d) {return yScale(d.customers);}
    })
    .style("fill", "steelblue");

  // bind data to text
  svg.selectAll("text")
    .data(data)
    .enter()
    .append("text")
    .text(function (d) { return d.customers; })
    .attr({
      "text-anchor": "middle",
      x: function(d, i) {return i * (width / data.length)+(width / data.length - 1) / 2;},
      y: function(d) { return height - yScale(d.customers)+14; },
      "font-family": "sans-serif",
      "font-size": 12,
      "fill": "#ffffff"
    });  
  </script>
{% endhighlight %}

Result:
<div class="example7">
</div>

Now that looks like a legit bar graph! All you need to know to add a axis to your data 
visualization is the scale and the orientation. D3.js needs to know how to create the 
axis based on a scale and where to put it in the svg canvas.

#### Conculsion
You can build any data visualization with the help of D3.js! D3.js makes creating 
graphs and charts simple using JavaScript and the benefit of using JavaScript is it allows 
you to create dynamic data visualization. There's many tutorials for learning how to use 
D3.js <a href="https://github.com/mbostock/d3/wiki/Tutorials" target="_blank">here</a>. The 
best resource is to look through the API <a href="https://github.com/mbostock/d3/wiki/API-Reference" target="_blank">here</a>, 
this API contains all the methods that you can use with D3.js. Here is a great tutorial 
for understanding the update pattern of D3.js <a href="http://bl.ocks.org/mbostock/3808218" target="_blank">here</a>

Result:
<div class="example8">
</div>
<script src="{{ "/assets/js/d3.min.js" | prepend: site.baseurl }}" charset="utf-8"></script>
<script>
  // example 1
  d3.select(".example1").append("svg")
    .style("display", "block")
    .style("margin", "0 auto")
    .attr("width", 50)
    .attr("height", 100)
    .append("rect")
      .attr("width", 50)
      .attr("height", 100)
      .style("fill", "steelblue");
  
  // example 2
  var data = [5, 10, 15, 20, 25],
      width = 200,
      height = 150;
  d3.select(".example2")
    .append("svg")
      .attr("width", width)
      .attr("height", height)
      .style("display", "block")
      .style("margin", "0 auto")
    .selectAll("rect")
      .data(data)
      .enter()
      .append("rect")
        .attr("x", function(d, i) { return i * (width / data.length); })
        .attr("y", function(d) { return height - (d*4); })
        .attr("width", width / data.length - 1)
        .attr("height", function(d) { return d*4 })
        .style("fill", "steelblue");
  
  // example 4    
  data = [23, 30, 11, 4, 8, 15];
  d3.select(".example3")
    .append("svg")
      .attr("width", width)
      .attr("height", height)
      .style("display", "block")
      .style("margin", "0 auto")
    .selectAll("rect")
      .data(data)
      .enter()
      .append("rect")
        .attr("x", function(d, i) { return i * (width / data.length); })
        .attr("y", function(d) { return height - (d*4); })
        .attr("width", width / data.length - 1)
        .attr("height", function(d) { return d*4 })
        .style("fill", "steelblue");
        
  // example 4
  var svg1 = d3.select(".example4")
            .append("svg")
            .attr("width", width)
            .attr("height", height)
            .style("display", "block")
            .style("margin", "0 auto");

  // bind data to rect
  svg1.selectAll("rect")
    .data(data)
    .enter()
    .append("rect")
    .attr({
      x: function(d, i) {return i * (width / data.length);},
      y: function(d) {return height - (d*4);},
      width: width / data.length - 1,
      height: function(d) {return d*4;}
    })
    .style("fill", "steelblue");

  // bind data to text
  svg1.selectAll("text")
    .data(data)
    .enter()
    .append("text")
    .text(function (d) { return d; })
    .attr({
      "text-anchor": "middle",
      x: function(d, i) {return i * (width / data.length)+(width / data.length - 1) / 2;},
      y: function(d) { return height - (d*4)+14; },
      "font-family": "sans-serif",
      "font-size": 12,
      "fill": "#ffffff"
    });
    
  // example 5
  var svg2 = d3.select(".example5")
            .append("svg")
            .attr("width", width)
            .attr("height", height)
            .style("display", "block")
            .style("margin", "0 auto");

  var y = d3.scale.linear()
              .domain([d3.max(data),0])
              .range([height,0]);
              
  // bind data to rect
  svg2.selectAll("rect")
    .data(data)
    .enter()
    .append("rect")
    .attr({
      x: function(d, i) {return i * (width / data.length);},
      y: function(d) {return height - y(d);},
      width: width / data.length - 1,
      height: function(d) {return y(d);}
    })
    .style("fill", "steelblue");

  // bind data to text
  svg2.selectAll("text")
    .data(data)
    .enter()
    .append("text")
    .text(function (d) { return d; })
    .attr({
      "text-anchor": "middle",
      x: function(d, i) {return i * (width / data.length)+(width / data.length - 1) / 2;},
      y: function(d) { return height - y(d)+14; },
      "font-family": "sans-serif",
      "font-size": 12,
      "fill": "#ffffff"
    });
    
    // example 6
    data = [10,38,34,56,79,100,57,88];
    width = 200,
    height = 250;
    var svg3 = d3.select(".example6")
                .append("svg")
                .attr("width", width)
                .attr("height", height)
                .style("display", "block")
                .style("margin", "0 auto");
                
    var y2 = d3.scale.linear()
                .domain([d3.max(data),0])
                .range([height,0]);
                
    // bind data to rect
    svg3.selectAll("rect")
      .data(data)
      .enter()
      .append("rect")
      .attr({
        x: function(d, i) {return i * (width / data.length);},
        y: function(d) {return height - y2(d);},
        width: width / data.length - 1,
        height: function(d) {return y2(d);}
      })
      .style("fill", "steelblue");

    // bind data to text
    svg3.selectAll("text")
      .data(data)
      .enter()
      .append("text")
      .text(function (d) { return d; })
      .attr({
        "text-anchor": "middle",
        x: function(d, i) {return i * (width / data.length)+(width / data.length - 1) / 2;},
        y: function(d) { return height - y2(d)+14; },
        "font-family": "sans-serif",
        "font-size": 12,
        "fill": "#ffffff"
      });
      
  // example 7
  data = [
    {"weekday":"Mon", "customers":156},
    {"weekday":"Tue", "customers":125},
    {"weekday":"Wed", "customers":186},
    {"weekday":"Thu", "customers":148},
    {"weekday":"Fri", "customers":99},
    {"weekday":"Sat", "customers":85},
    {"weekday":"Sun", "customers":53}
  ];
  var margin = {top: 0, right: 0, bottom: 30, left: 40};
  width = 250 - margin.left - margin.right;
  height = 300 - margin.top - margin.bottom;
              
  var yScale = d3.scale.linear()
              .domain([d3.max(data, function(data) { return data.customers; }),0])
              .range([height,0]);
              
  y = d3.scale.linear()
          .domain([d3.max(data, function(data) { return data.customers; }),0])
          .range([0,height]);
  
  var xScale = d3.scale.ordinal()
              .domain(data.map(function(d) { return d.weekday }))
              .rangeBands([0, width]);
  
  var xAxis = d3.svg.axis()
        .scale(xScale)
        .orient("bottom");
  
  var yAxis = d3.svg.axis()
        .scale(y)
        .orient("left");

  var svg4 = d3.select(".example7")
          .append("svg")
          .attr("width", width + margin.left + margin.right)
          .attr("height", height + margin.bottom + margin.top)
          .style("display", "block")
          .style("margin", "0 auto")
          .append("g")
            .attr("transform", "translate(" + margin.left + "," + margin.top + ")");
  
  // add x-axis
  svg4.append("g")
    .attr("class", "x-axis")
    .attr("transform", "translate(0," + height + ")")
    .call(xAxis);
    
  // add y-axis
  svg4.append("g")
    .attr("class", "y-axis")
    .call(yAxis);
    
  //bind data to rect
  svg4.selectAll("rect")
    .data(data)
    .enter()
    .append("rect")
    .attr({
      x: function(d, i) {return i * (width / data.length);},
      y: function(d) {return height - yScale(d.customers);},
      width: width / data.length - 1,
      height: function(d) {return yScale(d.customers);}
    })
    .style("fill", "steelblue");
    
    // example 8
    var alphabet = "abcdefghijklmnopqrstuvwxyz".split("");
    width = 300;
    height = 150;
    
    var svg5 = d3.select(".example8").append("svg")
            .attr("width",width)
            .attr("height",height)
            .append("g")
              .attr("transform", "translate(32," + (height/2) + ")");
    
    function update(data) {

      // DATA JOIN
      // Join new data with old elements, if any.
      var text = svg5.selectAll("text")
          .data(data, function(d) { return d; })
          .style("font", "bold 10px monospace");

      // UPDATE
      // Update old elements as needed.
      text.attr("class", "update")
        .style("fill","#333")
        .style("font", "bold 20px monospace")
        .transition()
          .duration(750)
          .attr("x", function(d, i) { return i * 10; });

      // ENTER
      // Create new elements as needed.
      text.enter().append("text")
          .attr("class", "enter")
          .attr("dy", ".35em")
          .attr("y", -60)
          .attr("x", function(d, i) { return i * 10; })
          .style("fill-opacity", 1e-6)
          .style("fill", "green")
          .style("font", "bold 20px monospace")
          .text(function(d) { return d; })
        .transition()
          .duration(750)
          .attr("y", 0)
          .style("fill-opacity", 1);

      // EXIT
      // Remove old elements as needed.
      text.exit()
          .attr("class", "exit")
        .transition()
          .duration(750)
          .attr("y", 60)
          .style("fill-opacity", 1e-6)
          .remove();
    }

    // The initial display.
    update(alphabet);

    // Grab a random sample of letters from the alphabet, in alphabetical order.
    setInterval(function() {
      update(d3.shuffle(alphabet)
          .slice(0, Math.floor(Math.random() * 26))
          .sort());
    }, 1500);
</script>
