---
layout: post
title:  Differences between dissolve and union in geoproceesing
author: Bruce Liu
#last update date
date:   2020-07-21 00:35:00 +0200
#first published date
published: 2020-07-20 01:20:00 +0200
categories: [post]
tags: [gis, gee, ArcGIS, GeoPandas]
description: 
header-image: 
permalink: /dissolve_and_union/
---

When geometris intersect, how to union them? And if they aren't intersected, how would these tools work?
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

Commonly used geographic vector objects include three levels: [featureCollection], [feature], and [geometry]. `dissolve` and `union` will be compared in the context of [geometry].

# dissolve

Aggregates some geometris into one geometry.

- It works on **one** object, eg [feature] or geometryCollection. The latter is a list of geometris and it may be one of multipolygon, multilines, and points.
- If two geometris touch, they will be unioned as one geometry.
- If two geometris untouch, they will be gathered to one multi-object geometry. Considering the sole input, nothing will change for a geometryCollection.
- Due to only one geometry for each feature, it is used to dissolve a multigemotry feature or geometryCollection coverted from multi features.
- A similar operation in ArcGIS, `Edit` -> Select the features to merge -> `merge`. It may produce a unioned feature or a multigeometry feature.
- `unary-union` in shapely have the same function.

# union

Computes a geometric union of the input geometris.

- It works on at leat **two** objects.
- If two input geometris touch, they will be unioned as one geometry.
- If two input geometris untouch, they will be gathered to one multi-object geometry. Two untoched geomtry objects has merged to one multigeometry object.
- A similar operation in ArcGIS, `Edit` -> Select the features to merge -> `merge`. It may produce a unioned feature or a multigeometry feature.
- Note that `union` of `analysis` tool box in ArcGIS won't create a unioned geometry for thoese touched each other. It will put all in one and split them by bounds.
- `union` in shapely have the same function.

>At end, we can say, `dissolve` or `unary-union` combines the sub-objects for a given geometryCollection object. `union` works for two independent objects. The outputs of them are very similar.

# buffer

## Google Earth Engine

- If two geometris touched, they will be unioned as one geometry after `ee.Geometry.buffer` operation.

## [GeoPandas]

- The number of geometris returen by `GeoSeries.buffer()` remains the same as input object.

# Reference
- [Union (analysis) in ArcGIS](https://pro.arcgis.com/en/pro-app/tool-reference/analysis/union.htm)
- [Dissolve (Data Management) in ArcGIS](https://desktop.arcgis.com/en/arcmap/latest/tools/data-management-toolbox/dissolve.htm)
- [Aggregation with dissolve - GeoPandas](https://geopandas.org/aggregation_with_dissolve.html)
- [Merging features in the same layer - ArcGIS](https://desktop.arcgis.com/en/arcmap/latest/manage-data/creating-new-features/merging-features-in-the-same-layer.htm)
- [union - shapely](https://shapely.readthedocs.io/en/latest/manual.html#object.union)
- [unary-union - shapely](https://shapely.readthedocs.io/en/latest/manual.html#shapely.ops.unary_union)
- [GeoSeries.buffer()](https://geopandas.org/geometric_manipulations.html?highlight=buffer#GeoSeries.buffer)

[FeatureCollection]: https://developers.arcgis.com/web-map-specification/objects/featureCollection/
[feature]: https://developers.arcgis.com/web-map-specification/objects/feature/
[geometry]: https://developers.arcgis.com/web-map-specification/objects/geometry/
[GeoPandas]: https://geopandas.org/
