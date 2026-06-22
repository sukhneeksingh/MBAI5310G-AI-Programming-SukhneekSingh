# Assignment 8: Natural Language Processing Pipeline and Text Classification

## Overview
This assignment implements a comprehensive **Natural Language Processing (NLP) pipeline** for automated customer support ticket classification in the smart home industry. The project demonstrates end-to-end NLP techniques including text preprocessing, feature extraction, and machine learning model training.

## Business Problem
HomeIQ Systems receives a high volume of customer support requests across multiple channels. Manual categorization presents challenges:
- **Inefficient Routing:** Support tickets must be manually routed to appropriate teams
- **High Operational Costs:** Resource-intensive manual triage process
- **Inconsistent Categorization:** Different agents may categorize similar issues differently
- **Service Level Agreement (SLA) Violations:** Delays in sorting lead to customer dissatisfaction

## Solution
An automated NLP classification system that categorizes support messages into six core categories:
- **Voice_Assistant** - Voice command and smart assistant issues
- **Security_Alert** - Security and alert system problems
- **Warranty_Return** - Warranty claims and product returns
- **Connectivity** - Network and connectivity issues
- **Energy_Saving** - Energy efficiency features and tips
- **Installation** - Setup and installation problems

## Dataset
**File:** `NLP_Dataset_16_Smart_Home_Device_Support.xlsx`

**Size:** 120 customer support messages with balanced class distribution (20 per category)

**Columns:**
| Column | Description |
|--------|-------------|
| SupportID | Unique ticket identifier |
| SupportDate | Date ticket was filed |
| Channel | Communication channel (Email, Chat, Phone, etc.) |
| City | Customer location |
| DeviceType | Smart home device type (Camera, Thermostat, Light, etc.) |
| CustomerSegment | Customer type (Homeowner, Renter, Business) |
| SupportMessage | Raw customer support text |
| SupportCategory | Target classification label |
| IssueSeverity | Priority level (Low, Medium, High) |

## Tasks Completed

### 1. **Data Loading & Exploration**
- Load dataset from Excel file
- Inspect shape, data types, and distributions
- Verify data quality and missing values
- Visualize target variable distribution (balanced dataset)

### 2. **Text Preprocessing**
Applied a comprehensive cleaning pipeline:
1. **Lowercasing** - Normalize case variations
2. **Punctuation Removal** - Strip special characters
3. **Tokenization** - Split text into individual words
4. **Stopword Removal** - Filter common English words (the, is, for, etc.)
5. **POS-Aware Lemmatization** - Reduce words to base forms using grammatical context

**Example:**
- Raw: *"The light works near the router but fails in the bedroom. #HomeIQ"*
- Cleaned: *"light work near router fail bedroom homeiq"*

### 3. **Exploratory Text Analysis**
- Identified top 15 most common words in the corpus
- Analyzed word frequencies to understand common issues
- Key findings:
  - Device-specific terms: `camera`, `light`, `thermostat`, `speaker`
  - Action/problem terms: `work`, `stop`, `fail`
  - Category indicators: `warranty`, `connect`, `install`

### 4. **Part-of-Speech (POS) Tagging & Named Entity Recognition (NER)**
Analyzed three representative messages:
- **POS Tags:** Identified nouns, verbs, adjectives for semantic understanding
- **NER Extraction:** Detected locations (GPE), organizations, and persons
- **Business Application:** Enable intelligent routing based on entity types and geographical dispatch

### 5. **Feature Extraction**
- Used **TF-IDF (Term Frequency-Inverse Document Frequency)** vectorization
- Converts text into numerical feature matrix (120 documents × 117 vocabulary size)
- TF-IDF advantages:
  - Balances word frequency with importance
  - Reduces weight of common terms
  - Highlights category-specific keywords

### 6. **Model Training**
- **Algorithm:** Logistic Regression
- **Data Split:** 80% training (96 samples), 20% testing (24 samples)
- **Stratified Split:** Maintains balanced class distribution in both sets

### 7. **Model Evaluation**
**Performance Metrics:**
- **Accuracy:** 100.00% on test set
- **Precision/Recall/F1-Score:** 1.00 across all categories
- **Confusion Matrix:** Perfect classification with no misclassifications

## Key NLP Concepts Demonstrated

### Text Preprocessing Importance
- **Dimensionality Reduction:** Lemmatization reduces vocabulary size and prevents overfitting
- **Noise Filtering:** Stopword removal forces model focus on high-information keywords
- **Generalization:** Standardization improves model performance on unseen data

### TF-IDF vs Bag of Words
- **TF-IDF:** Weights terms by importance (category-specific words > generic words)
- **Bag of Words:** Simple frequency counting (treats all words equally)
- **Advantage:** TF-IDF better captures semantic meaning for classification

### Logistic Regression for Text Classification
- Efficient and interpretable
- Fast training on TF-IDF matrices
- Provides probability scores for confidence estimation
- Industry standard baseline for text categorization

## Business Impact

### Immediate Benefits
1. **Instant Triage:** Automatic ticket routing within seconds
2. **Cost Reduction:** Eliminates manual categorization labor
3. **Consistency:** Objective, rule-based categorization
4. **SLA Compliance:** Faster ticket processing and resolution

### Advanced Applications
1. **Severity Detection:** Combine with additional NLP for automatic priority assignment
2. **Product Analytics:** Monitor which devices have most issues
3. **Geographic Insights:** Use NER to dispatch field technicians to problem areas
4. **Integration Tracking:** Monitor third-party ecosystem issues (Google Assistant, Alexa)

## Files in This Assignment

| File | Description |
|------|-------------|
| `Assignment 8.ipynb` | Complete Jupyter notebook with all code and analysis |
| `NLP_Dataset_16_Smart_Home_Device_Support.xlsx` | Dataset with 120 labeled support messages |
| `README.md` | This file - project documentation |

## Technical Stack

**Libraries Used:**
- **pandas** - Data manipulation and analysis
- **numpy** - Numerical computing
- **scikit-learn** - Machine learning and feature extraction
- **nltk** - Natural language processing
- **matplotlib & seaborn** - Data visualization

## How to Use

1. **Install Dependencies:**
   ```bash
   pip install pandas numpy scikit-learn nltk matplotlib seaborn openpyxl
   ```

2. **Download NLTK Resources:**
   The notebook automatically downloads required NLTK data (punkt, stopwords, wordnet, etc.)

3. **Run the Notebook:**
   - Open `Assignment 8.ipynb` in Jupyter Notebook
   - Execute cells sequentially to see full pipeline
   - Review outputs and visualizations

## Results Summary

The classification model successfully achieved **100% accuracy** on the test set, demonstrating the effectiveness of:
- Proper text preprocessing
- TF-IDF feature extraction
- Logistic Regression classification
- Balanced dataset with clear category distinctions

## Future Enhancements

1. **Cross-Validation:** Use k-fold validation for more robust evaluation
2. **Advanced Models:** Test Random Forest, SVM, or Neural Networks
3. **Hyperparameter Tuning:** Optimize model parameters using GridSearchCV
4. **Real-World Evaluation:** Test on imbalanced, noisy production data
5. **Multi-Label Classification:** Handle messages belonging to multiple categories
6. **Confidence Thresholding:** Flag low-confidence predictions for human review

## Author
Sukhneek Singh  
Course: MBAI5310G - AI Programming / Programming and Data Processing  
Date: June 2026

---

**Note:** This project is part of an academic assignment demonstrating NLP pipeline implementation and machine learning model development for business problem-solving.
