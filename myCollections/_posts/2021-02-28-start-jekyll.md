---
layout: post
title:  Set up and run Jekyll
author: Bruce Liu
#last update date
date:   2021-02-28 02:00:00 +0800
#first published date
published: 2021-02-28 02:00:00 +0800
categories: [post]
tags: [Jekyll, rubygems, githubpages]
description: 
header-image: 
permalink: /start-jekyll/
---
Steps to setup jekyll server.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

## install rubygem

```bash
sudo apt install rubygems
```


## install bundler and jekyll

```bash
sudo gem install bundler jekyll
```


## install the gems/dependencies specified in the Gemfile

```bash
bundle install
```


## run a jekyll site server

```bash
bundle exec jekyll serve
```


# 参考/References

- [Transform your plain text into static websites and blogs.](https://jekyllrb.com/)
- [Gem Command not found](https://stackoverflow.com/questions/9485083/gem-command-not-found/20593800#20593800)


