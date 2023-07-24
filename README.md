# Telecom Churn Case Study
> The main objective is to predict whether a particular customer will switch to another telecom provider (i.e. Churn) or not.


## Table of Contents
* [General Info](#general-information)
* [Conclusions](#conclusions)

<!-- You can include any other section that is pertinent to your problem -->

## General Information

- We have 3 different datasets
  1. 'churn_data.csv'
  2. 'customer_data.csv'
  3. 'internet_data.csv'
- After combining these dataset over the common column 'customerID', we get a dataset which contains 7043 rows & 21 columns
  
- It has
  -   '1' Float type variables
  -   '2' Integer type variables
  -   '18' Object type variables

 - 'Churn' is our Target variable i.e. the variables whose values we need to predict for unseen data.
   
 - In Data Cleaning & Manipulation part,
   - Rows with empty string in 'TotalCharges' are dropped & conveted the values of these column to float type.
     
 - For Data Preparation
   - Mapped 'Yes' & 'No' of these columns - 'PhoneService', 'PaperlessBilling', 'Churn', 'Partner', 'Dependents' - to 1 & 0 respectively.
   - Created dummy variables for various categorical columns - 'Contract', 'PaymentMethod', 'gender', 'InternetService', etc.
   - Did feature scaling using 'StandardScaler()'
   - Handled multi-collinearity issue by dropping high correlated variables - 'MultipleLines_No','OnlineSecurity_No','OnlineBackup_No','DeviceProtection_No','TechSupport_No', 'StreamingTV_No','StreamingMovies_No'
      
  - Model Building
    - First, we build a logistic regression model (with all features) & got good accuracy (0.81) but high 'False Negative' - 11.5% (574/4930) - on training data
    - Then, we did feature selection using RFE and selected top 15 contributor features. Using VIF & p-value, we dropped 2 columns to finally build a model with 13 features (with default cut-off : 0.5) & got similar accuracy (0.80) but a slighly higher 'False Negative' - 12% (590/4930) - on training data
    - Then, we build another model with the optimal cut-off (0.3) and got a decent accuracy (0.77) but a very good improvement on 'False Negative' - 6% (288/4930) - on training data.
    - Then, we test this model on test data and we got 0.74 accuracy & approx 8% 'False Negative' which is compare to what we got in training data. Therefore, our model is good.
    - We also calculated area under ROC curve and we got '0.83' which is quite decent.
    - Then, we build decision tree base line model which gives us 0.78 accuracy & approx 15% 'False Negative' on test data. After hypertunning to get the best model, we got '0.79' accuracy & aaprox 12.7% 'False Negative' The ROC curve give us '0.87' output.
    - Finally, we two random forest model - Base line & hypertunned - and got comparable result (accuracy - 0.80 & 0.79 and False Negative % - 13% & 13.5 respectively) on test data. The ROC curve gives us the '0.92' output.

## Conclusions
- As per the coefficient's values, the top 5 predictors are
1. tenure
2. TotalCharges
3. MonthlyCharges
4. InternetService_Fiber optic
5. OnlineSecurity_No


<!-- Optional -->
<!-- ## License -->
<!-- This project is open source and available under the [... License](). -->

<!-- You don't have to include all sections - just the one's relevant to your project -->
