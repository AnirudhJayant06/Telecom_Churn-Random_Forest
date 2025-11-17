# Problem Framing

## 1. Business problem
- Telecom companies lose a significant amount of revenue when existing customers discontinue their services ("churn")
- Acquiring new customers is 5–7× costlier (assumption) than retaining existing ones.
- The objective is to predict the probability that a customer will churn, so the retention team can take targeted action.

---
## 2. What is our objective?
1. Reduce customer loss
2. Lower revenue leakage
3. Improve retention campaign efficiency
4. Prioritize high-risk customers
5. Reduce cost of unnecessary offers (avoiding false positives)
6. Increase customer lifetime value (CLV)

---
## 3. KPIs
| KPI                         | Meaning                                      |
| --------------------------- | -------------------------------------------- |
| **Churn Rate (%)**          | Baseline business churn                      |
| **Precision (Churn Class)** | Avoid offering discounts to stable customers |
| **Recall (Churn Class)**    | Catch as many churners as possible           |
| **F2-score**                | Recall-heavy metric (preferred for churn)    |
| **Revenue Saved**           | Estimated savings from retention             |
| **Cost of False Negatives** | Lost revenue due to missed churners          |
| **Cost of False Positives** | Unnecessary retention / discount cost        |
| **PR-AUC**                  | Important metrics for imbalance dataset      |
| **PR-AUC**                  | Important metrics for imbalance dataset      |

> We haven't used AUC-ROC because it uses TPR (True Positive Rate) and FPR (False Positive Rate) which can be misleading in imbalanced datasets as FPR remains low. So, even a bad model can appear good.

---
## 4. Problem Statment
Build a machine learning model that predicts whether a telecom customer will churn in the next billing cycle, and provide a churn probability (%) and key drivers that influence the prediction

---
## 5. Target Variable
- Churn
    - "Yes" -> Churner (converted to 1)
    - "No"  -> non-churner (converted to 0)

---
## 6.Input features (Independent Variables)
High-level categories:
- Demographics (SeniorCitizen, gender, tenure)
- Charges (MonthlyCharges, TotalCharges)
- Contract Info (Contract type, Payment method)
- Services Taken (InternetService, TechSupport, OnlineBackup etc.)
- Billing Info (PaperlessBilling, payment method)

---
## 7. Constraints & Assumptions
- Data represents past billing cycle - no future leakage allowed.
- All feature engineering must be derived before churn happens
- Must handle class imbalance (~70–80% non-churn)
- Model needs to be interpretable for business → SHAP

---
## 8. Model acceptance criteria
1. Recall (Churn) ≥ 70% (catch most churners)
2. Precision (Churn) ≥ 40% (not spamming offers to everyone)
3. PR-AUC improves significantly over baseline
4. Business Expected Value is Positive
5. Model gives a clear explanation i.e. top churn drivers per customer
6. Streamlit app shows churn risk (%) and explainability

---
## 9. Summary
- This project aims to create a churn prediction model that produces a churn risk score and explainable drivers.
- The model will help the retention team reduce revenue leakage by targeting high-risk customers with appropriate actions.