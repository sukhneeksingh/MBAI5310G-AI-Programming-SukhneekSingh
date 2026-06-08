# MBAI5310G AI Programming
Student Name: Sukhneek Singh
Course: MBAI 5310G - AI Programming
This repository contains my weekly coding assignments and final AI programming project for MBAI 5310G.
The repository will include Jupyter/Colab notebooks, code, outputs, README files, and documentation for
reproducibility.

# MBAI 5310G – AI Programming
### Sukhneek Singh | Ontario Tech University

This repository contains coding assignments completed as part of **MBAI 5310G – AI Programming**. Each assignment builds progressively on core AI and machine learning concepts, moving from Python fundamentals through supervised and unsupervised learning, and applying results in business contexts.

---

## Repository Contents

| File | Description |
|------|-------------|
| `Assignment 2.ipynb` | Python Foundations & Exploratory Data Analysis |
| `Assignment 3.ipynb` | Supervised Learning – Regression & Classification Intro |
| `Assignment 4_ProcurePro_Decision_Tree.ipynb` | Decision Tree – ProcurePro Business Case |
| `Assignment 4_UrbanFleet_DecisionTree_Assignment.ipynb` | Decision Tree – UrbanFleet Logistics Business Case |
| `Assignment 5_unsupervised_learning_segmentation.ipynb` | Unsupervised Learning – Customer Segmentation |

---

## Assignment 2 – Python Foundations & Exploratory Data Analysis

### Overview
This assignment covers the core Python programming skills needed for AI and data science work. It includes hands-on practice with data structures, control flow, functions, and essential libraries, followed by an introductory exploratory data analysis (EDA) workflow.

### Topics Covered
- Python data types, lists, dictionaries, and loops
- Writing and calling functions
- Working with `pandas` for data loading, inspection, and cleaning
- Working with `numpy` for numerical operations
- Exploratory data analysis: shape, data types, missing values, descriptive statistics
- Basic data visualization using `matplotlib` and `seaborn`

### Libraries Used
`pandas` · `numpy` · `matplotlib` · `seaborn`


---

## Assignment 3 – Supervised Learning: Regression & Classification Introduction

### Overview
This assignment introduces supervised machine learning. It covers the end-to-end workflow of loading a dataset, preparing features, training a model, and evaluating its performance. Both regression and classification approaches are explored in the context of a financial business scenario.

### Dataset
**`financial_customer_investment_risk_dataset.xls`** — Contains customer financial and demographic information used to predict investment risk levels.

### Topics Covered
- Loading and inspecting a real-world dataset
- Handling missing values and encoding categorical variables
- Splitting data into training and testing sets
- Training a classification or regression model using `scikit-learn`
- Evaluating model performance (accuracy, confusion matrix, or RMSE depending on task)
- Interpreting model results in a business context

### Libraries Used
`pandas` · `numpy` · `scikit-learn` · `matplotlib` · `seaborn`


---

## Assignment 4 – Decision Tree Classification & Business Interpretation

Assignment 4 contains **two separate notebooks**, each applying a Decision Tree classification model to a different business scenario.

---

### 4A – ProcurePro Decision Tree

**File:** `Assignment 4_ProcurePro_Decision_Tree.ipynb`

#### Overview
This notebook applies a Decision Tree model to a procurement or supply chain business problem. The assignment follows the same four-task structure as the UrbanFleet case: understanding the business problem, preparing data, training the model, and interpreting results from a business perspective.

#### Topics Covered
- Business problem framing and target variable identification
- Data cleaning, encoding, and train-test split
- Decision Tree training and evaluation (confusion matrix, accuracy, precision, recall, F1-score)
- Training vs. testing accuracy comparison and overfitting analysis
- Feature importance analysis and business interpretation
- Discussion of false positives, false negatives, and evaluation metric priorities

#### Libraries Used
`pandas` · `numpy` · `scikit-learn` · `matplotlib` · `seaborn`



---

### 4B – UrbanFleet Logistics Decision Tree

**File:** `Assignment 4_UrbanFleet_DecisionTree_Assignment.ipynb`

#### Business Context
**UrbanFleet Logistics** is a same-day and next-day delivery company serving retail customers, small businesses, corporate clients, and marketplace sellers. The company wants to predict which orders are at **high risk of late delivery** before dispatch, so operations staff can take proactive action.

#### Dataset
**`urbanfleet_delivery_delay_risk_dataset.xlsx`** — 360 delivery orders with 18 features including delivery region, distance, warehouse load, weather conditions, traffic level, driver experience, and more.

**Target variable:** `Late_Delivery_Risk` (Yes / No)

#### Task Structure

| Task | Description |
|------|-------------|
| Task 1 | Business problem understanding and target/feature identification |
| Task 2 | Data loading, inspection, cleaning, encoding, and train-test split |
| Task 3 | Decision Tree training and evaluation (confusion matrix, accuracy, precision, recall, F1) |
| Task 4 | Business interpretation of model results |

#### Key Results

| Metric | Value |
|--------|-------|
| Training Accuracy | 100% |
| Testing Accuracy | 61.1% |
| Precision (High Risk) | 0.25 |
| Recall (High Risk) | 0.28 |
| F1-Score (High Risk) | 0.26 |

The large gap between training and testing accuracy (≈39 percentage points) is a clear sign of **overfitting**. The unconstrained Decision Tree memorised the training data rather than learning generalised patterns. Hyperparameter tuning (e.g., `max_depth`, `min_samples_leaf`) or an ensemble method such as Random Forest is recommended for improvement.

#### Top Features by Importance
1. `Package_Weight_Kg` (0.2149)
2. `Dispatch_Hour` (0.1284)
3. `Order_Value_USD` (0.1198)
4. `Distance_Km` (0.1182)
5. `Driver_Experience_Years` (0.0912)
6. `Weather_Condition_Rain` (0.0756)

#### Business Takeaways
- **Recall** is the most critical metric for UrbanFleet — missing a high-risk order (false negative) leads to a late delivery, customer dissatisfaction, and possible refunds
- Heavy packages, late dispatch hours, long distances, and rainy weather are the strongest signals of delivery risk
- The model should be used as a **decision-support tool**, with human staff reviewing predictions before acting

#### Libraries Used
`pandas` · `numpy` · `scikit-learn` · `matplotlib` · `seaborn`



---

## Assignment 5 – Unsupervised Learning: Customer Segmentation

**File:** `Assignment 5_unsupervised_learning_segmentation.ipynb`

### Overview
This assignment applies **unsupervised machine learning** to a customer segmentation problem. Unlike supervised learning, the model is not given labelled outcomes — instead, it discovers natural groupings within the data based on customer characteristics.

### Topics Covered
- Introduction to unsupervised learning and its business applications
- Data preparation and feature scaling for clustering
- K-Means Clustering — training and selecting the optimal number of clusters (Elbow Method / Silhouette Score)
- Cluster profiling and business interpretation: describing what each customer segment looks like
- Visualising clusters using dimensionality reduction (PCA) or 2D scatter plots
- Discussion of how segmentation results can inform marketing, product, and operational decisions

### Business Value
Customer segmentation allows businesses to:
- Tailor marketing campaigns to specific customer groups
- Identify high-value vs. at-risk customer segments
- Personalise product offerings and service levels
- Allocate resources more effectively across segments

### Libraries Used
`pandas` · `numpy` · `scikit-learn` · `matplotlib` · `seaborn`


---

## Requirements

All notebooks are written in **Python 3** and can be run in Jupyter Notebook or Google Colab. The main libraries required are:

```
pandas
numpy
scikit-learn
matplotlib
seaborn
openpyxl        # for reading .xlsx files
xlrd            # for reading .xls files
```

To install all dependencies at once:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn openpyxl xlrd
```

---

