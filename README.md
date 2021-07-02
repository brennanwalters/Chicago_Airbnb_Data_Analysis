
![Screen Shot 2021-07-01 at 10 54 46 PM](https://user-images.githubusercontent.com/54850909/124218192-5edbbd80-dabf-11eb-8251-41a01ad8759c.png)


# Table of Contents

* Introduction
* Data Overview
* Model Comparison and Selection
* Inference

# Introduction
This analysis was a collaborative project with my three statistics classmates. This project provided valuable experience working with real data and applying the statistical methods we had learned throughout the course. It also gave me the opportunity to work with peers who were equally as excited about data science as myself. All the visualizations and models shown below were produced using JMP. 

# Data Overview
The Airbnb dataset includes 500 Airbnb property listings in Chicago from August 2008 to May 2017. For our analysis, we wanted to predict the price of a property per night using the type of property, the number of bedrooms included, and the property’s review score. During our analysis we used 422 distinct Airbnb properties. 


* price (response) - quantitative variable for nightly rental price in U.S. dollars
* Room_type - categorical variable with three levels: entire home/apt., shared room, and private room (reference)
* Bedrooms - quantitative variable for number of bedrooms in the listing
* Review_score - ordinal, rating of the property broken into three categories: 6-8, 9, and 10 (reference)

# Model Comparison and Selection

![Screen Shot 2021-07-01 at 4 28 31 PM](https://user-images.githubusercontent.com/54850909/124191503-79933f80-da89-11eb-80c6-b2f1b6d210fe.png)

Log-log transformation:
* Largest adjusted R2 value 
* Highest number of significant factors from t test
* Significant overall in predicting price

### QQ Plot
![Screen Shot 2021-07-01 at 4 31 00 PM](https://user-images.githubusercontent.com/54850909/124191681-c37c2580-da89-11eb-9805-3e59d268dc86.png)

Since our data closely follows the diagonal line, it roughly follows a normal distribution.

### Residuals
![Screen Shot 2021-07-01 at 4 30 48 PM](https://user-images.githubusercontent.com/54850909/124191683-c4ad5280-da89-11eb-94e6-a88c9cd39a73.png)

Since there are no noticable patterns in the points of the residual plot and they appear to be scattered around zero, it is reasonable to assume that the variance in the error terms is constant.

### Visualization
![pasted image 0](https://user-images.githubusercontent.com/54850909/124191945-2a014380-da8a-11eb-812c-6ee8efc37656.png)

* Roughly linear after transformation
* No evidence of interaction 
* Leverage plot needed to analyze outliers  

Note: T tests showed ln(# of Bedrooms), Room Type, and Review Score to be statistically significant


# Transformation Model
Predicted ln(Price) = 4.1586668915 + .4888199043 * ln(Bedrooms) -0.372298926 (Shared Room) 
+ .5788651839 (Entire Home/apt)
-0.117819225 (Score 9) -0.003372088 (Scores 6-8)

### Interpretations

For a 10% increase in bedrooms, the predicted median price will increase by a multiplicative factor of 1.05, when the score and room type are held constant. 
Predicted median price for a shared room is lower than that of a private room by a multiplicative factor of 1.44 when score and bedrooms are held constant


### Leverage plot
![Screen Shot 2021-07-01 at 4 37 15 PM](https://user-images.githubusercontent.com/54850909/124192272-a09e4100-da8a-11eb-8d77-9c7108361dcc.png)

There aren’t any values with high influence but there are many values (29) with high leverage. There are 16 values with high residuals and 3 values with very high residuals.  

### Adjusted R Squared

47% of the variation in ln(price) can be explained with our linear model including ln(bedrooms), room type, and review scores after adjusting for the complexity of the model. 


# Inference

### Conditions For Inference

* Independance: Different listings shouldn’t affect each other. 
* Linearity: Met via residual plot. 
* Constant Variance: Met Via Residual plot
* Normality: Met Via QQ Plot

### Hypothesis test
Goal - Determine whether or not ln(bedrooms) is significant in predicting ln(price)

* ß1 = Coefficient for ln(Bedrooms)
* H0: ß1 = 0
* Ha: ß1 ≠ 0
* Test Statistic: t = 7.20 
* Prob > |t|: < .0001


Conclusion: There is overwhelming evidence to indicate that ln(bedrooms) is significant in predicting ln(price) on average, when holding all other explanatory variables constant. 

A model including ln(# of Bedrooms), Room Type, and Review Score is statistically significant in predicting ln(Price) for airbnb listings in the Chicago Area from August 2008 to May 2017.  









