---
title: Tableau >> Fundamentals (5) Mapping Data Geographically
date: 2022-06-16 13:37:51
tags:
 - Tableau
categories:
 - 【STUDY - Tableau】
 - Tableau - 2. Fundamentals
cover: 'https://z3.ax1x.com/2021/08/18/fo8Hat.png'
---



# Mapping Data Geographically

@[toc]



## 1. Concept: Mapping Your Data

* **Two map types in Tableau**

  1. symbol maps

     \- Use symbols to represent a central point of a geographic region

  2. filled maps

     \- Boundaries of a geographic region filled with color

     

* **Geographic Data**

  * Data that describes a physical location 
  * Basically consists of a latitude coordinate (위도 좌표) and a longitude coordinate (경도 좌표)
  * When combining latitude and longitude together, it's known as a coordinate point



* **9 geographic information types that Tableau can recognize**

  * US Area Codes
  * US-based CBSA / MSA
  * Cities Worldwide
  * US Congressional Districts
  * Worldwide Countries / Regions
  * US Countries
  * Worldwide States / Provinces
  * Postal Codes
  * Latitude and Longitude

   

* **Geocoding**

  * The process that Tableau automatically assigns coordinates to the places according to Tableau's recognized geographic information types mentioned above. 

