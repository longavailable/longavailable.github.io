---
layout: post
title:  Quick Conversion on GIS Metrics
author: Bruce Liu
# last update date
date:   2021-12-24 15:00:00 +0800
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

The formula for arc length of a circle:

$$
arc length=2\pi r\left ( \frac{\theta }{360} \right )=p\left ( \frac{\theta }{360} \right )
$$

If the equatorial plane is looked as a circle, then the arc length on the equator is calculated by:

$$
arc length=P\left ( \frac{longitude}{360} \right )=40075* \left ( \frac{longitude}{360} \right )=111*longitude
$$

Note taht the radius (R) and perimeter (P) of the earth at the equator is 6378 km, 40075km separately.

And the arc length on a specific parallel/latitude is calculated by:

$$
\begin{eqnarray}arc length & = & 2\pi R\cos(latitude)\left ( \frac{longitude}{360} \right ) 
\\ & = & P\left ( \frac{longitude}{360} \right )\cos(latitude) 
\\ & = & 40075* \left ( \frac{longitude}{360} \right )\cos(latitude)
\\ & = & 111*longitude \cos(latitude) \end{eqnarray}
$$

| longitude                   					| arc length  | quick check (latitude)   |||
| ^^                     						| ^^  		  |  25°		| 36° 	      | 44° 	    |
| --------------------------------------------- |:-----------:|:-----------:|:-----------:|:-----------:|
| 1 arc degree                                  | 111.32 km   | 100 km      | 90 km       | 80 km       |
| 0.5 arc degree (30 arc minutes)               | 55.66 km    | 50 km       | 45 km       | 40 km       |
| 0.25 arc degree (15 arc minutes)              | 27.83 km    | 25 km 		| 23 km       | 20 km       |
| 0.1 arc degree (6 arc minutes)                | 11.13 km    | 10 km       | 9 km        | 8 km        |
| 0.05 arc degree (3 arc minutes)               | 5.566 km	  |	5 km		| 4.5 km	  | 4 km	    |
| $$0.01\dot{6}$$ arc degree (1 arc minutes) 	| 1.855 km	  | 1.7 km      | 1.5 km      | 1.3 km      |
| 0.01 arc degree (36 arc seconds)              | 1.113 km	  |	1 km		| 900 m		  | 800 m		|
| $$0.008\dot{3}$$ arc degree (30 arc seconds)  | 928 m		  |	850 m		| 750 m	      | 670 m	    |
| $$0.001\dot{6}$$ arc degree (6 arc seconds) 	| 186 m		  | 170 m       | 150 m       | 130 m       |
| 0.001 arc degree (3.6 arc seconds)            | 111 m 	  | 100 m       | 90 m        | 80 m        |
| $$0.0002\dot{7}$$ arc degree (1 arc seconds) 	| 31 m	      | 30 km       | 25 km       | 22 km       |

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
- [Syntax for entering math using ASCIIMathML](https://www.intmath.com/help/send-math-email-syntax.php)
- [Arc Length Calculator - online ](https://www.omnicalculator.com/math/arc-length)
- [Earth radius - Wikipedia](https://en.wikipedia.org/wiki/Earth_radius)