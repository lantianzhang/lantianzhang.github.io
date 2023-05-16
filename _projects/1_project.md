---
layout: page
title: Rodents Complaints in NYC
description: Investigating the Factors that Contribute to Rodent Outbreaks
img: assets/img/rodent-header.jpeg
importance: 1
category: work
---

The project aims to identify the factors that contribute to high rates of rodent complaints in New York City using a variety of datasets found on NYC Open Data including 311 complaints, restaurant inspections and sanitation complaints using machine learning classification and prediction approaches.

The datasets we used included Rat Sightings and Sanitatory Conditions from 311 complaints, DOH Restaurant Inspections, and Subway entrances. The analysis is based on 5-year rodent related data (2018-2023), which is merged into the census block group spatial unit. The categorical data are encoded and all the data are scaled. For the analysis part we use Number of Rodent Sightings from 311 Complaints as the target variables, while the predictors include 311 Sanitation Complaints by Types, 311 Rodent Complaints by Location and Time, and Restaurant Inspection Results by Violation Type and Cuisine.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/12.png" title="New York City 311 Rodent Sightings Choropleth
Map (2019)" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    New York City 311 Rodent Sightings Choropleth Map (2019)
</div>

Fundamentally, the nature of this study was exploratory and not hypothesis driven. Hence, a large number of data sets available online were considered and finally a smaller but relevant subset was selected for analysis (a significant amount of the data that is available online is not directly predictive or indicative of rodents). Hence, the aforementioned data sources were used. The restaurants inspection, subway entrance locations and sanitation complaints are usually (by pure human intuition) considered to be very indicative of rodent problems. Hence, we decided to use the same to assess/check for any correlation between them and rodent sightings from 311 complaints.

For data processing, geospatial data was used to generate a census block level GeoDataframe. Then, all rodent sightings (individual 311 complaints) were mapped to geometric location and date of inspection. This was further processed for mapping rodent sightings count to census blocks with the sightings count being discretized for day of week, time of day and location type i.e., residential, offices etc.   Similar exercises were done for subway counts, restaurant inspections and DSNY complaints. DSNY complaints were discretized to dog waste, illegal dumping on street, dead animals and trash complaints (some of the data was discretized further). Similarly restaurant inspection data was discretized for different pest issues and cuisine type. Finally, considering socio-economic factors, median household income was mapped to the census blocks and was included the main data set as well.

The final data set contained census block groups mapping to rodent sighting and complaints for each year from 2018 to 2023.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/rodent_kmeans_clusters.png" title="New York City 311 Rodent Sightings Choropleth
Map (2019)" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
     Maps of each K-means cluster of Rodent Sighting per Census Block Groups (2019)
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-9 mt-3 mt-md-0">
        To understand how census blocks can be grouped together, unsupervised Kmeans was run using SKlearn based on 4 attributes: 311 rat sightings, restaurants rats/mice violations, sanitation related 311 reports of illegal dumping and unsecured trash in the street. The silhouette score of 0.56 was a peak at 6 clusters. Cluster 4 has the highest rates of sightings, violations and sanitation complaints. Clusters 1 and 5 are also suspect for intervention. For instance the census block area with Chelsea market showed up here with high rates of restaurant violations in cluster 5.
    </div>

    <div class="col-sm-3 mt-3 mt-md-0">
        {% include figure.html path="assets/img/KM_cluster_description.png" title="Description of the Clusters" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/rodent_kmeans_anomalies.png" title="Description of the Clusters" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/rodent_anomalies.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    On the left, map of census block groups K Means anomalies (2019); On the right, map of census block groups DBSCAN ensemble anomalies (2019)
</div>

For the  k-means anomaly analysis, a k-means model was fit to the dataset, then the distance of each point to its nearest cluster center was calculated. A threshold of 99 percent was set for the minimum distance that identifies anomalies as points with minimum distance above the threshold. 

To determine which areas had the most anamoulous rodent sightings: Filter the clusters to only the ones where there are fewer than 5 percent of the census block groups as clusters(i.e. very few clusters). Iterate over all results of the anomalies to find all possible epsilon and min sample hyperparameters that result in anomalies. Then, summarize the number of times the census block group is identified as an anomaly. 
Take the results of the summarization and create a heat map (choropleth) to show where the anomalies occur. This method of analyzing rodent sightings could be considered as a form of ensemble anomaly detection since it iterates over multiple combinations of hyperparameters (epsilon and min samples) to identify anomalies. 

The anomaly findings of Kmeans and DBSCAN highlight very different results. In the Kmeans, 25 census block groups that have high rates of rodent sightings and unsecured trash are anomalous. While in the DBSCAN results, anomalies show areas that have low rodent sightings. 

This clustering analysis could be improved by using the original latitude/longitude rather than the aggregated count of rodent sightings. Additionally, more environmental and socio-economic datasets could be used.

We then chose Decision Tree to look at the importance of each feature, based on the Gini importance.

Looking at the composition of the attributes, we decided our approach would be to use different ones as the target variables. First we used the number of complaints on rodent sightings from 3ll data as the target variable. The subset of attributes we used to fit the decision tree model for this target includes violations from DOH restaurant inspections, and 311 complaints on unsanitary conditions. Among these attributes, complaints on trash on street is the most important. Next, we used the restaurant violations as the target variable. This time, we used the number of 311 complaints on rodent sightings by reporting locations, and 311 complaints on unsanitary conditions by type as the predictors. Among these attributes, the most important ones are complaints on trash on street, on rodent sightings from commercial buildings, on missed trash collection, on trash in residential buildings, and on illegal dumping trash on street. Finally, we used the number of sanitation complaints as the target variable, and we used the number of 311 complaints on rodent sightings by reporting locations, as well as the restaurant violations as the predictors. 

It should be noted that the performance of the decision tree regression model on these 3 models is not ideal, with the in sample R-squared values between 0.1 and 0.2

Among these attributes, the most importance ones are complaints on rodent sightings in vacant space, in commercial space, and in residential space. 
<div class="row">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/dt_num_of_sightings.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/dt_restaurant_violations.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/dt_dsny_complaints.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    From left to right, Gini importances when target variable is rodent sightings, restaurant violations, and sanitaion complaints, respectively. 
</div>

The findings of this study can be summarized as follows: Kmeans was simple and useful approach that city officials could use to classify census block groups and identify problematic locations to target. DBSCAN is not recommended. Decision tree regression show limited correlation between the target variable and the predictors. Among the attributes, 311 complaints on street trash is the most important when using 311 complaints on rodent sightings as the indicator of rodent prevalence.

Upon reflection on these results, we have identified following areas for future research - census blocks may not be the best agglomeration unit since they may not capture the broader geospatial distribution of rodents. Future research could focus on larger geographic units to avoid getting sparse dataset.

Subway entrances may not be the best feature to assess for, if rodent populations depend on a broader but still localized network of subway station i.e., agglomeration of subway entrances (across different census blocks). 

More datasets with characteristics of the landscape and socio-economics could have improved findings. Other datasets used in literature include the following: Land zoning, vacant buildings, public spaces (parks, etc.), building construction permit data, education level data at the census block group level.

Reporting bias was not addressed in this study. There could be instances where certain geographies over-report or under-report to 311 citations, which could cause there to be a misunderstanding of rodent prevenlance in the area. 

