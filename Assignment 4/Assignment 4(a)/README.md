# Assignment 4(a): Decision Tree Model and Business Interpretation
## ProcurePro Office Supplies — Supplier Delivery Risk Prediction

---

## 📋 Overview

This assignment develops and evaluates a **Decision Tree Classification Model** to predict high-risk supplier purchase orders for **ProcurePro Office Supplies**, a B2B procurement service. The model enables procurement managers to identify orders at risk of delayed delivery and take proactive measures (e.g., contacting suppliers, activating backup vendors) before the promised delivery date.

---

## 🎯 Business Problem

### The Challenge
ProcurePro faces **supplier delivery uncertainty** that impacts customer satisfaction and operational efficiency. Some purchase orders arrive on time, while others are delayed due to:
- Supplier backorders
- Low historical on-time performance
- Long delivery distances
- Urgent order pressure
- Seasonal demand spikes
- Prior quality incidents

### The Opportunity
By predicting which orders are at high risk of delay, procurement managers can:
1. **Reduce late deliveries** through early intervention
2. **Avoid emergency shipping costs** by planning ahead
3. **Prevent customer dissatisfaction** caused by stockouts
4. **Improve supplier management** by identifying consistently unreliable vendors
5. **Prioritize staff effort** toward orders that genuinely need attention

---

## 📊 Dataset

### Dataset Overview
- **Source:** `procurepro_supplier_delay_risk_dataset.xlsx`
- **Records:** 360 historical purchase orders
- **Features:** 18 input features (after removing the ID column)
- **Target Variable:** `Supplier_Delay_Risk` (Binary: Yes/No)

### Class Distribution
| Class | Count | Percentage |
|-------|-------|-----------|
| **Yes** (High Risk) | 214 | 59.4% |
| **No** (Low Risk) | 146 | 40.6% |
*Note: Moderate class imbalance addressed using `class_weight='balanced'` in the Decision Tree.*

### Feature Groups

#### Supplier Profile (3 features)
- `Supplier_Category` — Type of supplier (Breakroom Supplies, IT Accessories, Packaging Materials, etc.)
- `Supplier_Region` — Geographic region (British Columbia, Alberta, Ontario, Quebec, US Midwest, etc.)
- `Contract_Type` — Vendor relationship tier (New Supplier, Approved Vendor, Preferred Vendor)

#### Order Characteristics (3 features)
- `Order_Value_CAD` — Purchase order value in Canadian dollars
- `Number_of_Line_Items` — Number of distinct items in the order
- `Urgent_Order` — Whether the order was marked urgent (Yes/No)

#### Delivery Conditions (3 features)
- `Shipping_Mode` — Delivery method (Local Courier, Expedited Ground, Air Freight, Standard Ground)
- `Promised_Lead_Time_Days` — Days between order and promised delivery
- `Distance_KM` — Distance from supplier to destination

#### Supplier Performance (3 features)
- `Past_On_Time_Rate` — Historical percentage of on-time deliveries (0–1)
- `Supplier_Rating` — Quality rating (1–5)
- `Prior_Delays_Last_6M` — Number of delays in the previous 6 months

#### Risk Indicators (6 features)
- `Backorder_History` — Frequency of backorders (Rare, Occasional, Frequent)
- `Quality_Incidents_Last_6M` — Count of quality issues in the last 6 months
- `Seasonal_Demand_Index` — Demand multiplier for the current season
- `Payment_Terms` — Invoice payment terms (Prepaid, Net 30, Net 60)
- `Seasonal_Period` — Season classification (Regular, Fiscal Year End, Holiday Rush)
- `Inventory_Buffer_Days` — Days of inventory safety stock

### Data Quality
| Issue | Finding |
|-------|---------|
| Missing Values | `Backorder_History`: 127 rows (35.3%) |
| Duplicate Rows | 0 |
| Data Types | 8 categorical, 10 numerical |

**Handling:** Missing values in `Backorder_History` are imputed using the mode (most frequent category) within the scikit-learn Pipeline to prevent data leakage.

---

## 🤖 Model

### Model Architecture

**Algorithm:** Decision Tree Classifier

**Hyperparameters:**
- `max_depth=5` — Limits tree depth to prevent overfitting
- `min_samples_leaf=10` — Requires minimum 10 samples per leaf to reduce noise
- `class_weight='balanced'` — Adjusts for class imbalance (59% vs. 41% split)
- `random_state=42` — Ensures reproducibility

### Preprocessing Pipeline

The model uses a scikit-learn `ColumnTransformer` pipeline:

| Step | Transformer | Input Features |
|------|-------------|-----------------|
| **Numerical** | StandardScaler (after median imputation) | 10 numerical features |
| **Categorical** | OneHotEncoder (after mode imputation) | 8 categorical features |

This ensures consistent preprocessing on training and test data without data leakage.

### Train/Test Split
- **Training Set:** 270 records (75%)
- **Testing Set:** 90 records (25%)
- **Stratification:** Used to preserve class proportions in both sets

---

## 📈 Model Performance

### Overall Accuracy
| Metric | Training | Testing | Gap |
|--------|----------|---------|-----|
| **Accuracy** | 86.3% | 70.0% | **16.3 pp** |

**Interpretation:** The 16.3 percentage point gap indicates **moderate-to-strong overfitting**. The model memorizes training patterns but generalizes less well to unseen data. This is mitigated by limiting tree depth and requiring minimum samples per leaf.

### High-Risk Class (Yes = Delay Risk) Performance
| Metric | Value |
|--------|-------|
| **Precision** | 74.1% |
| **Recall** | 75.5% |
| **F1-Score** | 74.8% |

**Interpretation:**
- **Precision (74.1%):** When the model predicts "high risk," it is correct 74% of the time (1 in 4 flagged orders is actually low-risk).
- **Recall (75.5%):** The model correctly identifies 75.5% of actual high-risk orders (misses ~25%).
- **F1-Score (74.8%):** Balanced harmonic mean; strong overall performance for the business-critical class.

### Confusion Matrix (Test Set)
```
                 Predicted No    Predicted Yes
Actual No              40              7
Actual Yes            22              21
```
- **True Negatives (TN):** 40 — Correctly identified as low-risk
- **False Positives (FP):** 7 — Flagged as high-risk but were actually low-risk
- **False Negatives (FN):** 22 — Missed actual high-risk orders
- **True Positives (TP):** 21 — Correctly identified as high-risk

---

## 🔍 Feature Importance

### Primary Driver: Historical On-Time Performance

| Feature | Importance | Interpretation |
|---------|-----------|-----------------|
| **`Past_On_Time_Rate`** | **62.4%** | **Dominant predictor.** Suppliers with low past on-time rates are much more likely to delay future orders. |
| Other features combined | 37.6% | Distance, demand index, urgency, and other factors collectively contribute to remaining predictive power. |

**Business Insight:** Historical supplier reliability is the strongest signal for predicting delivery risk. Procurement teams should implement an **early warning threshold** at `Past_On_Time_Rate < 75%` and consider transitioning suppliers below this level out of preferred tiers.

---

## 💡 Key Findings & Recommendations

### Executive Summary

1. **Model Accuracy:** 70% test accuracy with balanced high-risk class performance (F1=74.8%)
2. **Primary Risk Factor:** `Past_On_Time_Rate` accounts for 62.4% of model predictions
3. **Overfitting:** 16.3 pp gap between training and test accuracy (moderate concern, mitigated by tree depth limits)
4. **Data Limitation:** 35% missing data in `Backorder_History` may mask supplier uncertainty

### Actionable Recommendations

#### For Procurement Managers:
1. **Implement Early Warning System:** Flag orders from suppliers with `Past_On_Time_Rate < 75%` for proactive review.
2. **Supplier Transition Plan:** Consider moving suppliers with low on-time rates to lower-priority tiers.
3. **Backup Activation:** Use model predictions to preemptively activate backup suppliers for flagged orders.
4. **Lead-Time Adjustment:** For high-risk suppliers, increase promised lead times or add buffer time.

#### For Data Science Team:
1. **Improve Backorder Data:** Collect complete `Backorder_History` data to better capture supplier uncertainty.
2. **Monitor Model Drift:** Retrain the model quarterly as supplier performance and seasonal patterns evolve.
3. **Threshold Optimization:** Experiment with prediction probability thresholds to balance precision vs. recall based on business costs.
4. **Ensemble Exploration:** Compare Decision Tree performance against Random Forest or Gradient Boosting models.

---

## 📁 File Structure

```
Assignment 4(a)/
├── README.md                                          # This file
├── Assignment_4_ProcurePro_Decision_Tree.ipynb        # Main analysis notebook
└── procurepro_supplier_delay_risk_dataset.xlsx        # Dataset (360 orders)
```

---

## 🚀 How to Use

### Prerequisites
```python
pandas
numpy
matplotlib
seaborn
scikit-learn
openpyxl (for Excel import)
```

### Running the Notebook

1. **Clone or download** the repository
2. **Navigate** to `Assignment 4/Assignment 4(a)/`
3. **Open** `Assignment_4_ProcurePro_Decision_Tree.ipynb` in Jupyter Notebook or JupyterLab
4. **Run all cells** in order (or select individual sections)
5. **Review outputs:** Confusion matrices, feature importance plots, and business recommendations

### Key Sections in Notebook

| Section | Purpose |
|---------|---------|
| **Task 1** | Understand business problem and target variable |
| **Task 2** | Load, clean, and prepare data |
| **Task 3** | Train Decision Tree model and evaluate performance |
| **Task 4** | Visualize tree structure and feature importance |
| **Task 5** | Generate business recommendations |

---

## 📌 Limitations & Future Improvements

### Current Limitations
1. **Missing Data:** 35.3% of `Backorder_History` entries are missing
2. **Moderate Overfitting:** 16.3 pp gap suggests tree could overfit on training patterns
3. **Class Imbalance:** 59% vs. 41% split affects minority class recall
4. **Limited Features:** May not capture all supplier-specific or external factors (e.g., supply chain disruptions)

### Future Improvements
1. **Collect Complete Data:** Ensure `Backorder_History` is fully populated for future datasets
2. **Model Ensemble:** Compare Decision Tree with Random Forest, XGBoost, and Logistic Regression
3. **Cost-Sensitive Learning:** Weight false positives vs. false negatives based on business impact
4. **External Data:** Incorporate supply chain indices, weather, or geopolitical factors
5. **Real-Time Monitoring:** Deploy model as a live decision support tool with retraining pipelines

---

## 📚 References

- **Scikit-learn Documentation:** https://scikit-learn.org/
- **Decision Trees in Machine Learning:** https://en.wikipedia.org/wiki/Decision_tree_learning
- **Class Imbalance Handling:** https://imbalanced-learn.org/

---

## ✍️ Author

**Assignment:** MBAI 5310G — AI Programming  
**Student:** Sukhneek Singh  
**Date:** June 2026

---

## 📧 Contact & Questions

For questions about this assignment, please refer to the notebook documentation or contact your course instructor.

---

*Last Updated: June 9, 2026*
