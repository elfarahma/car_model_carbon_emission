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
### Single predictor

The predictor variable selected for analysis is the "Vehicle Class" feature, which consists of 16 categories of car models. The model fitting process was performed using the Ordinary Least Squares (OLS) technique to estimate the coefficients in a linear regression model of carbon emissions from various types of vehicles. Table 1 below illustrates the intercept, coefficients, and standard errors for each category of the predictor.
The baseline for this regression model is the "compact" car model. Thus, the interpretation of this model is that if the car model is "compact," the estimated carbon emissions are 217.64 g CO2/km. On the other hand, if the car model is a standard SUV, the estimated value is calculated as the intercept plus the coefficient, resulting in a predicted value of 306.73 g CO2/km.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/table_1.png" />
</div>

<p align="center"><em>Table 1. Coefficient and standard error without predictor transformation</em></p>

The inclusion of numerous categories in the predictor feature results in a rather lengthy formula. What if the predictor feature, which consists of categorical data, is transformed beforehand? During the transformation phase, the 16 existing categories are encoded using label encoding, resulting in 16 numerical values (0–15). We can see that after the transformation, the formula becomes simpler (Table 2).
It is important to assess whether this simplified formula is also reasonable. Let's re-interpret the results. The label value of zero represents the "compact" car model, indicating that the "compact" model yields emissions of 227.77 g CO2/km. What about other car models? Let's take small SUV as an example. After transformation, the small SUV model has 11 as the label value. If we estimate its emissions using the linear regression formula below, the result equals the intercept value plus the coefficient multiplied by 11 (3.69 × 11), resulting in emissions of 268 g CO2/km. The standard error value is relatively smaller compared to the previous untransformed regression model. However, this model doesn't perform well when it's tested for the r-squared value. The r-square is only 0.09. Far smaller from the untransformed one which is 0.36.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/table_2.png" />
</div>

<p align="center"><em>Table 2. Coefficient and standard error for a single predictor regression model</em></p>

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/15.png" />
</div>

<p align="center"><em>Figure 15. The fitted line for a single predictor regression model</em></p>

### Multi predictors

For the linear regression model with multiple predictors, the selected features for prediction are "Engine Size" and "Fuel Type." The variable "Fuel Type" is first transformed into numerical values. Subsequently, a comparison will be made between the model without interaction among variables and the model with interaction among variables. This analysis aims to evaluate the model's performance by considering several metrics, such as coefficients, standard errors, and R-squared. Additionally, the standardization of the "Engine Size" feature is also carried out by using z-scores. The result will then be compared to the unstandardized one.
From Table 3 below, we can see that there is no significant difference in performance based on the R-squared values.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/table_3.png" />
</div>

<p align="center"><em>Table 3. R-Square value for each multiple predictors regression model</em></p>

From a coefficient perspective, each model can be logically interpreted based on the data distribution. The interpretation is drawn using the rule of thumb that "Engine Size" will never be equal to zero. The logic is without a working engine, a car can't generate emissions. The data itself shows that the smallest engine size is 0.9 liters, and the largest is 8.4 liters. Therefore, we can assume that the logical range for engine size should be within this range.
The standardized models (models 2 and 4) have larger intercept values compared to the non-standardized models. This is expected because the standardized "Engine Size" values range from -1.66 to 3.83. Thus, the large intercept values would be compensated for smaller engine sizes. Figures 16 and 17 illustrate that larger intercept values tend to have smaller standard errors. The coefficients for "Fuel Type" are relatively small, except for model 3 (Figure 17). But model 3 also has a larger standard error for the coefficient. The coefficients for the interaction variables do not differ significantly. Although at smaller values, the standard errors are smaller. In general, for all coefficients, the model 2 and 4 tend to have the smallest standard error.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/16.png" />
</div>

<p align="center"><em>Figure 16. Coefficient and standard error - without interaction, unstandardized (left), standardized (right)</em></p>

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/17.png" />
</div>

<p align="center"><em>Figure 17. Coefficient and standard error - with interaction, unstandardized (left), standardized (right)</em></p>

All multi-predictor models have one common flaw. This may be due to the segmented data distributions of the "Fuel Type" predictor. The use of regular gasoline tends to concentrate within the engine size range of 1–4 liters, while premium gasoline is concentrated within the range of 4–7 liters. Diesel fuel is even only limited to the range of 2–3 liters. Consequently, if we attempt to predict carbon emissions for a vehicle type that uses premium gasoline but has an engine size of one or two liters, the results are likely to be highly deviated.

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/18.png" />
</div>

<p align="center"><em>Figure 18. Model 1 fitted regression line</em></p>

<div align="center">
  <img src="https://github.com/elfarahma/car_model_carbon_emission/blob/main/figures/19.png" />
</div>

<p align="center"><em>Figure 19. Model 3 fitted regression line</em></p>

From the distribution patterns, each "Fuel Type" category exhibits its own distinct pattern. However, their fitted lines don't reflect this. The lines tend to be parallel and have the same slope (Figure 18). By introducing an interaction variable between "Engine Size" and "Fuel Type", we can see that the fitted lines for each fuel type indeed have significantly different slopes. In the case of diesel fuel, which has a small sample frequency and a narrow range of engine size, the slope tends to be flatter.

## Conclusions

1. In three experiments comparing the mean values of two different categories of "Vehicle Class," t-tests indicated significant differences between each compared category. The emissions from compact cars are smaller than those from small SUVs. The emissions from small SUVs are smaller than those from standard SUVs. Lastly, the emissions from cargo vans are smaller than those from passenger vans.
2. Single predictor linear regression with "Vehicle Class" perform well in certain metrics, but very low in the others. The coefficients could be interpreted reasonably. And the standard error is also relatively small. The model is also versatile. To predict, a user is only required to put the car model into the input. But the performance is not good in terms of r-square value. The r-square for the untransformed and the transformed model is respectively 0.36 and 0.09. This value indicates that the car model alone is far from adequate to be the single predictor.
3. The r-squared value of the single predictor model is also indicative of the correlation between the car models and their emissions. The r-square which is under 0.5 can be considered as low correlation. But the selected t-tests show that there are significant differences among compared two groups. Therefore, a more comprehensive statistic test should be carried out.
4. The multi-predictor regression model with engine size and fuel type for predictor variables performs far better than the previous single-predictor model. The performance across different treatments (standardization and addition of variables interaction) is not significantly different. The r-square values are basically the same (around 0.73). The coefficient and standard errors can also be interpreted reasonably. However, a user should be aware that each fuel type has to be in a certain engine size range to ensure good predictions.

## Recommendations

1. T-test is not adequate to examine the mean difference between more than two groups. For testing differences within sixteen sub-groups under "Vehicle Class", it is suggested to use ANOVA instead. This is also useful if we attempt to reduce the number of sub-groups under "Vehicle Class". The car models that have insignificant mean differences could be put together in one group.
2. More experiments to add variables and the interactions for multi-predictors regression model and see how they might improve the model performance. It also should go hand in hand with proper transformation for predictor variables. The transformation might cover reducing the number of categories under features, especially "Vehicle Class". This one might need more researches to gain domain insights. And also using one-hot encoding for transforming nominal data instead of label encoding.
3. Collecting more samples for under-represented data such as diesel fuel data for "Fuel Type", manual transmission data for "Transmission", and many categories under "Vehicle Class".
4. The models above might not be well-representative when applied outside of North America. Some factors might not be applicable. For example, if we assume that North Americans are highly compliant with fuel type requirements, the model will not be appropriate for regions with far less compliant behavior. In addition, the type of fuel might be different or have different qualities. Not to mention other underlying factors in play. Hence, for other regions, it is better to develop a model from the dataset specifically generated from the said region.
5. To develop a time-series model that is able to estimate the carbon emission projection in regard to the shift of consumer preference toward huge car models such as SUVs and hybrid trucks.


## References

Podder, D. 2020. Basic EDA of the CO2 emissions by vehicle dataset. https://www.kaggle.com/code/debajyotipodder/basic-eda-of-the-co2-emissions-by-vehicle-dataset

European Parliamentary Research Service, 2021. Climate action in the Netherlands. https://www.cbs.nl/en-gb/news/2019/47/half-of-transport-ghg-emissions-are-from-aviation
