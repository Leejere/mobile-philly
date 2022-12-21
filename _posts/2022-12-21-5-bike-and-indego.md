---
title: "04 Yelp and Biking:Yelp in Philadelphia"
date: 2022/12/20
published: true
categories:
  - blog
tags:
  - Github Page
  - update
excerpt:"Embedding interactive Folium charts on static pages using Jekyll."
altair-loader:
  alt-plot-16: "assets/altair-charts/bike-ratio-by-bg.json"
folium-loader:
  folium-chart-1: ["assets/folium/Philadelphia-Rating-heatmap-Animation.html", "400"] 
  folium-chart-2: ["assets/folium/Philadelphia-Resturants-Review-heatmap-Animation.html", "400"]
toc: true
toc_sticky: true



---

# Yelp Dataset

In this blog, we will walk you through some analysis based Yelp dataset avaiables on [Yelp.dataset.com](https://www.yelp.com/dataset/documentation/main).
The original dataset contains 5 json file, we will mainly use 2 of them: Business and Check in 
business.json represents all business avaivable on Yelp platform data including unique id,lat,lng, attributes, and categories.
checkin.json cotains all the checkins based on each unique business id.

## Yelp in Philadelphia

We trim the original dataset to only focus on Philadelphai and did some basic data visualizations.

```python
business["city"]=='Philadelphia'
```
### Top categories for all yelp business in Philadelphia

![topyelp]({{ site.url }}{{ site.baseurl }}/assets/images/Top-Yelp-Categories.jpg)

### Star Ratings Distributions for all yelp business in Philadelphia

![topyelp]({{ site.url }}{{ site.baseurl }}/assets/images/Yelp-Star-Rating-Distribution-in-Philadelphia.jpg)

### Interactive folium heatmap 

Map shows the star ratings distribution in Philadelphia area, 1-9 represents stars from 1,1.5,2,2.5,3...5. You can see many 5 star rating Yelp business are located along the Board Street, and clustring at center city along Walnut,Chestnut and Market Street.

<div id="folium-chart-1"></div>

Bike ratio by block group:
<div id="alt-plot-16"></div>

![bike-from-where-to-where]({{ site.url }}{{ site.baseurl }}/assets/images/bike-from-where-to-where.jpg)

(Only aggregate trips > 5)


