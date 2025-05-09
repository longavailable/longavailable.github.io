---
layout: post
title:  How to write a Jekyll blog
author: Bruce Liu
# last update date
date:   2024-12-24 14:20:00 +0800
# first published date
published: 2019-09-01 00:50:00 +0200 
categories: [post]
tags: [first blog, Jekyll, markdown, map, picture, emoji]
description: Hello, Jekyll!
header-image: 
permalink: /jekyll_blog/
toc:
---

This is a templete to show how to write a post.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# How to test a blog using bundle:

- Navigate to path of the githubpages repository.

    ```sh
cd D:\git\githubPages\longavailable.github.io
    ```

- Execute the following command:

	```sh
bundle exec jekyll serve
	```
	
	or with `--drafts` tag.
	
	```sh
bundle exec jekyll serve --drafts
	```
	
- Check the githubpages website from [http://127.0.0.1:4000](http://127.0.0.1:4000).

- `Ctrl + C ` quit the bundle serve.

# Markdown skills

## Space, tab, and blank line

- [Paragraph: text line + blank line + text line](https://markdown-guide.readthedocs.io/en/latest/basics.html#paragraphs)

- [Plain code block: paragraph text line (+ blank line) + 1 Tab or 4 spaces + code + blank line](https://markdown-guide.readthedocs.io/en/latest/basics.html?highlight=space#code-block)

- [Plain code block in list (indented): (blank line) + '1 Tab + 2 spaces' or 6 spaces  + code (+ blank line)](https://markdown-guide.readthedocs.io/en/latest/basics.html?highlight=space#code-block)

	  Hello, world in list

- [Fenced code block: (blank line) +  ` ` `  + language identifier + enter + code + enter + ` ` ` (+ blank line)](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

```md
## Header line h2.
```

- [Fenced code block in list (indented): (blank line) + 1 Tab or 4 spaces +  ` ` `  + language identifier + enter + code + enter + 1 Tab or 4 spaces + ` ` ` (+ blank line)](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf). It didnot work for `<img>`, see [here](#NOTWORKING) 2nd item. Why?

	```md
### Header line h3.
	```

- [More than 1 space in a text snippet (non-breaking space): `&nbsp;` is 2 spaces, `&nbsp;&nbsp;` 4 spaces](https://stackoverflow.com/a/15721400/12371819)

- [Zero-width space: `&#8203;`](https://en.wikipedia.org/wiki/Zero-width_space)

<!--<a class="headerlink" href="#code-inline" title="Permalink to this headline">¶</a>-->


## How to add a picture
	
### The picture from the repository which the site belongs to {#NOTWORKING}

- Just the picture

	```md
![Pic01](/assets/pics/pic01_green_test.png)
	```
![Pic01](/assets/pics/pic01_green_test.png)

- A picture with defined position and size

```html
<div align="center"><img width="165" height="75" src="/assets/pics/pic01_green_test.png"/></div>
```

<div align="center"><img width="165" height="75" src="/assets/pics/pic01_green_test.png"/></div>

### The picture from internet
- Just the picture

	```md
![Pic01](https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/markdown/demo.png)
	```
![Pic01](https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/markdown/demo.png)

- A picture with defined position and size

```html
<div align="center"><img width="65" height="75" alt="Demo pic for test" src="https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/markdown/demo.png"/></div>
```

<div align="center"><img width="65" height="75" alt="Demo pic for test" src="https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/markdown/demo.png"/></div>

### 360° image

Place a `<a-scene>` tag and its scripts supported by [A-Frame](https://aframe.io/).

```html
<script src="https://aframe.io/releases/1.3.0/aframe.min.js"></script>

<a-scene style="aspect-ratio:1/1;width:100%" embedded>
  <a-sky src="/assets/pics/puydesancy.jpg" rotation="0 -130 0"></a-sky>
  <a-text font="kelsonsans" value="Puy de Sancy, France" width="6" position="-2.5 0.25 -1.5"
		  rotation="0 15 0"></a-text>
</a-scene>
```

<script src="https://aframe.io/releases/1.3.0/aframe.min.js"></script>

<a-scene style="aspect-ratio:1/1;width:100%" embedded>
  <a-sky src="/assets/pics/puydesancy.jpg" rotation="0 -130 0"></a-sky>
  <a-text font="kelsonsans" value="Puy de Sancy, France" width="6" position="-2.5 0.25 -1.5"
		  rotation="0 15 0"></a-text>
</a-scene>

Image courtesy: [A-Frame example](https://github.com/aframevr/aframe/tree/v1.0.4/examples/boilerplate/panorama)

## How to compare two pictures

There are ways to create a comparative iframe. For example, [How TO - Image Comparison Slider], [JuxtaposeJS]. Add the following to your post by using [JuxtaposeJS].

```html
<div class="juxtapose">
    <img src="/assets/pics/img_forest.jpg" />
    <img src="/assets/pics/img_snow.jpg" />
</div>
<script src="https://cdn.knightlab.com/libs/juxtapose/latest/js/juxtapose.min.js"></script>
<link rel="stylesheet" href="https://cdn.knightlab.com/libs/juxtapose/latest/css/juxtapose.css">
```

<div class="juxtapose">
    <img src="/assets/pics/img_forest.jpg"/>
    <img src="/assets/pics/img_snow.jpg"/>
</div>
<script src="https://cdn.knightlab.com/libs/juxtapose/latest/js/juxtapose.min.js"></script>
<link rel="stylesheet" href="https://cdn.knightlab.com/libs/juxtapose/latest/css/juxtapose.css">

## How to embed a map

### a own map - geoJSON map
- Place the following in any HTML page that supports javascript:

	```html
<script src="https://embed.github.com/view/geojson/<username>/<repo>/<ref>/<path_to_file>"></script>
	```

- Set height and weight, default 420px (h) x 620px (w)

    ```html
<script src="https://embed.github.com/view/geojson/<username>/<repo>/<ref>/<path_to_file>?width=<width>&height=<height>"></script>
    ```

- Example
	<div align="center">
		<script src="https://embed.github.com/view/geojson/longavailable/georepo/main/geojson/afg.json?width=600&height=600"></script>
	</div>


### a 3rd party map - google map
- [Tutorial to get the embed link of a google map or directions](https://support.google.com/maps/answer/144361?co=GENIE.Platform%3DDesktop&hl=en)
	<div align="center">
		<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d5938.9807235220605!2d12.447683826439667!3d41.903816266880455!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x132f60660c3e3925%3A0x498c3835506c3c!2s00120%20Vatican%20City!5e0!3m2!1sen!2snl!4v1576946140498!5m2!1sen!2snl" width="600" height="450" frameborder="0" style="border:0;" allowfullscreen=""></iframe>
	</div>

## How to assign a variable

Assigning a variable in Github Markdown:
{% assign variableTest = "This is a string variable." %}
{% capture variableTest2 %}This is a string variable for syntax 2.{% endcapture %}

```
{ % assign variableTest = "This is a string variable." % }
{ % capture variableTest2 % }This is a string variable for syntax 2.{ % endcapture % }
```

- Note that, there is no space between curly bracket `{`, `}` and percent sign `%`.

The content of variableTest is " {{variableTest}} ".

The content of variableTest2 is " {{variableTest2}} ".

The&#8203;content test.


# How to add a emoji 🙈

- The easiest way is copy and paste
	
	Visit [Emojipedia](https://emojipedia.org/), search , copy, and paste.
	
- Use [Jemoji](https://github.com/jekyll/jemoji)

	  gem install jemoji
	
	Add `gem 'jemoji'` to gemfile.
	
	Add it as a plugin in `_config.yml`.
	
	Note: It may cause other problem. For my site, it will confict with lunr.js.
	
# Add a reveal.js presentation

```html
<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=500 height=400 src="/slides/2020-08-07-demo-from-revealjs.html#/"></iframe>
```

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=500 height=400 src="/slides/2020-08-07-demo-from-revealjs.html#/"></iframe>

Press **F** to fullscreen mode.



# Reference
- [Basic syntax - Markdown guide](https://www.markdownguide.org/basic-syntax/)
- [markdown-guide](https://markdown-guide.readthedocs.io/en/latest/index.html)
- [MathJax in Markdown](https://hiltmon.com/blog/2017/01/28/mathjax-in-markdown/)
- [Equation Editor](https://www.codecogs.com/latex/eqneditor.php)
- [Host Math](https://www.hostmath.com)
- [Jekyll: Previous And Next Posts](https://www.bytedude.com/jekyll-previous-and-next-posts/)
- [Jekyll without plugins](https://jekyllcodex.org/without-plugins/)
- [Basic syntax - Liquid template language](https://shopify.github.io/liquid/basics/introduction/)
- [Emojipedia](https://emojipedia.org/)
- [How TO - Image Comparison Slider]
- [JuxtaposeJS - Easy-to-make frame comparisons](https://juxtapose.knightlab.com/)
- [List of Badges, in Markdown](https://github.com/Naereen/badges)
- [Basic HTML Codes for Beginners](https://www.websiteplanet.com/blog/html-guide-beginners/)
- [360° image - A-Frame](https://aframe.io/examples/showcase/sky/)
- [Google VRView with Jekyll](https://longqian.me/2017/07/25/vrview-with-jekyll/)


[How TO - Image Comparison Slider]: https://www.w3schools.com/howto/howto_js_image_comparison.asp
[JuxtaposeJS]: https://github.com/NUKnightLab/juxtapose
