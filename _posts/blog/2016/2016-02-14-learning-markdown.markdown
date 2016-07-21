---
layout: post
title:  "Learning Markdown"
date:   2016-02-14 00:15:00
categories: [blog]
---

Markdown is a software tool for text-to-HTML conversions, this tool allows you to write plain text then converts it into HTML. Any files with the extension `.md` is a Markdown file, for example a README.md file in a github repository. The Markdown syntax is very easy to pick up and is commonly used in websites. I recently started to use Markdown when writing my blog posts. I will go over some of the basic syntax in this blog.

#### Emphasis

Markdown syntax makes it easy to italics and bold any of your text. Here is some examples:

    italics, with *asterisks* or _underscores_.
    bold, with **asterisks** or __underscores__.
    combine them with **asterisks and _underscores_**.
    
The results:

italics, with *asterisks* or _underscores_.

bold, with **asterisks** or __underscores__.

combine them with **asterisks and _underscores_**.

#### Header

There is a HTML element called a heading element, this is used for introductory content. This has a range of sizes from `<h1>` to `<h6>`, `<h1>` being the biggest. Many website uses these html elements for the heading of a particular section of the page, just like the front page of a newspaper, each article can have its own heading. The markdown syntax for creating a HTML heading element is very simple. The Atx-style headers use 1-6 hash characters at the start of the line, for example:

    # This is an H1
    ## This is an H2
    ### This is a H3
    #### This is a H4
    ##### This is a H5
    ###### This is a H6

The results:

# This is an H1

## This is an H2

### This is a H3

#### This is a H4

##### This is a H5

###### This is a H6

#### Blockquotes

The blockquote is another HTML element used for quotes. This will create a blockquote HTML element which you can style using CSS. Here is the syntax for using blockquotes in Markdown:

    > Tell me, enigmatic man, whom do you love the best? Your father, or your mother, or your sister, or your brother?
    > I have neither father, nor mother, nor sister, nor brother.
    > Your friends?
    > You are using a word whose meaning remains unknown to me to this very day.
    > Your country?
    > I do not know under what latitude it lies.
    > Beauty?
    > I would love her gladly, goddess and immortal.
    > Gold?
    > I hate it as much as you hate God.
    > Well then!  What do you love, extraordinary stranger?
    > I love the clouds … the passing clouds … over there … over there … the marvelous clouds!
    > by Charles Baudelaire
    
The results:

> Tell me, enigmatic man, whom do you love the best? Your father, or your mother, or your sister, or your brother?

> I have neither father, nor mother, nor sister, nor brother.

> Your friends?

> You are using a word whose meaning remains unknown to me to this very day.

> Your country?

> I do not know under what latitude it lies.

> Beauty?

> I would love her gladly, goddess and immortal.

> Gold?

> I hate it as much as you hate God.

> Well then!  What do you love, extraordinary stranger?

> I love the clouds … the passing clouds … over there … over there … the marvelous clouds!

> by Charles Baudelaire

#### Lists

Let's say you want to make a list of your favorite artists, there is a Markdown syntax for making a unorder list. What if you want to list all the songs in a album? There is a markdown syntax for a ordered list.

    ##### Favorite Artist
    * Jackie Boyz
    * Claude Kelly
    * Johnta Austin
    * Jack Johnson
    * Secondhand Serenade
    
    ##### X album by Ed Sheeran
    1. One
    2. I'm a Mess
    3. Sing
    4. Don't
    5. Nina
    6. Photograph
    7. Bloodstream
    8. Tenerife Sea
    9. Runaway
    10. The Man
    11. Thinking Out Loud
    12. Afire Love
    13. Take It Back
    14. Shirtsleeves
    15. Even My Dad Does Sometimes
    16. I See Fire

The results:

##### Favorite Artist

* Jackie Boyz
* Claude Kelly
* Johnta Austin
* Jack Johnson
* Secondhand Serenade

##### X album by Ed Sheeran

1. One
2. I'm a Mess
3. Sing
4. Don't
5. Nina
6. Photograph
7. Bloodstream
8. Tenerife Sea
9. Runaway
10. The Man
11. Thinking Out Loud
12. Afire Love
13. Take It Back
14. Shirtsleeves
15. Even My Dad Does Sometimes
16. I See Fire

#### Links

Creating hyperlinks is quick and easy with the help of Markdown syntax. There are many ways you can create a link in Markdown, here are some of the common ways:

    [I'm an inline-style link](https://www.google.com)
    [I'm an inline-style link with title](https://www.google.com "Google's Homepage")
    [I'm a reference-style link][Arbitrary case-insensitive reference text]
    [I'm a relative reference to a repository file](/)
    [arbitrary case-insensitive reference text]: https://www.mozilla.org
    
The results:

[I'm an inline-style link](https://www.google.com)

[I'm an inline-style link with title](https://www.google.com "Google's Homepage")

[I'm a reference-style link][Arbitrary case-insensitive reference text]

[I'm a relative reference to a repository file](/)

[arbitrary case-insensitive reference text]: https://www.mozilla.org

#### Images

Markdown makes adding images to your web page simple, you can add a image from google by copying and pasting the url or you can add images from your repository folder.

    ![alt text](http://www.peterlewis.com/wp-content/uploads/2011/09/google-icon.png "Google Logo 1")
    ![alt text][logo]
    [logo]: http://netdna.copyblogger.com/images/google+logo.png "Google Logo 2"

The results:

![alt text](http://www.peterlewis.com/wp-content/uploads/2011/09/google-icon.png "Google Logo 1")

![alt text][logo]

[logo]: http://netdna.copyblogger.com/images/google+logo.png "Google Logo 2"
   
Markdown is amazing and makes you more productive when writing your posts. This is just the basic of using Markdown to write HTML element, if you want to learn more click this <a href="https://daringfireball.net/projects/markdown/" target="_blank">link</a>. My favorite part of Markdown is that you can write HTML in your plain text files and it will still work for example adding a youtube video.

<div class="video-container">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/YQHsXMglC9A" frameborder="0" allowfullscreen></iframe>
</div>

I'm currently using Markdown to write all my blog posts, but there are other alternatives for example <a href="http://commonmark.org/" target="_blank">CommonMark</a>. Learning how to use Markdown is easy, all you have to do is learn the syntax! 