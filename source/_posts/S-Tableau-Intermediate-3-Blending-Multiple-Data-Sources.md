---
title: Tableau >> Intermediate (3) Blending Multiple Data Sources
tags:
  - Talbeau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 47607
date: 2022-06-27 13:36:35
---

# Blending Multiple Data Sources

@[toc]

<br />

## **1. Data Blending**

> [[Tableau Help] -- Blend Your Data](https://help.tableau.com/current/pro/desktop/en-gb/multiple_connections.htm) ([中: 混合您的数据](https://help.tableau.com/current/pro/desktop/zh-cn/multiple_connections.htm) / [한: 데이터 혼합](https://help.tableau.com/current/pro/desktop/ko-kr/multiple_connections.htm))

<br />

### \>> Concept

Data blending is a method for combining data from multiple sources. Unlike relationships and joins, blends *never truly combine the data*, they query each data source independentyly and just simply *blend the results* from multiple data sources *in a visulisation*.

In a data blend, one data source is <font color = 'blue'>primary</font> and the other is <font color = 'orange'>secondary</font>. The primary data source is determined by the field you first *add to a view.* Data blending brings in additional information from the secondary data source and displays it with data from the primary data source *directly in the view.*

<br />

#### \>> Advantages

* can handle different levels of detail
* able to work with published data sources
* can be established individually on every sheet

<br />

<br />

## **2. Blending Your Data**

#### \>> Features

* Data blending requires that the data sources **<font color = 'darkblue'>share a common dimension</font>**.
* Data blending **<font color = 'darkblue'>works like a left join</font>**. It returns all results from the primary data source, and returns only the matching results from the secondary data source.
* Data blending is **<font color = 'darkblue'>Tableau worksheet specific</font>**, which means that you can change which data source is primary and which is secondary on different worksheets in the same workbook.

<br />

### \>> Steps for blending data

1. Ensure that the workbook has multiple data source
2. Drag a field to the view. (The data source this first field comes from will become the primary data source)
3. Switch to another data source and make sure there is a blend relationship to the primary data source
   * If there is an orange linking field icon (![image-20210604101207322](/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604101207322.png)), the data sources are automatically linked.
   * If there are grey, broken link icons (![image-20210604101254705](/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604101254705.png)), click the icon next to the field that should link the two data sources.
   * If a link icon does not appear next to the desired field, you need to define blend relationships for blending.
4. Drag a field into the view from the secondary data source

<br />

<br />

## **3. Left Join VS Blending**

### \>> Difference between joins and data blending

The main difference between left join and blending is when the aggregation is performed

* A join combines the data and then aggregates.

* A blend aggregates and then combines the data

<br />

### \>> Left join

When using left join to combine data, a query is sent to the database where the join is performed.

Order: 

1. A left join returns all rows from the left table and any corresponding rows from the right table 

2. then the results of the join are sent back to Tableau and aggregated for display in the visulisation

> [Left join] For each row of the left table, check the right table's rows one by one that whether corresponding information exsists:
>
> * If YES: that data is returned and *combined to the left table*
> * If NO: returns a null 

<br />

**<font color = 'darkblue'>[Example] : common colomns --> User ID & Patron ID</font>**

A  --left join-- B:

<img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604111544374.png" alt="image-20210604111544374" style="zoom:80%;" /> 

<br />

B --left join-- A:

<img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604111637226.png" alt="image-20210604111637226" style="zoom:80%;" /> 

<br />

### \>> Data blending

When using data blending to combine data, a query is sent to the database for each data source that is used on the sheet.

Order:

1. The results of the queries are sent back to Tableau as aggregated data 
2. and then presented together in the visualisation

> [Data blending] For each row of the left table, check the right table's rows one by one that whether corresponding information exsists:
>
> * If YES: that data is returned. However, different from the left join, 
>
>   * if there is only one row match the left table row in the right, it returns that value
>
>   * if there are several rows match the same left table row in the right, it returns an aggregate value
>
>     \- for dimensions:  returns an asterisk(*) that indicates multiple values
>
>     \- for measures:     return the aggregation (default: sum)
>
> * If NO: returns a null 

<br />

**<font color = 'darkblue'>[Example] : common colomns --> User ID & Patron ID</font>**

dimensions aggregation:

<img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604130926578.png" alt="image-20210604130926578" style="zoom:80%;" /> 

<br />

measures aggregation:

<img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604131010154.png" alt="image-20210604131010154" style="zoom:80%;" /> 

<br />

<br />

## **4. Blending Data without a Common Field**

If the data sources have a shared dimension with the same name, Tableau can automatically link them. 

However, if they do have the common member but with different names, we can manually link them in three ways:

1. Create a <font color = 'green'>custom relationship</font>

2. <font color = 'green'>Rename</font> one of them to match the other

3. [If the values are different too (e.g. use full names in one and abbreviations in another)]:

   <font color = 'green'>Edit aliases</font> of the values in a data source to make them match the other data source

<br />

**<font color = 'darkblue'>1. Create a custom relationship:</font>**

* [Data] menu --> [Edit Blend Relationship]

  <img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210607093907267.png" alt="image-20210607093907267" style="zoom:67%;" /> 

  <br />

* In the [Relationship] dialog box: 

  * select the primary and secondary data source

  * choose [Custom]

  * Add mapping fields

    <img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604133553537-16563147514931.png" alt="image-20210604133553537" style="zoom:67%;" />  <img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604133703236.png" alt="image-20210604133703236" style="zoom:67%;" />

    <br />

* The relationship appears, along with the automatic relationship Tableau found on State

  <img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604134148022.png" alt="image-20210604134148022" style="zoom:80%;" /> 

<br />

<br />

**<font color = 'darkblue'>2. Rename the common member:</font>**

* [Data] Pane --> common member field --> right-click --> [Rename]

  <img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604134356472-16563147740013.png" alt="image-20210604134356472" style="zoom:80%;" />    <img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604134428319.png" alt="image-20210604134428319" style="zoom:80%;" />

  <br />

* Tableau will now recognize the link between them

<br />

<br />

**<font color = 'darkblue'>3. Edit aliases:</font>**

* [Data] Menu --> select data source --> [Edit Aliases] --> choose the common member field

​		<img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604135203007-16563147922405.png" alt="image-20210604135203007" style="zoom:67%;" />    <img src="/images/S-Tableau-Intermediate-3-Blending-Multiple-Data-Sources/image-20210604140017281.png" alt="image-20210604140017281" style="zoom: 80%;" />

<br />

<br />
