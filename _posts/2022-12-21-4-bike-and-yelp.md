---
title: "04 Introducing the Yelp dataset"
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
  alt-plot-17: "assets/altair-charts/Number-of-Resutaurants-per-Neighborhood.json"
folium-loader:
  folium-chart-1: ["assets/folium/Philadelphia-Rating-heatmap-Animation.html", "400"] 
  folium-chart-2: ["assets/folium/Philadelphia-Resturants-Review-heatmap-Animation.html", "400"]
  folium-chart-3: ["assets/folium/Resturants-in-Philadelphia.html", "400"]
toc: true
toc_sticky: true
---

Now, let us look at some other datasets and see how they interact with our Replica dataset.

In this blog, we will walk you through some analysis based on Yelp dataset avaiables from [Yelp.dataset.com](https://www.yelp.com/dataset/documentation/main). From previous 3 blogs, you can see based on the Replica dataset, we analysis where people from, where people go, when people choose specific trip mode. Begining at this part, we will learn the pattern of business and restaurants in Philadelphia to see whether they match the Replica dataset.

The original dataset contains 5 json file, we will mainly use 2 of them: Business and Check-in.

`business.json` represents all business avaivable on Yelp platform data including unique id,lat,lng, attributes, and categories.

`checkin.json` cotains all the checkins based on each unique business id.

## Yelp in Philadelphia

We trimmed the original dataset to only focus on Philadelphia and did some basic data visualizations.

```python
business["city"]=='Philadelphia'
```
### Top categories for all yelp business in Philadelphia

![topyelp]({{ site.url }}{{ site.baseurl }}/assets/images/Top-Yelp-Categories.jpg)

### Star Ratings Distributions for all yelp business in Philadelphia

![paylepdsd]({{ site.url }}{{ site.baseurl }}/assets/images/Yelp-Star-Rating-Distribution-in-Philadelphia.jpg)

### Interactive folium heatmap 

Map shows the star ratings distribution in Philadelphia area, 1-9 represents stars from 1,1.5,2,2.5,3...5. You can see many 5 star-rating Yelp business are located along the Board Street, and clustring at center city along Walnut,Chestnut and Market Street.

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

For 5 stars restaruants, you will start to see some cluters on the south side of the city.

<div id="folium-chart-2"></div>

## Restaurants in Philadelphia 

Using mapbox and plotly, we can have a interactive map showing all the restaurants and their star ratings.

<div id="folium-chart-3"></div>

### Number of Restaurants per Neighborhood in Philadelphia

For this step,we joined the zillow neighborhood to find out number of restaurants per neighborhood in Philadelphia

<div id="alt-plot-17"></div>

# Checkins in Philadelphia

For checkin data,we also trimmed data to only look at Philadelphia. The original json file only has business id and all the checkin dates. We need to first split these dates. And convert it to datetime. Below are some visualizations for checkin distribution in Philadelphia.

### Philadelphia Restaurants Historical Yelp Check in by weekday

![restcheckwd]({{ site.url }}{{ site.baseurl }}/assets/images/Philadelphia-Restaurants-Historical-Yelp-Check-in-by-weekday.jpg)

### Philadelphia Restaurants Historical Yelp Check in by Time

![restchecktm]({{ site.url }}{{ site.baseurl }}/assets/images/Philadelphia-Restaurants-Historical-Yelp-Check-in-by-Time.jpg)

### Philadelphia Restaurants Historical Yelp Check in by Month

![restcheckmon]({{ site.url }}{{ site.baseurl }}/assets/images/Philadelphia-Restaurants-Historical-Yelp-Check-in-by-Month.jpg)

## Distribution of checkins on different weekday

![restcheckpwd]({{ site.url }}{{ site.baseurl }}/assets/images/Distribution-of-checkins-on-different-weekday-in-Philadelphia.jpg)

In the next blog, we will be focusing on replica bike trip data and yelp resturants data to predict block bike trip demand


