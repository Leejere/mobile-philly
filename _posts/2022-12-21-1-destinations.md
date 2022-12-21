---
title: "01 Philly's Destinations"
date: 2022/12/20
published: true
categories:
  - blog
tags: [dataviz, matplotlib, mobility]
altair-loader:
  alt-plot-1: "assets/altair-charts/arrivals-by-time.json"
  alt-plot-2: "assets/altair-charts/bg-clustering-map.json"
  alt-plot-3: "assets/altair-charts/cluster-dashboard.json"
hv-loader:
  hv-plot-1: ["assets/altair-charts/eat-destinations.html", "650"]
  hv-plot-2: ["assets/altair-charts/Shop-destinations.html", "650"]
  hv-plot-3: ["assets/altair-charts/Work-destinations.html", "650"]
  hv-plot-4: ["assets/altair-charts/School-destinations.html", "650"]
excert:
toc: true
toc_sticky: true
read_time: false

---

What are the major destinations of Philadelphia? When, how, and why do people travel? [Replica](https://studio.replicahq.com/)'s data may help us understand the question. Replica provides *modeled* *trip-level* data **in a typical weekday** using multivarious sources:

- Census and ACS;
- Travel surveys;
- In-auto GPS data;
- Data from transit agencies;

[Here](http://help.replicahq.com/en/articles/6625924-north-atlantic-fall-2021-release-notes) Replica talks more about data sources and its methodology. We subset only trips that start and end in Philadelphia. The modeled data for Philadelphia is [regarded as trustworthy](http://help.replicahq.com/en/articles/4000393-replica-places-certainty-indicators-overview).

# Data processing

Replica's data includes trip origin and destination (block-group-level), trip distance and durations, and trip-taker demographis data for every trip. We selected a few columns for our purpose. The data processing script can be found [here](https://github.com/MUSA-550-Fall-2022/final-project-mobile_philly/blob/main/notebooks/data-preprocessing.py).

# Philadelphia's destinations

![Arrivals-by-hour](../../assets/gif/destination-by-hour.gif)

Using `datashader` with the python `hvplot` library, we plotted every destination in Philadelphia at different times of the day. We can see that there are two **peak hours**, one in the morning, and the other in the afternoon. Destinations are highly **concentrated** in Center City, but are more **diffused** in the afternoon

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

# Code excerpt

Code excerpt to generate random points in a polygon. Adapted from Nick Hand's course materials.

```python
# Function to generates random points inside polygon
from shapely.geometry import Point

def generate_rand_pts_in_polygon(number, polygon):
  """
  Takes a shapely polygon, and the number of pts to be generated within this polygon
  Returns a list of shapely points randomly generated within this polygon
  """
  points = []

  # Get the bounds of the polygon
  try:
    min_x, min_y, max_x, max_y = polygon.bounds

    # Randomly generate points within the bounds
    # If falls in polygon, adds count
    # If falls outside of the polygon, disgard
    i = 0
    while i < number:
      this_point = Point(np.random.uniform(min_x, max_x), np.random.uniform(min_y, max_y))
      if polygon.contains(this_point):
        points.append(this_point)
        i = i + 1
    return points
  except:
    return []

# Function to make a pandas DataFrame of the x, y coords of each generated trips,
# randomly distributed in the corresponding block groups

def shade_destinations(df):
  # Join a geometry for later generating random points

  df = phila_block_groups_3857[['GEOID', 'geometry']].merge(
    df,
    how = 'right',
    left_on = 'GEOID',
    right_on = 'destination_GEOID'
  )

  pts = df.apply(
    lambda row: generate_rand_pts_in_polygon(
      row['count'], row['geometry']
    ),
    axis = 1,
  )

  pts = gpd.GeoSeries(pts.apply(pd.Series).stack(), dtype = object, crs = 'EPSG:3857')
  pts.name = 'geometry'
  pts = gpd.GeoDataFrame(pts)

  # Calculate the X and Y coordinates
  pts['x'] = pts.geometry.x
  pts['y'] = pts.geometry.y
  pts = (pts.reset_index())[['x', 'y', 'geometry']]

  return pts
```

Using the package `imageio` to create a GIF from a series of images.

```python
# For each hour, plot each destination, randomly distributed within the block group it belongs

for this_hour in range(24):
  this_hour_df = arrivals_by_hour.where(lambda x: x['trip_end_time'] == this_hour).dropna()
  this_pts = shade_destinations(this_hour_df)

  fig, ax = plt.subplots(figsize = (9, 12))

  
  dsshow(this_pts[['x', 'y']], ds.Point('x', 'y'), norm = 'eq_hist', cmap = 'inferno', ax = ax)
  phila_block_groups_3857.plot(facecolor = "none", edgecolor = "white", linewidth = 0.2, alpha = 0.5, ax = ax)
  ax.text(min_x + x_span * 0.07, max_y - y_span * 0.07, f'{str(this_hour).zfill(2)}:00', color = "#ffffff", fontsize = 16)

  ax.set_xlim(min_x, max_x)
  ax.set_ylim(min_y, max_y)
  ax.grid(False)
  ax.axis("off")

  print(f'{str(this_hour).zfill(2)}:00' + ' completed')

  fig.savefig(f'../data/destination-by-hour/hour{this_hour}', bbox_inches='tight')

# Make a GIF of the different hours
gif_images = []

for this_hour in range(24):
  gif_images.append(imageio.imread(f'../data/destination-by-hour/hour{this_hour}.png'))

kargs = { 'duration': 0.5 }
imageio.mimsave('../data/destination-by-hour/destination-by-hour.gif', gif_images, **kargs)

```
