# Predicting Air Turbulence with Machine Learning

## Description
Air turbulence is the irregular and unpredictable movement of air that can cause sudden jolts or shakes during a flight. It occurs due unstable airflow around an aircraft. While usually not dangerous, turbulence can be uncomfortable for passengers and pose challenges for pilots.

In recent years, incidents of air turbulence have been on the rise due to climate change, causing significant concern amongst airlines and passengers. Therefore, the aim of this project was to build a machine learning model to accurately predict air turbulence. Predicting turbulence is crucial for enhancing flight safety, reducing discomfort for passengers, and optimizing flight operations. By leveraging multiple data sources, including pilot reports, meteorological data, and aircraft specifications, this model aims to provide more accurate turbulence predictions, helping pilots and airlines make informed decisions.

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

## Key Features
Exploratory Data Analyses (EDA) revealed that these were the key predictors of air turbulence:
* Wind speed: Turbulence is worse with higher wind speeds
* Temperature: Turbulence is worse with higher temperatures
* Season: Turbulence is worse during winter and calmest during summer
* Time of day: Turbulence is worse during the day and calmest during the night/sunrise
* Ground elevation: Turbulence is worse when the ground is elevated
* Flight level: Turbulence is calmest at cruising altitude (30,000-40,000 ft)
* Weight class: Turbulence is worse for smaller aircrafts

## Results
Four classifiers were built: Random Forest, Decision Tree, XGBoost, and CatBoost

The aim of these ML models was to learn from the dataset and to predict and classify the severity of turbulence into 3 categories: Light, Moderate, or Severe.

The following table summarizes the performance of the models:
| Model | Train Accuracy | Test Accuracy | Train-test Difference | Runtime |
| --- | --- | --- | --- | --- |
| Decision Tree | 99.66% | 69.84%	| 29.82% | 20.6s |
| Random Forest | 81.67% | 81.58%	| 0.09% | 1m 50s |
| XGBoost | 81.85% | 81.58%	| 0.27% | 1m 28s |
| CatBoost | 81.66% | 81.57%	| 0.09% | 3m 54s |

By evaluating the trade-offs between train and test accuracy, model discrepancies, and runtime, XGBoost was been identified as the best model for demonstrating superior performance with no significant overfitting.

## Conclusion
This analysis is proof of concept that turbulence severity can be predicted relatively accurately using machine learning models. By utilizing a mega dataset of historical turbulence (over 1.5 million observations), the model uniquely predicts turbulence using ground-based meteorological data instead of data from plane sensors, and without traditional turbulence metrics commonly studied in the literature.

However, it is recommended that this analysis be repeated with real-time data from plane sensors to enhance its accuracy. Ground-based meteorological data may not be reflective of atmospheric conditions at various altitudes, and plane sensors also provide additional information on weather conditions in the air (e.g., wind shear, vertical wind gust, etc.). Ultimately, it is recommended that airlines integrate machine learning models into flight plans and pilot dashboards to help predict turbulence in real-time, in order to achieve smoother and safer flights for all. 

## Project Structure
project-folder/
<br>│── README.md
<br>│── 01_Code/
<br>│   │── Capstone_01_Importing_Data.ipynb
<br>│   │── Capstone_02_Data_Cleaning_and_Merging.ipynb
<br>│   │── Capstone_03_Feature_Engineering.ipynb
<br>│   │── Capstone_04_EDA.ipynb
<br>│   │── Capstone_05_Modelling.ipynb
<br>│── 02_Data/
<br>│── 03_Report/
<br>│── 04_Slides/
