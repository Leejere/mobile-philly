---
title: "05 Restaurants and Biking:Predicting Model"
date: 2022/12/21
published: true
categories:
  - blog
tags:
  - Github Page
  - update
excerpt:
toc: true
toc_sticky: true
---

Predicting census block bike trips demand in Philadelphia

At this step, we are going to first import Replica dataset and trim it to only look at trip's Primary mode is Biking. Because the Replica trip only has start and end
geoid, so we want to join it with census block data.

```python
from pygris import block_groups
phila_block_groups = block_groups(
  state = '42', 
  county = "101",
  year = 2015
)
```

### Total bike trips per block

![ttbikebl]({{ site.url }}{{ site.baseurl }}/assets/images/Total-bike-trips-per-block.jpg)

### Distance from bike trip start block to 10 nearest Yelp restaurants

Then we want to calcuate the distance from census blocks to the 10 nearest Resturants from Yelp Business and apply log10().

![disrestbl]({{ site.url }}{{ site.baseurl }}/assets/images/Distance-to-the-10-nearest-yelp-resturants.jpg)

After this step, we also import Indego stations from Indego API, and calculate the nearest Indego station distance

### Correlations for all features

Distance to the Indego stations also strongest positive correlation with total bike trips, distance to nearest resturants is not that correlated to bike trips and 
other features.

![corr]({{ site.url }}{{ site.baseurl }}/assets/images/Correlations.jpg)

After that we set up pipleline from  StandardScaler to RandomForestRegressor, and use GridSearchCV to find out the best params are ['randomforestregressor__max_depth': None,'randomforestregressor__n_estimators': 200]. And our current model is overfitting the grid score is over 0.99. At this step, the predicted and actual trips are pretty much the same. To further optimize our model, we may need to take off 


