---
title: Tableau >> Advanced (6) Dashboarding
date: 2022-06-27 15:46:47
tags:
  - Tableau
categories:
  - 【STUDY - Tableau】
  - Tableau - 4. Advanced
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
typora-root-url: ..
---

# Dashboarding

@[toc]

<br />

## **1. Swapping Sheets and Refining the Layout**

### \>> Sheet Swapping

Sheet swapping is where sheets are hidden/displayed (i.e. swapped) depending on user dashboard selections.

This is a very helpful and efficient way for us to share numerous views in a single dashboard, which can avoid squeezing in too much information or linking to several dashboards.

<br />

To swap sheets, we need **a parameter** used for selecting a view and **collapsing containers** to show the corresponding view.

Let's look at how this works through the following example:

<br />

**<font color = 'navy'><< Goal >></font>**

For a study about environment noise in Brooklyn, we want to include rotating views that show noise rankings (Slope Chart & Bump Chart) and control-chart data in the dashboard. Let's use a parameter to swap these views and employ layout and titling options.

<br />

**<font color = 'navy'><< Process >></font>**

**[STEP 1] Create a parameter for swapping the slope, bump, and control charts in the dashboard**

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210708111333540.png" alt="image-20210708111333540" style="zoom:67%;" />

<br />

**[STEP 2] Create a Select Sheet filter calculation to apply a filter to each view, which will enable the correct view to show, and hide the other views**

* Create the filter calculated field based on the parameter

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210708111502614.png" alt="image-20210708111502614" style="zoom:67%;" />

<br />

* Use the calculated field as a filter for each swapped view, show the parameter control and test the parameter

  * Display the [Slope Chart] sheet, drag the [Select a Chart Filter] field to [Filters], dropping it below [YEAR(Created Date)]

  * In the dialog box opened, 

    \- select [Custom value list], 

    \- type [Slope Chart] in the text field, 

    \- click "+" 

    \- and then click [OK]

  * Do the same work with [Bump Chart] and [Control Chart] . (P.S. The view will disappear at the end of this step)

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712105839024.png" alt="image-20210712105839024" style="zoom:40%;" />

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712105151323.png" alt="image-20210712105151323" style="zoom:40%;" />

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712105335881.png" alt="image-20210712105335881" style="zoom:40%;" />

  <br />

  * Return to [Slope Chart] sheet, show the parameter control and test the parameter. End with the Slope Chart selected and displayed

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712105733489.png" alt="image-20210712105733489" style="zoom:45%;" />

<br />

**[STEP 3] Drag the swapped views into the dashboard, and hide their titles**

* Use a container to contain the views to swap. This will allow the views to share the same space, rather than be tiled separately.

  \- Drag a Vertical container into the view and drop it below the existed views when the horizontal gray band is shown 

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712124751089.png" alt="image-20210712124751089" style="zoom:45%;" />

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712125248022.png" alt="image-20210712125248022" style="zoom:45%;" />

  <br />

* Drag the three charts into the container

  \- First drag in the slope chart, the view that is currently displayed in the parameter control

  \- Drop it when the container border appeared and highlighted in dark blue

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712125903509.png" alt="image-20210712125903509" style="zoom:45%;" />

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712125940385.png" alt="image-20210712125940385" style="zoom:45%;" />

  <br />

  \- Next, drag in the Bump Chart, being careful to drop it only when we see the horizontal gray band and the blue container border.

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712130244408.png" alt="image-20210712130244408" style="zoom:45%;" />

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712130325401.png" alt="image-20210712130325401" style="zoom:45%;" />

  <br />

  \- Finally, do the same thing for the Control Chart

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712130521443.png" alt="image-20210712130521443" style="zoom:45%;" />

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712130556710.png" alt="image-20210712130556710" style="zoom:45%;" />

  <br />

  This view brings in the parameter control, because the Slope Chart is the worksheet that we showed the control on. 

  And, note that only the Scatter Plot view displayed in the dashboard, based on its selection in the control. 

  <br />

* Hide the view titles for each of the swapped views

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712131453952.png" alt="image-20210712131453952" style="zoom:45%;" />

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712131422755.png" alt="image-20210712131422755" style="zoom:45%;" />

<br />

**[STEP 4] Remove all controls except the parameter control, move the dashboard title, and make the title dynamic**

* Close all controls and legends except for the parameter control

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712132159831.png" alt="image-20210712132159831" style="zoom:50%;" />

  <br /> 

* Enlarge the container with the swapped views:

  \- click it

  \- display its menu

  \- click [Select Container: Vertical]

  \- on the container's top border, drag the sizing handle upward to enlarge it

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712132530983.png" alt="image-20210712132530983" style="zoom:50%;" /> 

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712132918748.png" alt="image-20210712132918748" style="zoom:50%;" />   

<br />

* Reset the location and size of the title container

  \- click the title container to select it

  \- drag its handle to place the container between the top two views and the swapped-views container

  \- on the title container's bottom border, drag the sizing handle upward to make the container smaller

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712133715718.png" alt="image-20210712133715718" style="zoom:50%;" /> 

<br />

* Move the parameter control:

  \- click the parameter control to select it. display its menu, and click [Floating]

  \- position the control at the left end within the title container

  \- drag up its container border to fit within the title container

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712134655113.png" alt="image-20210712134655113" style="zoom:50%;" /> 

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712134626891.png" alt="image-20210712134626891" style="zoom:50%;" /> 

<br />

* Edit the dashboard title

  \- open the [Edit Title] dialog box

  \- remove the existed title

  \- on the [Insert] menu, select [Parameters.Select a Chart]

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712134943322.png" alt="image-20210712134943322" style="zoom:50%;" /> 

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712135032391.png" alt="image-20210712135032391" style="zoom:50%;" /> 

  <br />

   \- The title now updates with each view

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712135106398.png" alt="image-20210712135106398" style="zoom:50%;" /> 

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712135243343.png" alt="image-20210712135243343" style="zoom:50%;" />  

  <br /> 

**[STEP 5] Add container borders, padding, and a text container for an overall title, then make sizing adjustments**

* Add a border to the title container

  \- click the title container to select it

  \- click the [Layout] tab --> [Border] --> select a solid black line at a minimal thickness

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712135844389.png" alt="image-20210712135844389" style="zoom:50%;" /> 

<br />

* Add a similar border to the swapped-views container

  \- click it

  \- display its menu

  \- click [Select Container: Vertical]

  \- add the border

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712142157180.png" alt="image-20210712142157180" style="zoom:50%;" />  

<br />

* Add padding

  \- For example: select the sparklines view and add four points of Inner Padding

  \- do the same with the highlight table

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712140436538.png" alt="image-20210712140436538" style="zoom:50%;" />  

<br />

* Add an overall dashboard title

  \- from the [Dashboard] tab, drag a [Text] container onto the dashboard

  \- drop it at the top when the horizontal gray band above the two top views appears

  \- type the title and edit it

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712141223319.png" alt="image-20210712141223319" style="zoom:50%;" /> 

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712140734133.png" alt="image-20210712140734133" style="zoom:50%;" /> 

  <br />

  \- drag up the text container border for the ideal height

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712141635381.png" alt="image-20210712141635381" style="zoom:50%;" /> 

<br /><br />

## **2. Adding Context to Dashboard Filter Actions**

### \>> Context Filter

By default, all filters set in Tableau are computed independently, which means that each filter accesses all rows in the data source without regard to other filters. However, by setting one or more categorical filters as context filters, we can make other filters as dependent ones that process only the data that passes through the context filter.

<br />

We can create a context filter to:

* Improve performance --

  If we set a lot of filters or have a large data source, the queries can be slow. We can set one or more context filters to improve performance.

* Create a dependent numerical or top N filter --

  We can set a context filter to include only the data of interest, and then set a numerical or a top N filter.

<br />

### \>> Use Context Filters to Control Filter Actions

**<font color='navy'><< Goal >></font>**

For the main markets that use Superstore, we want to help users see only the top 25 cities for sales by Market and the top 10 products for sales by Market - City.

<br />

**<font color='navy'><< Process >></font>**

**[STEP 1] On the Top 10 Product Sales worksheet, add a filter for the top 10 Product Names by Sales**

* Drag [Product Name] from Dimensions to the [Filters] card

* In the dialog box opened: 

  \- click [Top] --> [By field] : [Top] [10] by [Sales] [Sum]

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712155732099.png" alt="image-20210712155732099" style="zoom:45%;" />

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712160023934.png" alt="image-20210712160023934" style="zoom:45%;" />

<br />

**[STEP 2] On the Top 25 Cities for Sales worksheet, add a filter for the [City and State] field for the top 25 by Sales**

* Drag the [City and State] field to [Filters] card

* In the dialog box opened: 

  \- click [Top] --> [By field] : [Top] [25] by [Sales] [Sum]

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712160721965.png" alt="image-20210712160721965" style="zoom:45%;" />

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712160803907.png" alt="image-20210712160803907" style="zoom:45%;" />

<br />

**[STEP 3] On the Worldwide Sales dashboard, use the Market sheet as a filter, then test it to observe the results**

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712161027261.png" alt="image-20210712161027261" style="zoom:45%;" />

<br />

* When we click a market to filter to its top 25 cities and top 10 products, the results are not what we are expected.

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712161301799.png" alt="image-20210712161301799" style="zoom:45%;" />

  <br />

  * USCA market shows only 7 cities and 3 products

  * The reason is that without using market as a context filter, the Top 25 Cities filter and Top 10 Products filter access all rows in the data:

    When we see 7 cities from the USCA market, that means seven of the top cities overall happen to be in the USCA market

  * To get each market to show its top cities and top products for sales,  we need to add context to the filter action

<br />

**[STEP 4] On the product and cities worksheets, add the Action (Market) filter to context**

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712162750768.png" alt="image-20210712162750768" style="zoom:45%;" />

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712162824982.png" alt="image-20210712162824982" style="zoom:45%;" />

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712162905014.png" alt="image-20210712162905014" style="zoom:45%;" />

<br />

**[STEP 5] Create a dashboard filter that shows the top 10 product sales for the selected city on the map**

* In the dashboard, make sure no markets are selected

* Create a filter action: [Dashboard] menu  --> [Actions]  --> [Add actions] : Filter

  ​	<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712164305607.png" alt="image-20210712164305607" style="zoom:50%;" />   	 <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712164433421-165631271936250.png" alt="image-20210712164433421" style="zoom:50%;" />

* Edit the filter action like follows and click [OK] --> [OK]

  ​	<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712164611493.png" alt="image-20210712164611493" style="zoom:50%;" /> 		<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712164901826-165631273369852.png" alt="image-20210712164901826" style="zoom:67%;" />

  <br />

* Test the filter on the map view, we find that the list of product names never has 10 entries.

  We want the filter action we just cerated to apply in the context of the city 

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712165144515.png" alt="image-20210712165144515" style="zoom:50%;" />

<br />

* In the Top 10 Product Sales sheet, add the action filter to context

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712165939041.png" alt="image-20210712165939041" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712170141434.png" alt="image-20210712170141434" style="zoom:50%;" />

  <img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712170051474.png" alt="image-20210712170051474" style="zoom:50%;" />

​		Now, the result is what we want.

<br />

**[STEP 6] Add the dashboard title**

* Click [Show dashboard title] to display the title, Worldwide Sales

<img src="/images/S-Tableau-Advanced-6-Dashboarding/image-20210712170317291-165631274862354.png" alt="image-20210712170317291" style="zoom:50%;" />

<br />

<br />
