---
layout: page
title: Flooding and Evacuation Analysis In Brooklyn
description: Using ArcGIS Pro as a Tool to Help for Better Evacuation Planning 
img: assets/img/BaseMapBKEvacZoneShelters.jpg
importance: 2
category: work
---

Ever since Hurricane Sandy hit New York City and surrounding areas a decade ago, City officials and residents alike have started to pay more and more attention to resiliency projects and flooding evacuation planning. 
New York City has implemented a comprehensive hurricane emergency evacuation system, including dividing the coastal areas into 6 evacuation zones - ranked by the risk of storm surge impact, as well as designating a number of sites on City property as Hurricane Shelters. 

There are mainly residential neighborhoods located in the 6 hurricane evacuation zones, and 18 Hurricane Shelters in Brooklyn. 

We are trying to find additional locations for Hurricane Shelters, and identifying bus stops and routes that need special attention from City officials. 

We loaded multiple related datasets to conduct the initial round of exploratory analysis. The 6 hurricane evacuation zones (see Cover Page) provided a good baseline boundary for all of our analysis. The following are the ones we thought might be of interest to our research topic, see Map No. 1, 2, 3, 4, and 5.
1. Low rise residential buildings, which are the most susceptible to flood.
2. Locations of existing Hurricane Shelters in Brooklyn, and all of them are located outside the evacuation zones.
3. Demographic characteristics in each census tract in the evacuation zones. 
4. Existing transit routes and stations in the evacuation zones.
5. Land use map of residential and non-residential lots in the evacuation zones. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/BaseMapBKEvacZoneLowRise.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Map No. 1 - low rise residential buildings
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/BaseMapBKEvacZoneShelters.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Map No. 2 - existing Hurricane Shelters in Brooklyn
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/BaseMapBKEvacZonePovertyDisabledCensusTracts.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Map No. 3 - demographic characteristics in each census tract in the evacuation zones
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/BaseMapBKExistingMTABus.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Map No. 4 - existing transit routes and stations in the evacuation zones
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/BaseMapBKEvacZoneNonRes.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Map No. 5 - land use map of residential and non-residential lots in the evacuation zones
</div>
To examine if the number of shelters meet the need, we decided to look at the disabled population living in the hurricane evacuation zones (about 9230 from the 2020 Census). Other vulnerable populations (like the elderly or people living below the poverty line) are too large to be meaningful. 

With the total disabled population (9720) and number of existing shelters (18) available, we will have that the current baseline is 513 disabled people per evacuation center. We then looked at the average floor area of the public schools in Brooklyn, and it is 50,000 SF per school. Since most disabled populations would need some type of special care during distressed situations, I used NYC Building Code’s use group Institutional-2 Sleeping Room (120 SF per Occupant1) to calculate the average capacity of each hurricane shelter. Based on these numbers, we can calculate that each school on average can house about 416 disabled people; a total of 22 shelters is needed to house all the disabled people inside the evacuation zones; and an additional 4 shelters will be needed.

With this information, we looked to identify where the optimal locations of these shelters would be. We first need to exclude all the public schools that are located inside the evacuation zones, then we look at the distribution of disabled population in those census tracts. Our ideal solution will be to divide the evacuation zones into 4 areas, each having the approximately same number of total disabled population. However, that would be difficult to implement as it requires computer graph theory knowledge. Our solution instead was to find these 4 shelters based on the approximate total disabled population, and proximity to those census tracts. 

At the same time, ensuring that these populations have easy access to shelter during a hurricane is a crucial part of disaster preparedness and response. Because of their relatively easy operation and accessibility, we picked MTA buses instead of MTA subway. We then spatially joined the bus stop dataset (locations, station name and route name) with the disabled population census tracts dataset. After setting the disabled population to be above 50, we filtered out these bus stops and routes that might need special attention during hurricane evacuation. Transit and City officials can potentially increase those bus routes’ frequency, and check the bus stops’ curb condition to make sure that people could access the buses.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/BaseMapBKFutureShelterLocations.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    sites of 4 potential hurricane shelters 
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/BusStopDisabled.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    bus stops and routes that might need special attention during hurricane evacuation 
</div>

From our analysis, we can see that Hurricane Shelters in Brooklyn are slightly over capacity based on disabled population, however, only additional 4 shelters will be needed. The existing bus stops are adequate for evacuation use but special attention will be paid to areas with high disabled population density. In the future, we wish to find out how to generate the four evacuation centers by algorithm instead of a manual selection. 

