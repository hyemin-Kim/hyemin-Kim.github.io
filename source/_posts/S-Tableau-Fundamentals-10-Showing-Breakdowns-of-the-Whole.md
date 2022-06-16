---
title: Tableau >> Fundamentals (10) Showing Breakdowns of the Whole
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 2. Fundamentals
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
abbrlink: 36035
date: 2022-06-16 14:35:43
typora-root-url: ..
---

# Showing the Breakdowns of the Whole (Pie Chart & Tree Map)

@[toc]

<br />

## **1. Pie Chart**

### \>> Create a pie chart

**Method 1:** Use Marks

* Mark : Pie Chart
* [Color] : dimension field   [best: within 5 dimension members]
* [Angle] : measure field

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531095837772-16553669238901.png" alt="image-20210531095837772" style="zoom:50%;" />

<br />

**Method 2:** Use [Show Me]

* Choose [dimension field] and [measure field]
* click [Show Me] --> [Pie Chart]

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531100157662-16553669238912.png" alt="image-20210531100157662" style="zoom:45%;" />

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531100358442-16553669238913.png" alt="image-20210531100358442" style="zoom:50%;" />

<br />

<br />

## **2. Tree Map**

If you have hierarchical data, or data with more than 5 dimension members, a pie chart is not ideal. Instead, a treemap may be a good choice.

**Treemaps**:

* using [nested rectangles] to show [hierarchical data] as a part of the whole
* the square shape helps your eye to compare relative sizes

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531102957245-16553669238914.png" alt="image-20210531102957245" style="zoom: 67%;" />

<br />

### \>> Build a treemap

#### Style 1: one dimension

* [Color] & [Size] : 1 measure field
* [Detail] :               1 dimension field
* [Label] :                measure & dimension

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531103536900-16553669238915.png" alt="image-20210531103536900" style="zoom: 80%;" />

<br />

#### Style 2: two dimensions (hierarchical data: Region -> Country) 

* [Color] :  1st dimension field (Region)   [best: within 7 colors]
* [Size] :     1 measure field
* [Detail] :  2nd dimension field (Country)
* [Label] :   measure & dimensions 

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531104030412-16553669238927.png" alt="image-20210531104030412" style="zoom:80%;" />

<br />

#### Style 3: add a second color (3 dimensions)

* [Color 1] :  1st dimension field (Region)   
* [Size] :        1 measure field
* [Detail] :     2nd dimension field (Country)
* [Color 2] :   3rd dimension field (Birth Rate Bin)  [*add shades of color*]
* [Label] :      measure & dimensions 

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531105001952-16553669238916.png" alt="image-20210531105001952" style="zoom:80%;" />

<br />

#### Style 4: Word Cloud

Treemap -->  change the Marks to [Text]

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531105309022-16553669238928.png" alt="image-20210531105309022" style="zoom:90%;" />

<br />

#### Style 5: Bubble Chart

Treemap --> change the Marks to [Circle]

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531105540971-16553669238929.png" alt="image-20210531105540971" style="zoom:90%;" />

<br />

#### Style 6: add a dimension to rows

<img src="/images/S-Tableau-Fundamentals-10-Showing-Breakdowns-of-the-Whole/image-20210531105703995-165536692389210.png" alt="image-20210531105703995" style="zoom:80%;" />

<br />

<br />
