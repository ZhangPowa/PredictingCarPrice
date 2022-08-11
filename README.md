# Predicting Car Price

## Table of Contents
* [Background](#background)
* [Dataset](#dataset)
* [Methodology](#methodology)
* [Findings](#findings)
* [Limitations](#limitations)
* [Learnings](#learnings) 
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

### Model Selection and Variable Transformation 
The next step in the process was to run the regsubsets function on all the predictors and see which predictors were the best through step-wise selection. Regsubsets gives out the best variables using three different methods, forward, backward, and exhaustive selection and aims to reduce the RSS. From our first set of resubsets we find that there are sublevels of Make considered in the best model: Cadillac, Audi, and Mercedes Benz. From my current understanding of cars, these makes all seem to be luxury brands. So I used information from Autotrader, a car selling website, to categorize the car makes of the dataset into luxury or not.
![Luxury Cars](https://user-images.githubusercontent.com/78633730/182769087-6a9dfab7-427a-4e30-ae02-008be26bba26.png)

After transformation, I tested the new make variable and found that it produced an R^2 of 0.5958. Although, the R^2 was a lot lower than previous, it only required the use of 2 betas. However, this is not the final transformation of the Make variable I used. One thing that had stood out from earlier was that specifically the level Mercedes-Benz 300E was the second best predictor after Horsepower. In addition, when finding the mean of the prices by make, Mercedes-Benz 300E was the highest at $63,248, $14,000 more than any other car. So I decided to make it its own category and see the result of the new transformation. By adding one more beta, the R^2 value went up almost 0.1. The final transformation of the Make variable was three categories: Luxury, Not Luxury, and Mercedes-Benz 300E. After finalizing the Make transformation, I once again ran regsubsets. I found another important categorical level AirBags None. I then created a new AirBags variable with the two levels: None and Not None. Many of the new creation of variables required less logic and instead just involved reducing the levels of the categorical variable to have less betas. This step was repeated over until I had created four new variables AirBags, Make, Type, and Cylinders. Type was split into Midsize and not Midsize and Cylinders was reduced to 5, 6 and not 5 or 6. Overall, by reducing amount of sublevels for the important categorical predictors, I was able to maximize the model’s R^2 while keeping the amount of betas to a minimum. After finishing all the creations of new variables, the final model with the highest testing model R^2 included seven predictors: Horsepower, Airbags, Width, Man.trans.avail, Fuel.tank.capacity, Make, and Cylinders.

### Validation of Model
![Model Summary](https://user-images.githubusercontent.com/78633730/182769091-02bae23c-55dc-4b6e-8ef0-471b473e5538.png)

While the final model does produce a high R^2 value, we also must check that the model meets the correct assumptions. First from the summary we can see that all betas are significant.

![GVIF Table](https://user-images.githubusercontent.com/78633730/182768928-698ec0b6-246a-4ee1-a577-476e95b0ca45.png)

When we check the VIF’s of each predictor we find that no single predictor has a VIF of over 5. The highest VIF score that we see in the able is 4.28 which means that no multicollinearity exists within the model.
![AssumptionsGraphs](https://user-images.githubusercontent.com/78633730/182769051-61109f33-edd2-46dc-a8d7-dbcaa744a1b2.png)

In the plots shown above we can analyze the other important assumptions needed to validate the model. From the residual vs fitted plot we see a pretty straight horizontal line centered around 0 meaning the linearity assumption holds. In the Normal Q-Q plot while there are points towards the top right of the graph that are off the line, overall most points follow, meaning the model’s error has a normal distribution. For the scale location plot while we do see a littler upwards and then downwards slope the line is mostly horizontal around the x axis. We can see that the car prices around the $60,000 price has a large influence on the scale-location plot by pulling it downwards. Overall the equal variance assumption still holds. While the final residuals vs leverage graph does not show us many potential influential points we created a table of leverage and outliers to see whether or not the model had bad leverage points. 
![Leverage Outlier Table](https://user-images.githubusercontent.com/78633730/182769062-cf4936e1-35cf-425d-b051-01d3c1a85f48.png)

From the table we can see that out of 1500 different data points there are 10 outliers that are also leverage points. To deal with these points, I decided to take these points out of the dataset to see how the model would be impacted. While the training model’s R^2 value went up the testing model had its R-2 value lowered, so I decided to keep the points in the model. I think one reason for this is because the testing data also contains some bad leverage points meaning its better to leave the points in the dataset than take them out. Overall, the final model included 3 newly created categorical variables and 4 numerical predictors. The model passed all the assumptions needed for linear regression, and the 10 bad leverage points were kept in the model. 

## Findings
The final training model has an R^2 value of 0.9228 and the final testing data model has an R^2 value of 0.90676. Although the results of the final model were pretty good, one cost is that the residual standard error of the model was 2922. This means that the model predicts car price with an average error of $2922. A close to $3000 error of price is a sizeable amount, however since the goal of this model is predictive power, this model was still used since it produced the highest R^2 value. If the goal was to minimize the residual standard error, maybe a different model would be better to achieve a lower RSE. Much of what I have discussed has been about the success trial and not about the failure trials that I also went through in the research process. One example is the mistake of categorizing the make variable by year. Initially I thought that the more recent cars would be pricier and with that logic in mind, I searched up all the car make years and organized the cars into three different categories: ancient (Before 2000), old (2000-2010), and new (Post 2010). After categorizing I saw the new R^2 value for this new variable and it was much lower than the categorization by luxury. 

## Limitations 
Although our final model did have a high R^2 value, there were many mistakes I made in the process of developing the final model. One limitation that may have lowered the R^2 score was the removal of strong predictors through reduction of categorical variables. One example is the Cylinders variable. After finalizing the model, I reran the regsubsets function without the newly created variables. Specifically for Cylinders, 4 and 8 were selected as the best levels to use instead of 5 and 6 in the forward and backward selection methods. So I may have wrongly created a new variable and removed the more significant levels that had better predictive power for price. 
Additionally, another limitation of my model is that it did not have any transformations. Because I wanted to keep my model as simple as possible I only looked to check whether the response variable required a transformation. Transforming some of the predictor variables may have made the residual graphs better, or even increased the R^2 score of the model. However, I did not perform any of these transformations to ensure a simple model that could be used and interpreted without complex steps. 
In conclusion, this research study has helped me understand many of the strategies to build a strong linear regression model. There are many other things in this world that are very valuable to be able to predict. And now with this information I not only can find powerful models, but also retool to specific purposes whether to reduce the error or fixate on predictability.

## Learnings

### Model Fitting
One of the main skills I learned is how to use different multiple linear regression strategies to find important factors for the price of a product. First I learned how to interpret and build models using lm. Then I learned how to analyze if the model was not only highly predictive but also valid (not multicollinear, and other assumptions). All of these concepts I learned to apply and use in R. 

### Next Steps
While multiple linear regression is an important skill to learn as a data analyst, this project taught me very basic skills. I did not design an experiment or collect data, all I did was analyze and fit a model. In the next project I will want to learn experimental design, and data collection. I also want to learn how to create visualizations of my findings to communicate my findings better to those that are not able to understand the higher level statsitics. 

## References
Luxury vehicles information, prices and inventory. Autotrader. (n.d.). Retrieved August 2, 2022, from https://www.autotrader.com/luxury 
Timmons, M. (2022, June 28). Car ownership statistics in the U.S. ValuePenguin. Retrieved August 2, 2022, from https://www.valuepenguin.com/auto-insurance/car-ownership-statistics#:~:text=The%20rate%20of%20car%20ownership,vehicles%20in%20the%20same%20period. 


