---
layout: post
title:  A simple way to map landuse
author: Bruce Liu
# last update date
date:   2020-02-25 11:08:00 +0100
# first published date
published: 2020-02-25 11:08:00 +0100
categories: [ArcGIS]
tags: [ArcGIS, GIS]
header-image: 
permalink: /simple_landuse/
---
Here is a simple way to create a landuse map.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->
## Step1: download landcover classification data

There are lots of good quality landcover products, likes [GlobeLand30](http://www.globallandcover.com/).

## Step2: extract the area you are interested in

ArcToolBox -> Spactial Analyst Tools -> Extraction -> Extract by Mask

<div align="center"><img width="300" src="/assets/pics/simplelanduse01.png"/></div>

## Step3: reclassify to reach the landuse

ArcToolBox -> Spactial Analyst Tools -> Reclass -> Reclassify

<div align="center"><img width="300" src="/assets/pics/simplelanduse02.png"/></div>

## Step4: summarize area of same type

For a relative small area, the grid will be regarded as same cell size. In other words, every grid has same cell area. Then the sum of each type is the cell area multiplied by the count.

Select the target layer -> Open Attribute Table -> Add Field -> Set Name and Type as needed -> Right-click at the new field -> Field Calculator -> Tyep [Count] * 300 * 300 (300 is the cell side length)

<div align="center"><img width="570" src="/assets/pics/simplelanduse03.png"/></div>

<br>
**Note the coordinate system. In my opinion, it's better to set as a local projected coordinate system.**
