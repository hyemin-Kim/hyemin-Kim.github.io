---
title: Tableau >> Start - (1) Basics of Reading Data
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 1. Start
Description: 'Basic data concept, Data structure, Common chart types'
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 28713
date: 2021-06-28 09:00:03
---

# Basics of Reading Data

@[toc]

<br />

## **1. Understanding Basic Data Concepts**

### 1-1. Data Sources

**\>> Common types of data sets**

* **Spreadsheets:**
  * e.g.: Excel, Google Sheets
  * the records are stored as single rows of data
* **Relational Databases:**
  * store data in multiple tables
  * "relational": logical connection between tables
  * users pull data from different tables using SQL
* **Cloud Data:**
  * e.g.: AWS, Microsoft Azure, Salesforce
* **Other Types:**
  * .kml, .shp, created in R

<br />

### 1-2. Data Field

\>> A field = A column

\>> Data Field automatically assigned a ***Role*** and a  ***Type***

* **Role**: "*Dimension*" or "*Measure*"
  * <font color = 'blue'>*Dimension*</font>: qualitative fields / (categorical data)   * blue in tableau
  * <font color = 'green'>*Measure*</font>: quantitative fields / (numerical data)      * green in tableau
* **Type**: String, Integer, Date, Date&Time, Boolean, Geographic, Mixed or cluster

<br />

<br />

## **2. Understanding Data Structure Details**

### 2-1. Granularity and Aggregation in Tableau

**\>> Data granularity(数据粒度):** the level of detail for a piece of data

* Less granular: describe as an *aggregation* / *aggregated data*

<br />

**\>> move dimensions & measures in /out of a view --> level of details changes**

* **Dimensions:** break down aggregated total by category
* **Measures:** aggregated as SUM (default), or average, median...

<br />

**\>> "SUM(Profit)/SUM(Sales)"  VS  "Profit/Sales"**

<font color = 'red'>Caution the trap of granularity</font> when aggregating

* "SUM(Profit) / SUM(Sales)"   [correct]
  1. first <font color = 'blue'>sums</font> the profits and sales <font color = 'blue'>to</font> whatever <font color = 'blue'>the granularity of the view is</font>
  2. <font color = 'blue'>then computes</font> the ratio at <font color = 'blue'>that</font> aggregation
* "Profit / Sales"  [incorrect]
  1. first <font color = 'blue'>compute</font> the profit ratio <font color = 'blue'>at the lowest level of granularity</font>
  2. <font color = 'blue'>then sum</font> the ratio <font color = 'blue'>to the requested aggregation</font> of the view

<br />

### 2-2. How data is represented in Tableau

#### 1. Dimensions & Measures

* Measures: aggregations

  \- aggregated up to the granularity set by the dimensions in the view

* Dimensions: categorical fields

  \- set the granularity, or the level of detail

<br />

#### 2. Discrete & Continuous

|                           |                           Discrete                           |                          Continuous                          |
| :-----------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|         **Value**         |                have distinct, separate values                |                 take on any value in a range                 |
|         **Color**         |               <font color = 'blue'>Blue</font>               |            <font color = 'viridans'>Green</font>             |
| **Label <br>vs<br> Axis** | Label<br><br><img src="/images/S-Tableau-Start-1/image-20210517161223334.png" alt="image-20210517161223334" style="zoom:50%;" /><br><br>*<font color = 'gray'>Market(discrete)</font>* | Axis<br/><br/><img src="/images/S-Tableau-Start-1/image-20210517160710233.png" alt="image-20210517160710233" style="zoom:50%;" /><br> <br>*<font color = 'gray'>profit (continuous)</font>* |
|         **Color**         | Color Palette<br/><br/><img src="/images/S-Tableau-Start-1/image-20210517161958731.png" alt="image-20210517161958731" style="zoom:25%;" /><br/><br/>*<font color = 'gray'>SUM(Sales - discrete)</font>* | Color Gradient<br/><br/><img src="/images/S-Tableau-Start-1/image-20210517162028994.png" alt="image-20210517162028994" style="zoom:25%;" /><br/> <br/>*<font color = 'gray'>SUM(Sales - continuous)</font>* |
| **Color <br>& <br>Maps**  | A **Dimension** on color -- **"Symbol Map"**<br><br><img src="/images/S-Tableau-Start-1/image-20210517162753289.png" alt="image-20210517162753289" style="zoom:67%;" /><br>A **Measure** on color -- **"Filled Map"**<br><br><img src="/images/S-Tableau-Start-1/image-20210517162915695.png" alt="image-20210517162915695" style="zoom: 67%;" /><br> | A **Dimension** on color -- **"Symbol Map"**<br/><br/><img src="/images/S-Tableau-Start-1/image-20210517163002064.png" alt="image-20210517163002064" style="zoom:67%;" /><br/>A **Measure** on color -- **"Filled Map"**<br/><br/><img src="/images/S-Tableau-Start-1/image-20210517163033554.png" alt="image-20210517163033554" style="zoom:67%;" /><br> |
|         **Dates**         | <img src="/images/S-Tableau-Start-1/image-20210517163347483.png" alt="image-20210517163347483" style="zoom: 50%;" /> | <img src="/images/S-Tableau-Start-1/image-20210517163408062.png" alt="image-20210517163408062" style="zoom:50%;" /> |
|       **Filtering**       | List<br><br><img src="/images/S-Tableau-Start-1/image-20210517163617518.png" alt="image-20210517163617518" style="zoom: 67%;" /> | Range<br/><br/><img src="/images/S-Tableau-Start-1/image-20210517163720510.png" alt="image-20210517163720510" style="zoom:67%;" /> |

<br />

<br />

## **3. Reading Common Chart Types**

### 3-1. Overview to reading charts

**\>> Elements of Charts**

* Quantitative Axis / Qualitative Axis
* Marks (View화면에서 Data를 표현하는 도구)
* Labels (축에 표시되는 값)
* Filter (Side bar)
* Legend (Side bar)
* Tooltip (show details about the data when clicking a mark)

<br />

**>> Appropriate Purpose**

* Bar Charts: Comparing categories of data

* Line Charts: Viewing data over time

* Scatter Plots: Viewing data relationships and outliers


<br />

<br />
