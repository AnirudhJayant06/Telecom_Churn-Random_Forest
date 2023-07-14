# House Price Prediction
> The main objective is to predict the price of the house using the given set of features


## Table of Contents
* [General Info](#general-information)
* [Conclusions](#conclusions)

<!-- You can include any other section that is pertinent to your problem -->

## General Information

- The dataset contains 1460 rows & 81 columns
  
- It has
  -   '3' Float type variables
  -   '35' Integer type variables
  -   '43' Object type variables

 - 'SalePrice' is our Target variable i.e. the variables whose values we need to predict for unseen data.
   
 - In Data Cleaning & Manipulation part,
   - Null values are handled by data imputation & dropping rows (One of the most difficult task)
   - Outliers has been handled by log transformation of 'SalePrice'
     
  - For EDA,
    - First, we categorizes our data into numerical columns, nominal categorical columns & ordinal categorical columns
    - For numeric variables, 'PairPlot' & Correlation 'Heatmap' was plotted.
    - For nominal categorical columns, 'boxplot' has been plotted to understand the trend & important variables.
    - For ordinal categorical columns, first the values has been mapped accordingly and, then, 'boxplot' has been plotted.
      
  - For Data Preparation
    - First, dummy variables have been created for nominal categorical variables.
    - Then, we did the train-test split
    - Finally, we did the feature scaling using 'MinMaxScaler()'
      
  - Model Building
    - First simple linear regression model was built but we notice overfitting.
    - So, we build 2 different regularization model & calculated important metrices for model evaluation
      - Ridge Regression
      - Lasso Regression
     - For hypertunning, we used 'GridSearchCV' to find the best value of alpha
     
      ![image](https://github.com/Anirudh-Jayant/Advance_Regression_House_Prediction/assets/98637152/c4058355-33f9-4371-9be7-ef420ad16a3f)

    - Based on the metric evaluation, Ridge Regression model comes out to be appropriate for the given problem
      

## Conclusions
- As per the coefficient's values of Ridge regression, the top 5 predictors are
1. OverallQual     
2. GrLivArea     
3. OverallCond     
4. TotRmsAbvGrd     
5. 1stFlrSF 



<!-- Optional -->
<!-- ## License -->
<!-- This project is open source and available under the [... License](). -->

<!-- You don't have to include all sections - just the one's relevant to your project -->
