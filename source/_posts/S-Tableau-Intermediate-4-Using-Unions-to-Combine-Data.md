---
title: Tableau >> Intermediate (4) Using Unions to Combine Data
tags: '-Tableau'
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 59472
date: 2022-06-27 13:42:11
---

# Using Unions to Combine Data 

@[toc]

<br />

## **1. Concept**

A union is way to connect multiple tables from a single data source. 

It combines rows from two or more tables to lengthen the scope of your data.

<br />

## **2. Union Your Data**

The tables that you combine using a union must have the same structure:

* same number of fields
* related fields must have matching field names and data types

<br />

After the data union, 

* all the rows are included in the union, even the duplicate values
* two new columns(Sheet & Table Name) will be automatically generated

<br />

## **3. Create a Union Manually**

Two ways to create a union:

1. drag and drop

   * clicking and dragging the first sheet to the empty canvas
   * click and drag the second sheet *underneath* the first sheet until the [Union] box appears
   * drop the second sheet when the box changes to a solid orange color

   <img src="/images/S-Tableau-Intermediate-4-Using-Unions-to-Combine-Data/image-20210604155657013.png" alt="image-20210604155657013" style="zoom:80%;" />

2. Use [New Union] option

   * double-click the New Union option 

     <img src="/images/S-Tableau-Intermediate-4-Using-Unions-to-Combine-Data/image-20210604155857525-16563146432711.png" alt="image-20210604155857525" style="zoom:80%;" />        <img src="/images/S-Tableau-Intermediate-4-Using-Unions-to-Combine-Data/image-20210604155935753.png" alt="image-20210604155935753" style="zoom:77%;" />


   1. Specific (manual):

      create unions manually by selecting specific files that are imported in the Data Source page.

   2. Wildcard (automatic):

      created automatically by searching for files through a directory

<br />

## **4. Merge Mismatched Fields**

For duplicate fields with mismatched field names but the same values, we can combine them by using Merge Mismatched Fields

<br />

Process:

1. Go to the [Data Source] page
2. Select the fields we want to merge
3. From the drop-down menu, click [Merge Mismatched Fields]
4. Rename the merged field

<br />

<br />
