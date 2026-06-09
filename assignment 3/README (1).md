# MBAI5310G AI Programming - Assignment 3

## Classification Models and Evaluation Metrics

### Course Topic
Model Evaluation, SVM vs. Logistic Regression, and Business Metrics

---

## 📋 Overview

This assignment implements and compares two prominent classification algorithms to predict **High Investment Risk** for financial customers:

1. **Logistic Regression** - A probabilistic linear classification model
2. **Support Vector Machine (SVM)** - A margin-maximizing classifier

Each model is trained in two variants:
- **Standard** - Default model without class weighting
- **Balanced** - With `class_weight='balanced'` to handle class imbalance

### Evaluation Metrics
- Confusion Matrix
- Accuracy
- Precision
- Recall
- F1-Score

---

## 💼 Business Problem Context

**Objective:** Predict `High_Investment_Risk` (Yes/No) using the Financial Customer Investment Risk Dataset.

**Why This Matters:**
- Missing a high-risk customer (False Negative) has severe financial and legal consequences
- The customer could invest in highly volatile assets, resulting in devastating losses
- Regulatory non-compliance and potential lawsuits may ensue
- Therefore, **Recall (sensitivity) on the High-Risk class is critical**

---

## 📁 Repository Structure

```
MBAI5310G-AI-Programming-SukhneekSingh-Assignment-3/
├── README.md                                          # This file
├── assignment 3.ipynb                                # Main Jupyter notebook with analysis
└── financial_customer_investment_risk_dataset (1).xls # Dataset (387 rows, ~95% class imbalance)
```

---

## 🔧 Installation & Setup

### Requirements
```python
pandas
numpy
matplotlib
seaborn
scikit-learn
```

### Install Dependencies
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

### Run the Notebook
```bash
jupyter notebook "assignment 3.ipynb"
```

---

## 📊 Dataset Details

**File:** `financial_customer_investment_risk_dataset (1).xls`

- **Rows:** 387 customer records
- **Target Variable:** `High_Investment_Risk` (Yes/No)
- **Class Distribution:** ~95% "No" (Low Risk) vs ~5% "Yes" (High Risk)
- **Features:** Customer demographics, financial metrics, and investment preferences

**Challenge:** Severe class imbalance requires special handling to avoid bias toward the majority class.

---

## 🚀 Key Findings

### Model Performance Comparison

| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| Standard Logistic Regression | 93.59% | 0% | 0% | 0% |
| Balanced Logistic Regression | 92.31% | 33.33% | 50.00% | 40.00% |
| Standard SVM (Linear) | 92.31% | 0% | 0% | 0% |
| Balanced SVM (Linear) | 91.03% | 28.57% | 50.00% | 36.36% |

### 🏆 Best Model: **Balanced Logistic Regression**

**Why?**
- Achieves the highest Recall (50%) while identifying at-risk customers
- Better precision than balanced SVM (33.33% vs 28.57%)
- Best F1-score (40.00%) balancing precision-recall tradeoff
- Logistic Regression is interpretable and efficient

### Critical Insights

1. **Standard models fail due to class imbalance**
   - Achieve high accuracy but 0% recall on the minority class
   - They simply predict "No Risk" for everyone, missing all high-risk customers

2. **Balanced models prioritize recall**
   - Logistic Regression with balanced classes detects 50% of high-risk customers
   - Trade-off: 33.33% precision (2 false alarms per correct prediction)

3. **Business Metric Priority: Recall > Precision**
   - Missing high-risk customers is more costly than false alarms
   - Better to over-flag and manually review than miss at-risk clients

---

## 📌 Business Interpretation

### False Positives (FP)
- **Definition:** Model predicts "High Risk" but customer is actually low risk
- **Business Impact:** Advisor might restrict profitable investments or waste resources on unnecessary analysis
- **Cost:** Low-medium (customer annoyance, opportunity loss)

### False Negatives (FN) ⚠️
- **Definition:** Model predicts "Low Risk" but customer is actually high risk
- **Business Impact:** Customer invests in volatile assets, suffers devastating losses, potential legal action
- **Cost:** High (financial loss, regulatory penalties, reputational damage)

**Conclusion:** FN is exponentially more costly → **Maximize Recall**

---

## ⚖️ Model Limitations & Biases

1. **Class Imbalance & Representation Bias**
   - Dataset has only ~20 high-risk customers out of 387
   - Model heavily biased toward majority class even with balancing

2. **Limited Data**
   - Small dataset (387 rows) limits model generalizability
   - Vulnerable to overfitting and outliers

3. **Qualitative Context Missing**
   - Model only sees numerical features
   - Cannot capture customer's life changes (health, employment, major expenses)
   - Lacks psychological factors affecting risk tolerance

4. **High False Positive Rate**
   - Balanced model misclassifies 66.67% of "high-risk" predictions as false positives
   - Requires significant manual review overhead

---

## 🧠 Why Human Judgment is Essential

1. **Contextual Understanding**
   - Humans understand qualitative factors (family situation, health status, life plans)
   - Models only see data in the feature columns

2. **Empathy & Communication**
   - Financial advisors can gauge psychological comfort with risk through conversation
   - Adapt recommendations based on emotional state and personal values

3. **Model Uncertainty**
   - Best model misses 50% of high-risk customers
   - 2 out of 3 "high-risk" predictions are false positives
   - Manual review is necessary to catch errors

4. **Regulatory & Ethical Responsibility**
   - Investment advisors have fiduciary duties
   - Cannot delegate all decisions to imperfect ML models
   - Need human oversight for compliance and ethics

---

## 🔍 Code Structure

### Step 0: Import Libraries
- Standard ML libraries (pandas, scikit-learn, matplotlib, seaborn)

### Step 1: Data Preprocessing
- Load data and define features/target
- 80/20 train-test split (stratified)
- Handle missing values and encode categorical variables

### Step 2-3: Model Training
- Build preprocessing pipelines (imputation + scaling/encoding)
- Train 4 model variants
- Evaluate using confusion matrix and standard metrics

### Step 4: Comparison & Visualization
- Create comparison DataFrame
- Generate bar plots and confusion matrices
- Interpret results in business context

---

## 📈 Visualizations Generated

1. **Model Comparison Bar Chart** - Compare accuracy, precision, recall, F1-score across models
2. **Confusion Matrices** - 2×2 grid showing TN, FP, FN, TP for each model

---

## 🎯 Conclusions & Recommendations

1. **Use Balanced Logistic Regression** for this problem
   - Superior recall identifies more high-risk customers
   - Better precision than balanced SVM
   - Simpler, more interpretable than SVM

2. **Implement Manual Review Process**
   - Every "high-risk" prediction should trigger advisor review
   - Combine model output with human judgment

3. **Collect More Data**
   - Current dataset is too small (~387 rows)
   - More high-risk examples would improve model robustness

4. **Monitor Model Performance**
   - Regularly retrain with new customer data
   - Track false negative rate in production
   - Adjust thresholds based on business cost of errors

---

## 👤 Author

**Sukhneek Singh**  
MBAI5310G - AI Programming  
Assignment 3

---

## 📚 References

- scikit-learn documentation: https://scikit-learn.org/
- Confusion Matrix & Metrics: https://scikit-learn.org/stable/modules/model_evaluation.html
- Class Imbalance Handling: https://imbalanced-learn.org/

---

## 📝 Notes

- All models use `random_state=42` for reproducibility
- SVM uses linear kernel for fair comparison with Logistic Regression
- Results are based on 80/20 train-test split with stratification
