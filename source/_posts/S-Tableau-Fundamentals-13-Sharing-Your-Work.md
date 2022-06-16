---
title: Tableau >> Fundamentals (13) Sharing Your Work
date: 2022-06-16 15:47:46
tags:
 - Tableau
categories:
 - 【STUDY - Tableau】
 - Tableau - 2. Fundamentals
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
---

# Sharing Your Work

@[toc]



## **1. The Tableau File Types**

**Four Tableau file types:**

* **.TDS (Tableau data source file)**
  * contains metadata changes, like group and calculated fields
  * does not contain any of the actual data necessary to create your viz
  * but store the information necessary to connect to the original data source
* **.TWB (Tableau workbook file)**
  * contains your worksheets and dashboards
  * store the information necessary to connect to the data source as well as the information needed to build the view
  * does not include the data from the underlying data source
  * when saving as a .TWB file, a link is established to the data source used. Therefore, the next time you open your .TWB file, the view will automatically update with any changed made to the original data source
* **.TWBX (packaged Tableau workbook file)**
  * stores the information necessary to connect to the data source, the information needed to build the viz, and also includes a copy of the local data used. 
  * does not create an extract of the data, but it contain both live connections and/or data extracts.
* **.TDE (Tableau data extract file)**
  * a snapshot of your data that Tableau saves locally. 
  * helpful when you're connecting to extremely large data sets, of which you only need some fields.





## **2. Sharing Your Work with Others**

* Publish to Tableau Online ( or Tableau Server):
  * [Server] Menu --> [Publish Workbook]
  * 1. [Tableau Online] button
    2. [Server] : https://online.tableau.com  
  * Click [Connect]
  * Sign in to Tableau Online

* Save your file as a Tableau packaged workbook (.twbx) 
  * others can work with it in Tableau Desktop or Tableau Reader
* Share only an image of a view or the data
  * [Worksheet] Menu --> [Export] --> Image / Data / Crosstab to Excel
