---
layout: post
title:  First blog
subtitle: how to write a blog
author: Bruce Liu
# last update date
date:   2019-11-23 19:27:00 +0200
# first published date
published: 2019-09-01 00:50:00 +0200 
categories: [blog, manual]
tags: [test, blog, first blog]
description: Hello, world!
header-image: 
permalink: /how_to_wirte_a_blog/
---
This is a templete to show how to write a post.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

This is a templete to show how to write a post.

How to test a blog using bundle:
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


How to add a picture:

The picture from the repository which the site belongs to:
# Just the picture
![Pic01](/assets/pics/pic01_green_test.png)
# A picture with defined position and size
<div align="center"><img width="165" height="75" src="/assets/pics/pic01_green_test.png"/></div>

The picture from internet:
# Just the picture
![Pic01](https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/markdown/demo.png)
# A picture with defined position and size
<div align="center"><img width="65" height="75" src="https://raw.githubusercontent.com/mzlogin/mzlogin.github.io/master/images/posts/markdown/demo.png"/></div>



