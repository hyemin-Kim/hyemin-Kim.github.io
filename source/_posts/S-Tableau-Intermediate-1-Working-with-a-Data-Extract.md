---
title: Tableau >> Intermediate (1) Working with a Data Extract
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 9545
date: 2022-06-27 13:23:13
---

# Working with a Data Extract

@[toc]

<br />

## **1. Extract Data**

### \>> Concept

An extract is a copy of the data that brought into the Tableau data engine.

<br />

### \>> Advantages

1.  Use the Tableau data engine to run queries rather than send a query to the data source
    * **<font color = 'green'>Reduce the time</font>** it takes for queries to run
2.  Allow you to keep a copy of the data:
    * **<font color = 'green'>Can be accessed offline</font>**
3.  May include only a **<font color = 'green'>subset of the data</font>**

<br />

### \>> Limitations

1. Data doesn't update automatically
   * Need to refresh the Extract
   * *A Live connection queries the data from the database and the data are updated every time you open your workbook*
2. Your extracted data source may not include all the fields required for the views
   * Because extracts may include only a subset of the data

<br />

<br />

## **2. Create and edit Extracts**

### \>> Two places to create extracts

* **<font color = 'darkblue'>From the Data Source page</font>**

  <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602152449487.png" alt="image-20210602152449487" style="zoom:67%;" />

  <br /> 

* **<font color = 'darkblue'>On the worksheet</font>**

  \- [Data] Pane --> right-click the data source --> [Use Extract] 

  \- Switch between a live or extracted data connection: check / uncheck [Use Extract]

  <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602152258117.png" alt="image-20210602152258117" style="zoom:50%;" /> 

  ​									<img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602152950020.png" alt="image-20210602152950020" style="zoom: 50%;" /> 

<br />

### \>> Two places to edit Extracts

* **<font color = 'darkblue'>From the data source page</font>**

  <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602161938019.png" alt="image-20210602161938019" style="zoom:80%;" />

  <br /> 

* **<font color = 'darkblue'>On the worksheet</font>**

  \- [Data] Pane --> right-click the data source --> [Extract Data] 

  <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602154111980.png" alt="image-20210602154111980" style="zoom:67%;" /> 

  <br />

  **<font color = 'darkblue'>[Edit extracts from the Extract Data dialog box]</font>**

  <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602152648443.png" alt="image-20210602152648443" style="zoom:67%;" /> 

<br />

### \>> Update Data

* [Data] Pane --> right-click the data source --> [Extract] --> [Refresh]

  <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602162736858.png" alt="image-20210602162736858" style="zoom: 67%;" /> 

  <br />

### \>> Hide / Unhide fields

* **<font color = 'darkblue'>Hide unused fields</font>**

  <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602164034539.png" alt="image-20210602164034539" style="zoom:67%;" /> 

  <br />

* **<font color = 'darkblue'>Unhide fields</font>**

  * [Data] Pane --> right-click --> [Show Hidden Fields]

    <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602164326135.png" alt="image-20210602164326135" style="zoom:67%;" /> 		<img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602164355176-16563148778111.png" alt="image-20210602164355176" style="zoom:67%;" />

  * Field to show --> right-click --> check [Unhide]

    <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602164533673.png" alt="image-20210602164533673" style="zoom:67%;" /> 

<br />

<br />


## **3. Refresh Extracts**

> [[Tableau Help] -- Refresh Extracts](https://help.tableau.com/current/pro/desktop/en-us/extracting_refresh.htm)  ([中： 刷新数据提取](https://help.tableau.com/current/pro/desktop/zh-cn/extracting_refresh.htm) / [한: 추출 새로 고침](https://help.tableau.com/current/pro/desktop/ko-kr/extracting_refresh.htm))

### \>> Two Types:

* **<font color = 'darkblue'>Full extract refresh</font>** (default) [完全刷新]
  * all of the rows are replaced with the data in the original data source
  * [good] ensures that you have an exact copy of what is in the original data
  * [bad]   can sometimes take a long time and be expensive on the database
* **<font color = 'darkblue'>Incremental extract refresh</font>** [增量刷新]
  *  configure a refresh to add only the rows that are new since the previous time you extracted the data
  *  **Note:** If the data structure of the source data changes (for example, a new column is added), you will need to do a full extract refresh before you can start doing incremental refreshes again.

<br />

### \>> Full Refresh (Default)

* [Data] Pane --> right-click the data source --> [Extract] --> [Refresh]

  <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602162736858.png" alt="image-20210602162736858" style="zoom: 67%;" /> 

<br />

### \>> Update the data extract

Overwrite the existing extract by creating a new extract after the data extract edit (e.g. unhide fields)

* [Data] Pane --> right-click --> [Extract Data]

* [Number of Rows] --> check [All rows] --> check [Incremental refresh]

* Click [Extract]

  <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602165123365-16563149058183.png" alt="image-20210602165123365" style="zoom:60%;" />		<img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210602165055997-16563149236555.png" alt="image-20210602165055997" style="zoom:60%;" /> <img src="/images/S-Tableau-Intermediate-1-Working-with-a-Data-Extract/image-20210603164635661.png" alt="image-20210603164635661" style="zoom: 67%;" />

<br />

<br />
