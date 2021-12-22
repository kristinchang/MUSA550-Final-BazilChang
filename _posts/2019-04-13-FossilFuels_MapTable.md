---
title: "Spatial Analysis of Fossil Fuel Infrastructure and Air Pollution"
date: 2021-12-15
published: true
tags: [dataviz, hvplot, holoviews]
hv-loader:
  hv-chart-1: ["charts/fossil_inf.html", "600"] # second argument is the height
  hv-chart-2: ["charts/dashboard_oneCol_v2.html", "600"]
toc: true
toc_sticky: true
---
## Fossil Fuel Infrastructure

Fossil fuel production in Louisiana occurs both along the Mississippi River delta and offshore in the Gulf Coast. Oil and gas (O&G) production in the Louisiana steadily increased from the first well drilled in Louisiana in 1901 to its peak in 1970. Most of the wetland loss in the Delta region can be attributed to O&G activities through the alteration of surface hydrology, fluid removal and fault activation, and toxic stress due to spilled oil.

The map below shows the main fossil fuel production infrastructures in Louisiana-- petroleum refineries and offshore oil rigs. Each parish color represents the number of days it had an ozone level that was above the regulatory standard in 2014. The petroleum refinery point size represents its capacity-- that is, how much petroleum is being processed at that location. The white points offshore each represent an oil rig, displaying the high concentation along the Gulf coast from Texas to Mississippi. 

<div id="hv-chart-1"></div>

## Dashboard

The dashboard below shows the number of days each parish in Louisiana had an ozone level that was above the regulatory standard in 2014, linked with a table displaying the petrolem refinery capacity per parish. Clicking on a parish on the map will highlight the relevant refinery capacity at that location. Unsurprisingly, the areas with high refinery capacity also experience poor air quality more frequently.

<div id="hv-chart-2"></div>


