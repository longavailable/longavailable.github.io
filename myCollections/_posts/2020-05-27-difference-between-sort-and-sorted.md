---
layout: post
title:  Difference between list.sort() and sorted() in Python
author: Bruce Liu
# last update date
date:   2020-05-27 12:40:00 +0200
# first published date
published: 2020-05-27 12:40:00 +0200
categories: [post]
tags: [python]
description: 
header-image: 
permalink: /py_sort_sorted/
---
Both `sort()` and `sorted()` can be used to sort a list. So what's the difference?

<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

There are 3 main differences between `list.sort()` and `sorted()`.

# What is it?

- `sort` is a method of [list](https://docs.python.org/3/tutorial/datastructures.html?highlight=lists#more-on-lists).

- `sorted` is a bult-in function.

# Suitable object

- `sort` is only for lists.

- `sorted` can be used for any iterable.

# Returns

- `sort` sorts the original list in-place and returns `None`.

- `sorted` returns a list without modification on the original list.

# Reference
- [Sorting HOW TO](https://docs.python.org/3/howto/sorting.html)
- [list.sort()](https://docs.python.org/3/library/stdtypes.html#list.sort)
- [sorted()](https://docs.python.org/3/library/functions.html#sorted)
- [Why does “return list.sort()” return None, not the list?](https://stackoverflow.com/a/7301126/12371819)
