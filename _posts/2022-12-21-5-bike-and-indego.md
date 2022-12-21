---
title: "04 Yelp and Biking:Yelp in Philadelphia"
date: 2022/12/20
published: true
categories:
  - blog
tags:
  - Github Page
  - update

excerpt:
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

![paylepdsd]({{ site.url }}{{ site.baseurl }}/assets/images/Yelp-Star-Rating-Distribution-in-Philadelphia.jpg)

### Interactive folium heatmap 

Map shows the star ratings distribution in Philadelphia area, 1-9 represents stars from 1,1.5,2,2.5,3...5. You can see many 5 star rating Yelp business are located along the Board Street, and clustring at center city along Walnut,Chestnut and Market Street.

<div id="folium-chart-1"></div>

## Next we trim to look at only Restaurants business on Yelp in Philadelphia

```python
rest =payelp[payelp['categories'].str.contains('Restaurant.*')==True].reset_index()
```
### Restaurants Star Rating Distribution

![reststar]({{ site.url }}{{ site.baseurl }}/assets/images/Resturants-Star-Rating-Distribution-in-Philadelphia.jpg)

### Restaurants Categories Distribution

Interesting to see Nightlife is the Top1 categories for restaurants in Philadelphia

![restcate]({{ site.url }}{{ site.baseurl }}/assets/images/top-restaurants-categories-in-Philadelphia.jpg)

### Interactive folium heatmap for Restaurants

<div id="folium-chart-2"></div>



Bike ratio by block group:
<div id="alt-plot-16"></div>



(Only aggregate trips > 5)


