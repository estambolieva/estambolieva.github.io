---
date: 2020-05-24 21:17:00
layout: post
title: How I made and reshaped a GIF
subtitle:
description: 
image: https://raw.githubusercontent.com/estambolieva/estambolieva.github.io/master/assets/img/uploads/I_speaking/Katia_New_Space.png
category: portfolio
tags:
  - machine learning
  - speaking
  - space tech
  - programming
  - business
author: estambolieva
---

I needed to create a 6-second GIF overlaying different satellite images on top of another so it will be easier for me to present our work of satellite image analysis. 

So I needed to:
- get screenshots of he slideshow of images for the GIF
- glue them one after another to actually create the GIF
- crop the GIF as the screenshots show the address bar in Mozilla and my Ubuntu menu.


Creating the GIF and executing all of the steps above is super simple in Ubuntu ➡️ by using [ImageGick](https://imagemagick.org/index.php). This is how it goes


### 1. Choose all separate images	


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

