# Potential Impacts of 5ft Sea Level Rise on Atlantic City, New Jersey<br/>
## Jonathan DeLura, Rutgers University

It was predicted with 17% confidence by the [2019 STAP Report](https://climatechange.rutgers.edu/resources/climate-change-and-new-jersey/nj-sea-level-rise-reports), that the Atlantic Ocean would rise by 5ft by the year 2100 along the New Jersey Coast. The following pdf maps and interactive map, created by Jonathan DeLura, as a final project for Command Line GIS, offered as part of the Master of Public Informatics program at the Rutgers University Edward J. Bloustein School of Planning and Public Policy, visualize the potential impact of this Sea Level Rise (SLR) on the tax base and some of the critical infrastucture in Atlantic City, New Jersey.

<iframe src="Atlantic_City_5ft_SLR.pdf" width = "1000" height = "1035"></iframe><br/>

<iframe src="Atlantic_City_Parcel_Census_BG.pdf" width = "1020" height = "1000"></iframe><br/>

You can also explore [this map as its own web page here](Atlantic_City_5ft_SLR.html)

### Notes:

From National Historical Geographic Information System, the Shoreline-Clipped Block Group shapefile provided earlier in this class was used. From the New Jersey Geographic Information Network, Municipal Boundaries of NJ, School Point Locations of NJ, Hospitals in NJ, as well as the most current Parcels and MOD-IV Composite of NJ, which includes 2022 tax data, were used. For Census data, the US Census API was used to access 2019 ACS Census Block Group Total Population and Median Household Income data for Atlantic County. For long-term care facilities (LTCF), the Long-Term Care Facilities of New Jersey geojson, provided earlier in this class, was used. To represent 5ft SLR, a 5ft Total Water Level (TWL) dataset created by the author for the NJAES Office of Research Analytics was used.
Because of the size of the Parcels and MOD-IV Composite dataset, it was cliped to Atlantic City in ArcPro before reading it in. For the 5ft TWL datasets, all polygons were dissolved and they were clipped to both Atlantic County and Atlantic City before reading in.

To create the Census and Parcel Data by Block Group geodataframe (ac_parcel_mod4_5ftTWL_bg), the Atlantic County Census data was merged with the Atlantic City block group geometry, which effectively clipped it to Atlantic City. The Parcel dataset was then spatially joined with the block group geometry to determine which block group each parcel was within. Next, the parcel block group geodatframe was spatially joined with the 5ft TWL geometry, to determine which parcels intersected the flood zone. The total number of parcels and total net assessed value as well as the number of intersecting parcels, and the net assessed value of these parcels were then grouped and aggregated by block group. From these fields, the percent of parcels and the percent of net assessed value that were vulnerable to 5ft SLR by block group were calculated. Last, the parcel data by block group geodataframe was merged with the Census data by block group geodataframe.
The critical infrastructure layer was created by concatenating the hospitals, schools, and LTCF datasets. To do this the names of some columns had to be changed so they matched.

The parcel and critical infrastructure geodataframes were spatially joined with the 5ft TWL level geodataframe to determine which parcels and sites intersected it. This is not an accurate way to determine inundation for parcels, because it does not show how much of each parcel intersects with the flood zone, but the author was not sure how to run Zonal Statistics or a similar process in GeoPandas. This is why intersecting parcels are referred to as “vulnerable” as opposed to “inundated.” Atlantic City 5ft TWL was used for spatial joins because it was smaller in size, but the Atlantic County 5ft TWL level for the interactive map, so the flood zone did not end awkwardly at the municipal boundary. 

The first static map simply visualizes the parcels and the critical infrastructure points in relation to the flood zone to introduce the subject matter. It does not provide any detailed information. The second static map shows the choropleth maps initially intende to be included in the interactive map. They were not included in the interactive map because the choropleth legends did not look good and overlapped with other map elements. The compromise was to include them in their own map and include their data in the pop-ups of the interactive map. The interactive map includes all the data processed for the entire project. The parcel layer was not included to keep the size of the file small enough to upload to GitHub.

Data sources:
2019 STAP report: https://climatechange.rutgers.edu/resources/climate-change-and-new-jersey/nj-sea-level-rise-reports<br/>
Municipal Boundaries of NJ: https://njogis-newjersey.opendata.arcgis.com/datasets/1c6b26a9a14e4132895194e80d6b30f8_0/explore<br/>
School Point Locations of NJ: https://njogis-newjersey.opendata.arcgis.com/datasets/d8223610010a4c3887cfb88b904545ff/explore<br/>
Hospitals in NJ: https://njogis-newjersey.opendata.arcgis.com/datasets/newjersey::hospitals-in-nj/explore<br/>
Parcels and MOD-IV Composite of NJ: https://njogis-newjersey.opendata.arcgis.com/documents/406cf6860390467d9f328ed19daa359d/about<br/>

