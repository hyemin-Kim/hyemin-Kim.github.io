---
title: Tableau >> Intermediate (12) Using Parameters to Control Data in the View
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 3. Intermediate
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 30412
date: 2022-06-27 14:35:57
---

# Using Parameters to Control Data in the View

@[toc]

<br />

## **1. Concept**

A parameter is a workbook variable that can replace a constant value in a calculation, filter, or reference line. It allows you to customize the view according to your needs.

The parameters are global. This means that the value of the parameter is applied to every sheet where it is used. 

<br />

<br />

## **2. Use a Parameter in a Calculation**

### Step 1. Create a parameter

* [Data] pane --> [Create Parameter] --> [Create parameter] dialog box

​	   <img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611085437341-16563141659221.png" alt="image-20210611085437341" style="zoom:67%;" /> 			<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611091113430.png" alt="image-20210611091113430" style="zoom:67%;" />

<br />

* Settings:

  *<font color = 'darkblue'>[Name]</font>*

  *<font color = 'darkblue'>[Data type]</font>* : Float / Integer / String / Boolean / Date / Date & Time

  *<font color = 'darkblue'>[Current value]</font>* : the first number the parameter will use

  *<font color = 'darkblue'>[Display format]</font>*

  *<font color = 'darkblue'>[Allowable values]</font>* : All / List / Range

  <br />

### Step 2. Use the parameter

* Create a calculated field

  <img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611090401553-16563142111963.png" alt="image-20210611090401553" style="zoom:67%;" />			<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611091146937.png" alt="image-20210611091146937" style="zoom:67%;" />	

  <br />

### Step 3. Show parameter control

* Right-click the parameter, and select [Show Parameter Control]

  <img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611090801657-16563142464645.png" alt="image-20210611090801657" style="zoom:67%;" />			![image-20210611090916567](/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611090916567.png)

<br />

<br />

## **3. Use a Parameter with a Filter**

**[Mission] Make a < Top N Filter> parameter**

### Step 1. Add a parameter to a filter

* a) Drag the dimension field to [Rows] / [Columns]  --> click [Filter and then add]  --> open the Filter dialog box

  b) Drag the dimension field to [Filter] --> open the Filter dialog box

  ​				<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611091755122-16563142644887.png" alt="image-20210611091755122" style="zoom:67%;" />			<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611091620060.png" alt="image-20210611091620060" style="zoom:67%;" />

<br />

### Step 2. Create and save the parameter

* [Top]  --> [By field]  --> [Create a new parameter]  --> Settings -->  [OK]

  <img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611092143936-16563142848899.png" alt="image-20210611092143936" style="zoom:50%;" />		<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611092346025-165631429595711.png" alt="image-20210611092346025" style="zoom: 50%;" />		<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611092524428.png" alt="image-20210611092524428" style="zoom:67%;" />

  <br />

* Both the filter and parameter are created

  <img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611092939904.png" alt="image-20210611092939904" style="zoom: 67%;" />

<br />

### Step 3. Show parameter control

* Right-click the parameter, and select [Show Parameter Control]

  ![image-20210611093058789](/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611093058789-165631432561313.png)			<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611093137142.png" alt="image-20210611093137142" style="zoom:120%;" />

<br />

<br />

## **4. Use a Parameter to Swap Measures**

Using a parameter, you can create one view and give users the ability to choose which measure to display, which is called *dynamic measure selection*. 

<br />

### Step 1. Create a parameter

* Create the parameter and include a list of values that represents each measure we want to show.

  <img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611104005746.png" alt="image-20210611104005746" style="zoom: 67%;" />

<br />

### Step 2. Use the parameter in a calculation

* Tie a parameter to something you'll use in the view, such as a calculation, filter, or reference line.

* use a CASE statement to match the parameter variables and return the correct measure data

  <img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611104353589.png" alt="image-20210611104353589" style="zoom: 67%;" />

<br />

### Step 3. Show parameter control

* Use the parameter in the view and display the parameter control to enable users to switch among the measures

<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611104549840.png" alt="image-20210611104549840" style="zoom:120%;" />

<br />

### Step 4. Apply a dynamic title with the parameter

<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611110246784-165631438763515.png" alt="image-20210611110246784" style="zoom:67%;" /> 		<img src="/images/S-Tableau-Intermediate-12-Using-Parameters-to-Control-Data-in-the-View/image-20210611110317775.png" alt="image-20210611110317775" style="zoom: 80%;" />

<br />

<br />
