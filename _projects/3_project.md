---
layout: page
title: Did NYC Open Street Make the Streets Unsafe?
description: a project aims to offer insight into whether Open Street affected street safety through spatial analysis
img: assets/img/smith-st-open-streets.jpg
redirect:
importance: 3
category: work
---

To examine the street safety implications of Open Streets, we compared the frequency of incidents before it was introduced in 2019 to 2021 during its operation. Our research question can be summarized as follows:

Did Open Streets increase vehicle accidents in the surrounding area?
    Did the number of collisions increase?
    Did the number of people killed or injured in each group (pedestrians, cyclists, motorists) increase?
Did Open Streets increase the number of parking violations?

To investigate the questions, we used Open Streets Location data released by the New York Department of Transportation through the NYC Open Data Portal (Open Streets Location Data). The data includes location, when Open Streets was approved, and operating days and hours. 

Since Open Street blocks the traffic with barricades, it is unlikely that any incidents will occur on the street while the event is happening; therefore, we selected the surrounding area of the streets to observe. To define the surrounding area, we used census tracts with which the segments of Open Streets intersect since the census tract is a population-controlled unit. We used 2020 Census Tracts data from NYC Open Data Portal (2020 Census Tracts). A 60ft buffer representing the actual street width was subtracted from the census tracts polygons to offer the same baseline. When there are more than one census tracts a certain Open Street program intersects with, they were conjoined into one union.

<div class="row justify-content-sm-center">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/open-street-area.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-8 mt-3 mt-md-0 pt-4">
        {% include figure.html path="assets/img/vehicle-data-pipeline.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Left: a sample census tract containing Open Street; Right: data pipeline diagram
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/os_surroudingn-area.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Open Street plotted in NYC
</div>

After extracting the census tracts where Open Streets intersect, we combined the data with vehicle collision data from the NYC Open Data portal (Motor Vehicle Collisions - crashes). Vehicle collision data offer the date and time of the accident, the number of injuries and deaths for motorists, cyclists, and pedestrians, and the locations of collisions. We spatially joined the collision data with Open Streets surrounding area (Census Tracts) to filter out incidents outside our interest zone. After spatial filtering, we did additional data filtering based on each Open Street program's opening and closing date and times, e.g., which month it starts, which days in the week it operates, as well as the specific opening times in the day. Therefore, the incidents occurred only on the effective days and time that were counted for the study. Then the same time window was applied to the data from 2019, the year before Open Street was introduced, to use it as a control group. We counted the number of accidents and summed the number of people injured or killed in each mobility group in the Open Streets surrounding area with the refined data.

To measure the impact of Open Streets over time, we divided the data into two time periods; before (2019) and after its operation started (2021). We gave dummy variables to each period as after=0 and after=1. The data from each period was normalized by the total number of accidents of the year. We did an exploratory examination of each data. Then we ran the ks-test between the samples first to see if they showed different distributions. Afterward, the time period was used as a categorical predictor for linear regressions, with the number of collisions (and the number of people injured and killed) as dependent variables. 


<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/vehicle_collision_comp.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0 pt-8">
        {% include figure.html path="assets/img/collision_comp.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    difference of the normalized vehicle collision between 2019 and 2021
</div>

We can observe that most areas show values close to zeros, with a few outliers.

In our parking violation analysis, we looked at datasets from June of 2019 and 2021, in Brooklyn and Manhattan. The overall number of parking violations increased about 1.3 times in 2021 in both boroughs from 2019.

We processed the parking violation data the same way we processed the collision data. After filtering out the parking violations that occurred during Open Streets’ operation in 2021 and comparing it to the parking violations that occurred in the same time period and census tract, we got the total number of parking violations in the month of June in 2019 and 2021.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/BK2019.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0 pt-8">
        {% include figure.html path="assets/img/BK2021.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    parking violations mapped in Brooklyn
</div>

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/MN2019.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0 pt-8">
        {% include figure.html path="assets/img/MN2021.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    parking violations mapped in Manhattan
</div>

The results are different in Brooklyn and Manhattan. In Brooklyn, the parking violations in those Open Street census tracts decreased to about 91.63% of the number of 2019 parking violations in 2021, whereas in Manhattan the parking violations increased dramatically in 2021, to about 188.68% of the number of 2019 parking violations.

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/BK.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0 pt-8">
        {% include figure.html path="assets/img/MN.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    parking violations by Census Tracts' surrounding Open Street - normalized
</div>

Subsequently we ran T-tests for both Manhattan and Brooklyn parking violations data, however, the p values for both are above 0.05 (0.1046 and 0.1611, for Manhattan and Brooklyn, respectively), too high to be incorporated into our study.

Test results show that Open Streets have a weak influence on the number of incidents. Some of the DOT-listed Open Streets were reported not to be active. Considering whether an Open Street was operational had a significant effect on how many cars drove through the space. Based on the study, it is difficult to say that Open Streets brought a difference to street safety overall. However, we could observe some Open Streets with a noticeable increase in crashes, which might explain residents' concerns.

