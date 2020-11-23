---
date: 2020-11-18 21:17:00
layout: post
title: How I made and reshaped a GIF
subtitle:
description: 
image: https://raw.githubusercontent.com/estambolieva/estambolieva.github.io/master/assets/gif/sat_images_1210_720p.gif
category: portfolio
tags:
  - imagegick
  - GIF
  - ubuntu
  - tech
author: estambolieva
---

I needed to create a 6-second GIF overlaying different 🛰️ satellite images on top of another so it will be easier for me to present our work of satellite image analysis. 

So I needed to:
- get screenshots of he slideshow of images for the GIF
- glue them one after another to actually create the GIF
- crop the GIF as the screenshots show the address bar in Mozilla and my Ubuntu menu.


Creating the GIF and executing all of the steps above is super simple in Ubuntu ➡️ by using [ImageGick](https://imagemagick.org/index.php). This is how it goes


### 1. Choose all separate images	


I decided that I wanted to take a look at the burnt area of the 2020 August Complex in California, U.S.A. Here is how the burned area is visualized by Wikipedia, for example:

![2020 August Complex Burnt Area](https://upload.wikimedia.org/wikipedia/commons/thumb/8/85/2020_California_wildfires.png/800px-2020_California_wildfires.png)


**Note**: Find more imformation about all 2020 California fires [here](https://www.fire.ca.gov/incidents/2020/) under the official fire department's page.


I knew the area of the world I wanted to explore satellite images for, and then I visualized it in [Sentinel hub](https://apps.sentinel-hub.com/eo-browser/?zoom=8&lat=40.15247&lng=-124.62891&themeId=DEFAULT-THEME&datasetId=S2L2A&fromTime=2020-09-24T00%3A00%3A00.000Z&toTime=2020-09-24T23%3A59%3A59.999Z&layerId=2_FALSE_COLOR&visualizationUrl=https%3A%2F%2Fservices.sentinel-hub.com%2Fogc%2Fwms%2Fbd86bcc0-f318-402b-a145-015f85b9427e). Sentinel Hub is a platform which allows for the easy discovery and visualization in the browser of satellite images coming from different providers, which makes it very handy to work with.

I chose to view images from Sentinel 2, which are two twin satellites - built by [ESA](https://www.esa.int/), orbiting Earth and taking images of the reflectance of not only the visible light off the surface of the ground, but also of somethings which is invisible to the human eye - such as near-infrared light and short-wave infrared light.

I chose 4 different representations of the same satellite image taken on 24 September 2020, which show me the following:
- the true colour image, e.g. what we can see with the human eyey - titled **August_complex_True_Colour.png**
- the vegetation image, which relies on near-infrared readings to highlight the vegetation on the ground - titled **August_complex_NDVI.png**
- the moisture image, which relies on near-infrared and short-wave infrared readings to highlight the moisture of the soil - titled **August_complex_Moisture.png**
- the image built on top of short-wave infrared readings - titled **August_complex_SWIR.png**

I saved all of these images as screenshots - PNG images with resolution of 1920x108o pixels. 1920 is the width of the image, and 1080 - the height of the image (e.g. the image is 1080 pixels high).



### 2. Glue the images together to create the GIF


### 3. Crop the GIF to custom dimensions




---

### Additional Reading


https://apps.sentinel-hub.com/eo-browser/?zoom=8&lat=40.15247&lng=-124.62891&themeId=DEFAULT-THEME&datasetId=S2L2A&fromTime=2020-09-24T00%3A00%3A00.000Z&toTime=2020-09-24T23%3A59%3A59.999Z&layerId=2_FALSE_COLOR&visualizationUrl=https%3A%2F%2Fservices.sentinel-hub.com%2Fogc%2Fwms%2Fbd86bcc0-f318-402b-a145-015f85b9427e

https://www.fire.ca.gov/incidents/2020/

https://en.wikipedia.org/wiki/2020_California_wildfires#/media/File:2020_California_wildfires.png

https://stackoverflow.com/questions/14036765/how-do-i-crop-an-animated-gif-using-imagemagick

GIF
convert -delay 1500 August_complex_True_Colour.png August_complex_SWIR.png August_complex_NDVI.png August_complex_Moisture.png August_complex_gif.gif

CROP GIF
convert August_complex.gif -coalesce -repage 0x0 -crop 1210x720+642+199 +repage output.gif

