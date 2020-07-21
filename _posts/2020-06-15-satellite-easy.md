---
date: 2020-06-15 15:34:00
layout: post
title: Satellite Images - easy to work with
subtitle:
description: 
image: https://images.unsplash.com/photo-1497436072909-60f360e1d4b1?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1489&q=80
category: programming
tags:
  - goal
  - 30 years
author: estambolieva
---

I have been in the business of analysing satellite images for over 2 years now. I and my collaborators code primarily in Python for our back-end. There are several Python libraries which make our lives much easier to manupulate geographical data. 

Here is the list of these libraries:

1. [Rasterio](https://rasterio.readthedocs.io/en/latest/)
2. [Fiona](https://fiona.readthedocs.io/en/latest/)

Honorable mentions:

1. [Geopandas](https://geopandas.org/) - builds upon [pandas](http://pandas.pydata.org/), [shapely](https://shapely.readthedocs.io/), [descartes](https://pypi.python.org/pypi/descartes) and [matplotlib](http://matplotlib.org/).
2. [GDAL](https://gdal.org/)


Now let's showcase what they can do in an example scenario.

Imagine that we have downloaded 1 *tif* (tif stands for [geotiff](https://gdal.org/drivers/raster/gtiff.html)) image which contains the NVDI indices calculated based on a particular satellite image. [NDVI](https://en.wikipedia.org/wiki/Normalized_difference_vegetation_index) stands for Normalized Difference Vegetation Index and it is the go-to vegetation index for developers and geospatial specialists when inspecting the state of vegetation on Earth. The index is calculated by using the values of the *red* and *near-infra red* radiation captured by the satellite image. 

A Typical NDVI image looks something like this:

![NDVI original](https://raw.githubusercontent.com/estambolieva/estambolieva.github.io/master/assets/img/uploads/satellite_images/Monchique_NDVI.png)


![NDVI before and after polygons' overlay](https://raw.githubusercontent.com/estambolieva/estambolieva.github.io/master/assets/img/uploads/satellite_images/Monchique1.gif)


FYI - I used this Linux terminal command to create the *GIF* of two *PNG* images I had generated:

```sh
convert -delay 60 -loop 0 img1.png img2.png result.gif
```

#### Interesting Reads

[Calculate and Classify Normalized Difference Results with EarthPy](https://earthpy.readthedocs.io/en/latest/gallery_vignettes/plot_calculate_classify_ndvi.html)

[Handling the error *TypeError: unhashable type: 'MultiPolygon'*](https://leblancfg.com/unhashable-python-unique-locations-geometry-geodataframe.html)

[Expanding MultiPolygons to Polygons in GeoPandas](https://stackoverflow.com/questions/46240895/expanding-multipolygon-in-geopanda-dataframe)