---
title: Tableau >> Intermediate (5) Filtering Across Data Sources
date: 2022-06-27 13:48:55
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
---

# Filtering Across Data Sources

@[toc]

<br />

## **1. Concept**

While working with multiple data sources in a workbook, you might want to compare the data between them using a field they have in common. To do so, you can apply a cross-database filter to filter data across multiple primary data sources.

<br />

## **2. Create a cross-database filter**

1. ### Establish a relationship between the data sources with the common fields

   * Automatically

   * Manually: [Data] Menu --> [Edit Blend Relationships]

     <br />

2. ### Create and apply a cross-database filter

   * **<font color = 'darkblue'>In the dashboard</font>**

     1) dashboard --> source worksheet --> down arrow [Menu] --> [Filters] --> [*common field*]

     <img src="/images/S-Tableau-Intermediate-5-Filtering-Across-Data-Sources/image-20210607090719281.png" alt="image-20210607090719281" style="zoom: 67%;" />

     <br />

     2) filter card appeared --> down arrow [Menu] --> [Apply to Worksheets] --> [All using Related Data Sources]

     <img src="/images/S-Tableau-Intermediate-5-Filtering-Across-Data-Sources/image-20210607091123611.png" alt="image-20210607091123611" style="zoom: 50%;" />

     <br />

   * **<font color = 'darkblue'>In the view</font>**

     1) Source worksheet --> drag the common field to [Filters] --> click [All]

     <img src="/images/S-Tableau-Intermediate-5-Filtering-Across-Data-Sources/image-20210607093344614.png" alt="image-20210607093344614" style="zoom: 67%;" />

     2) [Filters] card --> [common field] --> [Apply to Worksheets] --> [All Using Related Data Sources]

     <img src="/images/S-Tableau-Intermediate-5-Filtering-Across-Data-Sources/image-20210607092036185.png" alt="image-20210607092036185" style="zoom:67%;" />

     <br />

   <br />

