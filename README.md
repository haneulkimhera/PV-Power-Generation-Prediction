# PV-Power-Generation-Prediction
Built Machine learning models to predict the amount of photovoltaic power generation for each generator

## 1. Topic description
+ The Korean government has announced a plan to increase the proportion of renewable energy, especially focusing on photovoltaic solar power.
+ Variability of solar power makes the prediction difficult, which is crucial to achieving the goal.
+ 1st goal: Identifying the climate factors that have a significant impact, specific to each power plant
+ 2nd goal: Analyzing the relationship between climate factors & solar power generation / each climate factors
+ 3rd goal: Proposing optimal conditions to maximize solar power generation, specialized for each power plant

## 2. Data
+ 1st source: The amount of power generation of each generator unit of each power plant, for each hour from 9 power plants between 22.01 and 23.10
+ 2nd source: Hour basis climate data for each region, including temperature, humidity, and cloud, etc. from 9 regions between 22.01 and 23.10
+ 3rd source: The time of sunrise and sunset in Korea, for each date between 22.01 and 23.10
+ We make training Data set by integrating Power Generation Data, Sunrise/Sunset Data, Climate Data

## 3. Preprocessing
### 1) Preprocess Power Generation Data
#### 1.1 Combine Power Generation of Every Month
+ The raw data of power generation can be obtained for each month from 2022.01 – 2023.10. So we had to combine them for a single dataset.
#### 1.2 Extract PV Generation Data
+ The raw data includes all power generation data, not only PV generation like fuel cell, wind power, steam power, etc. So, we had to extract only PV generation data.
#### 1.3 Reshape PV Generation Data
+ In the original file, data points are based on date and the power generation of each hour is represented as individual features. So, Each data point should be the amount of power generation of each hour, for each date and each generator.
+ After reshaping, the ‘date’ column now includes time information, the columns for each hour have disappeared, and a single power generation column that represents the generation of the corresponding time has been created.

### 2) Filter using Sunrise/Sunset Data
#### 2.1 Merge Sunrise/Sunset Data into PV Generation Data
#### 2.2 Filter Datapoints Between Sunrise – Sunset
+ The original power generation data includes power generation every hour of the day. Because there can not be PV power generation without sunlight, we considered those to be wrong data. So we had to cut it based on the time of sunset-sunrise, only to consider the time when the sun is up.
+ After filtering, The dataset now only includes data points that are within the range from sunrise to sunset

### 3) Merge Climate Data
#### 3.1 Merge Climate Data into PV Generation Data
+ Create a 'region' column in PV generation using the get_region() method, to map the climate data of a region to the corresponding region.
+ Merge climate data with PV generation data to the corresponding region and date, using the ‘region’ & ‘date’ columns.

### 4) Merge Climate Data
























