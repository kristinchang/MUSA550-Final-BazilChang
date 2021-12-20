---
title: "Air Pollution in Louisiana 2001-2014"
date: 2021-12-15
published: true
tags: [dataviz, hvplot, holoviews]
hv-loader:
  hv-chart-1: ["charts/ozHvplot.html", "500"] # second argument is the height
  hv-chart-2: ["charts/pmHvplot.html", "500"]
toc: true
toc_sticky: true
---

## Ozone Contaminant

The chart below shows the number of days each parish in Louisiana had an ozone level that was above the regulatory standard, from 2001-2014:

<div id="hv-chart-1"></div>

## Pm 2.5 Contaminant

This chart is the same as above, but for the Pm 2.5 Contaminant level for each parish:

<div id="hv-chart-2"></div>

These charts were produced using hvplot and holoviews and embedded in this static web page. The following python code is replicable for any air pollutant data available in this format:

```python
import altair as alt
alt.renderers.enable('notebook')
```
