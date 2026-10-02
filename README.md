# Customer Churn Prediction

Predicting which telecom customers are likely to leave, using Python 
(Logistic Regression & Random Forest) and visualizing the insights in 
a Power BI dashboard — a full pipeline from raw data to business dashboard.

## Overview

Customer churn (customers leaving) is costly for telecom companies. This 
project analyzes 700 customers to answer three questions: which customers 
are likely to churn, what drives churn, and how reliably we can predict it. 
It covers the full workflow — data cleaning, exploratory analysis, encoding, 
machine learning, and a Power BI dashboard.

## Tools Used

- Python (pandas, scikit-learn)
- Logistic Regression & Random Forest
- Power BI (dashboard)

## The Data

700 customers with: Age, Tenure (months), MonthlyCharges, Contract type, 
PaymentMethod, InternetService, and Churn (Yes/No — the target). About 21% 
of customers churned (an imbalanced dataset).

## Data Preparation

- Filled missing values in Tenure and MonthlyCharges with the median
- One-hot encoded the text columns (Contract, PaymentMethod, InternetService) 
  into numeric form for modeling

## Key Findings (EDA)

Customers who churn tend to be:
- **On month-to-month contracts** — by far the highest churn rate
- **Paying by electronic check** — highest churn among payment methods
- **Newer customers** — churners averaged 21 months tenure vs 34 for those who stayed
- **Paying higher monthly charges**

Age had almost no relationship with churn.

## Modeling

Built and compared two models (both using class_weight='balanced' to handle 
the 21% churn imbalance), focusing on **recall** — catching customers about 
to leave matters more than avoiding false alarms.

| Model | Recall (churners, 5-fold CV) |
|-------|------------------------------|
| Logistic Regression | 0.89 |
| Random Forest | 0.67 |

**Logistic Regression was the better model here**, catching ~89% of churning 
customers (confirmed with 5-fold cross-validation). Its trade-off is more 
false alarms (lower precision), but for churn, catching at-risk customers is 
the priority.

## What Drives Churn (feature importance)

Top predictors from the Random Forest:
1. Tenure
2. MonthlyCharges
3. Contract type

This confirms the EDA: short tenure, high charges, and month-to-month 
contracts are the strongest churn signals.

## Dashboard

A Power BI dashboard visualizes the key findings — total customers, churn by 
contract type, and churn by payment method — for a non-technical audience.
(See dashboard screenshot in this repo.)

## Business Recommendations

- Focus retention on **new customers** (first months are the danger zone)
- Encourage **longer contracts** (month-to-month customers churn most)
- Promote **auto-pay** over electronic check

## What I'd Explore Next

- Tune the decision threshold to balance recall and precision
- Add more customer features (support calls, add-on services)
- Try gradient boosting models
