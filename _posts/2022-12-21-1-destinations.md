---
title: "01 Philly's Destinations"
date: 2022/12/20
published: true
categories:
  - blog
tags:
  - Github Page
  - update
altair-loader:
  alt-plot-1: "assets/altair-charts/arrivals-by-time.json"
  alt-plot-2: "assets/altair-charts/bg-clustering-map.json"
  alt-plot-3: "assets/altair-charts/cluster-dashboard.json"
hv-loader:
  hv-plot-1: ["assets/altair-charts/eat-destinations.html", "750"]
  hv-plot-2: ["assets/altair-charts/Shop-destinations.html", "750"]
  hv-plot-3: ["assets/altair-charts/Work-destinations.html", "750"]
  hv-plot-4: ["assets/altair-charts/School-destinations.html", "750"]
excert:

---

# Introduction

What are the major destinations of Philadelphia? When, how, and why do people travel? [Replica](https://studio.replicahq.com/)'s data may help us understand the question. Replica provides *modeled* *trip-level* data **in a typical weekday** using multivarious sources:

- Census and ACS;
- Travel surveys;
- In-auto GPS data;
- Data from transit agencies;

[Here](http://help.replicahq.com/en/articles/6625924-north-atlantic-fall-2021-release-notes) Replica talks more about data sources and its methodology. We subset only trips that start and end in Philadelphia. The modeled data for Philadelphia is [regarded as trustworthy](http://help.replicahq.com/en/articles/4000393-replica-places-certainty-indicators-overview).

# Data processing

Replica's data includes trip origin and destination (block-group-level), trip distance and durations, and trip-taker demographis data for every trip. We selected a few columns for our purpose. The data processing script can be found [here](https://github.com/MUSA-550-Fall-2022/final-project-mobile_philly/blob/main/notebooks/data-preprocessing.py).

# Philadelphia's destinations

Using `datashader` with the python `hvplot` library, we plotted every destination in Philadelphia at different times of the day. We can see that there are two **peak hours**, one in the morning, and the other in the afternoon. Destinations are highly **concentrated** in Center City, but are more **diffused** in the afternoon

![Arrivals-by-hour](../../assets/gif/destination-by-hour.gif)

Note: each dot represents an arrival. The dot is randomly generated within the block group in which the arrival falls.

# Destination typology

It is reasonable that the overall number of arrivals have two peaks in one day, as shown in the below graph, but what about each individual block group? 

<div id="alt-plot-1"></div>

We can do a clustering study using the k-means method. For each block group, we calculated the *number of arrivals* of each hour, and *normalized* the arrival couns by *the trip count of 12-1pm* of each block group. Using a scree-plot method, we chose $k=8$ as the number of clusters.

<div id="alt-plot-3"></div>

The interactive chart demonstrate the "arrival pattern" of each block group. **Click-select** the block group(s) in the left bar-plot and observe the arrival patterns in the right plot. We can see that some clusters have two clear peaks, whereas other clusters have one dominant peak. The clusters with the morning peak indicates more business-oriented land uses, and those with afternoon-peaks indicate residential or some commercial land uses.

A map of the different types of destinations is shown as follows.

<div id="alt-plot-2"></div>

# Destinations of different trip purposes

The below four charts document the destinations of different trip purposes. Each dot represents an arrival and is randomly generated within the block group in which the arrival falls. Compared to eating and shopping trips, work destinations are most spatially concentrated. Shopping destinations and schooling destinations are more spatially diffused.

<div id="hv-plot-1"></div>
<div id="hv-plot-2"></div>
<div id="hv-plot-3"></div>
<div id="hv-plot-4"></div>

To find out the more specific OD's of these trips, read [the next blog](https://leejere.github.io/mobile-philly/2-trip-netflows/).
