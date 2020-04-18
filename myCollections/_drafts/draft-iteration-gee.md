---
layout: post
title:  Iteration in Google Earth Engine
author: Bruce Liu
#last update date
#date:   2020-04-18 20:07:00 +0200
#first published date
#published: 2020-04-18 20:07:00 +0200
categories: [post]
tags: [python, google earth engine, gee]
description: 
header-image: 
permalink: /gee_iterate/
---
This is a templete to show how to write a post.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

# 

First, create/define a function for iterative algorithm.

Note: it must be a two-argument function: an element of the collection and the value from the previous iteration.

```py
def featureIterating(element, eeFeature0):
	'''
	element: an element from an ee.List or an ee.Feature from an ee.FeatureCollection. Actually, it can any type of object.
		Type: ee.Geometry(), ee.Feature(), ee.FeatureCollection, or others
	'''
	
	# do somthing here. Get a new object 'object_new', it should be an object which can be casted to an ee.Feature.
	
	return ee.Feature(eeFeature0).union(ee.Feature(object_new))
```

Then, invoke it:

- iterate over an ee.FeatureCollection

	```py
eeFeatColl = ee.FeatureCollection('<your assetId>')
eeFeature0 = ee.Feature(None)	# initialize a Null ee.Feature object, or set one existing
contiguous = eeFeatColl.iterate(featureIterating, eeFeature0)
	```

- iterate over an ee.List

	```py
eeList = ee.List('<an ee.List object, and anything can be casted to an ee.List>')
eeFeature0 = ee.Feature(None)	# initialize a Null ee.Feature object, or set one existing
contiguous = eeList.iterate(featureIterating, eeFeature0)
	```






# Reference
- [Basic syntax - Markdown guide](https://www.markdownguide.org/basic-syntax/)
- [markdown-guide](https://markdown-guide.readthedocs.io/en/latest/index.html)
- [MathJax in Markdown](https://hiltmon.com/blog/2017/01/28/mathjax-in-markdown/)
- [Equation Editor](https://www.codecogs.com/latex/eqneditor.php)
- [Jekyll: Previous And Next Posts](https://www.bytedude.com/jekyll-previous-and-next-posts/)
- [Jekyll without plugins](https://jekyllcodex.org/without-plugins/)
- [Basic syntax - Liquid template language](https://shopify.github.io/liquid/basics/introduction/)
- [Emojipedia](https://emojipedia.org/)
