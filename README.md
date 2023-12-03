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

### 4) Disunite for Each Power Plant
+ Disunite the dataset into 9 individual datasets for each solar power plant to consider the specific characteristics of each power plant. There are several generators in each power plant.
+ To integrate the several units in Samcheonpo and Yeongheung power plants into one value, we calculated the weighted average value based on each unit’s capacity at each time and then summed up these values. So, we could get one generation amount value in each time.

### 5) Handle Missing Values
#### 5.1 Drop features with high null percentage
+ Remove columns if a column has a proportion of null values of 40% or more. After removing columns, we interpolated the remaining null values using Linear Interpolation method.
#### 5.2 Interpolate null values
+ We use Linear Interpolation Method


## 4. Feature Engineering
  1) Extract the month, day, and hour information from the data to generate new features.
  2) To compensate for the inability to well represent cyclicity in a 1D linear representation, we use a circular coordinate system.
  3) Each unit (month, day, hour) is mapped onto a circle, preserving its cyclicity. This is done by multiplying the unit by the ratio of 2π to the maximum value of the unit, and then taking the sine and cosine of the result.
  4) Through this process, new features named 'month_x', 'month_y', 'day_x', 'day_y', 'hour_x', 'hour_y' are created. These represent the sine and cosine values of the month, day, and hour.
  5) With these generated features, the machine learning model can understand the cyclical nature of time, enabling it to make more accurate predictions.


## 5. Make Model
### 5.1 Random Forest Regression
+ Random Forest regression is an ensemble technique performing both regression and classification with the use of multiple decision trees.
+ The model is used to predict the amount of PV power generation, which has a large variation, using Climate and PV performance data set.
### 5.2 XGBoost Regression
+ XGBoost regression is the implementation of gradient boosting for regression predictive modeling and has very good prediction.
+ The model is used to predict the amount of PV power generation, which has a large variation, using Climate and PV performance data set.
### 5.3 LightGBM Regression
+ Light GBM is a gradient-boosting framework that uses tree-based learning algorithms. It's designed for distributed and efficient training and is particularly useful for large datasets.
+ The model is employed to predict the amount of PV power generation using Climate and PV performance datasets.
### 5.4 CatBoost Regression
+ CatBoost is another gradient-boosting algorithm designed to handle categorical features seamlessly.
+ The model is utilized to predict the amount of PV power generation based on the Climate and PV performance datasets.


## 6. Evaluation























