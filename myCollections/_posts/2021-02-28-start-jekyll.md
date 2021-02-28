---
layout: post
title:  Set up and serve Jekyll
author: Bruce Liu
#last update date
date:   2021-02-28 10:40:00 +0800
#first published date
published: 2021-02-28 02:00:00 +0800
categories: [post]
tags: [Jekyll, rubygems, Github Pages]
description: 
header-image: 
permalink: /serve-jekyll/
---
Steps to setup a jekyll server.
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


## References

- [Transform your plain text into static websites and blogs](https://jekyllrb.com/)
- [Gem Command not found](https://stackoverflow.com/questions/9485083/gem-command-not-found/20593800#20593800)
- [Bundler: bundle install](https://bundler.io/man/bundle-install.1.html)


