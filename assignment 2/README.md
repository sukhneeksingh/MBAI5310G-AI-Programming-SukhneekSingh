MBAI5310G-AI-Programming-SukhneekSingh-Assignment-2
Overview
This repository contains Assignment 2: End-to-End Machine Learning Pipeline for the course Machine Learning Lifecycle & Pipeline Development. The project demonstrates a complete ML workflow for predicting high investment risk customers in the financial services industry.

Business Problem
In the financial services industry, wealth managers and investment advisors must understand their clients' risk profiles to:

Ensure Regulatory Compliance (KYC regulations)
Maintain Client Trust by recommending suitable investment products
Enable Risk Management through balanced portfolio construction
This project builds an end-to-end machine learning pipeline to predict whether a customer is a High Investment Risk client based on demographic and financial data.

Dataset
File: financial_customer_investment_risk_dataset (1).xls
Format: CSV (despite .xls extension)
Samples: 387 customer records
Features: 13 columns (11 features + 1 target + 1 identifier)
Class Distribution: Highly imbalanced (~95% No Risk, ~5% High Risk)
Features Used
Numerical Features (7)
Age - Customer age in years
Annual_Income - Customer's annual income
Investment_Experience_Years - Years of investment experience
Portfolio_Value - Total portfolio value
Number_of_Investment_Products - Count of investment products held
Market_Volatility_Concern - Concern level about market volatility
Financial_Literacy_Score - Financial knowledge score
Categorical Features (4)
Employment_Status - Current employment status
Risk_Tolerance - Customer's risk tolerance level
Advisor_Contacted - Whether customer has consulted an advisor
Previous_Investment_Loss - History of investment losses
Target Variable
High_Investment_Risk - Binary classification (Yes/No or 1/0)
Pipeline Architecture
Step 1: Data Loading & Exploration
Load and inspect dataset dimensions and data types
Perform exploratory data analysis (EDA)
Visualize target variable distribution
Analyze relationships between features and target
Compute correlation matrix
Step 2: Data Preprocessing
The preprocessing pipeline handles:

Numerical Features:

Imputation: Median strategy (robust to outliers)
Scaling: StandardScaler (mean=0, variance=1)
Categorical Features:

Imputation: Most frequent value (mode)
Encoding: OneHotEncoder (creates dummy variables)
Data Leakage Prevention:

All preprocessing fitted only on training data
Applied to test data separately to prevent data leakage
Step 3: Train-Test Split
Train: 80% (309 samples)
Test: 20% (78 samples)
Stratification: Maintains class proportions in both sets
Step 4: Model Training & Evaluation
Baseline Model (Standard Logistic Regression)
Accuracy: 93.59%
Precision (Class 1): 0.00
Recall (Class 1): 0.00
F1-Score (Class 1): 0.00
Issue: Predicts all samples as "No Risk" due to class imbalance
Improved Model (Balanced Logistic Regression)
Accuracy: 92.31%
Precision (Class 1): 0.50
Recall (Class 1): 0.50
F1-Score (Class 1): 0.50
Improvement: Successfully identifies 50% of high-risk clients
Key Results
Problem Identification: The baseline model achieves high accuracy (93.59%) but fails to identify any high-risk customers.

Solution: Using class_weight='balanced' in Logistic Regression addresses the class imbalance by penalizing misclassifications on the minority class.

Trade-off: Slight accuracy decrease (93.59% → 92.31%) but significant improvement in identifying high-risk customers (Recall: 0% → 50%).

Files in Repository
assignment 2.ipynb - Main Jupyter notebook with complete pipeline implementation
financial_customer_investment_risk_dataset (1).xls - Raw dataset
README.md - This file
Technologies & Libraries
pandas - Data manipulation and analysis
numpy - Numerical computations
scikit-learn - Machine learning pipeline and models
Pipeline - End-to-end workflow
ColumnTransformer - Feature preprocessing
LogisticRegression - Classification model
train_test_split - Data splitting
StandardScaler - Feature scaling
SimpleImputer - Missing value handling
OneHotEncoder - Categorical encoding
Classification metrics and confusion matrices
matplotlib - Visualization
seaborn - Statistical visualization
Model Limitations & Future Work
Current Limitations
Extreme Class Imbalance: Only 20 positive examples out of 387 total samples
Small Dataset: Limited samples for training robust models
Potential Data Leakage Risk: In real-world scenarios, need to verify feature definitions
Model Complexity: Logistic Regression is simple but may not capture complex patterns
Future Improvements
Test advanced algorithms (Random Forest, Gradient Boosting)
Implement SMOTE for oversampling minority class
Perform hyperparameter tuning with cross-validation
Feature engineering and selection
Ensemble methods for better generalization
Conclusion
This project demonstrates a complete ML pipeline from raw data to model evaluation, highlighting the importance of:

Proper data preprocessing and feature engineering
Handling class imbalance in real-world datasets
Choosing appropriate evaluation metrics beyond accuracy
Understanding the business context when building models
Course: MBAI5310G - AI Programming
Author: Sukhneek Singh
Assignment: 2
Date: 2026