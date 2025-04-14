# Predicting Air Turbulence with Machine Learning
![image](https://github.com/user-attachments/assets/6524f930-dc0f-4bb0-9fcc-c7aa7a3548fb)

## Description
Air turbulence is the irregular and unpredictable movement of air that can cause sudden jolts or shakes during a flight. It occurs due unstable airflow around an aircraft. While usually not dangerous, turbulence can be uncomfortable for passengers and pose challenges for pilots.

In recent years, incidents of air turbulence have been on the rise due to climate change, causing significant concern amongst airlines and passengers. Therefore, the aim of this project was to build a machine learning model to accurately predict air turbulence, specifically over U.S mainland from 2015-2024. Predicting turbulence is crucial for enhancing flight safety, reducing discomfort for passengers, and optimizing flight operations. By leveraging multiple data sources, including pilot reports, meteorological data, and aircraft specifications, this model aims to provide more accurate turbulence predictions, helping pilots and airlines make informed decisions.
![image](https://github.com/user-attachments/assets/bb268555-01fc-4309-915b-4b936f3bc6cb)

## Data Sources
All data were extracted from official U.S. government agencies using Application Programming Interface (API):

1) Pilot reports (PIREPs): [Iowa State University Environmental Mesonet](https://mesonet.agron.iastate.edu/request/gis/pireps.php)

2) Meteorological data: [Iowa State University Environmental Mesonet](https://mesonet.agron.iastate.edu/request/daily.phtml#)

3) Elevation data: [United States Geological Survey (USGS)](https://apps.nationalmap.gov/epqs/)

4) Aircraft specifications: [International Civil Aviation Organization (ICAO)](https://www.icao.int/publications/DOC8643/Pages/Search.aspx)

## Data Dictionary
The following table details the data and their respective sources:
| Source	| Feature	| Column Name	| Description	| Data Type |
| --- | --- | --- | --- | --- |
| Pilot Reports (PIREPs)	| Date and time	| DATETIME	| Local date and time of report | Datetime |
|  |	Time of day	| TIME_OF_DAY	| When: Day, night, sunrise, or sunset	| String |
|  |	Year	| YEAR	| Year of report	| Integer |
|  |	Hour	| HOUR	| Hour of report	| Integer |
|  |	Month	| MONTH	| Month of report	| Integer |
|  |	Season	| SEASON	| When: Spring, summer, autumn, winter	| String |
|  |	Flight level	| FL	| Flight level of incident (ft)	| Integer |
|  |	Distance	| DISTANCE_TO_GROUND	| Distance to ground (ft)	| Integer |
|  |	Aircraft	| AC	| Aircraft type designator	| String |
|  |	Turbulence	| TURB_CAT	| Category of turbulence	| String |
|  |	Severity	| TURB_DEG	| Severity of turbulence	| Integer |
|  |	Longitude	| LON	| Longitude of report	| Integer |
|  |	Latitude	| LAT	| Latitude of report	| Integer |
|  |	State	| STATE	| State of location	| String |
|  |	Urgent	| URGENT	| Whether the report was filed as urgent	| Boolean |
| Elevation (USGS)	| Elevation	| ELEV	| Ground elevation at location (ft)	| Integer |
| Aircraft Specs (ICAO)	| Manufacturer	| MANUFACTURER	| Manufacturer of plane	| String |
|  |	Model	| MODEL	| Model of plane	| String |
|  |	Description	| DESCRIPTION	| Type of plane	| String |
|  |	Engine type	| ENGINE_TYPE	| Type of engine	| String |
|  |	Engine count	| ENGINE_COUNT	| Number of engines	| Integer |
|  |	Weight class	| WTC	| Weight class of plane	| String |
| Meteorological data (NWS)	| Wind speed	| WIND	| Daily average wind speed at location	| Integer |
|  |	Wind direction	| WIND_DRCT	| Daily average wind direction at location	| Integer |
|  |	Cardinal wind	| WIND_DIR	| Daily average cardinal wind direction	| String |
|  |	Max temp	| MAX_TEMP	| Daily maximum temperature at location	| Integer |
|  |	Min temp	| MIN_TEMP	| Daily minimum temperature at location	| Integer |
|  |	Humidity	| HUM	| Daily relative humidity at location	| Integer |

## Exploratory Data Analyses
Exploratory Data Analyses (EDA) revealed that these were the key predictors of air turbulence:
* Wind speed: Turbulence is worse with higher wind speeds
  ![image](https://github.com/user-attachments/assets/92345592-f1ab-4073-9921-de3fca34628c)

* Temperature: Turbulence is worse with higher temperatures
  ![image](https://github.com/user-attachments/assets/28315eb6-27e7-4baa-b7b7-6afcaab24ded)

* Season: Turbulence is worse during winter and calmest during summer
  ![image](https://github.com/user-attachments/assets/a1ccf44a-15d2-4372-bd0d-7ae1ee686211)

* Time of day: Turbulence is worse during the day and calmest during the night/sunrise
  ![image](https://github.com/user-attachments/assets/61cb5a9e-94f6-4ed1-821a-90ef76abbcf4)

* Ground elevation: Turbulence is worse when the ground is elevated
  ![image](https://github.com/user-attachments/assets/e0aee959-030e-4cfb-9953-ff68206ba246)

* Flight level: Turbulence is calmest at cruising altitude (30,000-40,000 ft)
* Weight class: Turbulence is worse for smaller aircrafts

The following density heatmap shows the severity of turbulence across U.S. mainland. 
![image](https://github.com/user-attachments/assets/eed3eb72-ab34-4eea-abb1-9c33e3c2b184)
1) Evidently, areas near high altitudes (around the mountains) typically experience greater turbulence. The main reason is that the air is forced up and down as it passes through mountains, and this generates a wide range of turbulent structures that can shake the plane. This turbulence can propagate far from the mountains, sometimes in the form of rolling trains of vortices known as mountain waves. At cruising altitudes the wind in the U.S. is from west to east, therefore, most of the turbulence is located at the eastern side of the mountains.
2) In contrast, the Great Plains and Great Lakes states (North Dakota, South Dakota, Minnesota, Iowa, Wisconsin) present the lowest levels of turbulence in the U.S., with the flat terrain being an important factor. The plains are also sheltered from the Pacific and Atlantic winds by the Rockies and Appalachians. These two factors bring a peaceful patch of air with very low turbulence levels.
3) Lastly, turbulence levels around the south (Texas, Louisiana, Mississippi) are also large due to the Gulf of Mexico's warm waters, which enhance convection, moisture, and instability in the atmosphere. Land-sea breezes, warm eddies from the Loop Current, and river plume interactions further contribute to vertical air movement and turbulent weather. Additionally, the region is frequently impacted by tropical systems that intensify atmospheric disturbances.

## Results
Four classifiers were built: Random Forest, Decision Tree, XGBoost, and CatBoost

The aim of these ML models was to learn from the dataset and to predict and classify the severity of turbulence into 3 categories: Light, Moderate, or Severe.

The following table summarizes the performance of the models:
![image](https://github.com/user-attachments/assets/33942ac8-e57c-484d-9253-e90d6d573d5b)

By evaluating the trade-offs between train and test accuracy, model discrepancies, and runtime, XGBoost was been identified as the best model for demonstrating superior performance with no significant overfitting.

## Conclusion
This analysis is proof of concept that turbulence severity can be predicted relatively accurately using machine learning models. By utilizing a mega dataset of historical turbulence (over 1.5 million observations), the model uniquely predicts turbulence using ground-based meteorological data instead of data from plane sensors, and without traditional turbulence metrics commonly studied in the literature.

However, it is recommended that this analysis be repeated with real-time data from plane sensors to enhance its accuracy. Ground-based meteorological data may not be reflective of atmospheric conditions at various altitudes, and plane sensors also provide additional information on weather conditions in the air (e.g., wind shear, vertical wind gust, etc.). Ultimately, it is recommended that airlines integrate machine learning models into flight plans and pilot dashboards to help predict turbulence in real-time, in order to achieve smoother and safer flights for all. 

## Project Structure
project-folder/
<br>│── README.md
<br>│── 01_Code/
<br>│   │── Code_01_Importing_Data.ipynb
<br>│   │── Code_02_Data_Cleaning_and_Merging.ipynb
<br>│   │── Code_03_Feature_Engineering.ipynb
<br>│   │── Code_04_EDA.ipynb
<br>│   │── Code_05_Modelling.ipynb
<br>│── 02_Data/
<br>│   │── Raw
<br>│   │   │── combined_data.csv
<br>│   │   │── elevation.csv
<br>│   │   │── ICAO_aircraft_type.csv
<br>│   │   │── PIREPs_all.csv
<br>│   │   │── weather_all.csv
<br>│   │── Cleaned
<br>│   │   │── cleaned_data.csv
<br>│── 03_Report/
<br>│── 04_Slides/
