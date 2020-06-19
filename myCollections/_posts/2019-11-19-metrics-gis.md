---
layout: post
title:  Quick Conversion on GIS Metrics
author: Bruce Liu
# last update date
date:   2020-06-19 22:30:00 +0200
# first published date
published: 2019-11-19 13:00:00 +0100 
categories: [post]
tags: [GIS, metrics conversion]
header-image: 
permalink: /metrics_gis/
# Enable the mathjax in post
mathjax: true
---
How to quick convert some GIS metrics?
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

Basic parameter for the planet:<br>
- `r` or Radius: 6371 km
- `p` or Perimeter: 40,075 km

And the formula for arc length:

$$
arc length=2\pi r\left ( \frac{\theta }{360} \right )=p\left ( \frac{\theta }{360} \right )
$$

| $$\theta$$(central angle)                     | arc length  | quick check |
| --------------------------------------------- |:-----------:|:-----------:|
| 1 arc degree                                  | 111.1 km    | 100 km      |
| 0.5 arc degree (30 arc minutest)              | 55.7 km     | 50 km       |
| 0.25 arc degree (15 arc minutest)             | 27.8 km     | 25 km 		|
| 0.1 arc degree (6 arc minutes)                | 11.1 km     | 10 km       |
| 0.05 arc degree (3 arc minutes)               | 5.6 km	  |	5 km		|
| 0.01 arc degree (36 arc seconds)              | 1.1 km	  |	1 km		|
| $$0.008\dot{3}$$ arc degree (30 arc seconds)  | 928 m		  |	900 m		|
| $$0.001\dot{6}$$ arc degree (6 arc seconds) 	| 186 m		  | 200 m       |
| 0.001 arc degree (3.6 arc seconds)            | 111 m 	  | 100 m       |

>坐地日行八万里。By毛泽东

The arc length i.e. perimeter of the Earth is about 40,000 km, which equals 80,000 Li (Chinese mile). Our planet rotates per day. According to elative motion, a people stays at the surface will have a 360 arc degrees motion. In some way, the people moves 40,000 km per day. Roughly, 1 arc degree equals 100 km at the surface of earth.  

<div class="omni-calculator" data-calculator="math/arc-length" data-width="300" data-config='{}' data-currency="EUR" data-show-row-controls="false" data-version="3" data-t="1592598747186">
  <div class="omni-calculator-header">Arc Length Calculator</div>
  <div class="omni-calculator-footer">
    <a href="https://www.omnicalculator.com/math/arc-length" target="_blank"><img alt="Omni" class="omni-calculator-logo" src="https://cdn.omnicalculator.com/embed/omni-calculator-logo-long.svg" /></a>
  </div>
</div>
<script async src="https://cdn.omnicalculator.com/sdk.js"></script>

Reference:
- [Jekyll Supports Math Notation](https://www.katarinahoeger.com/2017/12/08/jekyll-supports-math)
- [MathJax in Markdown](https://hiltmon.com/blog/2017/01/28/mathjax-in-markdown/)
- [Equation Editor](https://www.codecogs.com/latex/eqneditor.php)
- [Arc Length Calculator - online ](https://www.omnicalculator.com/math/arc-length)