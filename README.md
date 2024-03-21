# Carbon Emissions Prediction Based on Car Model Analysis in North America
## Introduction

Urban planning in North America is designed to prioritize unlimited convenience for car drivers, often neglecting public transportation. As a result, people have limited options other than using cars for mobility. This phenomenon is highly problematic in the current climate crisis era, as studies have shown that a car-centric lifestyle is a major contributor to climate change. The United States, for instance, accounts for 29% of total greenhouse gas emissions from the transportation sector, making it the largest source compared to other sectors. This percentage is 5% higher than the transportation emissions proportion of European Union countries. Even more significant when compared to other developed countries like the Netherlands, where transportation emissions constitute 12.5% (European Parliamentary Research Service, 2021).

These figures highlight the need to transform the transportation sector into a more efficient and sustainable one in order to reduce carbon emissions. Unfortunately, the shift from private car usage to public transportation has not significantly occurred. Instead, there is a worrying trend in North America where consumers are increasingly inclined to purchase SUVs, which consume more fuel compared to smaller car models. The higher fuel consumption of SUVs is positively correlated with greenhouse gas emissions. If large vehicles like SUVs continue to dominate the roads, it is predicted that global transportation-related greenhouse gas emissions will further increase.

Given this background, it is necessary to investigate the relationship between the characteristics of a car model and its emission levels. These characteristics may include vehicle class, engine size, cylinders, transmission, and fuel type. The findings from such investigations can serve as a basis for formulating appropriate regulations related to the automotive industry, particularly for high-emission car products.

## Project Goals
The objectives of this final project are as follows:

- Identify the differences in carbon emission output between two groups of car types with different characteristics.
- Determine the relationship between the variables using regression analysis.
- Predict the emission levels (outcome variable) based on the predictor variables of car characteristics using a regression model.

## Datasets

### Description

The dataset used is obtained from the official website of the Canadian government and re-uploaded on Kaggle by Podder (2020). The dataset contains information on CO2 emission values with 11 features related to the characteristics of a car type from the year 2020 in Canada. The features in the dataset are as follows (Figure 1):

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/1.png" />
</div>

<p align="center"><em>Figure 1. The dataset features.</em></p>

The CO2 emissions feature is the outcome variable, while the other 10 features are predictor variables. Out of these ten predictors, three are categorical variables and the remaining seven are numerical.

### Cleaning and transformation

The original dataset has 7385 rows and 12 columns. After removing the duplicates, the total number of rows is reduced to 6282. Null data was not found in this dataset. The "Make" feature, which represents the manufacturer, will be removed. And also the "Model" feature. The two features contain too many unique names.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/2.png" />
</div>

<p align="center"><em>Figure 2. Correlation heatmap between features.</em></p>

From the correlation heatmap (Figure 2), it can be observed that the features "Fuel Consumption City (L/100 km)" and "Fuel Consumption Hwy (L/100 km)" have a near-collinear relationship with the feature "Fuel Consumption Comb (L/100 km)". This is not surprising since the latter feature represents the aggregation of fuel consumption in urban and highway driving conditions. Based on this, the project will only use the combined fuel consumption feature. The feature "Fuel Consumption Comb (mpg)" is also removed because it essentially represents the same information as "Fuel Consumption Comb (L/100 km)" but in a different unit of measurement.
This project adopts some approaches used by Podder, such as modifying the unique names in the "Fuel Type" feature to make the data easier to understand. Another adoption is reducing the unique names in the "Transmission" feature from 27 to only 5 types of transmissions.
### Distribution
From the categorical features in the dataset, distribution patterns can be observed. In the "Fuel Type" feature, regular and premium gasoline are the most dominant compared to ethanol and diesel (Figure 3). There is also a single entry for natural gas in the dataset. This entry is considered an outlier and hence removed. The "Transmission" feature indicates a significant dominance of automatic transmissions and their variants compared to manual transmissions (Figure 4). The "Vehicle Class" feature covers 16 car models. Small-sized SUVs have the highest frequency, while standard-sized SUVs rank fourth (Figure 5). This distribution pattern reveals a trend of manufacturers abandoning practical car models such as station wagons, pickup trucks, vans, and minivans. A practical model refers to a car design with sufficient cargo and passenger capacity without excessively large dimensions. In contrast with SUV models, which tend to have large dimensions but limited cargo capacity.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/3.png" />
</div>

<p align="center"><em>Figure 3. Distribution for the "Fuel Type" feature</em></p>

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/4.png" />
</div>

<p align="center"><em>Figure 4. Distribution for the "Transmission" feature</em></p>

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/5.png" />
</div>

<p align="center"><em>Figure 5. Distribution for the "Vehicle Class" feature</em></p>

### Relationships among variables

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/6.png" />
</div>

<p align="center"><em>Figure 6. Vehicle Class vs Engine Size</em></p>

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/7.png" />
</div>

<p align="center"><em>Figure 7. Relationship between two predictors (Engine Size and Fuel Type) and CO2 Emission</em></p>

From Figure 6, it is evident that there is a positive correlation between the size of the car model and the engine size. As the dimensions of a car type increase, so does the engine size. The engine size itself (as shown in Figure 2) correlates positively with fuel consumption and CO2 emissions. Furthermore, as seen in Figure 7, larger engine sizes tend to use premium gasoline, specifically engine sizes ranging from 3 liters to above 8 liters. On the other hand, regular gasoline is typically used in car types with engine sizes ranging from one to four liters.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/8.png" />
</div>

<p align="center"><em>Figure 8. Vehicle Class vs CO2 Emission</em></p>

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/9.png" />
</div>

<p align="center"><em>Figure 9. Vehicle Class vs Combined Fuel Consumption (Urban and Highway)</em></p>

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/10.png" />
</div>

<p align="center"><em>Figure 10. Vehicle Class vs Cylinders</em></p>

We can also observe the distribution comparison of each car model in Figure 8. The interquartile range of the sixteen categories indeed indicates an increase in carbon emission values. In the small station wagon category which has the smallest engine size, the interquartile range for this category ranges from 190 to 230 g CO2/km. Meanwhile, the passenger van falls within the range of 350 to 450 g CO2/km. Furthermore, this distribution pattern appears to be almost identical to the distribution pattern between "Vehicle Class" and "Fuel Comb (L/100 km)" (Figure 9), as well as with "Cylinders."

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/11.png" />
</div>

<p align="center"><em>Figure 11. Final Dataset</em></p>



The final dataset can be seen in Figure 11. The dataset consists of six predictor features and one outcome variable. Among the predictors, there are three categorical features and three numerical features.


## Statistical Test
The statistical test focuses on comparing the impact of vehicle models in the "Vehicle Class" feature on carbon emissions (the "CO2 emission (g/km)" feature). The t-test is used for statistical analysis due to the unequal sample variance and unknown population standard deviation. Before conducting the test, it is important to ensure that sample members from the compared groups are sufficiently representative. Therefore, other influential variables need to fall into a similar category. The variables here are "Fuel Type" and "Transmission." The chosen category for "Fuel Type" is regular gasoline. For "Transmission," the category is the automatic transmission. These categories are picked due to the relatively fair size of samples.
How about the numerical variables? From the above exploration, the "Vehicle Class" feature shows a positive correlation with numerical features such as "Cylinders," "Fuel Consumption Comb," and "Engine Size." This suggests that each vehicle type is strongly embedded with a certain engine size and the number of cylinders. Larger engine sizes also require greater fuel consumption. Therefore, the numerical variables are not set to be in similar values.
This project will conduct three comparisons among multiple categories, which can be seen as follows:

1. Compact vs Small SUV


The null (H0) and alternative (H1) hypotheses are defined as follows:
<blockquote>
𝐻0: The compact cars' emissions are greater or equal to small SUVs.

H1: The compact car's emissions are less than small SUVs.
</blockquote>

The significant level (alpha) is 0.05.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/12.png" />
</div>

<p align="center"><em>Figure 12. Distribution Plot (Compact vs Small SUV)</em></p>

The test results indicate that the p-value is less than the alpha value, leading to the rejection of the null hypothesis (H0). Therefore, we can say that compact cars' emissions are less than small SUVs (H1). Using a 95% confidence level, the test results indicate that the confidence interval falls between minus infinity (lower bound) and -45.09 (upper bound).

2. Small SUV vs Standard SUV

   
The null (H0) and alternative (H1) hypotheses are defined as follows:
<blockquote>
𝐻0: The small SUV cars' emissions are greater or equal to standard SUVs.
  
H1: The small SUV car's emissions are less than standard SUVs.
</blockquote>  

The significant level (alpha) is 0.05.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/13.png" />
</div>

<p align="center"><em>Figure 13. Distribution Plot (Small SUV vs Standard SUV)</em></p>

The test results indicate that the p-value is less than the alpha value, leading to the rejection of the null hypothesis (H0). Therefore, we can say that small SUV cars' emissions are less than standard SUVs (H1). Using a 95% confidence level, the test results indicate that the confidence interval falls between minus infinity (lower bound) and -52.55 (upper bound).

3. Cargo Van vs Passenger Van
   
The null (H0) and alternative (H1) hypotheses are defined as follows:

<blockquote>
𝐻0: The cargo van cars' emissions are greater or equal to passenger van's.
  
H1: The cargo van car's emissions are less than passenger van's.
</blockquote>

The significant level (alpha) is 0.05.


<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/14.png" />
</div>

<p align="center"><em>Figure 14. Distribution Plot (Passenger van vs cargo van)</em></p>

The test results indicate that the p-value is less than the alpha value, leading to the rejection of the null hypothesis (H0). Therefore, we can say that small passenger van cars' emissions are less than cargo van's (H1). Using a 95% confidence level, the test results indicate that the confidence interval falls between minus infinity (lower bound) and -43.73 (upper bound).

## Regression Model
### Single Predictor

The predictor variable selected for analysis is the "Vehicle Class" feature, which consists of 16 categories of car models. The model fitting process was performed using the Ordinary Least Squares (OLS) technique to estimate the coefficients in a linear regression model of carbon emissions from various types of vehicles. Table 1 below illustrates the intercept, coefficients, and standard errors for each category of the predictor.
The baseline for this regression model is the "compact" car model. Thus, the interpretation of this model is that if the car model is "compact," the estimated carbon emissions are 217.64 g CO2/km. On the other hand, if the car model is a standard SUV, the estimated value is calculated as the intercept plus the coefficient, resulting in a predicted value of 306.73 g CO2/km.
