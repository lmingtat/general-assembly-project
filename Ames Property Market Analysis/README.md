# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Ames Housing Property Market Analysis

### Problem Statement

GA Properties is planning to conduct a property investment seminar in Ames, Iowa. They have invited various stakeholders, from property developers to the community in Ames to attend this conference. This particular event will not only help the community to gain an edge whether they are a seller or a buyer, but also pull in interests from developers to build townships in Ames.

They have consulted with us to come up with a model that can best allow them to better understand the property market in Ames.

1. What are the top 10 features most important to a house in Ames?
2. What are the worst 3 features that will devalue a house?

Using the Ames Housing Dataset, we will try to come up with a model after going through the 70+ features of the current housing market.

### Executive Summary

The first thing we did was to import our data and proceed to clean up for any outliers or incorrect input. Once done, an explratory data analysis was conducted to identify any trends between each features. Any interesting trends or feature were noted down. Data visualisation using scatterplots, boxplots and heatmap greatly helped to point out further insights. Once we have our data and observations sorted, we decided to do some feature engineering, combining or reducing some features into a format that is more usable. After all features are sorted, we fit into a null linear regression model and performed regularisation technique to check if our model is overfitting. Refer to below for our insights and recommendations.

**Overall Report Structure**
1. Problem Statement
2. Data Import and Cleaning
3. EDA
4. Feature Selection
5. Feature Engineering
6. Linear Regression Modelling and Regularization
7. Conclusion & Recommendations
8. Final Kaggle Submission

### Data Dictionary

A detailed data dictionary is available at [AMSTAT](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt)

### Conclusion/Recommendations

The final production model we came up with had 47 predictors (which covers 28 features of any house)

Lasso Model  
Kaggle competition:  
<span style='color:blue'>**Private Score : 31194.29992**<span>  
**Public Score  : 28799.35619**

Train and hold out set scores:

| Model      | Train (RMSE) | Hold_Out (RMSE) |
|------------|-------|----------|
| Linear     | 23925 | 24990    |
| Ridge      | 23724 | 24961    |
| Lasso      | 23677 | 24999    |
| ElasticNet | 23721 | 24964    |

**Features Most Important to a House**

A good house in Ames must have:

1. An excellent external quality
    - First impression matters!
2. Be located in a good neighborhood
    - Location! Location! Location!
    - A house staying in tier 1 area will generally be USD $22,361 more expensive than the tier 2
3. An excelent kitchen
   - Kitchen is a very important space to Americans
4. Huge ground living area
   - The bigger the house, the higher its value
5. Good overall quality
   - Materials and the finish of the house will influence the house buyers
6. Good basement exposure
   - Better with a walkout or garden level walls, for easy access
7. Big furnished basement 
   - Americans do use their basements as a living space, so space and furnishing is important
8. Big second floor level
   - The bigger the upper floor, the better it is
   
**Features That Will Devalue a House**

The top 3 elements are:

1. Age of a house
   - Old houses are not as attractive as new ones! Also comes with a lot of issues to fix!
2. Poor heating quality and condition
   - Our model above had already zero-ed out all but 2 categories (Excellent and Average), thus TA is considered bad in this case
   - Generally, heating in especially important in countries with 4 seasons
3. Rough garage finish
   - A garage is also considered as an important space to most Americans. A poor finish will lessen the house value.
   
**What this will mean to all stakeholders**

<u>As a buyer</u>
- Buyers can use our model to calculate the market value of any given house in Ames after observing the house of interest
- This can help them to make wiser decisions!

<u>As a seller</u>
- Sellers can refer to our model to find ways that can push up the value of their home, and simultaneously avoid the bad characteristics of a house that have been identified by us!
- This way they will be able to maximise the value of their houses and earn more, especially if they are property flippers or are treating property as an investment vehicle.

<u>As a property developer / state housing department</u>
- Property developers or even the government can also use our model to 
    - influence the design of future houses
    - plan which location to build
    - identify up and coming residential areas with high potential
    - make better decision and plan (to resolve affordable housing crisis)
