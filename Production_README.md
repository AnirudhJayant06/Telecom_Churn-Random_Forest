# Telecom Churn Prediction – Industry-Style Refactor (v2)

> The main objective is to predict whether a telecom customer will churn or not.
> The secondary objective is to turn a legacy notebook project into an industry-style, modular ML pipeline.

---

## 1. Project Overview

This project started as a single-notebook case study to predict customer churn for a telecom company using Logistic Regression, Decision Trees, and Random Forest.

I am now refactoring it into an **industry-style ML project** with:

- Clear business framing  
- Modular, reusable code (`src/`)  
- Proper train/validation strategy with imbalance handling  
- Model explainability using SHAP  
- A Streamlit app for interactive churn risk scoring  
- A basic model monitoring plan

---

## 2. Business Problem

Telecom companies lose significant revenue when customers churn.  
The goal is to:

- **Predict churn risk** for each customer
- **Prioritize retention efforts** (discounts, calls, offers)
- **Minimize False Negatives** (churners predicted as non-churn)

Key KPIs:

- Churn rate (%)
- Retention cost vs revenue saved
- False Negative rate for churn prediction
- Revenue at risk saved by the model

---

## 3. Dataset

The project uses 3 CSV files:

- `churn_data.csv`
- `customer_data.csv`
- `internet_data.csv`

These are joined on `customerID` to create a unified table with customer demographics, contract details, service usage, and churn label.

A `Data Dictionary.pdf` is provided for column descriptions.

---

## 4. Project Workflow - Planned

1. **Problem Framing**  
   - Define KPIs (Churn %, Retention cost, Revenue at Risk)  
   - Identify dependent/independent variables  
   - Split into train-test early to avoid leakage  
   - Document business assumptions & scope in README  

2. **Data Understanding**  
   - Explore data dictionary / metadata  
   - Identify data types and domain meanings  
   - Check for anomalies (tenure = 0, missing charges, inconsistent values)  
   - Understand business processes (billing cycle, contract type)  
   - Identify potential data leakage sources early  

3. **Data Cleaning & EDA**  
   - Handle missing values, duplicates  
   - Correct inconsistent entries (spaces, casing, Yes/No vs 1/0)  
   - Univariate & bivariate plots  
   - Detect outliers using IQR / Z-score  
   - Correlation heatmaps & Cramér’s V for categorical correlation  
   - Generate concise EDA summary report for business  

4. **Imbalance and Leakage Checks**  
   - Check class imbalance (churn %, non-churn %)  
   - Apply imbalance handling: class weights, SMOTE, SMOTEENN  
   - Check for leakage variables (features that reveal churn outcome)  
   - Remove post-churn features (if any)  
   - Ensure train-test split happens before SMOTE  

5. **Feature Engineering**  
   - Encode categorical variables (Label, OneHot)  
   - Scale numeric features (StandardScaler / MinMaxScaler)  
   - Feature selection (RFE, VIF, mutual information)  
   - Create interaction features (Tenure × MonthlyCharges)  
   - Create domain-driven features (Tenure buckets, PaymentType groups)  

6. **Pipeline & Column Transformer**  
   - Define preprocessing pipelines for categorical and numeric features  
   - Combine transformations with `ColumnTransformer`  
   - Wrap preprocessing + model into a single `sklearn.Pipeline`  
   - Use the same pipeline for training, CV, tuning, and inference  
   - Prevent data leakage by fitting only on training split  

7. **Model Building**  
   - Train baseline: Logistic Regression  
   - Train tree-based models: DecisionTree → RandomForest → XGBoost  
   - Compare models using Recall, F1, PR-AUC, ROC-AUC  
   - Use stratified cross-validation  

8. **Model Evaluation (Metrics, Threshold, Cost-based Analysis)**  
   - Generate metrics: Accuracy, Precision, Recall, F1, ROC-AUC, PR-AUC  
   - Plot confusion matrix, ROC, and Precision-Recall curves  
   - Perform threshold tuning (F1-max, F2-max, Youden’s J)  
   - Apply cost-based evaluation (FP vs FN cost)  
   - Plot churn probability distribution  
   - Choose optimal operating point for business  

9. **Model Tuning (Hyperparameter + Cross-Validation)**  
   - Use Optuna (preferred) or GridSearchCV  
   - Apply Stratified K-Fold  
   - Optimize for Recall or F2-score  
   - Store best hyperparameters + CV metrics  
   - Compare tuned model vs baseline  

10. **Model Explainability**  
    - Use SHAP to identify top churn drivers  
    - SHAP summary plot (global explanation)  
    - SHAP dependence plots (feature interactions)  
    - SHAP force plot for individual predictions  
    - Summarize insights for business stakeholders  

11. **Deployment**  
    - Save the best model + preprocessing pipeline using `joblib`  
    - Build Streamlit app with input sliders/dropdowns  
    - Display churn prediction + **churn probability (%)**  
    - Show SHAP force plot for user-specific explanation  
    - Add input validation for all user fields  
    - (Optional) Add a simple **model reliability indicator** based on calibration  
    - (Optional) Add **What-if analysis** (effect of changing key features)  

12. **Model Monitoring Plan**  
    - Define monitoring metrics (data drift, prediction drift, recall drop)  
    - Track churn rate distribution monthly  
    - Monitor feature drift (KS-test, PSI, or EvidentlyAI)  
    - Set alerts for performance degradation  
    - Define retraining triggers (time-based or drift-based)  

13. **Documentation**  
    - Finalize README (workflow, architecture, results, examples)  
    - Add a model card (description, limitations, ethical notes)  
    - Document folder structure + reproducibility instructions  
    - Add versioning details (dataset + model versions)  
    - Add Streamlit usage/deployment guide  

---

## 5. Repository Structure (Work in Progress)

```text
Telecom_Churn-Random_Forest/
├── data/
│   ├── raw/            
│   └── processed/      

├── notebooks/
│   ├── legacy_Telecom_Churn_Random_Forest.ipynb
│   ├── 01_eda.ipynb               
│   └── 02_modeling_pipeline.ipynb 
├── src/
│   ├── data_prep.py               
│   ├── features.py                
│   ├── train_model.py             
│   ├── evaluate.py                
│   └── explain.py                 
├── models/                        
├── streamlit_app/
│   └── app.py                     
├── README.md
└── requirements.txt               
