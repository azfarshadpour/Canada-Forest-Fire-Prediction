# Forest-fire-intensity-prediction 
The purpose of this project is to predict the intensity of fires in Canada's wildlife according to the geographical coordinates of an area using supervised machine learning multi-classification algorithms.

For this project data is collected from NASA data (https://firms.modaps.eosdis.nasa.gov/download/), Viirs instruments, for the perid of 2021. 

In this repository you will find two notebooks for Exploratory data analysis(EDA) and modeling process. 

Below is the description of features in the dataset based on NASA website: https://earthdata.nasa.gov/earth-observation-data/near-real-time/firms/v1-vnp14imgt#ed-viirs-375m-attributes

# Feature Descriptions:

- Latitude : Center of nominal 375 m fire pixel 
- Longitude : Center of nominal 375 m fire pixel 
- Bright_ti4 : Brightness temperature I-4  - VIIRS I-4 channel brightness temperature of the fire pixel measured in Kelvin
- Scan : Along Scan pixel size - The algorithm produces approximately 375 m pixels at nadir. Scan and track reflect actual pixel size. 
- Track : Along Track pixel size - The algorithm produces approximately 375 m pixels at nadir. Scan and track reflect actual pixel size. 
- Acq_Date : Acquisition Date - Date of VIIRS acquisition. 
- Acq_Time : Acquisition Time - Time of acquisition/overpass of the satellite (in UTC). 
- Satellite : N= Suomi National Polar-orbiting Partnership (Suomi NPP) 
- Confidence : This value is based on a collection of intermediate algorithm quantities used in the detection process. It is intended to help users gauge the quality of individual hotspot/fire pixels. Confidence values are set to low, nominal and high. Low confidence daytime fire pixels are typically associated with areas of sun glint and lower relative temperature anomaly (<15K) in the mid-infrared channel I4. Nominal confidence pixels are those free of potential sun glint contamination during the day and marked by strong (>15K) temperature anomaly in either day or nighttime data. High confidence fire pixels are associated with day or nighttime saturated pixels. 
- Version : Version (Collection and source) - Version identifies the collection (e.g. VIIRS Collection 1) and source of data processing: Near Real-Time (NRT suffix added to collection) or Standard Processing (collection only). 
"1.0NRT" - Collection 1 NRT processing. 
"1.0" - Collection 1 Standard processing. 
- Bright_ti5 : Brightness temperature I-5 - I-5 Channel brightness temperature of the fire pixel measured in Kelvin. 
- FRP : Fire Radiative Power - FRP depicts the pixel-integrated fire radiative power in MW (megawatts). Given the unique spatial and spectral resolution of the data, the VIIRS 375 m fire detection algorithm was customized and tuned in order to optimize its response over small fires while balancing the occurrence of false alarms. Frequent saturation of the mid-infrared I4 channel (3.55-3.93 µm) driving the detection of active fires requires additional tests and procedures to avoid pixel classification errors. As a result, sub-pixel fire characterization (e.g., fire radiative power [FRP] retrieval) is only viable across small and/or low-intensity fires. Systematic FRP retrievals are based on a hybrid approach combining 375 and 750 m data. In fact, starting in 2015 the algorithm incorporated additional VIIRS channel M13 (3.973-4.128 µm) 750 m data in both aggregated and unaggregated format. 
- Type: Inferred hot spot type 
   - 0 = presumed vegetation fire
   - 1 = active volcano
   - 2 = other static land source
   - 3 = offshore detection (includes all detections over water) 
- DayNight : Day or Night - D= Daytime fire, N= Nighttime fire 
# Data pre-proccessing 

Before starting this step data splitted into 70% train and 30% test sets.  

During EDA proccess, an imbalanced pattern in classes determind. This skewness would couse bias in prediction and therfore a poor performance in the model, hence I applied SMOTE an oversampling technique to handle this problem. 

Feature selection is done with correlation matrix and features with negative correlation are removed 

# Modeling step 

This step started with defining target variable which is 'confidence'(y) and then dropping from dataframe to define independant variables(X). 

Because it is a multi-classification problem the following algorithms are tested to check which one has a better accuracy. 
- Naive bayes classifier
- Random Forest
- XGboost 

For Random Forest and XGBoost hyperparameters are tunned with Gridsearch. 
As a result and after measuring metrics such as precision, recall, f1 score as well as confusion matrix, Random Forest and XGboost demonstrate an accuracy of 98.76% for test set. 






