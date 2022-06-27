---
title: Tableau >> Intermediate (14) Viewing Distribution
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 26142
date: 2022-06-27 14:58:30
---

# Viewing Distribution

@[toc]

<br />

## **1. Building Histograms**

### \>> Methods to create histograms

**[Method 1] : Use *Show Me***

* Select [Measure] field  --> click [Show Me]  --> click the histogram thumbnail

​			<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614090214293.png" alt="image-20210614090214293" style="zoom: 67%;" />	<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614090252568-16563138518251.png" alt="image-20210614090252568" style="zoom:67%;" />

<br />

* Edit bins : Right-click [Age (bin)] --> [Edit]

  ​	<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614094434541.png" alt="image-20210614094434541" style="zoom:67%;" /><img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614094518358-16563138585103.png" alt="image-20210614094518358" style="zoom:67%;" />  

<br />

**[Method 2] : In the *Data* pane**

* Right-click [Measure] field  --> select [Create]  --> select [Bins]  --> edit bins --> click [OK]

  ​	<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614090452204-16563138656405.png" alt="image-20210614090452204" style="zoom:80%;" />	<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614091832293.png" alt="image-20210614091832293" style="zoom:67%;" />

  * **<font color = 'darkblue'>Size of bins</font>**: Default value  -- Tableau suggested size

  * **<font color = 'darkblue'>Bin range:</font>** 

    \-  [a, b)       a<= x < b

    \-  For a bin size of 5, on data starting at 0:  

    ​	[0, 4] -- [5, 9] -- [10, 14] ...    /  [0, 5) -- [5, 10) -- [10, 15) ...

    <br />

* Binning a measure creates a dimension : [Age (bin)]

  ![image-20210614093247671](/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614093247671.png)

* Build the view:

  * Drag <font color = 'viridans'>[Age]</font> to [Rows]

  * Drag <font color = 'blue'>[Age (bin)]</font> to [Columns]

  * Change the aggregation of <font color = 'viridans'>[Age]</font> from Sum to Count

    Change <font color = 'blue'>[Age (bin)]</font> into continuous field <font color = 'viridans'>[Age (bin)]</font>

  <img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614094121764.png" alt="image-20210614094121764" style="zoom: 50%;" />

  <br />

* Fix the tick marks to the bin size

  * Right-click the x-axis  --> click [Edit Axis]

  * [Tick Marks] Tab  --> [Major tick marks]  --> [Fixed]  --> [Every] : (*size of bins*) 

    ![image-20210614095218159](/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614095218159.png)	<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614095105087-16563138867437.png" alt="image-20210614095105087" style="zoom:80%;" />

<br />

<br />

## **2. Building Box and Whisker Plots**

### \>> Box Plot

<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/scode=mtistory2&fname=https%253A%252F%252Ft1.daumcdn.png" alt="boxplot" style="zoom:67%;" />

* IQR:                 Q3 - Q1

  Upper fence: Q3 + 1.5 * IQR

  Lower fence:  Q1 - 1.5 * IQR

* The bottom and top whiskers are not always the same length:

  the whiskers will show the last *data point* that is within the 1.5*IQR

<br />

### \>> Methods to create box plot

**[Method 1] In the *Data* pane**

* [Columns] : [Dimension] field

  [Rows]       : [Measure] field

  [Details]    : [Dimension] field  

  <img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614102522465.png" alt="image-20210614102522465" style="zoom: 67%;" />

  <br />

* [Analytics] Pane  --> Drag [Box Plot] to the view  --> [Cell]

  ​			<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614102707088.png" alt="image-20210614102707088" style="zoom:80%;" />	<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614102805162-16563138976839.png" alt="image-20210614102805162" style="zoom:67%;" />

  <br />

* Edit the box plot

  ​			<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614102853313.png" alt="image-20210614102853313" style="zoom:67%;" />	<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614102924358-165631390273611.png" alt="image-20210614102924358"  />

<br />

**[Method 2] : Use *Show Me***

* Hold [Ctrl] and select [Dimension] field and [Measure] field
* [Show Me]  --> click the box and whisker icon

<img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614103215928.png" alt="image-20210614103215928" style="zoom: 67%;" />

* Using the Marks card to adjust the formatting

  * Mark Type : Circle
  * Size & Color

  <img src="/images/S-Tableau-Intermediate-14-Viewing-Distribution/image-20210614103542826.png" alt="image-20210614103542826" style="zoom:67%;" />

<br />

<br />
