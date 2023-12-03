# PV-Power-Generation-Prediction
Built deep learning models to predict the amount of photovoltaic power generation for each generator

## 1. Topic description
+ The Korean government has announced a plan of increasing the proportion of renewable energy, especially focusing on photovoltaic solar power.
+ Variability of solar power makes the prediction difficult, which is crucial to achieve the goal.
+ 1st goal : Identifying the climate factors that have significant impact,specific to each power plant
+ 2nd goal : Analyzing the relationship between climate factors & solar power generation / each climate factors
+ 3rd goal : Proposing optimal conditions to maximize solar power generation,specialized for each power plant

## 2. Data
+ 1st source : The amount of power generation of each generator unit of each power plant, for each hour from 9 power plants between 22.01 and 23.10
+ 2nd source : Hour basis climate data for each region, including temperature, humidity, and cloud, etc. from 9 regions between 22.01 and 23.10
+ 3rd source : The time of sunrise and sunset in Korea, for each date between 22.01 and 23.10
+ We make training Data set by integrating Power Generation Data, Sunrise/Sunset Data, Climate Data

## 3. Preprocessing
### 1) Preprocess Power Generation Data
#### 1.1 Combine Power Generation of Every Month
+ The raw data of power generation can be obtained for each month from 2022.01 – 2023.10. So we had to combine them for a single dataset
















