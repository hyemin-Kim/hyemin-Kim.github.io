---
title: Tableau >> Advanced (2) Time-Based Data
date: 2022-06-27 15:26:47
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 4. Advanced
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
---

# Time-Based Data

@[toc]

<br />

## **1. Using Sparklines to Show Trends Over Time**

Sparkline charts are small line charts that displayed without axes and headers. 

Sparkline charts present high level comparisons of data over a period of time. Also, they fit in a small area and are mostly used to show trends in a simple, condensed way.

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705085649245.png" alt="image-20210705085649245" style="zoom: 67%;" />

<br />

<br />

### \>> Create a sparklines chart

**<font color = 'navy'><< Goal >></font>**

We want to analyze sales by country over time. We'll create a chart with sparklines to view the general trend for each country at a glance.

<br />

**<font color='navy'><< Process >></font>**

**[STEP 1] Create a line chart**

Build a view that displays Sales by Country against discrete month of Order Date and let the chart fit height.

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705091450773.png" alt="image-20210705091450773" style="zoom:45%;" />

<br />

**[STEP 2] Use an independent axis range for sales**

By default, the rows display the same range. To make the individual lines more distinct, we can set the Sales axis to display as independent ranges per row. 

* Right-click the Sales axis --> [Edit Axis]
* [Range] --> select [Independent axis ranges for each row or column]

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705092253903-165631147574938.png" alt="image-20210705092253903" style="zoom:40%;" /><img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705092450515.png" alt="image-20210705092450515" style="zoom:45%;" />

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705092722627.png" alt="image-20210705092722627" style="zoom:50%;" />

<br />

**[STEP 3] Highlight the last data point for each country**

* Create a calculated field that calculates the last sales mark of 2016

  * This calculation finds the last row in each pane, 

    \- If the value is not null, then returns SUM(Sales)

    \- If the value is null, then returns 0

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705093756770.png" alt="image-20210705093756770" style="zoom:50%;" />

* Create a synchronized dual axis chart with "Last Sales" and "SUM(Sales)"

* Hide the nulls from the view and change the circle marks color

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705101158559.png" alt="image-20210705101158559" style="zoom:45%;" />

<br />

**[STEP 4] Hide the axes and set default number to standard currency** 

* Hide the date and sales headers

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705101440095.png" alt="image-20210705101440095" style="zoom:50%;" />

<br />

* Set default number to standard currency

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705102202194.png" alt="image-20210705102202194" style="zoom:45%;" />

<br />

**[STEP 5] Add the sparklines sheet to the dashboard**

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705102751579.png" alt="image-20210705102751579" style="zoom:50%;" />

<br />

<br />

## **2. Using a Slope Chart to Tell a Before and After Story**

When you have time-based data that is shown by rank, an interesting way to summarize change over time is by using a slope chart. 

Slope charts show changes in rank or position for a dimension using a start point and an end point. You can use a slope chart when you want to show whether a particular dimension has increased or decreased between two points in time. 

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705112102150.png" alt="image-20210705112102150" style="zoom:50%;" />

<br />

### \>> Create a slope chart

**<font color = 'navy'><< Goal >></font>**

We want to know the rank of the top 10 names and see if these names have decreased or increased in popularity.

<br />

**<font color='navy'><< Process >></font>**

**[STEP 1] Remain data of the two time points to compare**

* **Columns:** Discrete [Birth Year]  	**Rows:**        SUM(Count)
* Filter the Birth Year to 2011 and 2013, and widen rows in the view (Ctrl + '->' arrow)

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705135923667.png" alt="image-20210705135923667" style="zoom:50%;" />

<br />

**[STEP 2] Rank the names of two years by count**

* Label the marks with Name
* Add a Rank quick table calculation, and compute using Name

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705140429955.png" alt="image-20210705140429955" style="zoom:50%;" />

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705140509304.png" alt="image-20210705140509304" style="zoom:50%;" />

<br />

**[STEP 3] Show only the top 10 names**

* Ctrl + drag [SUM(Count)] rank calculation in Rows to Filters pane
* set the range from 1 to 10

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705141345386.png" alt="image-20210705141345386" style="zoom:50%;" />

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705141404426.png" alt="image-20210705141404426" style="zoom:50%;" />

<br />

* Reverse the rank of Count axis, and show line ends

  * Right-click the Count axis --> Edit Axis --> Scale: [Reversed]

    <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705141803003.png" alt="image-20210705141803003" style="zoom:50%;" /> 

  <br />

  * On Marks card, click [Label] --> Marks to Label: Line Ends

    <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705141936224.png" alt="image-20210705141936224" style="zoom:50%;" /> 

    <br />

  * Edit the labels to display rank before name, and align the view to top left

    <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705144048930.png" alt="image-20210705144048930" style="zoom:50%;" /> 

    <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705144154646.png" alt="image-20210705144154646" style="zoom:50%;" /> 

<br />

**[STEP 4] Hide the Rank of Count axis and the row grid lines in the view**

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705144418294.png" alt="image-20210705144418294" style="zoom:50%;" />

<br />

<br />

## **3. Monitoring Quality Control with a Control Chart**

Control charts are used to study how a process changes over time. It is a statistical process control tool to determine if a manufacturing or business process is either inside or outside a predefined boundary.

Control charts are based on the line charts. By adding a mean line and an upper and lower control limits, which are typically based on the standard deviation, the simple line chart is transformed into a control chart. The control limits allow you to easily identify when the process is in or out of control.

<br />

### \>> Create a control chart

**<font color = 'navy'><< Goal >></font>**

When analyzing company's sales over the past few years, we want to know whether there are seasonal effects on sales: Are sales lower or higher than a predicted range during certain months?

<br />

**<font color='navy'><< Process >></font>**

**[STEP 1] Create the base line chart that showing sales over the order date**

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705163543273.png" alt="image-20210705163543273" style="zoom:50%;" />

<br />

**[STEP 2] Add a reference line for average sales by pane**

* [Analytics] Pane --> Drag [Reference Line] to the view --> Drop it on [Pane]

* Set the mean reference line:

  * Value: SUM(Sales) set to Average
  * Label: None
  * Line: Gray dashed line 

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705164442375-165631151607540.png" alt="image-20210705164442375" style="zoom:40%;" /><img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705163910350.png" alt="image-20210705163910350" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705170924058.png" alt="image-20210705170924058" style="zoom:50%;" /> 

<br />

**[STEP 3] Add the upper and lower control limits line by pane**

* Calculate the upper and lower control limits using a window standard deviation:

  ​	Upper control limit: `WINDOW_AVG(SUM([Sales])) + WINDOW_STDEV(SUM([Sales]))`

  ​	Lower control limit: `WINDOW_AVG(SUM([Sales])) - WINDOW_STDEV(SUM([Sales]))`

  <br />

* Add the control limits band to the view

  * Add the Upper and Lower Control Limit fields to Detail

  * Add a reference band using the control limits as boundaries

    \- [Analytics] Pane --> Drag [Reference Line] to the view --> Drop it on [Pane] 

    \- Set the reference band:

    	* Band From Value: Lower Control Limit set to Minimum
    	* Band To Value: Upper Control Limit set to Maximum
    	* Label: None on both
    	* Line: Red dashed line
    	* Fill: Light gray

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705170616393-165631155928542.png" alt="image-20210705170616393" style="zoom:40%;" /><img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705165723714.png" alt="image-20210705165723714" style="zoom:55%;" />

<img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705171326710.png" alt="image-20210705171326710" style="zoom:50%;" />

<br />

* Set the Upper and Lower Control Limit fields to Compute Using: Pane (across)

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705171458678.png" alt="image-20210705171458678" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705171546539.png" alt="image-20210705171546539" style="zoom:50%;" />

<br />

**[STEP 4] Highlight the points out of the control boundaries**

* Create a synchronized dual axis using another instance of Sales on Rows, and hide the right axis

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705171914939.png" alt="image-20210705171914939" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705172002211.png" alt="image-20210705172002211" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705172030100.png" alt="image-20210705172030100" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705172152903.png" alt="image-20210705172152903" style="zoom:50%;" />

  <br />

* Remove the [Lower Control Limit] and [Upper Control Limit] fields under the [SUM(Sales) (2)] Marks card, and change the mark type to Circle

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705172515621.png" alt="image-20210705172515621" style="zoom:50%;" />

<br />

* Create a calculated field named "KPI" to highlight marks outside of the control boundaries, and rename the color legend to "KPI"

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705172832868.png" alt="image-20210705172832868" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-2-Time-Based-Data/image-20210705172914273.png" alt="image-20210705172914273" style="zoom:50%;" />

<br />

<br />
