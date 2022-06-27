---
title: Tableau >> Intermediate (6) Using Sets to Highlight Data
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 17048
date: 2022-06-27 13:52:19
---

#  Using Sets to Highlight Data

@[toc]

<br />

## **1. Creating Sets**

### Method 1. From the Dimensions Pane

* [Data] Pane --> Dimension field --> Drop down [Menu] --> [Create] --> [Set]

  ​					<img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607160552672.png" alt="image-20210607160552672" style="zoom:67%;" /> 

  <br />

* [Create Set] dialog box

  1. [General]

     \- Specifically select individual dimension members to include in your set

     ​				<img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607160943419.png" alt="image-20210607160943419" style="zoom:67%;" /> 

     <br />

  2. [Condition]

     \- Create a set on a condition

     ​				<img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607160918594.png" alt="image-20210607160918594" style="zoom: 67%;" /> 

     <br />

  3. [Top]

     \- Select the top / bottom X member on a specific metric

     ​				<img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607161201221.png" alt="image-20210607161201221" style="zoom:67%;" /> 

<br />

<br />

### Method 2. Create sets by selecting the marks in the view

* Select multiple marks by clicking and dragging your mouse

* Hover your mouse over the set until you see a tooptip menu

* Click the sets icon that looks like two conjoined circles  --> Click [Create Set]

  <img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607161742384.png" alt="image-20210607161742384" style="zoom: 50%;" /> <img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607162033804-16563145766931.png" alt="image-20210607162033804" style="zoom: 50%;" />

* [Create Set] dialog box

  ​				<img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607162150178.png" alt="image-20210607162150178" style="zoom:67%;" /> 

<br />

<br />

## **2. Uses for Sets**

* **Viewing in / out sets**

  Dragging the set into the view can identify all the dimension members that are in and out of the set

  <img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607162835832.png" alt="image-20210607162835832" style="zoom:67%;" /> 

  <br />

* **Use sets to compare members in a set to members not in the set**

  \- Show In/Out of Set

  <img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607163345551.png" alt="image-20210607163345551" style="zoom:67%;" /> 

  <br />

  \- Show Members in Set

  <img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607163547344.png" alt="image-20210607163547344" style="zoom:67%;" /> 

  <img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607163615578.png" alt="image-20210607163615578" style="zoom:67%;" /> 

<br />

* **Use as a filter**

  Sets can by used as a reusable filter by dragging the set into the Filters shelf.

  Any set you create can be used across all worksheets in a workbook.

  <br />

<br />

## **3. Combining Sets**

A combined set allows you to compare multiple sets with one another to determine intersections or differences across the sets.

Notice: You can only combine sets that have been created with the same dimensions.

<br />

**Steps for combining sets:**

* Select sets to combine

* right-click --> [Create Combined Set]

  <img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607164233557.png" alt="image-20210607164233557" style="zoom: 80%;" /> 

* Choose the combine style in [Create Set] dialog box

  <img src="/images/S-Tableau-Intermediate-6-Using-Sets-to-Highlight-Data/image-20210607164427597.png" alt="image-20210607164427597" style="zoom:80%;" /> 

<br />

<br />
