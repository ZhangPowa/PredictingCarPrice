# Predicting Car Price

## Table of Contents
* [Background](#background)
* [Dataset](#dataset)
* [Methodology](#methodology)
* [Findings](#findings)
* [Limitations](#limitations)
* [Application](#application) 
* [References](#references)

## Background
An essential part of life is the need to travel. Whether to work, to school, or to leisure activities, using a method of transportation is required. Unlike many other countries in the world with mass public transportation systems, the United States has a singular method of travel: cars. With over 91.55% of households in the U.S having access to at least one vehicle, one essential issue that many businesses and profit-seeking entrepreneurs have is predicting the prices of these vehicles (Timmons, 2022). By determining which factors in a car influences the price, businesses can have access to crucial information that will allow them to manipulate car designs to achieve a certain price threshhold. 

This project uses linear regression modeling in order to find out the best predictor variables of the response variable price. The goal is to achieve the highest predictive power. To quantify highest predictive power we will use the R^2 score as the basis for determing how good our model is. R^2 score is a score beteen 0 and 1 that tells how much percentage of variation the independent variables explains of the dependent variable. It is a very good measurement to base predictive power. 

## Dataset
The data set was given to me by my professor through Kaggle. There are two data set, one for the training and one for the testing model. The training dataset has 15000 observations of 21 different car features. 14 of the features are numerical predictors: MPG.highway, EngineSize, HorsePower, RPM, Rev.per.mile, Fuel.tank.capacity, Passengers, Length, Wheelbase, Width, Turn.Circle, Rear.seat.room, Luggage.room, and Weight. The other 7 features are categorical predictors: Type, AirBags, DriveTrain, Cylinders, Man.trans.avail, Origin, and Make. The training data set also contains the Price response variable. The testing model contains just the predictors and only 938 observations.

## Methodology 

### Initial Understanding
Before doing any advanced statistical analysis the first step in the research process was to figure out which numerical predictors and which categorical predictors had a strong correlation to the price variable. First, for the numerical predictors I created a correlation matrix and analyzed the correlations of each predictor to the price variable. In the numerical predictor correlation matrix we can see that out of the numerical predictors Horsepower has the highest correlation to price (0.79). 
![CorrelationMatrix](https://user-images.githubusercontent.com/78633730/182768925-107914cc-f261-4bda-ae28-ed60a443fe08.png)
Instead of doing a correlation matrix for the categorical predictors, I simply ran a simple linear regression of all the categorical predictors with the price variable and saw which predictor produced the highest R^2 value. Make ended up being the best categorical variable with a R^2 value of 0.991. For one predictor this was an extremely high value, but it came with a cost. Through the summary we saw that although it was one variable there was way more than 10 betas, which made the model too complex. From these two very simple analyses of the variables, we already found key information about our potential model. First Horsepower would likely be apart of our model due to its high correlation, and second that while the Make variable was highly predictive of price, it needed to be transformed into less categories in order to keep the model less complex. 

![GVIF Table](https://user-images.githubusercontent.com/78633730/182768928-698ec0b6-246a-4ee1-a577-476e95b0ca45.png)

![AssumptionsGraphs](https://user-images.githubusercontent.com/78633730/182769051-61109f33-edd2-46dc-a8d7-dbcaa744a1b2.png)
![Leverage Outlier Table](https://user-images.githubusercontent.com/78633730/182769062-cf4936e1-35cf-425d-b051-01d3c1a85f48.png)
![Luxury Cars](https://user-images.githubusercontent.com/78633730/182769087-6a9dfab7-427a-4e30-ae02-008be26bba26.png)
![Model Summary](https://user-images.githubusercontent.com/78633730/182769091-02bae23c-55dc-4b6e-8ef0-471b473e5538.png)

