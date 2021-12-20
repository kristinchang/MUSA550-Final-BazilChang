---
title: "Air Pollution in Louisiana 2001-2014"
date: 2021-12-15
published: true
tags: [dataviz, hvplot, holoviews]
hv-loader:
  hv-chart-1: ["charts/ozHvplot2.html", "600"] # second argument is the height
  hv-chart-2: ["charts/pmHvplot2.html", "600"]
toc: true
toc_sticky: true
---

## Ozone Contaminant

The chart below shows the number of days each parish in Louisiana had an ozone contaminant level that was above the regulatory standard, using the slider to observe levels from 2009-2014:

<div id="hv-chart-1"></div>

Days that ozone levels were highest for all parishes peaks in 2010. The general accumulation of contamination is concentrated in the southern and northwestern areas of the state. These are the parishes that also contain the state's oil refineries. From 2010 to 2014, there is a decrease in the number of parishes that observed an ozone level above the regulatory standard. However, some southern parishes that consistently had high ozone levels during this time period experienced an increase.

## Pm 2.5 Contaminant

This chart is similar to the one above, but for the Pm 2.5 Contaminant level for each parish:

<div id="hv-chart-2"></div>

From 2010 to 2014 there is an obvious increase in Pm 2.5 contamination across the state of Louisiana. The accumulation of this pollution is concentrated in the southern and northwester parishes where oil refineries are located. There is some fluctuation in Pm 2.5 levels in several southern parishes during this time period, but contamination in Bossier and Caddo parishes (hover over map for names) in the northwest is consistently increasing over time.
