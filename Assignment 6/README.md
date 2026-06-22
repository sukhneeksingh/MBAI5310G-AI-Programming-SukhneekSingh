# Assignment 6: Model Evaluation, Explainability, and Fairness Reflection

## Overview

This assignment demonstrates a complete machine learning workflow for predicting vehicle-service customer rebooking behavior. The project covers data loading, preprocessing, model training, comprehensive evaluation, model explainability, and fairness analysis.

## Business Objective

**Goal:** Predict whether a vehicle-service customer will rebook a future service appointment.

**Target Variable:** `service_rebooked` (1 = rebooked, 0 = not rebooked)

**Use Case:** This prediction helps the business understand customer loyalty patterns and identify at-risk customers who may not return for future service appointments.

## Dataset

### File: `vehicle_service_rebooking_dataset.csv`

**Size:** 360 customer records with 17 features

**Key Features:**
- **Customer Demographics:** age, age_group, gender, region
- **Vehicle Information:** vehicle_type, vehicle_age_years, mileage_km
- **Service Details:** service_type, service_rating, last_service_cost
- **Behavioral Metrics:** number_of_previous_services, days_since_last_service, waiting_time_minutes
- **Promotions:** coupon_used
- **Loyalty:** customer_segment (New, Returning, Loyal, Fleet)

### Data Characteristics

- **Target Distribution:** 80% negative class (not rebooked), 20% positive class (rebooked) → imbalanced dataset
- **Missing Values:** 8 values in `number_of_previous_services` column (handled via median imputation)
- **No Duplicate Records:** Each customer ID is unique

## Project Structure

### Files Included

```
Assignment 6/
├── Assignment 6.ipynb                           # Main Jupyter notebook
├── vehicle_service_rebooking_dataset.csv        # Dataset
└── README.md                                     # This file
```

### Notebook Contents

#### **Task 1: Load and Understand the Dataset**
- Extract and parse customer service data
- Perform exploratory data analysis (EDA)
- Analyze feature distributions and target variable imbalance
- Check for missing values and duplicates

#### **Task 2: Define Features and Target Variable**
- Identify 10 model input features (excluding identifiers and fairness columns)
- Separate fairness-sensitive attributes (gender, age_group, region) for bias analysis
- Establish clear feature engineering approach

#### **Task 3: Data Preprocessing**
- Implement a preprocessing pipeline using scikit-learn
- Handle missing values with median imputation for numeric features
- Encode categorical variables using One-Hot Encoding
- Ensure reproducibility with consistent random states

#### **Task 4: Train/Test Split**
- Use stratified 75-25 train-test split to preserve class distribution
- Training set: 270 records
- Testing set: 90 records

#### **Task 5: Train a Decision Tree Classifier**
- Build a baseline Decision Tree model
- Tune hyperparameters (max_depth, min_samples_split, min_samples_leaf)
- Handle class imbalance during training

#### **Task 6: Evaluation Metrics**
Comprehensive evaluation using:
- **Accuracy:** Overall correctness (80% baseline threshold consideration)
- **Precision:** False positive rate impact on business
- **Recall:** False negative rate - missing rebooking customers
- **F1-Score:** Balanced performance metric
- **Confusion Matrix:** TP, TN, FP, FN visualization

#### **Task 7: Error Analysis**
- Analyze misclassified predictions
- Identify patterns in false positives and false negatives
- Understand model limitations and bias sources

#### **Task 8: Cross-Validation**
- Implement Stratified K-Fold cross-validation (k=5)
- Evaluate model stability across different data splits
- Compare cross-val scores with test set performance

#### **Task 9: Overfitting Analysis**
- Compare training vs. test set performance
- Examine learning curves
- Assess model generalization capability

#### **Task 10: Model Explainability**
Two complementary explainability approaches:

##### **SHAP (SHapley Additive exPlanations)**
- Global feature importance
- Local individual prediction explanations
- Force plots and summary plots

##### **LIME (Local Interpretable Model-agnostic Explanations)**
- Model-agnostic local explanations
- Feature contribution for specific predictions
- Easy-to-understand visualizations

#### **Task 11: Fairness Reflection**
Critical analysis of potential fairness issues:
- **Demographic Parity:** Are reboking rates equal across protected groups?
- **Equal Opportunity:** Do different groups have equal true positive rates?
- **Calibration:** Are prediction confidences accurate across groups?
- **Bias Mitigation Strategies:** Recommendations for fair AI deployment

## Key Dependencies

```python
pandas              # Data manipulation
numpy              # Numerical computing
scikit-learn       # Machine learning models and preprocessing
matplotlib         # Data visualization
seaborn            # Statistical data visualization
shap               # Model explainability
lime               # Local interpretable explanations
```

## Model Architecture

```
Input Features (10 features)
          ↓
Preprocessing Pipeline
  ├─ Numeric: Median Imputation
  └─ Categorical: One-Hot Encoding
          ↓
Decision Tree Classifier
          ↓
Predictions (Binary: 0 or 1)
```

## Running the Notebook

1. **Install Dependencies:**
   ```bash
   pip install pandas numpy scikit-learn matplotlib seaborn shap lime
   ```

2. **Run All Cells:**
   - Execute cells sequentially in Jupyter
   - The notebook is designed to run end-to-end without manual intervention

3. **Output:**
   - Console outputs show metrics and analysis
   - Visualizations are embedded in notebook cells
   - CSV files are saved for reference

## Key Results & Insights

### Model Performance
- Model demonstrates ability to identify rebooking patterns
- Imbalanced dataset requires careful metric interpretation
- Recall is critical to identify customers likely to rebook

### Fairness Findings
- Key demographics (gender, age_group, region) should be monitored for disparate impact
- Recommendation: Regular fairness audits before deployment
- Consider fairness constraints if significant disparities detected

### Explainability Insights
- SHAP identifies most important features driving predictions
- LIME provides customer-level explanations
- Both methods agree on top feature importance

## Recommendations for Deployment

1. **Monitor for Bias:** Track model performance across demographic groups
2. **Threshold Tuning:** Adjust decision threshold based on business costs
3. **Regular Retraining:** Update model with new customer data quarterly
4. **Fairness Constraints:** Consider debiasing techniques if disparities found
5. **Human Oversight:** Use model as decision support, not replacement

## References & Further Reading

- [scikit-learn Documentation](https://scikit-learn.org/)
- [SHAP Paper](https://arxiv.org/abs/1705.07874)
- [LIME Paper](https://arxiv.org/abs/1602.04938)
- [Fairness in Machine Learning](https://fairmlbook.org/)

## Author Information

**Course:** MBAI5310G - AI Programming  
**Assignment:** 6  
**Student:** Sukhneek Singh

---

**Last Updated:** June 22, 2026
