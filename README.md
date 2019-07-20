# UFO_mapping

Extract:
For this project we decided to do an analysis of UFO Sightings and compare this with the location of military databases in the United States. For the analysis we used two csv files imported from Kaggle and Open Data Soft. Both files were imported into Jupyter notebook for analysis and transformation.
•   Data Source: Military Bases (https://public.opendatasoft.com/explore/dataset/military-bases/export/)
o   Format: CSV

•   Data Source: UFO Sightings (https://www.kaggle.com/NUFORC/ufo-sightings)
o   Format: CSV

Transform:
Our first steps in cleaning up the datasets involved figuring out which variables were not relevant. For the UFO sightings data set we dropped the duration (seconds), duration (hours/min) and comments columns. After dropping the columns we filtered by country selecting the US only. 
 
After this we dropped duplicate rows with and rows with NA values and renamed the country from “us” to “United States”. 
 
Moving on to the military bases file 8 columns were dropped and renamed the remaining columns to Base Status, state, Base Name, Base Type, latitude, country and longitude. We filtered the remaining information by country keeping only data for the United States. After this we dropped duplicates keeping only the first row of each “Base name”. This was done to ensure we didn’t have duplicate coordinates for the location of each base. Finally NA values were dropped to ensure only rows with information were kept.

For the analysis two different methods were considered to join the tables.
A simple first approximation was to use matching citynames, to get bases and sightings that happened very close to one another.
However, the more useful (and computationally interesting) method was to calculate the distance to the nearest miltary base (and nearest airforce base) for each of the remaining 63k+ sightings. 

This calculated, the tables could be loaded into postgres and the closest base names could be used as the joining element, many-to-one, from bases to sightings, to determine if there were any commonalities or other oddities. In order to fully determine if there is anything statistically significant about the recorded sightings however, a density map of population within the united states would be required. It isn't enough to simply say that the average sighting occurs within 
