---
title: Tableau >> Intermediate (16) Using Advanced Filter Actions
date: 2022-06-27 15:10:39
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
---

# Using Advanced Filter Actions

@[toc]

<br />

## **1. Filter Data Across Different Data Sources** 

**[Mission] Filter data by regions**

* Create space for the region filter: 

  * Drag [Horizontal] to the dashboard view

    <br />

* Create a view that can act as the filter

  * Open a new worksheet, named as "Region Selection"

  * Drag [Region] to [Columns] & [Text]

  * Hide the header of the Region

    <img src="/images/S-Tableau-Intermediate-16-Using-Advanced-Filter-Actions/image-20210614155749738.png" alt="image-20210614155749738" style="zoom: 50%;" />

    <br /> 

* Put this worksheet (Region filter) in the empty space we created on the dashboard

  <img src="/images/S-Tableau-Intermediate-16-Using-Advanced-Filter-Actions/image-20210614160119054.png" alt="image-20210614160119054" style="zoom:67%;" /> 

  <br />

* Use this view as a filter

  <img src="/images/S-Tableau-Intermediate-16-Using-Advanced-Filter-Actions/image-20210614160217191.png" alt="image-20210614160217191" style="zoom:80%;" /> 

  * Now, only superstore data are filtered when making a selection on the custom filter, but not the coffee chain data.

    <br />

* Using a filter action to set the target worksheets

  * [Dashboard] menu  --> [Actions]  --> [Add Action] -- [Filter]

    <img src="/images/S-Tableau-Intermediate-16-Using-Advanced-Filter-Actions/image-20210614160854722.png" alt="image-20210614160854722" style="zoom:67%;" /> 

  * Edit the filter action:

    \- Set the source sheet and target sheets

    \- Run action on: [Select]

      <img src="/images/S-Tableau-Intermediate-16-Using-Advanced-Filter-Actions/image-20210720174528043.png" alt="image-20210720174528043" style="zoom: 50%;" /> 

      <img src="/images/S-Tableau-Intermediate-16-Using-Advanced-Filter-Actions/image-20210720174605575.png" alt="image-20210720174605575" style="zoom:50%;" /> 

    \- Target Filters: help you filter on specific fields (mapping the common field with different names)

    * [Selected Fields]  --> [Add Filter]

      <img src="/images/S-Tableau-Intermediate-16-Using-Advanced-Filter-Actions/image-20210720174723959-165631039174110.png" alt="image-20210720174723959" style="zoom:50%;" />   <img src="/images/S-Tableau-Intermediate-16-Using-Advanced-Filter-Actions/image-20210614161509780.png" alt="image-20210614161509780" style="zoom: 67%;" /> 

      <br />

<br />

## **2. Create a Link for Navigating to a different dashboard**

* Create a view that can act as the link, named as "Navigate"

* Create a calculated field "Navigate" :

  `"Click here to view the Profit by Location dashboard."`

* Add this calculation to the view  -->

  Change the mark type to a [Shape]  -->

  Make the shape an [arrow]   -->

  Make the cell size bigger: [Format] menu  /  Ctrl + Shift + B  -->

  Hide field label

* Add the navigation link to the Profit Analysis dashboard

* Create a filter action

  * [Dashboard]  --> [Actions]  --> [Add Action]  --> [Filter]

  * Edit the filter action

    <br />

  <img src="/images/S-Tableau-Intermediate-16-Using-Advanced-Filter-Actions/image-20210614162941336.png" alt="image-20210614162941336" style="zoom:67%;" />

<br />

<br />
