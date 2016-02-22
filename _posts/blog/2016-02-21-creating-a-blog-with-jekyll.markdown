---
layout: post
title:  "Creating a Blog With Jekyll"
date:   2016-02-21 13:15:00
categories: [blog]
---
Creating your own blog isn't complicated and is free. Jekyll is great for 
creating blogs by transforming your plain text into static websites. With Jekyll 
you have more control over your site from styling to adding more features. When 
using Jekyll you don't have to worry about hosting companies, you can easily 
deploy your site using GitHub for free. In this blog I will cover how to create 
a blog site with Jekyll.

#  Getting Started

Jekyll is a parsing engine bundled as a ruby gem, the first thing you would need to 
do is install ruby onto your machine. There are many resources online for installing 
ruby and it varies depending on your operating system. Once you have ruby installed, 
you are able to install gems which is a shareable code. Once you installed ruby, 
run the following commands inside your terminal.
 
{% highlight shell %}
  ~ $ gem install jekyll
  ~ $ jekyll new myblog
  ~ $ cd myblog
  ~ $ jekyll serve
{% endhighlight %}
 
The first command `gem install jekyll` will install this gem into your machine, this allow 
you to use the command line interface (CLI) `jekyll` in your terminal. The command `jekyll new 
blog` will create the jekyll structure for your blog site. This basically creates all 
the directories and files you will need to get started with jekyll inside a directory 
called myblog. The command `cd myblog` is a built-in CLI that says change directory to 
myblog, this will enter the directory you just created. The last command is a jekyll CLI 
that creates a local server on your machine on port 4000, which you can see the website by 
going to `localhost:4000` on any browser. 
 
It's important to understand what is going on when creating a 
local server on your machine. In web development all the files for a web page is saved on a 
hosting server, we are doing something similar by creating local server on our machine for all the files to 
be served. When you go to `localhost:4000` on any browser, it is getting all the files like 
HTML, CSS, and Javascript needed to render your web page. The port number is just a TCP port 
that is available on your machine. To close your server run `ctrl + c`.

# Jekyll Structure

{% highlight markdown %}
  myblog
  ├── _includes
  |   ├── footer.html
  |   └── head.html
  |   └── header.html
  |   └── icon-github.html
  |   └── icon-github.svg
  |   └── icon-twitter.html
  |   └── icon-twitter.svg
  ├── _layouts
  |   ├── default.html
  |   └── page.html
  |   └── post.html
  ├── _posts
  |   ├── 2016-02-21-welcome-to-jekyll.markdown
  ├── _sass
  |   └── _base.scss
  |   └── _layout.scss
  |   └── _syntax-highlighting.scss
  ├── css
  |   └── main.scss
  ├── .gitignore
  ├── _config.yml
  ├── about.md
  ├── feed.xml
  └── index.html
{% endhighlight %}

All this was created when you ran the `jekyll new myblog` CLI command in your terminal. 
This provides you with an example of a blog site using jekyll and understanding all the files 
is essential to creating your own custom blog site. It's important to know what Jekyl uses the 
`Liquid` templating language, for more information 
click <a href="https://docs.shopify.com/themes/liquid" target="_blank">here</a>). 
What is great about this language is that it allows HTML reuse and has built-in filtering 
methods which is great for filtering your posts.

## _includes

This folder is used when you have reuseable html that you might want to include into your 
HTML page. A great examples is having a `navbar.html`, you can include this navbar 
in all your static websites. In the blog structure, jekyll included a footer, head, header, and 
other files like svg. Scalable Vector Graphic (SVG) are very popular in web development when 
rendering logos in the browser for their scalability in varies device screens.

# _layouts

This folder is used for creating HTML for different static pages on your websites. You might 
want a page to look different depending on the content you want to display. For example if you 
had a `post.html` for all your post, this HTML page will be use to display all your posts so that 
every post looks uniform. Jekyll provides you with some example html files, you can easily 
customize them to your needs.

# _posts

This folder is where you create all your posts in a specific format, following this format is 
important since the jekyll will parse your files in a conventional way. These files can be 
saved as HTML or Markdown. **All post must have 
<a href="http://jekyllrb.com/docs/frontmatter/" target="_blank">YAML Front Matter</a>**. 
The YAML Front Matter is how jekyll know how to build your static websites. When creating a post 
the naming convention is `YEAR-MONTH-DAY-name-of-blog.md`. In addition Jekyll allows you to add tags and 
categories to your post. Using the categories allows you to have different types of post like 
blog, music, anime, etc. You can also add tags your post for different topics like web development, 
html, css, javascript, etc. Just remember this folder is where you store all your posts.

# _sass
This folder is where you store all the styles for your website. Syntactically Awesome Style 
Sheet (Sass) is a extension of CSS. This extension is a better way of writing CSS and follows 
the Don't Repeat Yourself (DRY) principle. Sass allows you to write less code by introducing 
variables, nested rules, mixins, inline imports, and more. At the end of the day your sass files 
will be converted into css which jekyll does for you. To learn more about Sass click 
<a href="http://sass-lang.com/guide" target="_blank">here</a>. Just remember this folder is where you can 
style your blog site, there are many jekyll themes you can look at and implement. Here are a few jekyll 
themes sites: 

* <a href="http://jekyllthemes.org/" target="_blank">jekyllthemes.org</a>
* <a href="https://github.com/jekyll/jekyll/wiki/Themes" target="_blank">wikiThemes</a>
* <a href="http://jekyllthemes.io/" target="_blank">jekyllthemes.io/</a>

# css
This is the folder that converts all your sass files into css. This folder is important when 
using the jekyll with sass, you need this `main.scss` for jekyll to convert your sass files to 
css files. This is where you import all your sass files and jekyll will add them into your 
static websites.

# .gitignore
This file is used when using git by excluding any specific files you don't want to save, example will be 
personal information like key and secret when accessing a API. Git is a version control 
system which allows you to save coding project on your local machine. The power of git is 
that you do not need internet to save you projects and allows you to save snapshot of 
your project every time you make a commit. Learn more about git by reading this book 
, <a href="https://git-scm.com/book/en/v2" target="_blank">Pro Git</a>.

# _config.yml
This is all the configuration for your jekyll website. This file is where you can store 
global variables which you can use in your static website, some example will be your name, 
email address, github username, linkedin url, etc. Any plugin you want to use like pagination 
will also go in this file. If you want more information about configuration for jekyll 
click <a href="http://jekyllrb.com/docs/configuration/" target="_blank">here</a>.

# about.md and index.html
These are the static website page that jekyll will render. The index.html is where all your 
posts will be rendered and is the home page. The about page will contain 
information about yourself in Markdown. **Note these pages must have YAML Front Matter**. You can create 
more static pages by saving a new html or markdown file at the root of this project. Examples of creating 
more html file might be a project page, contact page, etc.

# feed.xml
This is used for a RSS feed which allows users to subscribe to your content. Jekyll already 
included everything you need for the RSS feed, all you have to do is change the name, description, 
and url in the `_config.yml` to your own.

# Hosting on GitHub
Github will host one site for you and unlimited project sites for free. It is very easy to use and 
allows you to show off your projects to the world. They provide a quick get started tutorial, 
check it out by clicking this <a href="https://pages.github.com/" target="_blank">link</a>.

# Conclusion

Jekyll allows you to customize your blog website by allowing you to add more features to 
your blog site. There are many features you can add to your 
blog site like pagination, 404.html, Disqus, Archive, etc. The web provides many 
resources on how to add these features to your jekyll project. Creating your blog website 
with Jekyll give you more control over your site than other CMS blog platforms. 
This is just a basic tutorial on how to use Jekyll to create your own blog site. 
Anyone can create a blog site using Jekyll and host it on GitHub!