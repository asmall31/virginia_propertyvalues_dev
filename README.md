# New Kent County Virginia Parcel Data

## Summary and Motivating Question

This analysis set out to better understand residential parcel data and what factors contributed to its assessed value and the price for which it was sold at. The analysis was specifically focused on New Kent County, Virginia. These factors included looking at block group demographics such as total population and finding percent of the total population that was white, black, American Indian and Asian. As well as the median age for the block group, median earnings and if they had children. 

The analysis looked specifically at the top ten residential parcels comparing the sold price/assessment value. It was analyzed to see what factors influenced these top ten parcels. This included looking at school districts, selling history and block group data. 

#### **Findings**
From this analysis there were several main findings. 
+ It was found that in the top two median earning block groups - $65,188 and $59,211 subsequently were comprised of 87% and 86% white population. The total percentage of housing owned within these block groups was 94% and 100%.
+ The lowest earning median block groups - $25,919 and $32,188 were comprised of 89% and 65% white population. The percentage owned of total housing was 89% and 65%. 
+ The top assessed land values for parcels in the County were mainly government owned. These parcels included schools, a courthouse, a hospital, a race building, a church, strip stores and a commercial building. 
+ The top ten residential parcels consisted of farmhouses, ranch style homes as well as a historical dwelling. These top parcels were very closely geographically correlated with nearby schools. 
+ There was a substantial number of parcels with no "PARCELID" attribute as these parcels had been bought by Patriots Landing Management Corporation. These parcels were bought in two phases, seeming for future development purposes. These parcels were mainly located in the city of Virginia Beach. 


## Input Data
For this analysis several data sources were used including:

Parcel data for New Kent County 
+ Available via 

Real estate data for New Kent County
+ Available via New Kent County, VA website http://www.co.newkent.state.va.us/200/Parcel-Data 

Information regarding the shape file of New Kent County 
+ Available via US Census Bureau - TIGER/Line Shapefiles: Counties https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2021&layergroup=Counties+%28and+equivalent%29 

Demographic data for New Kent County  
+ Available via US Census Bureau - American Community Survey https://www.census.gov/data/developers/data-sets/acs-5year.html
+ This data was available after downloading an individual Census API key

Information regarding the block group data
+ Available via US Census Bureau - TIGER/Line Shapefiles: Block Groups https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2021&layergroup=Block+Groups

## Repository Data
#### This repository contains *six* scripts of code
##### These scripts should be run in order 1 to 6

#### 1. virginia_NewKent.py
- This script is written in order to trim down the original real estate data
- This script ran the real estate files downloaded from the New Kent website
- The original assessment file contained 66 columns of data and some of them were irrelevant for this analysis 
- The data was trimmed down to contain 33 columns which were relevant for this analysis 
- These 33 columns were renamed to be easily to read throughout the rest of the scripts 

#### 2. trim_NK.py
- This script was written to attach the real estate trimmed down file from virginia_NewKent.py and merged it onto the parcel data from the county
- The real estate file was trimmed again as there were other states with the same name - New Kent County, not in Virginia. This was done by setting 
```
NKassessment = NKassessment.query(' STATE == "VA"')
```
- The script then trimmed down the file to only contain parcels were there was a valid "PARCELID". It is noted that many of these parcels that do not have a "PARCELID" have been bought for future development. 
- The two files were merged together using the "PARCELID" as both files contained the Parcel ID for each parcel 
- The script then looked at what the top assessed land parcels were within the county, these were found to be mostly government owned
- The script was trimmed again to only look at parcels that were residential. This was done by filtering the merged data set to drop all parcels that did not contain a value for "NUM_BED"  
- The script then looking at residential parcels only, compared the sale price for the parcel to the assessment price. The top and bottom ten parcels were identified. The top ten parcels were noted to be in close proximity to the school districts. 
- The script then looked at different features of each residential parcel such as if they were occupied, the grade, utilities and square footage. All of these characteristics can be viewed in the Tableau map

#### 3. county.py
- This script utilized the county file from the census website
- This script created a border for the county to be outlined in QGIS
- noted that New Kent County's FIPS code is 51127

#### 4. demographics.py
- This script was written to find different demographic data within New Kent County
- This script utilized the data from the American Community Survey 
- The demographics included in this script were: total population, total white population, total black population, total American Indian population and total Asian population. It also looked at sex by age and median age. It also contained information on total housing owned and rented. And finally, if there was a presence of children
- This data was run from the twelve block groups that made up the county

#### 5. NKmergedemo.py
- This script took the demographic data from demographics.py and merged it onto the block group spatial data from the US Census Bureau
- Within this script new columns were made looking at the percentage makeup of each racial group and total population. As well as the percentage makeup of owned and rented housing 
- In the top two median earning block groups the percentage total of the population that was white was 87%, and 86%. The percentage of housing that was owned was 94% and 100%. 
- In the bottom two median earning block groups the percentage total of the population that was white was 89% and 65%. The percentage of the housing that was owned was 69% and 88%. 

#### 6. join.py
- The main goal of this script was to join together the original parcel data with the real estate merged onto it, from script trim_NK.py and merge it onto the demographic data from script NKmergedemo.py 
-


## Figures

