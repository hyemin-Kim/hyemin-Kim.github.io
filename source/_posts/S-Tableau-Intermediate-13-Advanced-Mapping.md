---
title: Tableau >> Intermediate (13) Advanced Mapping
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 25623
date: 2022-06-27 14:53:35
---

# Advanced Mapping

@[toc]

<br />

## **1. Modifying Locations**

### \>> Edit errors in geocode data

**[Problem] Not all the counties are shown in the map**

* <font color = 'red'>Error: [Ambiguous]</font> : same counties in other states have the same names

* <font color = 'red'>Error: [Unrecognized]</font> : typos (spelling errors)

  <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611142730705.png" alt="image-20210611142730705" style="zoom: 50%;" /> 

<br />

**[Fix the problems]**

* **Fix the ambiguous errors**

  * [Map] menu --> [Edit Locations]

  ​				![image-20210611133106539](/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611133106539.png) 	<img class = "inline-img"  src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611133132793-16563139674001.png" alt="image-20210611133132793" style="zoom:67%;" />

  <br />

  * Fix the state to Washington

  ​								<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611134212289.png" alt="image-20210611134212289" style="zoom:67%;" /> 

  <br />

* **Fix the typos (spelling errors)**

  * [Edit Locations] dialog box

    ​						<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611135850152.png" alt="image-20210611135850152" style="zoom:67%;" /> 

    <br />

  * click the error and type the correct spelling

  ​								<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611134402850.png" alt="image-20210611134402850" style="zoom: 80%;" /> 

<br />

<br />

### \>> Assign locations to data

**[Mission] Add the location of each region's corporate headquarters**

<br />

**[Problem] Values in the field are North, South, East, and West, which Tableau doesn't have a default location for.**

<br />

**[Fix the problem]** -- Add specific locations

* Select the warning box --> Select [Edit Locations] {% inlineImg  /images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611140725873.png %} 

  <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611140725873.png" alt="image-20210611140725873" style="zoom:150%;" /> <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611140820483-16563139806243.png" alt="image-20210611140820483" style="zoom:80%;" />

  <br />

* match the data to specific values (match our regions to specific cities)

  <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611140903967.png" alt="image-20210611140903967" style="zoom: 67%;" />	<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611141123526-16563139852945.png" alt="image-20210611141123526" style="zoom: 67%;" />

  <br />

* Problem fixed

  <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611141330274.png" alt="image-20210611141330274" style="zoom: 67%;" /> 

<br />

<br />

## **2. Customizing Geocodes for Addresses**

When there are geographic fields that Tableau doesn't recognize, you can assign your own Custom Geocodes to map your data.

<br />

**[Mission] Map the various tour sites located around the city**

<br />

**[Problem] Tableau cannot recognize *Street Address* as geographic data** 

​																<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611142902652.png" alt="image-20210611142902652" style="zoom:80%;" />		<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611142927831-16563139932607.png" alt="image-20210611142927831" style="zoom:80%;" />

<br />

**[Fix the problem] Custom geocode addresses by matching a *street address* to a specific *latitude and longitude coordinate***

* Generate the latitude and longitude coordinate with address using a batch geocoding website

* Create an excel spreadsheet (named as "Geocoded addresses") which contains each Tour Site along with its matching latitude and longitude coordinate

  <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611145803655.png" alt="image-20210611145803655" style="zoom:67%;" />

* Add the data source "Geocoded addresses"

* **<font color = 'green'>[First]</font>** Start with the "Geocoded addresses" data source:

  * [Rows] : Latitude

    [Columns] : Longitude

  * [Label] : [Tour Site]

  <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611150700556.png" alt="image-20210611150700556" style="zoom:50%;" />

  <br />

* **<font color = 'green'>[Second]</font>** Switch to the original data source:

  * blend two data sources with the common field [Tour Site]

    <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611151314021.png" alt="image-20210611151314021" style="zoom:80%;" />

  * [Size] : [Number of Records]

  <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611151444104.png" alt="image-20210611151444104" style="zoom:50%;" />

  <br />

* Add streets and highways into the map

  * [Map] menu --> [Map layers]

    ​			<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611152346166.png" alt="image-20210611152346166" style="zoom:80%;" /> 

  * check the [Streets and Highways]

    ​			<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611152429750.png" alt="image-20210611152429750" style="zoom:80%;" /> 

<br />

<br />

## **3. Using a Background Image**

We can use an background image and X/Y coordinates to show locations  on a map

<br />

**[Mission] Create an interactive map that shows the location of meeting rooms and their seating capacity in a company's building**

* Add a background image of an office layout, and 
* Then plot the meeting room data on top of it

<br />

**[Data]**

* Room information and X / Y coordinates for each room
* Contains no X / Y coordinate values (NULL) for the room Woodland

<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611154316516.png" alt="image-20210611154316516" style="zoom: 50%;" />

<br />

**[Process]**

* Add [X] to [Columns]

  Add [Y] to [Rows]

  remove axis

  <br />

* Add the background image

  * [Map] menu --> [Background images] --> Data source name

    <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611155035997.png" alt="image-20210611155035997" style="zoom: 50%;" />

  * Add Image

    \- X Field:  Left -- 0, Right -- 627 (pixels value) 

    \- Y Field:  Right -- 0, Left -- 673 (pixels value)

     <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611155349612-16563141127019.png" alt="image-20210611155349612" style="zoom:40%;" />	<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611155531723.png" alt="image-20210611155531723" style="zoom:40%;" />

  <br />

* Drag [Room Name] to [Detail]

  Drag [Room Capacity] to [Size]

  Set [Tooltip]

  <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611155930497.png" alt="image-20210611155930497" style="zoom: 67%;" />

* Deal with the NULL data

  * Right-click anywhere on the view --> [Annotate] --> [Point]

    ​	<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611160129997.png" alt="image-20210611160129997" style="zoom: 50%;" />	<img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611160210010-165631413185611.png" alt="image-20210611160210010" style="zoom:40%;" />

  * Drag the annotation to the location of Room Woodland

    <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611160451072.png" alt="image-20210611160451072" style="zoom:50%;" />

    <br />

    

  * Update the room information file with Room Woodland's X / Y coordinates

  * Refresh the data source connection in Tableau by pressing F5

    <img src="/images/S-Tableau-Intermediate-13-Advanced-Mapping/image-20210611160920327.png" alt="image-20210611160920327" style="zoom:50%;" />

    <br />

  * Delete the annotation (coordinate tool) by selecting it and pressing the Delete key on the keyboard 

<br />

<br />
