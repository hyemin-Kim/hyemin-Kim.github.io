---
title: Tableau >> Fundamentals (3) Organize Data and Create Filters
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 2. Fundamentals
Description: 'Creating groups, Creating hierarchies, Filteirng, Sorting'
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
abbrlink: 14020
date: 2021-06-28 10:16:18
---

# Organize Data and Create Filters

@[toc]

<br />

## **1. Creating Groups in Your Data**

#### \>> Groups in Tableau

Groups in Tableau are represented by a <font color = 'blue'>paper clip</font>: <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520102251965.png" alt="image-20210520102251965" style="zoom:10%;" />

* In the [Data] Pane: displayed to the left of the field 
* In the [tooltip]: represents the *Group Members* button that is used to create a group.

<br />

#### \>> Methods to create groups

* Create a group based on a field in the Data pane.
* Create a group based on labels in the view.
* Create a group based on marks in the view.

<br />

#### \>> Details for each method

##### *Method 1.* Creating a group from the Data pane

1. Create a group

   * Field --> right-click / click the arrow --> [Create] > [Group]

2. Adding members

   * <font color = 'blue'>Select</font> relative terms <font color = 'blue'>directly</font>

   * <font color = 'blue'>Use [Find]</font>to find terms <font color = 'blue'>with specific pattern</font>

     <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520132444788.png" alt="image-20210520132444788" style="zoom:50%;" /> 

   * <font color = 'blue'>Dragging fields</font> into the existing group 

3. Group remaining members as the group [Other]

   * check <font color = 'blue'>[Include 'Other']</font>

4. Editing a group

   * <font color = 'blue'>Rename</font> the group

<br />

**[[실습]]** 

>  *Create a Group in the Data pane with World Indicators.twbx*

**<font color = 'darkblue'>\<Scenario></font>**

You want to find out average life expectancy for three countries within the Oceania region, and then compare that with other regions. 

You will create a group named Oceania for the  three countries, **Australia**, **New Zealand**, and **Papua New Guinea**, and compare the group with the rest of the countries.

<br />

**<font color = 'darkblue'>\<실현></font>**

1. Create a group on [Country] that includes [Australia], [New Zealand], and [Papua New Guinea], and name it [Oceania]

   * [Country] --> [Create] --> [Group]
   * Ctrl + select [Australia], [New Zealand], and [Papua New Guinea] and click [Group]
   * Rename the alias [Oceania]

   ​					<img src="D:\1. 아이투맥스\3. Tableau 학습\Typora Note\E_Analyst\2. Tableau Fundamentals\2-3. Organize Data and Create Filters.assets\image-20210520130248760.png" alt="image-20210520130248760" style="zoom: 50%;" />					<img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520130831794.png" alt="image-20210520130831794" style="zoom: 67%;" />

   <br />

2. Group all other countries together as [Other]

   * Check the [Include "Other"] checkbox

   <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520131328568.png" alt="image-20210520131328568" style="zoom: 50%;" />

   <br />

3. Name the group field

   <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520131734622.png" alt="image-20210520131734622" style="zoom:50%;" />

   <br />

4. Compare the [AVG(Life Expectancy Female)] of Oceania group with others

   <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520132228954.png" alt="image-20210520132228954" style="zoom:50%;" />

<br />

<br />

##### *Method 2.* Creating a group from within the view

* Creating a group by selecting marks from within the view
  1. Click and drag to select the marks
  2. In the tooltip opens, click the paper clip
  3. choose the dimensions to be applied

* Creating a group using labels in the view
  1. Hold [Ctrl] to select the marks in the view
  2. Use the dropdown or right-click one of the selected fields, then select the Group (paper clip) icon 
  3. choose the dimensions to be applied

<br />

**[[실습]]** 

>  *Create a Group in the View with World Indicators.twbx*

<br />

**<font color = 'darkblue'>\<Scenario></font>**

You want to quickly compare the income of two separate country groups to determine if tourism is similar based on the size in a treemap.

You will create a group from **Spain**, **France**, and **Germany** to compare to tourism in the **United States** within the view.

<br />

**<font color = 'darkblue'>\<실현></font>**

1. Create a group in the treemap that contains [Spain], [France], and [Germany]. Group on [All Dimensions].

   * drag to select [Spain], [France], and [Germany]

     <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520135604712.png" alt="image-20210520135604712" style="zoom: 50%;" />

     <br />

   * In the dialog opened, click the paper clip, then select [All Dimensions]

     <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520135836155.png" alt="image-20210520135836155" style="zoom:50%;" />

     <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520135919816.png" alt="image-20210520135919816" style="zoom:50%;" />

     <br />

2. Create a second group from a single mark: [United States]

   * Click [United States] to select it
   * In the dialog that opens, click the paper clip

   <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520140146128.png" alt="image-20210520140146128" style="zoom:50%;" />

   <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520140201714.png" alt="image-20210520140201714" style="zoom:50%;" />

   <br />

3. Compare the size of each group

   * The two groups are roughly the same size

<br />

<br />

## **2. Creating Hierarchies (계층) in Your Data**

#### \>>  Hierarchies in Tableau

* In Tableau, a hierarchy is an arrangement of data fields in a hierarchical format with an 'above' and 'below' structure.
* Hierarchies are represented by a hierarchy icon: <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520142502277.png" alt="image-20210520142502277" style="zoom:5%;" />

<br />

#### \>> Date hierarchies

*  dates and times are automatically placed in the dimensions area of the [Data] pane and are identified by the date <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520142835197.png" alt="image-20210520142835197" style="zoom:10%;" /> or date-time <img src="D:\1. 아이투맥스\3. Tableau 학습\Typora Note\E_Analyst\2. Tableau Fundamentals\2-3. Organize Data and Create Filters.assets\image-20210520142901428.png" alt="image-20210520142901428" style="zoom:10%;" /> icon, and can be drilled up and down as a hierarchy.
*  Date fields can consist of the following:
   - Year
   - Quarter
   - Month
   - Day
   - Time

<br />

#### \>> Methods to create hierarchies

**3 Steps:** 

1. Method 1: Field --> right-click --> Hierarchy (계층) --> Create Hierarchy (계층 만들기)

   Method 2: In the [Data] Pane, drag one field onto the other field

2. dialog box opened --> name the hierarchy

3. drag other fields into the existing hierarchy

<br />

<br />

## **3. Understanding Filtering in Tableau**

#### \>> Filter types in Tableau

* **Extract Filters**

  * When you connect to data, you can choose to extract it. As part of this process, you can filter out data that isn't relevant to your analysis.

  [e.g.] you are querying a data source that has data for the last 20 years, but you only want last 5 years of data. 

  <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520155333200.png" alt="image-20210520155333200" style="zoom: 67%;" />

<br />

* **Data Source Filters**

  * Reduce the amount of data being fed into Tableau
  * Restrict what data the viewer sees  (like filtering sensitive data out)

  [e.g.] Filter the data of United States

  <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520160131923.png" alt="image-20210520160131923" style="zoom: 80%;" />

<br />

* **Context Filters**

  * All filters in Tableau are computed independently. If you want one filter to be applied before other filters, make it a context filter so it will be processed first.

  [e.g.] you have two dimension filters, one on Region and another top 10 on products, both filters will apply to the entire data set. If you want to see the top 10 products in each region, set the Region filter as the context filter. 

  <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520160538065.png" alt="image-20210520160538065" style="zoom:67%;" />

<br />

* **Dimension Filters**

  * Dimensions contain discrete categorical data, so filtering this type of field generally involves selecting the values to include or exclude.

  [e.g.] Show products that have low sales in specific regions.

  <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520160815384.png" alt="image-20210520160815384" style="zoom:80%;" />

<br />

* **Measure Filters**

  * Measures contain quantitative data, so filtering this type of field generally involves selecting a range of values that you want to include.

  [e.g.] Show only products that have sales greater than 10,000.

  <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520161045931.png" alt="image-20210520161045931" style="zoom:80%;" />

<br />

* **Date Filters**

  * Date filters allow you to filter data by a range of dates, relative dates, or exact dates. 

  [e.g.] Show products that have been ordered starting January 2017.

  <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520161203700.png" alt="image-20210520161203700" style="zoom:80%;" />

<br />

* **Table Calculation Filters**

  * If you want to filter the view without filtering the underlying data, Table Calculations filters are the way to go.

  [e.g.] Filter data using a table calculation

  <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520161333305.png" alt="image-20210520161333305" style="zoom:80%;" />

<br />

#### \>> Filtering order of operations

When you use multiple filters on your data, the filters get applied in a very specific order, called the order of operations.

Tableau executes filters in the following order:

<img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210520161944956.png" alt="image-20210520161944956" style="zoom:80%;" />

<br />

<br />

## **4. Filtering Your Data**

#### \>> Filtering on Dimensions

**Methods to create a dimension filter**

* Filter by including or excluding data points

  1. Drag to select data points in the view

  2. On the tooltip that appears, 

     select [Keep Only] to include the selected marks 

     select [Exclude] to exclude the selected marks

  3. Tableau add the filter to the Filters shelf automatically

* Filter by dragging dimensions to the Filters shelf

  1. Drag the dimension field from the [Data] pane to the [Filters] shelf

<br />

#### \>> Filtering on Measures

**Method to create a measure filter**

1. Drag a measure to the [Filters] shelf --> [Filter Field] dialog box appears
2. Select an aggregation
3. Select a filter type
   * Range of Values
   * At Least
   * At Most
   * Special: Filter on Null values

<br />

#### \>> Filtering on Dates

**Method to create a date filter**

1. Drag a date field to the [Filters] shelf --> [Filter Field] dialog box appears
2. Select to filter by <font color = 'blue'>[Discrete date parts]</font> or <font color = 'viridis'>[Continuous date values]</font>
   * *Discrete date parts:* years, quarters, months etc.
   * *Continuous date values:* 
     * Relative dates (相对日期)  [可以设置“基准日期”（Anchor）：默认为“today” ] 
     * Range of dates
     * Starting date
     * Ending date
     * Special: filter on Null value

<br />

<br />

## **5. Sorting Your Data**

#### \>> Two sorting methods:

* Computed sorts
  * organize the data by applying rules
  * update dynamically
* manual sorts
  * a specific order that you want your data to be in
  * maintain the order that you put things in

<br />

#### \>> Customizing the sort using the Sort menu

* **정렬 기준 (Sort By):** 

  * Data source order
  * Alphabetic
  * Field (비중첩)
  * Manual
  * Nested (중첩)

  <br />

* **정렬 수단 (Sort from):** 

  * axis            (축)                    --- 중첩 
  * header       (머리글)
  * field label  (필드 레이블)   --- 비중첩

  <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210521132025109.png" alt="image-20210521132025109" style="zoom: 67%;" />

  > 모든 경우에:
  >
  > * 1 click:    sorts descending   [한 번 클릭: 내림차순]
  > * 2 clicks:  sorts ascending      [두 번 클릭: 오름차순]
  > * 3 clicks:  clear the sort          [세 번 클릭: 정렬 해제]

<br />

* **중첩 (Nested) VS 비중첩**

  |                             중첩                             |                            비중첩                            |
  | :----------------------------------------------------------: | :----------------------------------------------------------: |
  | <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210521133253249.png" alt="image-20210521133253249" style="zoom:80%;" /> | <img src="/images/S-Tableau-Fundamentals-3-Organize-Data-and-Create-Filters/image-20210521133326272.png" alt="image-20210521133326272" style="zoom:80%;" /> |
  |    * 각 Pane을 독립적으로 고려함 <br>* Pane별로 행을 정렬    | * 전체 Table 기준으로 집계 후 차원값을 정렬 <br>* 모든 Pane에서 같은 값 순서를 적용 |
  |              Sort by Nested;<br/>Sort form Axis              |           Sort by Field;<br>Sort form Field Label            |

  <br />

* **Disable the sort**

  Menu bar --> [Worksheet] --> uncheck [Show Sort Controls]

<br />

<br />
