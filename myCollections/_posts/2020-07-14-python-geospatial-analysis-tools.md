---
layout: post
title:  Ports of python geospatial analysis tools
author: Bruce Liu
#last update date
date:   2021-03-29 08:00:00 +0800
#first published date
published: 2020-07-14 09:50:00 +0200
categories: [post]
tags: [python, gis, gdal, geos, jts, rasterio, shapely]
description: 
header-image: 
permalink: /python_geo_tools/
---

There are lots of python packages for geospatial analysis. This post lists some famous ones.
<!--the above is the excerpt-->
<!--more-->
<!--the following is the text-->

## Ports of python packages

[geopy](https://github.com/geopy/geopy) &nbsp;
[contextily](https://github.com/geopandas/contextily) &nbsp;
[pyproj](https://github.com/pyproj4/pyproj) &nbsp;
[pyepsg](https://github.com/rhattersley/pyepsg) &nbsp;
[GDAL Python API] &nbsp;
[Rasterio] &nbsp;
[Fiona] &nbsp;
[Shapely] &nbsp;
[GeoPandas] &nbsp;
[geoplot] &nbsp;
[Cartopy] &nbsp;
[Folium] &nbsp;

## Ports of galleries

[GeoPandas](https://geopandas.org/gallery/index.html) &nbsp;
[GeoPlot](https://residentmario.github.io/geoplot/gallery/index.html) &nbsp;
[Cartopy](https://scitools.org.uk/cartopy/docs/latest/gallery/index.html) &nbsp;

# Fundamental tools/libraries


![non-python badge](https://img.shields.io/badge/Non--python-blue.svg)

## [GDAL] 

![analysis badge](https://img.shields.io/badge/analysis-blue.svg) 
![raster badge](https://img.shields.io/badge/raster-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)
![C++ badge](https://img.shields.io/badge/C++-blue.svg)

- [Main site](https://gdal.org/)
- [GitHub](https://github.com/OSGeo/gdal)
- [GDAL python api autotest / example ](https://github.com/OSGeo/gdal/tree/master/autotest/utilities)

## [OGR]

![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)
![C++ badge](https://img.shields.io/badge/C++-blue.svg)

***With the GDAL 2.0 release, the GDAL and OGR components were integrated together.***

[GDAL] is equivalent to GDAL / OGR in this context.


## [JTS Topology Suite]

![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)
![java badge](https://img.shields.io/badge/java-blue.svg)

- [GitHub](https://github.com/locationtech/jts) (v1.15 ~ current)
- [SourceForge](https://sourceforge.net/projects/jts-topo-suite/) (previous ~ v1.14)

## [GEOS]

![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)
![C++ badge](https://img.shields.io/badge/C++-blue.svg)

- A C++ port of the [JTS Topology Suite] .
- [GitHub](https://github.com/libgeos/geos)

# Python packages

![Python Wrapper badge](https://img.shields.io/badge/Python%20Wrapper-blue.svg)

## [GDAL Python API]

![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![raster badge](https://img.shields.io/badge/raster-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)

- Dependencies:
	- Non-python denpendencies: [GDAL] including `gdal-bin` and `libgdal-dev`
	- Python denpendencies: [NumPy]
- [GitHub](https://github.com/OSGeo/gdal/tree/master/gdal/swig/python)
- [PyPI](https://pypi.org/project/GDAL/)
- [Python GDAL/OGR Cookbook]

## [Rasterio]

![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![raster badge](https://img.shields.io/badge/raster-blue.svg)

- Dependencies: 
	- Non-python denpendencies: [GDAL]
	- Python denpendencies: [NumPy] and [more](https://rasterio.readthedocs.io/en/latest/installation.html#dependencies).
- [GitHub](https://github.com/mapbox/rasterio)
- [PyPI](https://pypi.org/project/rasterio/)

## [Fiona]

![data importing badge](https://img.shields.io/badge/data%20importing-blue.svg)
![data exporting badge](https://img.shields.io/badge/data%20exporting-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)

- Dependencies: 
	- Non-python denpendencies: [GDAL]
	- Python denpendencies: [six] and [more](https://github.com/Toblerity/Fiona#python-requirements).
- [GitHub](https://github.com/Toblerity/Fiona)
- [PyPI](https://pypi.org/project/fiona/)

## [Shapely]

![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)
[![read and write badge](https://img.shields.io/badge/NO%20file%20read/write-blue.svg)](https://shapely.readthedocs.io/en/latest/project.html?highlight=read#integration)

- Dependencies: 
	- Non-python denpendencies: [GEOS]
	- Python denpendencies: None.
- [GitHub](https://github.com/Toblerity/Shapely)
- [PyPI](https://pypi.org/project/Shapely/)

## [GeoPandas]

![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![visualization badge](https://img.shields.io/badge/visualization-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)

- Dependencies: 
	- Non-python denpendencies (indirectly): [GEOS], [GDAL] and [PROJ].
	- Python denpendencies: [NumPy], [pandas], [Shapely], [Fiona], [pyproj]; optinally, [Matplotlib] and [more](https://geopandas.org/install.html#dependencies).
- [GitHub](https://github.com/geopandas/geopandas)
- [PyPI](https://pypi.org/project/geopandas/)
- [Gallery](https://geopandas.org/gallery/index.html)

## [geoplot]

![visualization badge](https://img.shields.io/badge/visualization-blue.svg)
![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)

- Dependencies:
	- Python denpendencies: [Matplotlib], [seaborn], [pandas], [GeoPandas] and [more](https://github.com/ResidentMario/geoplot/blob/master/setup.py).
- [GitHub](https://github.com/ResidentMario/geoplot)
- [PyPI](https://pypi.org/project/geoplot/)
- [Gallery](https://residentmario.github.io/geoplot/gallery/index.html), [more](https://residentmario.github.io/geoplot/plot_references/plot_reference.html)

## [Cartopy]

![visualization badge](https://img.shields.io/badge/visualization-blue.svg)
![analysis badge](https://img.shields.io/badge/analysis-blue.svg)

- Dependencies:
	- Non-python denpendencies: [GEOS] and [PROJ]; optinally, [GDAL]
	- Python denpendencies: [NumPy], [Cython], [Shapely], [pyshp], and [six]; optinally, [Matplotlib] and [more](https://scitools.org.uk/cartopy/docs/latest/installing.html#optional-dependencies).
- [GitHub](https://github.com/SciTools/cartopy)
- [PyPI](https://pypi.org/project/Cartopy/)
- [Gallery](https://scitools.org.uk/cartopy/docs/latest/gallery/index.html)

## [Folium]

![pure-python map badge](https://img.shields.io/badge/pure%20Python-blue.svg)
![interactive map badge](https://img.shields.io/badge/interactive%20map-blue.svg)
![visualization badge](https://img.shields.io/badge/visualization-blue.svg)
![raster badge](https://img.shields.io/badge/raster-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)

- Python implementation of [Leaflet.js]
- [GitHub](https://github.com/python-visualization/folium)
- [PyPI](https://pypi.org/project/folium/)

## [ArcPy]

![Non-standalone badge](https://img.shields.io/badge/non--standalone-blue.svg)
![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![raster badge](https://img.shields.io/badge/raster-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)

Python module of ArcGIS. ***Need an ArcGIS license.***

## [QGIS Python API]

![Non-standalone badge](https://img.shields.io/badge/non--standalone-blue.svg)
![analysis badge](https://img.shields.io/badge/analysis-blue.svg)
![raster badge](https://img.shields.io/badge/raster-blue.svg)
![vector badge](https://img.shields.io/badge/vector-blue.svg)

Python module of QGIS.

# Reference
- [Data Analysis in Python]
- [GIS in Python]



[GDAL]: https://gdal.org/
[GDAL Python API]: https://gdal.org/python/index.html
[Python GDAL/OGR Cookbook]: https://pcjericks.github.io/py-gdalogr-cookbook/
[Rasterio]: https://rasterio.readthedocs.io/en/latest/
[Cartopy]: https://scitools.org.uk/cartopy/docs/latest/
[GEOS]: https://trac.osgeo.org/geos/
[PROJ]: https://proj.org/
[NumPy]: https://numpy.org/
[Cython]: https://cython.org/
[Shapely]: https://shapely.readthedocs.io/en/latest/
[pyshp]: https://github.com/GeospatialPython/pyshp
[six]: https://github.com/benjaminp/six
[Matplotlib]: https://matplotlib.org/
[JTS Topology Suite]: https://locationtech.github.io/jts/
[OGR]: https://gdal.org/faq.html#what-is-this-ogr-stuff
[Fiona]: https://fiona.readthedocs.io/en/latest/
[Folium]: https://python-visualization.github.io/folium/
[ArcPy]: https://pro.arcgis.com/en/pro-app/arcpy/
[QGIS Python API]: https://qgis.org/pyqgis/
[Leaflet.js]: https://leafletjs.com/
[GeoPandas]: https://geopandas.org/
[pandas]: https://pandas.pydata.org/
[pyproj]: http://pyproj4.github.io/pyproj/stable/
[Data Analysis in Python]: http://www.data-analysis-in-python.org/
[GIS in Python]: http://www.data-analysis-in-python.org/t_gis.html
[geoplot]: https://residentmario.github.io/geoplot/index.html
[seaborn]: https://seaborn.pydata.org/

