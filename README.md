# Telecom Churn Prediction

This project focuses on predicting customer churn in the telecom industry using machine learning techniques. Churn refers to customers switching from their current telecom provider to another, which can significantly impact a company's revenue. By identifying potential churners, telecom operators can take proactive measures to retain customers and reduce churn rates.

---

## Problem Statement

The annual switching rate in the telecom industry ranges from **15-25%**, and retaining customers is **5-10 times cheaper** than acquiring new ones. This project aims to:
- Predict customer churn using historical data.
- Identify key features influencing churn.
- Provide actionable insights for telecom companies to mitigate churn.

---

## Dataset

The dataset was sourced from Kaggle and contains telecom customer-level data for June to September:
- **Rows**: 100,000
- **Columns**: 226
- **Key Features**:
  - Recharge amount and type.
  - Time spent on calls.
  - Internet usage.
  - Churn status.

The dataset primarily focuses on the South Asian market, where over 90% of users have prepaid recharge plans.

---

## Objectives

1. Predict when and why customers switch telecom providers.
2. Identify major reasons for churn and focus on high-value customers.
3. Provide strategies for reducing churn based on key insights.

---

## Methodology

### Data Preprocessing
1. Dropped columns with more than 70% missing values, reducing column count to 210.
2. Imputed numerical null values (e.g., recharge data) with `0` and categorical null values with `-1`.
3. Used **KNN Imputer** for remaining null values.
4. Created:
   - A "high-value customers" column (total recharge > 70th percentile).
   - A "churn" column (1 = churned, 0 = retained) based on call minutes and internet usage.
5. Addressed class imbalance in the churn column during modeling.

### Exploratory Data Analysis (EDA)
- Conducted univariate and bivariate analysis.
- Used K-Sigma technique for outlier detection and capping.
- Confirmed data distribution was suitable for regression analysis.

### Modeling
#### 1. PCA (Principal Component Analysis)
- Reduced dimensionality to improve interpretability.
- Findings:
  - **60 components** explained 90% variance.
  - Sensitivity: **0.85**, Specificity: **0.81**, AUC: **0.9**.

#### 2. PCA with Logistic Regression
- Hyperparameter tuning via Grid Search:
  - Best parameters: `C = 0.1`, `Penalty = l2`, `PCA Components = 80`.
  - Sensitivity: **0.86**, Specificity: **0.81**, AUC: **0.91**.

#### 3. Random Forest
- Addressed class imbalance by assigning weights (`churn = 1`: 0.9, `churn = 0`: 0.1).
- Hyperparameters tuned via Grid Search.
  - Sensitivity: **0.5**, Specificity: **0.98**, AUC: **0.93**.

### Results
- **PCA with Logistic Regression** emerged as the best model:
  - Sensitivity: **0.86**, Specificity: **0.81**, AUC: **0.91**.
- Random Forest achieved high specificity but poor sensitivity, making it less suitable.

---

## Key Insights

### Top Features Influencing Churn
1. **total_ic_mou_8** (Incoming Call Minutes)
   - Customers with fewer incoming calls are more likely to churn.
   - **Strategy**: Encourage incoming calls through incentives.

2. **total_rech_amt_diff** (Recharge Discrepancy)
   - Customers with consistent high recharges are less likely to churn.
   - **Strategy**: Target consistent rechargers with loyalty programs.

3. **total_og_mou_8** (Outgoing Call Minutes)
   - Decreasing outgoing call minutes increases churn probability.
   - **Strategy**: Offer discounts or bundles for outgoing calls.

4. **arpu_8** (Average Revenue Per User)
   - Higher ARPU correlates with lower churn rates.
   - **Strategy**: Maintain or increase ARPU through tailored offers.

---

## Technologies Used

- **Python**: Data preprocessing, modeling, and visualization.
- **Pandas** and **NumPy**: Data manipulation.
- **Scikit-learn**: Machine learning models and preprocessing techniques.
- **KNN Imputer**: Handling missing values.
- **Grid Search**: Hyperparameter tuning.

---

## Conclusion

The combination of **PCA** and **Logistic Regression** with hyperparameter tuning proved to be the most effective model for churn prediction. This approach provides a balanced and accurate solution, enabling telecom operators to identify high-risk customers and implement retention strategies effectively.

For further insights, future iterations could focus on real-time prediction systems and deeper analysis of customer behavior trends.
