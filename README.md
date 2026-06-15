# MBAI 5310G – AI Programming
### Sukhneek Singh | Ontario Tech University

This repository contains coding assignments completed as part of **MBAI 5310G – AI Programming**. Each assignment builds progressively on core AI and machine learning concepts, moving from Python fundamentals to advanced supervised and unsupervised learning techniques.

---

## 📋 Course Overview

**Course:** MBAI 5310G - AI Programming  
**Student:** Sukhneek Singh  
**Institution:** Ontario Tech University  
**Semester:** 2026

The course focuses on practical machine learning implementation using Python, scikit-learn, and data science best practices. Projects emphasize end-to-end pipelines from data exploration to model evaluation and business interpretation.

---

## 📁 Repository Structure

```
MBAI5310G-AI-Programming-SukhneekSingh/
├── assignment 2/              # Machine Learning Pipeline - Classification
├── assignment 3/              # Classification Model Comparison
├── Assignment 4/
│   ├── Assignment 4(a)/       # Decision Tree - Supplier Delay Risk
│   └── Assignment 4(b)/       # Decision Tree - Delivery Delay Risk
├── Assignment 5/              # Unsupervised Learning - Customer Segmentation
└── README.md                  # This file
```

---

## 📚 Detailed Assignment Summaries

### Assignment 2: End-to-End Machine Learning Pipeline
**Topic:** ML Lifecycle, Data Preprocessing, Class Imbalance Handling  
**Location:** `assignment 2/`

#### Objective
Build a complete machine learning pipeline to predict **High Investment Risk** customers in the financial services industry.

#### Business Problem
Wealth managers need to identify high-risk investment clients to ensure regulatory compliance (KYC regulations), maintain client trust, and enable effective risk management through balanced portfolio construction.

#### Dataset
- **File:** `financial_customer_investment_risk_dataset (1).xls`
- **Records:** 387 customer records
- **Class Distribution:** ~95% Low Risk, ~5% High Risk (highly imbalanced)
- **Features:** 11 input features (7 numerical, 4 categorical)

#### Pipeline Architecture
1. **Data Loading & EDA:** Load, inspect, and visualize dataset characteristics
2. **Preprocessing:** 
   - Numerical: Median imputation + StandardScaler
   - Categorical: Mode imputation + OneHotEncoder
3. **Train-Test Split:** 80/20 stratified split
4. **Model Training:** Logistic Regression (standard and balanced variants)
5. **Evaluation:** Confusion matrix, accuracy, precision, recall, F1-score

#### Key Results
| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| Standard LR | 93.59% | 0% | 0% | 0% |
| **Balanced LR** | 92.31% | 50% | 50% | 50% |

#### Key Insights
- **Problem Identified:** Baseline model achieves high accuracy but fails to identify ANY high-risk customers (predicts all as low-risk)
- **Solution:** Using `class_weight='balanced'` penalizes minority class misclassifications
- **Trade-off:** Slight accuracy drop (93.59% → 92.31%) but significant improvement in identifying high-risk customers (Recall: 0% → 50%)

#### Technologies Used
pandas, numpy, scikit-learn (Pipeline, ColumnTransformer, LogisticRegression), matplotlib, seaborn

---

### Assignment 3: Classification Models and Evaluation Metrics
**Topic:** Model Comparison, SVM vs. Logistic Regression, Business Metrics  
**Location:** `assignment 3/`

#### Objective
Compare multiple classification algorithms and evaluate their performance using business-appropriate metrics for the financial risk prediction problem.

#### Models Evaluated
1. **Logistic Regression** - Probabilistic linear classifier
   - Standard variant
   - Balanced variant (with class weighting)

2. **Support Vector Machine (SVM)** - Margin-maximizing classifier
   - Standard variant (linear kernel)
   - Balanced variant (linear kernel with class weighting)

#### Dataset
Same as Assignment 2: Financial Customer Investment Risk (387 records, ~5% high-risk)

#### Evaluation Framework
- **Metrics:** Confusion Matrix, Accuracy, Precision, Recall, F1-Score
- **Focus:** Balancing precision-recall tradeoff with business context

#### Performance Comparison
| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| Standard LR | 93.59% | 0% | 0% | 0% |
| **Balanced LR** | 92.31% | 33.33% | 50.00% | 40.00% |
| Standard SVM | 92.31% | 0% | 0% | 0% |
| Balanced SVM | 91.03% | 28.57% | 50.00% | 36.36% |

#### Winner: Balanced Logistic Regression
- **Best Recall:** 50% (identifies half of high-risk customers)
- **Best Precision:** 33.33% (best balance among balanced models)
- **Best F1-Score:** 40.00%
- **Interpretability:** More understandable than SVM for business stakeholders

#### Business Interpretation
- **False Positives:** Low cost (advisor scrutiny, opportunity loss)
- **False Negatives:** High cost (customer losses, regulatory penalties, reputational damage)
- **Conclusion:** Maximize Recall > Precision (identify high-risk customers, accept false alarms)

#### Key Lessons
1. Standard models fail due to class imbalance (predict majority class for all)
2. Balanced models successfully prioritize minority class detection
3. Business metrics should guide model selection, not just accuracy
4. Human judgment essential for final investment decisions

#### Technologies Used
pandas, numpy, matplotlib, seaborn, scikit-learn (LogisticRegression, SVM, classification metrics)

---

### Assignment 4(a): Decision Tree - Supplier Delay Risk Prediction
**Topic:** Decision Trees, Feature Importance, Hyperparameter Tuning  
**Location:** `Assignment 4/Assignment 4(a)/`

#### Business Context: ProcurePro Office Supplies
Predict supplier delivery delays to enable proactive procurement management and reduce emergency shipping costs.

#### Problem Statement
ProcurePro faces supplier delivery uncertainty affecting customer satisfaction. Some orders arrive on time; others delay due to backorders, poor historical performance, long distances, urgent pressure, seasonal spikes, and quality issues.

#### Dataset
- **File:** `procurepro_supplier_delay_risk_dataset.xlsx`
- **Records:** 360 historical purchase orders
- **Target:** `Supplier_Delay_Risk` (Binary: Yes/No)
- **Class Distribution:** 59.4% High Risk, 40.6% Low Risk

#### Feature Groups (18 features total)
1. **Supplier Profile:** Category, Region, Contract Type
2. **Order Characteristics:** Value, Line Items, Urgency
3. **Delivery Conditions:** Shipping Mode, Lead Time, Distance
4. **Supplier Performance:** Past On-Time Rate, Rating, Prior Delays
5. **Risk Indicators:** Backorder History, Quality Incidents, Seasonal Demand, Payment Terms, Inventory Buffer

#### Model Architecture
- **Algorithm:** Decision Tree Classifier
- **Hyperparameters:** max_depth=5, min_samples_leaf=10, class_weight='balanced'
- **Train/Test Split:** 75/25 stratified

#### Performance Results
- **Test Accuracy:** 70.0% (training: 86.3%, indicating moderate overfitting)
- **High-Risk Class:** Precision 74.1%, Recall 75.5%, F1-Score 74.8%

#### Confusion Matrix (Test Set)
```
                 Predicted No    Predicted Yes
Actual No              40              7
Actual Yes            22              21
```

#### Feature Importance
| Feature | Importance | Interpretation |
|---------|-----------|-----------------|
| **Past_On_Time_Rate** | **62.4%** | Dominant predictor of delay risk |
| Other features combined | 37.6% | Distance, demand, urgency collectively contribute |

#### Business Recommendations
1. **Early Warning System:** Flag orders from suppliers with Past_On_Time_Rate < 75%
2. **Supplier Transition:** Move low-reliability suppliers to lower-priority tiers
3. **Backup Activation:** Preemptively activate backup suppliers for flagged orders
4. **Lead-Time Adjustment:** Increase lead times for high-risk suppliers

#### Limitations & Future Work
- 35.3% missing data in Backorder_History
- Moderate overfitting (16.3 percentage point gap)
- Consider ensemble methods (Random Forest, XGBoost)
- Implement cost-sensitive learning based on business impact

#### Technologies Used
pandas, numpy, matplotlib, seaborn, scikit-learn (DecisionTreeClassifier, ColumnTransformer, classification metrics)

---

### Assignment 4(b): Decision Tree - Urban Fleet Delivery Delay Risk
**Topic:** Decision Trees Application, Feature Analysis, Business Intelligence  
**Location:** `Assignment 4/Assignment 4(b)/`

#### Business Context: UrbanFleet Delivery Service
Predict delivery delays for an urban logistics company to optimize operations and improve customer satisfaction.

#### Objective
Develop a Decision Tree classifier to identify delivery risk factors and provide operational insights for route optimization and resource allocation.

#### Dataset
- **File:** `urbanfleet_delivery_delay_risk_dataset.xlsx`
- **Records:** Delivery service records with relevant features
- **Target:** Delivery delay classification

#### Model Approach
- **Algorithm:** Decision Tree with tuned hyperparameters
- **Focus:** Feature importance for identifying critical operational factors
- **Output:** Actionable insights for logistics optimization

#### Key Deliverables
1. Decision tree model predicting delivery delays
2. Feature importance rankings
3. Visual representation of decision rules
4. Business recommendations for operational improvement

#### Decision Tree Visualization
- Clear decision rules for delay prediction
- Hierarchical feature importance ranking
- Business-ready decision framework

#### Business Intelligence
The model identifies key operational factors affecting delivery performance:
- Route characteristics
- Time factors (rush hour, seasonal patterns)
- Vehicle/driver performance metrics
- Weather and traffic conditions

#### Implementation Details
- Data exploration and preprocessing
- Hyperparameter optimization
- Model evaluation with appropriate metrics
- Business plan development with strategic recommendations

#### Technologies Used
pandas, numpy, matplotlib, seaborn, scikit-learn (DecisionTreeClassifier, feature analysis, visualization)

---

### Assignment 5: Unsupervised Learning - Customer Segmentation
**Topic:** Clustering, K-Means, Unsupervised Learning, Business Segmentation  
**Location:** `Assignment 5/`

#### Business Context: PayFlow Customer Segmentation
Discover patterns in customer payment behavior to identify high-risk segments and enable targeted support strategies.

#### Problem Statement
Late invoice payments create significant cash-flow challenges for small and medium-sized businesses (SMEs). PayFlow aims to identify customer segments with distinct payment behaviors to prioritize support and optimize collection strategies.

#### Dataset
- **File:** `payflow_invoice_late_payment_dataset.xlsx`
- **Records:** 360 B2B invoice records
- **Attributes:** Invoice ID, Customer ID, behavioral metrics

#### Clustering Features (7 features)
1. **Invoice Amount:** Total dollar value of invoice
2. **Payment Terms Days:** Agreed-upon payment window
3. **Customer Tenure Months:** Relationship length with PayFlow
4. **Prior Late Payments:** Historical frequency of delays
5. **Avg Days To Pay:** Average settlement time for past invoices
6. **Days Since Last Order:** Recency of customer engagement
7. **Reminder Count:** Manual/automated reminders sent

#### Methodology
1. **Data Scaling:** StandardScaler normalization (distance-based algorithm requirement)
2. **Algorithm:** K-Means clustering with k-means++ initialization
3. **K Selection:** Elbow Method analysis → **K = 4 chosen**
   - WCSS decrease slows significantly after 4 clusters
   - Balance between model complexity and interpretability

#### Cluster Results

| Cluster | Name | Key Characteristics | Business Strategy |
|---------|------|-------------------|-------------------|
| **0** | **High Risk** | Highest prior late payments (3.29), max reminders (3.31), lowest invoice amounts | Early intervention, automated reminders 5 days pre-due |
| **1** | **Reliable Small/Mid** | Fastest payers (31.3 days), very low late history (0.56) | Light-touch automation, loyalty incentives |
| **2** | **Enterprise Loyalists** | Highest invoice value (~$65k), longest tenure (76+ months) | Dedicated account managers, VIP support |
| **3** | **Extended Terms** | Longest agreed terms (50 days), lowest reminders (0.88) | Payment planning tools, dashboards |

#### Business Recommendations by Segment

**High Risk (Cluster 0):**
- Implement early intervention processes
- Send automated reminders 5 days before due date
- Consider stricter credit terms for new orders
- Increase monitoring frequency

**Reliable (Cluster 1):**
- Maintain automated "light touch" nudges
- Offer loyalty incentives for continued on-time performance
- Consider VIP treatment to retain valuable customers
- Use as benchmark for expectations

**Enterprise Loyalists (Cluster 2):**
- Assign dedicated account managers
- Provide white-glove customer service
- Regular business reviews to strengthen relationships
- Ensure high retention through personalized attention

**Extended Terms (Cluster 3):**
- Provide digital payment planning tools
- Offer interactive dashboards for payment tracking
- Supply flexible payment options
- Educate on payment planning best practices

#### Business Impact
- **Targeted Support:** Allocate resources proportional to risk level
- **Retention:** Prioritize high-value enterprise customers
- **Collection Optimization:** Customize collection strategies by segment
- **Predictive Planning:** Anticipate cash-flow patterns per segment

#### Clustering Insights
- **Natural Groupings:** K-Means identified distinct customer behavior patterns
- **Actionability:** Each cluster has clear, implementable strategies
- **Scalability:** Approach easily applied to new invoice data
- **Dynamic:** Recommend periodic re-clustering as behaviors evolve

#### Limitations & Considerations
- **External Factors Not Captured:** Economic conditions, industry downturns, recessions
- **Static Snapshot:** K-Means provides point-in-time analysis; customer behavior evolves
- **Ethical Note:** Automated decisions should have human review to avoid unfair treatment
- **Fairness:** Consider contextual factors before implementing differential terms

#### Files Included
- `Assignment 5.ipynb` - Complete clustering analysis and visualizations
- `payflow_invoice_late_payment_dataset.xlsx` - Raw dataset (360 invoices)
- `payflow_invoice_late_payment_business_plan.docx` - Strategic recommendations

#### Technologies Used
pandas, numpy, matplotlib, seaborn, scikit-learn (KMeans, StandardScaler, clustering metrics), openpyxl

---

## 🎯 Key Themes Across Assignments

### Progressive Skill Development
1. **Assignment 2:** ML fundamentals - pipelines, preprocessing, class imbalance
2. **Assignment 3:** Model evaluation - metrics selection, business interpretation
3. **Assignment 4:** Supervised learning - decision trees, feature importance, real business cases
4. **Assignment 5:** Unsupervised learning - clustering, customer segmentation, strategy

### Business-Centric Approach
- Each assignment connects machine learning to real business problems
- Focus on actionable insights, not just model metrics
- Emphasis on stakeholder communication and recommendations
- Understanding cost-benefit tradeoffs in decisions

### Technical Excellence
- Proper data preprocessing and pipeline construction
- Handling class imbalance and data quality issues
- Appropriate evaluation metrics for problem context
- Clear code documentation and reproducibility

---

## 🛠️ Technologies & Libraries

### Core Data Science Stack
- **Python 3.x** - Programming language
- **pandas** - Data manipulation and analysis
- **numpy** - Numerical computations
- **scikit-learn** - Machine learning algorithms and utilities
  - Preprocessing (Pipeline, ColumnTransformer, StandardScaler, SimpleImputer, OneHotEncoder)
  - Models (LogisticRegression, SVM, DecisionTreeClassifier, KMeans)
  - Model Selection (train_test_split, stratification)
  - Metrics (confusion_matrix, accuracy_score, precision_recall_fscore_support, silhouette_score)

### Visualization
- **matplotlib** - Core visualization library
- **seaborn** - Statistical visualization and plotting

### Data Formats
- **openpyxl** - Excel file handling
- **Jupyter Notebook** - Interactive development environment

---

## 📊 Learning Outcomes

By completing these assignments, I have demonstrated:

1. **ML Pipeline Development**
   - End-to-end workflow from raw data to deployment-ready model
   - Proper handling of data leakage prevention
   - Scalable pipeline architecture

2. **Model Evaluation & Selection**
   - Choosing appropriate metrics based on business context
   - Understanding precision-recall tradeoffs
   - Avoiding accuracy bias with imbalanced data

3. **Supervised Learning**
   - Linear models (Logistic Regression)
   - Non-linear models (SVM, Decision Trees)
   - Feature importance interpretation

4. **Unsupervised Learning**
   - Clustering algorithms (K-Means)
   - Determining optimal number of clusters
   - Segment interpretation and business application

5. **Business Communication**
   - Translating technical results to business language
   - Providing actionable recommendations
   - Communicating model limitations and ethical considerations

6. **Data Literacy**
   - Exploratory data analysis (EDA)
   - Handling missing values and data quality issues
   - Feature engineering and selection

---

## 🚀 How to Use This Repository

### Running the Notebooks

1. **Clone the repository:**
   ```bash
   git clone https://github.com/sukhneeksingh/MBAI5310G-AI-Programming-SukhneekSingh.git
   cd MBAI5310G-AI-Programming-SukhneekSingh
   ```

2. **Install dependencies:**
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter openpyxl
   ```

3. **Launch Jupyter:**
   ```bash
   jupyter notebook
   ```

4. **Navigate to desired assignment folder and open the .ipynb notebook**

### Exploring Specific Assignments

- **Assignment 2:** `assignment 2/assignment 2.ipynb`
- **Assignment 3:** `assignment 3/assignment 3.ipynb`
- **Assignment 4(a):** `Assignment 4/Assignment 4(a)/Assignment 4_ProcurePro_Decision_Tree.ipynb`
- **Assignment 4(b):** `Assignment 4/Assignment 4(b)/Assignment 4_UrbanFleet_DecisionTree_Assignment.ipynb`
- **Assignment 5:** `Assignment 5/Assignment 5.ipynb`

Each notebook is self-contained with detailed comments and markdown cells explaining each step.

---

## 📝 Notes

- All models use `random_state=42` for reproducibility
- Data preprocessing is performed within sklearn Pipelines to prevent data leakage
- Each assignment includes comprehensive README files with detailed explanations
- Business plan documents (.docx) provide strategic context and recommendations

---

## 📚 References

- [Scikit-learn Documentation](https://scikit-learn.org/)
- [Pandas Documentation](https://pandas.pydata.org/)
- [Matplotlib Documentation](https://matplotlib.org/)
- [Class Imbalance Handling](https://imbalanced-learn.org/)
- [Confusion Matrix & Metrics](https://scikit-learn.org/stable/modules/model_evaluation.html)
- [Decision Trees](https://en.wikipedia.org/wiki/Decision_tree_learning)
- [K-Means Clustering](https://en.wikipedia.org/wiki/K-means_clustering)

---

## 👤 Author

**Sukhneek Singh**  
Ontario Tech University  
MBAI 5310G - AI Programming  
**Date:** June 2026

---

## 📧 Contact

For questions about specific assignments or technical details, please refer to the individual assignment README files in each folder.

---

*Last Updated: June 15, 2026*
