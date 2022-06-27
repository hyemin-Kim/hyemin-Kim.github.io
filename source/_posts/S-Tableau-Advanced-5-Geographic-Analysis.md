---
title: Tableau >> Advanced (5) Geographic Analysis
date: 2022-06-27 15:41:21
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 4. Advanced
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
---

# Geographic Analysis

@[toc]

<br />

## **1. Map Dense Data with Hexbins**

When we want to see a distribution with just one measure, we use bins to create a histogram. However, if we want to show the density of values across two measures, hexbins (also called as density plots) would be a good choice. 

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706160651101.png" alt="image-20210706160651101" style="zoom: 60%;" />

**“hexbins”** = **"hexagons"** + **"bins"**

* **"bins"** : Much like the bins we create for histograms, hexbins create buckets in the view, which help us to understand the distribution of data.
* **"hexagons"** : Tessellate -- they can cover the view without overlapping or gaps

<br />

To create hexbins, 

* we use two Tableau built-in calculations:  HEXBINX(x, y)  &  HEXBINY(x, y) 
  * HEXBINX assigns values to a bin on the x-axis
  * HEXBINY assigns values to the bin for the y-axis

* and use them both as **continuous dimensions**:
  * Continuous: let tableau to present an axis, rather than headers
  * Dimensions: let them to behave categorically, rather than aggregate to a sum of HEXBINX, or sum of HEXBINY

<br />

### \>> Create a hexbin map

**<font color = 'navy'><< Goal >></font>**

With the data from downtown New York City, we want to see taxi activity by time of day and location. 

Create a hexbin map that shows density of taxicab pickups, and filter by the time of day.

<br />

**<font color = 'navy'><< Process >></font>**

**[STEP 1] Build the basic map**

* Columns: Pickuplon (set to dimension)
* Rows:        Pickuplat (set to dimension)

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706161847081.png" alt="image-20210706161847081" style="zoom:50%;" />

<br />

**[STEP 2] Filter the view by Pickup TimeRanges, and change the mark type to Shape**

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706162123838.png" alt="image-20210706162123838" style="zoom:50%;" />

<br />

**[STEP 3] Create a Scale Factor parameter**

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706171924852.png" alt="image-20210706171924852" style="zoom:60%;" />

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706162658024.png" alt="image-20210706162658024" style="zoom:50%;" />

<br />

<br />

**[STEP 4] Create HexbinX and HexbinY calculations and set their geographic roles**

* Create HexbinX and HexbinY calculations that scale based on the Scale Factor parameter
  * <font color='blue'>HexbinX:</font> `HEXBINX([Pickuplon]*[Scale Factor], [Pickuplat]*[Scale Factor]) / [Scale Factor]`
  * <font color='blue'>HexbinY:</font> `HEXBINY([Pickuplon]*[Scale Factor], [Pickuplat]*[Scale Factor]) / [Scale Factor]` 

<br />

* Set the geographic roles of the HexbinX and HexbinY calculations

  * Drag both the HexbinX and HexbinY fields from Measures to <font color='blue'>Dimensions</font>
  * Set the geographic Role for <font color='blue'>HexbinX to Longitude</font>, and <font color='blue'>HexbinY to Latitude</font>

  <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706164933649.png" alt="image-20210706164933649" style="zoom:50%;" />

<br />

<br />

**[STEP 5] Update the view with HexbinX and HexbinY, colored by Number of Records**

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706172918043.png" alt="image-20210706172918043" style="zoom:50%;" />

<br />

<br />

**[STEP 6] Edit the color and shape of the marks**

* **Color:** 

  * Choose a [Blue] color palette
  * Select [Stepped Color], with 5 steps
  * Click [Advanced]  --> adjust the range of the scale: 1 ~ 500
  * transparency: 80%

  <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707093550434.png" alt="image-20210707093550434" style="zoom:50%;" /> 



<br />

* **Shape:** Add the hexagon custom shape, and apply the hexagon to the marks in the view

  * Create a new folder called "Hex" in the [My Tableau Repository] --> [Shapes] folder

    \- Windows: `Documents\My Tableau Repository\Shapes\Hex`

    \- Mac: `Documents/My Tableau Repository/Shapes/Hex`

    <br />

  * Download or copy the 'hex_solid.png' to the Hex folder 

    <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706170740697.png" alt="image-20210706170740697" style="zoom:50%;" /> 

    <br />

  * [Marks] card  --> click [Shape]  --> click [More Shapes]

  * Click [Reload Shapes]  --> click [Apply]

    <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707094442673.png" alt="image-20210707094442673" style="zoom:50%;" /> 

    <br />

  * [Select Shape Palette]  --> select [Hex]

  * Click the solid hexagon image  -> click [Apply]  -> click [OK] 

    <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706171455051-165631225173024.png" alt="image-20210706171455051" style="zoom:60%;" />	 <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210706171536059.png" alt="image-20210706171536059" style="zoom:60%;" />

    <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707094543671.png" alt="image-20210707094543671" style="zoom:50%;" /> 

 <br />

**[STEP 7] Adjust the formatting of the view, using the parameter and mark size**

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707094739294.png" alt="image-20210707094739294" style="zoom:50%;" />

<br />

**[STEP 8] Update the map layers to show highways**

* [Map] --> [Map Layers]

* check [Streets and Highways] 

  <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707094924608.png" alt="image-20210707094924608" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707094956056.png" alt="image-20210707094956056" style="zoom:50%;" />

<br />

<br />



## **2. Map Shapes Using Spatial Files**

If geography influences our data questions or business, or location is a vital part of our analysis, we may need to work with spatial files to create maps. 

A spatial file contains geographic data that identifies types of natural and man-made features on Earth, and encodes geographic features as geometrical shapes, which we use to visualize and analyze geographic data. 

* Three types of geographic features we can use spatial files to map 
  * *Discrete locations on the ground*:        wells, mountain peaks, building entrances, or railway stops
  * *Geographic features or designations*:  lakes, farms, park boundaries, neighborhoods, or school districts
  * *Linear features*:                                      rivers, roads, trails, or highways

* Types of geometrical shapes that Tableau Desktop supports:
  * *Points, Circles*:  for distinct locations on the ground
  * *Polygons*:          for geographic features or designations
  * *Lines*:                for linear features

<br />

**[Examples]**

* **Locations:**

  Show railway stops to explore the frequency of usage at each stop. 

  <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707105154024.png" alt="image-20210707105154024" style="zoom: 67%;" />

  <br />

* **Areas:**

  Show a country's population broken down by government designations such as prefecture and municipality.

  <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707105635118.png" alt="image-20210707105635118" style="zoom:67%;" />

  <br />

* **Linear features:**

  Explore the relationship between a highway network and the median income of local residents near it.

  <img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707105827515.png" alt="image-20210707105827515" style="zoom:67%;" />

<br />

<br />

### \>> Use spatial files to map data

**<font color = 'navy'><< Goal >></font>**

For a study on railway usage in areas of the United Kingdom, we would like to use a spatial file to create a map that shows a network of stations as well as the number of entries and exits, per station, for specific years.

<br />

**<font color = 'navy'><< Process >></font>**

**[STEP 1] Connect to the spatial file**

* [Connect] Pane  --> [Spatial file] 

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707125304915.png" alt="image-20210707125304915" style="zoom:50%;" />

\* When connecting to the spatial data, a Geometry field is created to represent the point, polygon, or linear geometries. 

<br />

**[STEP 2] In the worksheet, drag the Geometry field to Detail**

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707125652711.png" alt="image-20210707125652711" style="zoom:50%;" />

\* It works in conjunction with latitude and longitude to create the map

\* Tableau Desktop aggregates the Geometry measure using the COLLECT aggregation.

​	\- By default, the geometry measure is aggregated into a single mark when added to the view

​	\- We can add dimensions to disaggregate the data 

<br />

**[STEP 3] Add and Edit the Color, Detail, and Size Marks**

* Add Network Route on Color, Station name on Detail, and 2015-2016 Entries & Exits on Size

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707132149895.png" alt="image-20210707132149895" style="zoom:50%;" />

<br />

* Increase the mark size, decrease the mark-color opacity, and give marks a gray border.

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210707132756910.png" alt="image-20210707132756910" style="zoom:50%;" />

<br />

**[STEP 4] Use map layers to edit the background**

* Change the background style to [Normal]
* Add the coastline, county borders, and county names

<img src="/images/S-Tableau-Advanced-5-Geographic-Analysis/image-20210708092758858-165631228248326.png" alt="image-20210708092758858" style="zoom:50%;" />

<br />

<br />
