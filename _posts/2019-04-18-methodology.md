---
title: "Methodology"
date: 2021-12-15
categories:
  - blog
tags:
  - Github Page
  - update
---

The following describes the methods used to produce each Green New Deal analysis tool.

**Air Pollution over Time(2001-2014) Visualization**
* Data

We downloaded a csv of ozone and pm2.5 contaminants data from the [Louisiana Department of Health portal](https://healthdata.ldh.la.gov/). We also downloaded parish geo data from the Louisiana Department of Transportation. Then, we cleaned the data by simplifying columns and renaming and converting the datatype of primary and foreign key columns to match to be joined. We converted both dataframes from wide to long form. We also converted the year column to a datetime object and extracted just the year for a clean year column.

* Spatial Joins

We then merged both the to the parish dataframe separately. Finally, we
  - trimmed to the most recent 6 years so the file would be the appropriate size for github pages. 
  - Projected both dataframes in crs 4326. 


* Visualizations

We generated interactive maps using hvplot, grouping by year such that change over time can be observed. Finally, we saved both plots as html files to be embedded in github pages.

**Fossil Fuel Production Dashboard**
* Data

We again use parish-level geographies, and the air quality data leveraged in part 1 of our toolkit. We then read in point data on the location and capacity of petroleum refineries in 2020 in the United States from the [Energy Information Administration](https://www.eia.gov/maps/layer_info-m.php). We filter the refinery data to Louisiana, and use atmospheric distillation thousands of barrels per day (AD_Mbpd) as a proxy for general facility capacity. We also leverage point data representing offshore drilling platform locations in the Gulf of Mexico. This data was collected as a part of the second iteration of the Designing a Green New Deal studio and was retrieved from the studio Box folder.

* Spatial Joins

We merge the air pollution data with the parish data to create a choropleth map of Louisiana with the colors representing the number of days each parish recorded ozone contaminants above the recommended level in 2014. We then spatially join the refinery point data to the air pollution by parish polygons. 
Because multiple parishes contain more than one refinery, we use the dissolve function to aggregate refinery capacity numbers by parish. The result is one refinery capacity number per parish that is a sum of capacity across the parish. 

* Data Link

We use data link to combine the choropleth map of ozone contamination by parish with a table of aggregated refinery capacity by parish. Clicking on a parish on the map will highlight the corresponding row in the table.

* Visualizations

  - The first visualization displays the fossil fuel infrastructure in Louisiana over the choropleth map of ozone contamination. The refinery locations are represented by circles on the map with their sizes corresponding to refinery capacity. Hovering over a refinery location will display it’s lat lon and capacity. The white dots represent offshore drilling locations in the Gulf between Texas and Mississippi. On hover, the choropleth map displays the parish name and corresponding ozone contamination indicator which is encoded as the color of the polygons. The goal of this visualization is to display the higher levels of pollution that correspond with higher concentration and capacity of O&G production in Louisiana.

  - The second visualization links the choropleth map of ozone contamination with a table displaying the refinery capacity numbers by parish. This allows the user to click on a parish and then have the corresponding row containing aggregated capacity information to be highlighted. The goal of this dashboard is to easily see the aggregate refinery capacity by parish and how it relates to ozone contamination. For example, East Baton Rouge has a level of ozone contamination (bright orange on the map). Once clicked on, the user can see that the refinery capacity for this parish is high as well – 539 Ad_MDP.

**Senitment Analysis: #GreenNewDeal**
