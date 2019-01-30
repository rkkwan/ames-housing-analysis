# Project 2 - Ames Housing Data and Kaggle Challenge


## Problem Statement

1. As certain features of a house change, how does the sale price of the house change?

2. What neighborhoods seem like they might be a good investment?

3. Does this study generalize to other cities?

## Presentation

[Ames Housing Analysis](https://docs.google.com/presentation/d/1wShSibF8PrpeBBkfB1rxIaAOS7vhRldA3wG-Dtk06eE/edit?usp=sharing)


## Assumptions

The study was conducted under the assumption that the features of a house, such as square footage, overall quality, and number of bedrooms, _affect the value of the home consistently_ in the city of Ames.


## Executive Summary

When asked about predictors of the value of a home, the first features to come to mind might be overall square footage, number of bedrooms, number of bathrooms, proximity to places of interest. These assumptions are made by the fact that most homebuyers will shop for a house using these metrics. This analysis shows that, in fact, the most accurate predictors of home value are generally categorical, not numerical.  The top predictors were determined by the biggest coefficients of a `Lasso` model.

### Top predictors of a house in Ames
1. `gr_liv_area` : Above ground living area in square feet
2. `overall_qual` : Overall quality rating
3. `bsmtfin_sf_1` : Finished basement area in square foot
4. `neighborhood` : Physical locations within Ames city limits
5. `total_bsmt_sf` : Total basement area square feet
6. `year_remod/add` : Year of remodel date
7. `lot_area` : Lot size in square feet
8. `year_built` : Year of original construction date
9. `gr_liv_area kitchen_qual` : Interactive feature of above ground living area and kitchen quality
10. `kitchen_qual` : Kitchen quality rating

**Above ground living area**

To no surprise, the amount of living space is a strong predictor of home value.

**Overall / Kitchen Quality**

The features that measure quality are subject to the opinion of a credible reviewer, most likely an appraiser. The overall quality rating is scored from 1 to 10, while the other ratings are scored from Poor, Fair, Average, Good, to Excellent. What makes a kitchen excellent or poor is subject to the reviewer. Since these ratings are made by opinion and not judgment, they are considered categorical. The kitchen in particular is a major selling point.

**Basement size**

Finished basements add a considerable amount of living space to a house.

**Neighborhood**

Location, location, location. Neighborhoods command a huge influence over the value of a home. Neighborhoods are contained with district lines, which dictate which school district a child will attend. HOAs assure the overall cleanliness of the neighborhood, which will affect the value of the individual homes. The value of a beautiful house may be brought down by shoddy homes adjacent to it.

**Lot Area**

Parking space is a highly desired statistic, especially in cities where parking can cost money. Parking space also dictates how easily guests can visit a house.

**Year built / remodeled**

The age of a home implies the quality of the home. The older a home gets, the lesser quality it becomes through natural wear and tear. The newer the home, the higher the price. Remodeling a home to give it new life can boost its value by looking like new.


### Estimating the value of categories

To be considered for regression modeling, categorical values must somehow be converted to numerical values. The sale prices were grouped by category, then by each different value. Every unique value was assigned the median sale price and then scaled down by the highest value of that category. This conversion method revealed that ranking features (such as quality) tend to have a non-linear, quadratic relationship with the sale price.  Strictly categorical features that do not imply a ranking followed a more linear relationship.

### Feature Selection

Features to be used for the predictive model were selected by measuring their correlation with the sale price. Interactive features were automatically generated using the `PolynomialFeatures` class. The coefficients of the `Lasso` model reveal the strongest predictors of sale price.

### Predictive Modeling

Predictive models were generated using the following `sklearn` classes:
1. `LinearRegression`
2. `RidgeCV`
3. `LassoCV`


## Table of Contents
1. [EDA and Data Cleaning](#EDA-and-Data-Cleaning)  
    - Explore the data: Column names, data types, summaries (`describe`), outliers (`boxplots`), missing values  
    - Clean the data: Column names, remove invalid data, remove outliers, impute missing data  
    - Explore more data: Median value per categorical value per category  
    - Clean more data: Convert categorical values to numerical, create dummy columns  
    - Explore even more data: Visualize relationships of features to target, correlation
2. [Preprocessing and Feature Engineering](02-Preprocessing-and-Feature-Engineering.ipynb)  
    - Select features to use as predictors
    - Transform data
        - Train test split
        - Standardization
        - Interactive features
3. [Modeling Benchmarks](03-Model-Benchmarks.ipynb)  
    - `LinearRegression()`
4. [Model Tuning](04-Model-Tuning.ipynb)  
    - `RidgeCV`
    - `LassoCV`
    - `ElasticNetCV`
    - Cross Validation testing with KFold
5. [Production Model and Insights](05-Production-Model-and-Insights.ipynb)  
    - `RidgeCV`
    - `LassoCV`
    - Reveal correlated features
