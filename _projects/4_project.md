---
layout: page
title: Noise Pollution in New York City
description: Investigating the Factors that Contribute to Disruptive Noise Exposure
img: assets/img/noise-header.png
importance: 4
category: work
---

The main objective of this project is to predict noise complaints in New York City, identify the variables that most significantly influence noise complaints, and explore the spatio-temporal patterns by exploring noise complaint data from 311 service requests in New York City between 2021 and 2022. The results reveal that noise pollution is a critical urban issue, with negative health outcomes ranging from minor annoyance to severe health problems. Low-income residential areas are correlated with several noise complaint descriptors, and zoning-residential attributes as significant factors in noise pollution. However, using noise complaints as a proxy measure for noise pollution has limitations due to inherent biases in self-reported data. To enhance future research, more comprehensive traffic volume measurements and ground truth validity through sensor recordings of ambient noise are recommended. The findings can inform targeted preventative measures and community outreach efforts to mitigate noise pollution.

<div class="row">
    <div class="col-sm mt-6 mt-md-0">
        {% include figure.html path="assets/img/percent_total_census_tracts.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-6 mt-md-0">
        {% include figure.html path="assets/img/percent_total_complaints.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: number of census tract that have noise complaints, per type; Right: percent of complaints per complaint type
</div>

The data sources we used included Noise Complaints from 311, Zoning Information from MapPluto, Longitudinal Employer-Household Dynamics, Road Density - Road Length and Width in each Census Tract, Construction Permits, and Point of Interests.

The analysis is based on 2-year noise complaint data (2021-2022), which is merged into the census tract spatial unit. The categorical data are encoded and all the data are scaled. For the analysis part we use the noise complaints number as the target variable, while the predictors include construction permit type, zoning type, point of interest type, road density, and Longitudinal Employer-Household Dynamics (LEHD). The data shape is 4330 by 91.

The target variable is derived from the noise complaints events data from 311, and we have collected several datasets that we believe could contribute to noise complaints, such as road density, zoning, number of points of interest, LEHD, and construction permit. To ensure the relevance of all datasets, we have decided to use 2 years noise complaint data from 2021 to 2022 and aggregate all the data under the same spatial scale of census tracts. For the subsequent analysis, we will use the total number of noise complaints as the target variable and construction permit type, zoning type, poi type, road density, and LEHD as the predictors.

<div class="row">
    <div class="col-sm mt-6 mt-md-0">
        {% include figure.html path="assets/img/noise_complaints.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-6 mt-md-0">
        {% include figure.html path="assets/img/noise_kmeans_clusters.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: 311 Noise Complaints Choropleth; Right: 7 noise clusters from K-Means method
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/noise_communities.png" title="pycombo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    PyCombo noise communities
</div>
In addition to clustering, we also conducted time series analysis on the noise complaints. However, there appears to be no significant trend from the time series over total noise complaints, except noise complaints are usually higher in the summer and fall months.

<div class="row">
    <div class="col-sm mt-6 mt-md-0 pt-4">
        {% include figure.html path="assets/img/TS_temporal_trend.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-6 mt-md-0">
        {% include figure.html path="assets/img/TS_noise_complaint_by_day.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: overall temporal trend of noise complaints; Right: noise complaint trend by day of week
</div>


<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/TS_cluster_temporal_by_day.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    cluster by day
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/TS_cluster_temporal_trend_by_hour.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    cluster by hour
</div>

linear regression was used to find out the most relevant features that significantly impact the number of noise complaints in this study. First, Ordinary Least Squares (OLS) regression as all the relevant features as predictors was conducted. The coefficient of determinant(R²) for the train data set was 0.426, and for the test data set was 0.391. The OLS regression shows 15 predictors with the p-values less than 95 percent significance level. The predictors include various kinds of POIs and the number of different kinds of construction permits, along with roade density and zoning for high residential density.

<div class="row">
    <div class="col-sm mt-6 mt-md-0">
        {% include figure.html path="assets/img/ols-result.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-6 mt-md-0">
        {% include figure.html path="assets/img/ols-predictors-low-pval.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: OLS result; Right: Predictors with p-value less than 0.05
</div>


We then chose Decision Tree to look at the importance of each feature, based on the gini importance.

Of all the features, Zoning-Residential have a significant importance, it is understandable as residents in the heavily residential neighborhoods tend to have more complaints compared with commercial or manufacturing neighborhoods.

The performance of the decision tree regressor is acceptable although not ideal, with the in-sample R-squared at 0.51, out-of-sample R-squared at 0.37

Since the zoning-residential attributes are overwhelming, we then looked at other subsets of the attributes, like Points of Interest and Construction, to see the Decision Tree Regression results, as well as each attribute's Gini importance within the subset. For the Construction subset of attributes, AlterationMinor:OtherLocation-Sum is the most important. And for the POI subset of attributes, food and beverage, commerce, parks are all important features. However, it should be noted that the in-sample R-squared values for all of these decision tree regression models are relatively low, ranging from 0.2 to 0.4. 

<div class="row">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/DT_gini_importatnce_overall.png" title="DT-overall" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/DT_gini_importatnce_C_attributes.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/DT_gini_importatnce_P_attributes.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    From left to right, Gini importances among all attributes, construction attributes, and points of interest attributes, respectively. 
</div>

When using a Random Forest regressor to predict each census tract’s number of complaints, the RF model is potentially overfitting, with an in-sample R-squared at 0.94, out-of-sample R-squared at 0.57. 

Our key findings are as follows: 4 percent of all noise complaints in 2021-22 were attributed to intermittent peak noises (loud party, banging/pounding, vehicular noise). 54 percent of noise complaints are characterized as Noise-Residential, indicating that more than half of noise complaints come from residential areas. Distinct communities that share the burden of noise can be identified from spatial distribution analysis and be targeted for mitigation. However, inherent biases in the complaint patters need to be assessed and balanced
before resource allocation. Low-income residential CT areas feature in the top 5 correlated attributes with several noise complaint descriptors. Zoning-Residential attributes have significant importance, with a total of 0.6 measured in Gini importance.




