---
title: "Is your flight going to be delayed? Well, it depends..."
excerpt: "The aim of this post is to identify meaningful clusters of flight delays for FAA regulated airports in the US"
header:
  overlay_image: air_logo2.jpg
  overlay_filter: 0.4
  caption: ""
  cta_label: " "
categories:
  - data science
tags:
  - hierarchical clustering
  - principal component analysis 
  - k-means clustering
  - silhouette score
  - distortion
author: "Marina Drus"
date: "15 November 2016"
---

{% include base_path %}

### Introduction

In this project, the main goal was to identify meaningful and useful (sharing common characteristics) clusters of flight delays for FAA regulated airports in the US. Data included name of airport, state, city, operational year (from 2004 to 2010), departures, arrivals, cancelations, numbers of delays and diversions, average delay times for a number of operational processes (such as taxi-out, taxi-in, airborne time, etc.). Please see detailed description of the features [here](http://aspmhelp.faa.gov/index.php/APM:_Analysis:_Definitions_of_Variables). Because some of the features were measured in minutes and some were measured in percentage, the data was normalized (scaled) before the analyses was conducted. 


### Principal Components Analysis


Principle components analysis (PCA) is dimension-reduction technique that is completely different from clustering methods such k-means clustering and hierarchical clustering. PCA seeks to find the best possible low-dimensional representation that explains the maximum amount of variance. Clustering (whether it is k-means analysis or agglomerative hierarchical analysis) looks for similar subgroups in observation data. Before conducting PCA, I needed to see whether features have large enough relationships with each other to conduct PCA. As seen below from the correlational table, features that reflect measures of airport delays are highly correlated among each other.


![Correlational Table]({{ site.url }}{{ site.baseurl }}/images/pic5_1.png){: .align-center} 


Next, I identified eigenvalues in my PCA model. The analysis distinguish 17 eigenvalues. The very fisrt eigenvalue had the largest value, while the fisrt three eigenvalues indicated values larger than 1. 


![Eigenvalues]({{ site.url }}{{ site.baseurl }}/images/pic5_2.png){: .align-center}


As seen below, the first three eigenvalues formed three major components that that cumulatively explained 85.51% of variance for airport delays. PC1 explained 53.91% of all airport delays while PC1 and PC2 together explained 78.37% of all airport delays. I used Kaiser’s stopping rule to select the first three components. Kaiser’s stopping rule states that only the number of factors with eigenvalues over 1.00 should be considered in the analysis. However, this was an arbitrary decision. In this case, I am solely interested in identifying meaningful and useful clusters. In some way, PCA is helping me to clean my clusters from the features that are less likely to share common characteristics with major meaningful clusters. In other cases, different rules to selecting major components from PCA would be applied. 


![Major Components]({{ site.url }}{{ site.baseurl }}/images/pic5_3.png){: .align-center}

|   |dept_comp|arriv_comp|ontime_gate_dept|ontime_air_dept|ontime_gate_arriv|gate_delay|taxi_out_time|taxi_out_delay|
|---|---|---|---|---|---|---|---|---|
|PC1|.78|.78|-.50|-.83|-.45|.61|.82|.83|
|PC2|-.55|-.56|-.71|-.47|-.82|.70|-.08|-.04|
|PC3|.08|.09|-.36|.002|-.10|.28|-.46|-.44|

|   |air_dept_delay|airborn_delay|taxi_in_delay|block_delay|gate_arrive_delay|dept_cancel|arriv_cancel|dept_diversions|arriv_diversions|
|---|---|---|---
|PC1|
|PC2|
|PC3|


### K-means Analysis

K-means analysis is a clustering technique that seeks to group the observations into pre-existing number of clusters. In this type of clustering analysis, researchers have to specify the desired number of clusters. Here, several k-means analyses were conducted with various number of clusters. Also, k-means were conducted on original data and PCA-transformed data (the first three components identified in PCA). Inertia values, a measure of how internally coherent clusters are, below indicate that PCA-reduced clusters have less distortion that the original features do. In general, the inertia values below indicate high distortion in the clusters (ideally, the less this number is the less distortion), indicating that clusters are far from homogenous.  Since Euclidean distances tend to become inflated (“curse of dimensionality”), running a PCA prior to k-means alleviates this problem.


![Inertia Values]({{ site.url }}{{ site.baseurl }}/images/pic5_4.png){: .align-center}


























