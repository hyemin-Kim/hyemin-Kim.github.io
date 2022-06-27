---
title: Tableau >> Advanced (3) Seasonality Show Trends with Cycle Plots
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 4. Advanced
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 48540
date: 2022-06-27 15:35:45
---

# Seasonality: Show Trends with Cycle Plots

@[toc]

<br />

## **1. Seasonality**

**Seasonality** is any predictable change in a time series that repeats over a one-year period. 

Discovering seasonality in our data is important because it helps us identify cyclic trends in our data that can help us with forecasting or making changes to our processes. 

<br />

When you want to show seasonality over time, there are some options that can show a clear picture:

* **Single Line Chart:** Shows seasonality over a one year period

  <img src="/images/S-Tableau-Advanced-3-Seasonality-Show-Trends-with-Cycle-Plots/image-20210706090238793.png" alt="image-20210706090238793" style="zoom:67%;" /> 

  <br />

* **Highlight Table:** Shows seasonality using various colors and shades

  <img src="/images/S-Tableau-Advanced-3-Seasonality-Show-Trends-with-Cycle-Plots/image-20210706090403568.png" alt="image-20210706090403568" style="zoom:67%;" /> 

  <br />

* **Multiple Lines Chart:** Shows seasonality over several years using multiple lines

  <img src="/images/S-Tableau-Advanced-3-Seasonality-Show-Trends-with-Cycle-Plots/image-20210706090515046.png" alt="image-20210706090515046" style="zoom:67%;" /> 

<br />

<br />

## **2. Cycle Plots**

Except these, **Cycle plots** are another way to show seasonality. 

**Cycle plots** are line charts that show the trends of ***<font color = 'navy'>two different time periods</font>*** simultaneously (e.g. showing both month and year). The seasonal variations by month can be seen more easily with a cycle plot because it shows ***<font color = 'navy'>both the trend and the month-of-the-year effect.</font>***

<img src="/images/S-Tableau-Advanced-3-Seasonality-Show-Trends-with-Cycle-Plots/image-20210706091115235.png" alt="image-20210706091115235" style="zoom: 67%;" />

<br />

<br />

## **3. Create a Cycle plot**

**<font color = 'navy'><< Goal >></font>**

We have four years of sales data and have noticed peak sales during some months throughout the years. Does this indicate there is seasonality in our data? We would like to build a cycle plot to find out it.  

<br />

**<font color = 'navy'><< Process >></font>**

**[STEP 1] Expand the Order Date in the view to show only discrete Year and Month**

<img src="/images/S-Tableau-Advanced-3-Seasonality-Show-Trends-with-Cycle-Plots/image-20210706101729860.png" alt="image-20210706101729860" style="zoom:50%;" />

<br />

**[STEP 2] Invert the order of YEAR and MONTH and add an average line per pane**

<img src="/images/S-Tableau-Advanced-3-Seasonality-Show-Trends-with-Cycle-Plots/image-20210706101954644.png" alt="image-20210706101954644" style="zoom:50%;" /> <img src="/images/S-Tableau-Advanced-3-Seasonality-Show-Trends-with-Cycle-Plots/image-20210706102014377-165631183817810.png" alt="image-20210706102014377" style="zoom:45%;" />

<br />

**[STEP 3] Change the marks to a light blue area**

<img src="/images/S-Tableau-Advanced-3-Seasonality-Show-Trends-with-Cycle-Plots/image-20210706102121146.png" alt="image-20210706102121146" style="zoom:50%;" />

<br />

<br />

**[STEP 4] Add a dark blue line to the marks using a synchronized dual axis chart**

<img src="/images/S-Tableau-Advanced-3-Seasonality-Show-Trends-with-Cycle-Plots/image-20210706102257272.png" alt="image-20210706102257272" style="zoom:50%;" />

<br />

<br />
