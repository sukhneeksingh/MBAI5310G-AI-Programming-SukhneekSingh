# MBAI5310G-AI-Programming-SukhneekSingh-Assignment-5

# PayFlow Customer Segmentation Analysis

This project uses unsupervised learning (K-Means Clustering) to discover patterns in customer payment behavior for **PayFlow Business Solutions**, a B2B financial operations company.

## Business Problem
Late invoice payments create significant cash-flow challenges for small and medium-sized businesses (SMEs). PayFlow aims to identify high-risk customer segments to prioritize support, optimize collection workflows, and improve overall financial stability.

## Dataset
The dataset consists of 360 B2B invoice records. The data includes both categorical information (Invoice ID, Customer ID) and numerical features used for behavioral analysis.

## Selected Clustering Features
To group customers based on behavior, the following numerical features were selected:
- **Invoice Amount:** Total dollar value of the invoice.
- **Payment Terms Days:** Agreed-upon window for payment.
- **Customer Tenure Months:** Length of the relationship with PayFlow.
- **Prior Late Payments:** Historical frequency of payment delays.
- **Avg Days To Pay:** Average time taken to settle past invoices.
- **Days Since Last Order:** Recency of customer engagement.
- **Reminder Count:** Number of manual/automated reminders sent for the current invoice.

## Methodology
1. **Scaling:** Data was normalized using `StandardScaler` to ensure distance-based K-means wasn't biased by feature ranges.
2. **K-Means Method:** Applied the K-Means algorithm with `k-means++` initialization.
3. **Determining K:** The **Elbow Method** was used. A value of **K = 4** was chosen because the Within-Cluster Sum of Squares (WCSS) decrease slowed significantly after this point, providing a balance between detail and simplicity.

## Main Cluster Results
| Cluster | Name | Key Characteristics |
| :--- | :--- | :--- |
| **0** | **High Risk** | Highest prior late payments (3.29) and reminders (3.31). Lowest invoice amounts. |
| **1** | **Reliable Small/Mid** | Fastest payers (31.3 days) with very low late payment history (0.56). |
| **2** | **Enterprise Loyalists** | Highest invoice value (~$65k) and longest tenure (76+ months). |
| **3** | **Extended Terms** | Longest agreed terms (50 days) and lowest reminder count (0.88). |

## Business Recommendation
- **High Risk (Cluster 0):** Implement early intervention and automated reminders 5 days before due date. Consider stricter credit terms.
- **Reliable (Cluster 1):** Use automated "light touch" nudges and offer loyalty incentives for continued on-time performance.
- **Enterprise (Cluster 2):** Assign dedicated account managers and provide VIP support to ensure high retention.
- **Extended Terms (Cluster 3):** Provide digital payment planning tools and dashboards to help them manage their long payment cycles.

## Limitations
- **External Factors:** The model does not account for broader economic conditions (recessions, industry downturns) that might cause temporary late payments.
- **Static Analysis:** K-means provides a snapshot; customer behavior may evolve over time, requiring periodic re-clustering.
- **Ethical Note:** Automated decisions based on these labels should always be reviewed by a human to avoid unfair treatment due to economic context.

## How to Run the Notebook
1. Ensure you have Python installed with the following libraries:
   - `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `openpyxl`
2. Download the `unsupervised_learning_segmentation.ipynb` and `payflow_invoice_late_payment_dataset.xlsx` files.
3. Open the notebook in Jupyter or VS Code.
4. Run all cells to see the clustering analysis and visualizations.
