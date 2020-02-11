---
layout: post
title:  General concepts of matplotlib
author: Bruce Liu
# last update date
date:   2020-02-11 11:20:00 +0100
# first published date
published: 2020-02-11 11:20:00 +0100
categories: [python, matplotlib]
tags: [python, matplotlib]
header-image: 
permalink: /matplotlib_concepts/
---
What is figure, axes and axis in matplotlib? Check the introduction of general concepts firstly.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

## Some concepts of a figure
<div align="center"><img width="600" height="600" alt="Anatomy of a figure" src="https://matplotlib.org/_images/anatomy.png"/></div>

## Figure VS axes

### [Figure](https://matplotlib.org/tutorials/introductory/usage.html#figure)
The <b>whole</b> figure. The figure keeps track of all the child [Axes](#AXES), a smattering of 'special' [artists](#ARTIST) (titles, figure legends, etc), and the [canvas](#CANVAS). A figure can have any number of Axes, but to be useful should have at least one.<br>
`A figure is everything in a final plot.`

### [Axes](https://matplotlib.org/tutorials/introductory/usage.html#axes) {#AXES}
This is what you think of as 'a plot', it is the region of the image with the data space. A given figure can contain many Axes, but a given Axes object can only be in one Figure. The Axes contains two (or three in the case of 3D) [Axis](#AXIS) objects (be aware of the difference between Axes and Axis) which take care of the data limits (the data limits can also be controlled via set via the `set_xlim()` and `set_ylim()` Axes methods). Each Axes has a title (set via `set_title()`), an x-label (set via `set_xlabel()`), and a y-label set via `set_ylabel()`).<br>
`A axes concludes two (or three) axis, a x-label, a y-label, a title and the space surrounded by them.`

## Axes VS axis

### [Axes](#AXES)

### [Axis](https://matplotlib.org/tutorials/introductory/usage.html#axis) {#AXIS}
These are the number-line-like objects. They take care of setting the graph limits and generating the ticks (the marks on the axis) and ticklabels (strings labeling the ticks). The location of the ticks is determined by a Locator object and the ticklabel strings are formatted by a Formatter. The combination of the correct Locator and Formatter gives very fine control over the tick locations and labels.<br>
[Spines](https://matplotlib.org/api/spines_api.html#module-matplotlib.spines)<br>
`A axis concludes spines, ticks and ticklabels.`

<br>
# Reference:
- [Matplotlib - User's Guide - Tutorials - Usage Guide](https://matplotlib.org/tutorials/introductory/usage.html#usage-guide)


