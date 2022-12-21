# Final Project: Mobile Philadelphia

Authors: [@Jie Li](https://github.com/Leejere)
[@Jie Wang](https://github.com/Buduwang)


In **MUSA 5550** with Nick Hand, fall 2022, University of Pennsylvania

______

**For the end-product of this project, please go to [the deployed pages at this link](https://leejere.github.io/mobile-philly/), or the corresponding [GitHub repository](https://github.com/Leejere/mobile-philly).**

This project produces five blog posts about mobility and some other related topics. We used [Replica](https://studio.replicahq.com/) as a main source for mobility data, which is further introduced in the [first blog post](https://leejere.github.io/mobile-philly/blog/1-destinations/). Two other data sources are [restaurants reviews data from Yelp](), which we used to dive deeper into dining-related trips, and [Indego data](), which we used to explore more on bike travel.

## Navigation

The raw data from Replica is in this [Google Drive link](https://drive.google.com/file/d/1bh51nx7r2AMikcaxt7Gt2Y4OqKca_c3T/view?usp=sharing), and the processed data is stored as ten `.csv` files under `data/cleaned-data` in [the repository](https://github.com/Leejere/mobile-philly/). The script used to process the data is in `notebooks/data-processing.py` in the same repository.

The Yelp dataset is available in [Yelp](https://www.yelp.com/dataset/download), and the processed data is stored as `checkinpa.csv`,`philadelphiabusinessyelp.csv` and 
`zillow_neighborhoods.geojson` under `data/` [in this repository](https://github.com/MUSA-550-Fall-2022/final-project-mobile_philly). 

All the other scripts for data processing, analysis, and visualizing are in either `replica-visualization.ipynb` or `yelp_bike.ipynb` under `notebooks/`. All other data used or imported is under `data/` in [the repository]https://github.com/MUSA-550-Fall-2022/final-project-mobile_philly).
