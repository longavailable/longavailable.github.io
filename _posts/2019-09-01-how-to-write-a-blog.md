---
layout: post
title:  First blog
subtitle: how to write a blog
author: Bruce Liu
# last update date
date:   2019-11-23 19:27:00 +0200
# first published date
published: 2019-09-01 00:50:00 +0200 
categories: [Jekyll, markdown]
tags: [first blog]
description: Hello, world!
header-image: 
permalink: /how_to_wirte_a_blog/
---
This is a templete to show how to write a post.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# How to test a blog using bundle:
- Navigate to path of the githubpages repository. 
	```
	cd D:\git\githubPages\longavailable.github.io
	```
- Execute the following command:
	```
	bundle exec jekyll serve
	```
- Check the githubpages website from [http://127.0.0.1:4000](http://127.0.0.1:4000).
- `Ctrl + C ` quit the bundle serve.

<br>
# How to add a picture:

## The picture from the repository which the site belongs to
- Just the picture
![Pic01](/assets/pics/pic01_green_test.png)
- A picture with defined position and size
<div align="center"><img width="165" height="75" src="/assets/pics/pic01_green_test.png"/></div>

## The picture from internet
- Just the picture
![Pic01](https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/markdown/demo.png)
- A picture with defined position and size
<div align="center"><img width="65" height="75" src="https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/markdown/demo.png"/></div>

<br>
# How to embed a map:

## a own map - geoJSON map
- Place the following in any HTML page that supports javascript:
	```
	<script src="https://embed.github.com/view/geojson/<username>/<repo>/<ref>/<path_to_file>"></script>
	```
- Set height and weight, default 420px (h) x 620px (w)
	```
	<script src="https://embed.github.com/view/geojson/<username>/<repo>/<ref>/<path_to_file>?width=<width>&height=<height>"></script>
	```
- Example
	<div align="center">
		<script src="https://embed.github.com/view/geojson/longavailable/Polygon/master/afg.json?width=600&height=600"></script>
	</div>


## a 3rd party map - google map
- [Tutorial to get the embed link of a google map or directions](https://support.google.com/maps/answer/144361?co=GENIE.Platform%3DDesktop&hl=en)
	<div align="center">
		<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d5938.9807235220605!2d12.447683826439667!3d41.903816266880455!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x132f60660c3e3925%3A0x498c3835506c3c!2s00120%20Vatican%20City!5e0!3m2!1sen!2snl!4v1576946140498!5m2!1sen!2snl" width="600" height="450" frameborder="0" style="border:0;" allowfullscreen=""></iframe>
	</div>

# Reference
- [Basic syntax - Markdown guide](https://www.markdownguide.org/basic-syntax/)
- [MathJax in Markdown](https://hiltmon.com/blog/2017/01/28/mathjax-in-markdown/)
- [Equation Editor](https://www.codecogs.com/latex/eqneditor.php)
