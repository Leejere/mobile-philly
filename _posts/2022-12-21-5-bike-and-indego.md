---
title: "04 Yelp and Biking:Yelp in Philadelphia"
date: 2022/12/20
published: true
categories:
  - blog
tags:
  - Github Page
  - update
altair-loader:
  alt-plot-16: "assets/altair-charts/bike-ratio-by-bg.json"

excert:

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
### 
![topyelp]({{ site.url }}{{ site.baseurl }}/assets/images/Top-Yelp-Categories.jpg)


Bike ratio by block group:
<div id="alt-plot-16"></div>

![bike-from-where-to-where]({{ site.url }}{{ site.baseurl }}/assets/images/bike-from-where-to-where.jpg)

(Only aggregate trips > 5)


