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

1. [Rasterio](https://rasterio.readthedocs.io/en/latest/) - useful for plotting
2. [Fiona](https://fiona.readthedocs.io/en/latest/) - useful for coordinate system discovery
3. [Shapefile](https://pypi.org/project/pyshp/) - useful for loading satellite image data

Honorable mentions:

1. [Geopandas](https://geopandas.org/) - builds upon [pandas](http://pandas.pydata.org/), [shapely](https://shapely.readthedocs.io/), [descartes](https://pypi.python.org/pypi/descartes) and [matplotlib](http://matplotlib.org/) - very useful for data manipulation similar to pandas & coordinate system manipulaton.
2. [GDAL](https://gdal.org/)


Now let's showcase what they can do in an example scenario.

Imagine that we have downloaded 1 *tif* (tif stands for [geotiff](https://gdal.org/drivers/raster/gtiff.html)) image which contains the NVDI indices calculated based on a particular satellite image. [NDVI](https://en.wikipedia.org/wiki/Normalized_difference_vegetation_index) stands for Normalized Difference Vegetation Index and it is the go-to vegetation index for developers and geospatial specialists when inspecting the state of vegetation on Earth. The index is calculated by using the values of the *red* and *near-infra red* radiation captured by the satellite image. 

A Typical NDVI image looks something like this:

____________ image
![NDVI original](https://raw.githubusercontent.com/estambolieva/estambolieva.github.io/master/assets/img/uploads/satellite_images/Monchique_NDVI.png)


The darker the green colour is, the denser the vegetation is. NVDI takes values between 0 and 1. A commonly used rule of thumb says that when the NVDI value is smaller than 0.2 - what we see on the image is bare soil or soil with a some grass. When the values are smaller than 0.4, we usually look at bushes, and when the values are greather than 0.5 - we see a forest (-.8 for a very dense forest). 


#### Find out what the coordinate system of the image is

When a *tif* image is opened in Python, one of the first things we want to know is what the coordinate system of the satellite image is. Fiona comes in handy in here:

```python
import fiona
import shapefile as shp

path_to_image = 'path/image.tif'

c = fiona.open(path_to_image)
original_crs = c.crs['init']
print(original_crs)

>> 'epsg:3763'
```


#### Convert an image to a different coordinate system

`epsg:3763` is one of the coordinate systems available. A Standard coordinate system is WSG84 (WSG stands for (World Geodetic System](https://en.wikipedia.org/wiki/World_Geodetic_System)) and 84 is its laest revision. The `espg` code for WSG84 is `espg:4326`. We can see that the example image I chose to load is based on a different coordinate system so it is good to convert it to WSG84.  used geopandas to do this:

```python
import geopandas as gpd

gpd_shape = gpd.read_file(path_to_image)
gpd_shape.crs = original_crs['init'] # we set the CRS we have identified when we loaded the image using fiona
gpd_shape = gpd_shape.to_crs("EPSG:4326")
```

#### Export the image to GeoJSON format

```python
path_to_image_geojson= 'path/image.geojson'

gpd_shape.to_file(path_to_image_geojson, driver='GeoJSON')
```

#### Find the Bouding Box of shapes

_____ separate this blog post into 2 - 1 for shapes, and 2 for satellite images, and 3- putting it all together

``` python
bbox = shape.bbox

>> [-47903.63338843786, -265251.9380933815, -31310.261804120528, -257247.52285356744]
```

#### Write Bounding Box to a file

```python
upper_left = [bbox[0], bbox[1]]
upper_right = [bbox[0], bbox[3]]
lower_left = [bbox[2], bbox[1]]
lower_right = [bbox[2], bbox[3]]

# write bbox to a shape file (just to visualize in Google Earth)
w = shp.Writer(path_to_aglomerados_bbox)
# assign POLYGON (5) as shapeType
w.shapeType = shp.POLYGON
# add a "name" field of type "Character"
w.field('BBOX', 'C')
w.poly([[upper_left,  # upper left
        upper_right,   # upper right
        lower_right,   # lower right
        lower_left,   # lower left
        upper_left]]) # first point again
w.record('Shape_Bbox')
w.close()
```

![NDVI before and after polygons' overlay](https://raw.githubusercontent.com/estambolieva/estambolieva.github.io/master/assets/img/uploads/satellite_images/Monchique1.gif)


FYI - I used this Linux terminal command to create the *GIF* of two *PNG* images I had generated:

```sh
convert -delay 60 -loop 0 img1.png img2.png result.gif
```


#### Interesting Reads

1. [Calculate and Classify Normalized Difference Results with EarthPy](https://earthpy.readthedocs.io/en/latest/gallery_vignettes/plot_calculate_classify_ndvi.html)

2. [Handling the error *TypeError: unhashable type: 'MultiPolygon'*](https://leblancfg.com/unhashable-python-unique-locations-geometry-geodataframe.html)

3. [Expanding MultiPolygons to Polygons in GeoPandas](https://stackoverflow.com/questions/46240895/expanding-multipolygon-in-geopanda-dataframe)