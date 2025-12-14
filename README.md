```markdown
# RFM Customer Segmentation using K-Means

## Overview
This project focuses on performing Customer Segmentation using the RFM (Recency, Frequency, Monetary) model, combined with the K-Means clustering algorithm. The goal is to identify distinct customer groups based on their purchasing behavior, which can then be used for targeted marketing strategies.

## Dataset
The analysis uses a retail transactional dataset, `preprocessed_retail_data.csv`, containing details of customer purchases. Key columns include:
- `InvoiceNo`: Invoice number
- `StockCode`: Product code
- `Description`: Product description
- `Quantity`: Quantity of the product purchased
- `InvoiceDate`: Date and time of the invoice
- `UnitPrice`: Unit price of the product
- `CustomerID`: Unique identifier for each customer
- `Country`: Country of purchase
- `TotalPrice`: Total price for the item (Quantity * UnitPrice)

## Methodology
The following steps were performed to achieve customer segmentation:

1.  **Data Loading & Preprocessing**: The dataset was loaded into a Pandas DataFrame. The `InvoiceDate` column was converted to datetime objects, and a `TotalPrice` column was calculated.
2.  **RFM Calculation**: For each unique `CustomerID`, the following metrics were calculated:
    *   **Recency**: Number of days since the last purchase.
    *   **Frequency**: Total number of unique invoices (transactions).
    *   **Monetary**: Total amount spent by the customer.
3.  **Data Scaling**: The RFM features were scaled using `StandardScaler` to ensure that all features contribute equally to the clustering process.
4.  **Determining Optimal Number of Clusters (K)**:
    *   The Elbow Method (using SSE) was employed to observe the optimal `k` value.
    *   The Silhouette Score was calculated for different `k` values (from 2 to 10) to identify the best-fitting number of clusters, which was found to be 4 in this analysis.
5.  **K-Means Clustering**: The K-Means algorithm was applied to the scaled RFM data with the optimal `k` (4) to group customers into clusters.
6.  **Cluster Interpretation**: The mean RFM values for each cluster were analyzed to understand the characteristics of each segment. Visualizations (scatter plots and heatmaps) were used to further interpret the clusters.
7.  **Customer Segmentation**: Based on the RFM values and cluster characteristics, custom segment names were assigned:
    *   **VIP**: High Frequency, High Monetary, Low Recency.
    *   **Loyal**: Good Frequency, Medium Monetary, Good Recency.
    *   **At-Risk**: Good Frequency, High Monetary, High Recency (but not too high).
    *   **Lost**: Very High Recency, Low Frequency, Low Monetary.
    *   **Low-Value**: Low Frequency, Low Monetary, Recency varies.
8.  **Model Saving**: The trained K-Means model was saved as `kmeans_model.pkl` using `joblib` for future use.

## Results & Insights
The analysis identified 4 distinct customer clusters. After interpretation, these clusters were further categorized into 5 segments: VIP, Loyal, At-Risk, Lost, and Low-Value. Each segment has unique purchasing behaviors, allowing for tailored marketing and retention strategies.

*   **VIP Customers**: These are your most valuable customers, purchasing recently, frequently, and spending the most. They require exclusive offers and loyalty programs.
*   **Loyal Customers**: These customers buy often and spend a decent amount. They can be nurtured to become VIPs through reward programs.
*   **At-Risk Customers**: These were once good customers but haven't purchased recently. Re-engagement campaigns are crucial for this segment.
*   **Lost Customers**: Customers who haven't purchased for a long time. Aggressive promotions might be needed, but they are a lower priority.
*   **Low-Value Customers**: New or infrequent buyers with low spending. Focus on product education and light acquisition campaigns.

## How to Replicate
To replicate this analysis, follow these steps:

1.  **Environment Setup**: Ensure you have Python installed. It's recommended to use a virtual environment.
2.  **Install Dependencies**: Install the required libraries using pip:
    ```bash
    pip install pandas numpy scikit-learn matplotlib seaborn plotly joblib
    ```
3.  **Download Dataset**: Obtain the `preprocessed_retail_data.csv` file and place it in the appropriate directory (e.g., `/content/drive/MyDrive/Dataset/` if running in Google Colab, or adjust the path in the code).
4.  **Run the Notebook**: Execute the Python code cells sequentially in the provided Jupyter/Colab notebook. The notebook walks through each step of the RFM calculation, clustering, and segmentation.

## Dependencies
- `pandas`
- `numpy`
- `scikit-learn`
- `matplotlib`
- `seaborn`
- `plotly`
- `joblib`

```
