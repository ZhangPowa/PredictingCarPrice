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

![CorrelationMatrix](https://user-images.githubusercontent.com/78633730/182768925-107914cc-f261-4bda-ae28-ed60a443fe08.png)
![GVIF Table](https://user-images.githubusercontent.com/78633730/182768928-698ec0b6-246a-4ee1-a577-476e95b0ca45.png)


