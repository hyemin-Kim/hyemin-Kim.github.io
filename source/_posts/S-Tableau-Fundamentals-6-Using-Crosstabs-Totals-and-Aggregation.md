---
title: Tableau >> Fundamentals (6) Using Crosstabs Totals and Aggregation
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 2. Fundamentals
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
abbrlink: 10643
date: 2022-06-16 14:18:29
typora-root-url: ..
---



# Using Crosstabs

@[toc]

<br />

## **1. Creating and Editing Crosstabs**

### \>> Create a Crosstab (Data table)

1. Drag [dimension] to [Columns] / [Rows]

2. Drag [measures] to the [View]

   <img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526140941075-16553658383002.png" alt="image-20210526140941075" style="zoom:50%;" />

   \- Automatically brings in [Measure Names], [Measure Values] and [Measure values shelf ] 

   <br />

### \>> Edit the gridline

1. right-click on a value in the crosstab

2. select [Format]

   ​		<img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526141958945-16553658383003.png" alt="image-20210526141958945" style="zoom:50%;" />

<br />

<br />



## **2. Working with Totals and Aggregation**

### \>> Add totals and subtotals

1. **<font color = 'darkblue'>Form the Analysis Menu:</font>**

   [Menu] - [Analysis] --> 

   [Totals] --> 

   [Show Row Grand Totals] / [Show Column Grand Totals] / [Add All Subtotals]

   <img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526143521096-16553658383004.png" alt="image-20210526143521096" style="zoom: 67%;" />

   

   <img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526143456694-16553658383005.png" alt="image-20210526143456694" style="zoom: 80%;" />

   <br />

2. **<font color = 'darkblue'>From the Analytics Pane</font>**

   <img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526143709607-16553658383006.png" alt="image-20210526143709607" style="zoom:67%;" />

<br />

<br />

### \>> Change the aggregation type of the view

When calculating [Average] for total, be careful with the difference between [weighted average] and [average]

<br />

* For **<font color = 'green'>weighted average</font>**, change the aggregation on the **<font color = 'green'>measure field</font>** 

  ​		<img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526143836193-16553658383007.png" alt="image-20210526143836193" style="zoom:67%;" /> 

<br />

* For **<font color = 'blue'>average</font>** of the values showed **<font color = 'blue'>in the view</font>**, change the aggregation from the **<font color = 'blue'>Analysis Menu</font>**.

  ​		<img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526145935997-16553658383008.png" alt="image-20210526145935997" style="zoom:80%;" /> 

<br />

<br />

## **3. Creating Highlight Tables**

### \>> Why building highlight tables?

Crosstabs is difficult to find outliers or make comparisons across categories.

However, with highlight we can easily emphasize outliers and trends.

<br />

### \>> How to build a highlight table?

* **Method 1: Normal Way (use Marks)** 

  1. A highlight table encodes the measure on Text and Color

     * Drag the [measure] field to [Text] Mark
     * Hold [Ctrl] and drag the [measure] [Text] Mark to the [Color] Mark 

  2. Set the mark type to [Square]

  3. Set the [Columns] dimension and [Rows] dimension

     <img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526170544332-16553658383009.png" alt="image-20210526170544332" style="zoom:67%;" />

  4. Edit colors to highlight outliers

     * If you want to distinguish data that below or above a particular value by color:

       choose a color palette with white in the center first

       then set the particular value as the midpoint ( [Center] ) of the color gradient 

     <img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526170411482-165536583830110.png" alt="image-20210526170411482" style="zoom: 67%;" />

     <img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210527092546019-165536583830111.png" alt="image-20210527092546019" style="zoom: 80%;" />

     <br />

* **Method 2: use [Show Me]**

  1. select the measures and dimensions you're interested in

  2. click the [highlight table] icon in the [Show Me] menu

     ​		<img src="/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210526170921504-165536583830112.png" alt="image-20210526170921504" style="zoom: 67%;" /> 

<br />

<br />

## **4. Creating Heat Maps**

* Create a heat map:

  * Need 1 or more [dimensions], and 1 or 2 [measures] 
  * can create by using [Color] and [Size] marks or use the [Show me]

* Adjust the view:

  * Edit Color: 

    \- For color-blindness, [Orange - (White) - Blue] palette is a good choice

  * Adjust Size:

    \- Two small tick marks on the slider indicate the best range for the mark size

    ![image-20210528085803966](/images/S-Tableau-Fundamentals-6-Using-Crosstabs-Totals-and-Aggregation/image-20210528085803966-165536583830113.png) 

<br />

<br />

