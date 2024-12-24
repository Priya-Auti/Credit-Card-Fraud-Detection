# Credit Card Fraud Detection Dashboard

### Dashboard Link :https://dnyanamcoachingcenter-my.sharepoint.com/:u:/g/personal/priyaauti_dnyanamcoachingcenter_onmicrosoft_com/EaWY9CcPjT5OofMXqtcRFpkBujoT2TlEYnXLA_3leKGJWQ?e=705nPX


## Problem Statement

This dashboard helps detect fraudulent transactions in a credit card transaction dataset. By analyzing the patterns of legitimate and fraudulent transactions, this dashboard provides insights into the types of transactions that are likely to be fraudulent. The goal is to assist financial institutions in identifying potential fraud, enabling better detection systems, and reducing losses due to fraudulent activities.

The dataset contains anonymized features, with the **Class** column indicating whether a transaction is fraudulent (1) or not (0). The dashboard provides key metrics such as the average transaction amount, fraud detection rates, and transaction distribution.


### Steps Followed

- **Step 1**: Load data into Power BI from the Kaggle Credit Card Fraud Detection dataset.
- **Step 2**: Open Power Query editor and ensure proper data types and clean up any missing or erroneous values.
- **Step 3**: Clean and preprocess the dataset, checking for null values and ensuring that important columns like **Amount** and **Class** are correctly formatted.
- **Step 4**: Create **DAX Measures** to calculate key metrics, such as the **Mean Transaction Amount**, **Standard Deviation of Amount**, **Total Fraud Transactions**, and **Total Normal Transactions**.
  
  - **Measures Created**:
    - **Mean Amount**: Calculates the average value of all transactions in the dataset.
      ```DAX
      MeanAmount = AVERAGE('creditcard'[Amount])
      ```

    - **Standard Deviation of Amount**: Calculates how much the transaction values deviate from the average.
      ```DAX
      StdDevAmount = STDEVX.P('creditcard', 'creditcard'[Amount])
      ```

    - **Total Fraud Transactions**: Counts the number of fraudulent transactions.
      ```DAX
      TotalFraud = CALCULATE(COUNTROWS('creditcard'), 'creditcard'[Class] = 1)
      ```

    - **Total Normal Transactions**: Counts the number of normal (non-fraudulent) transactions.
      ```DAX
      TotalNormal = CALCULATE(COUNTROWS('creditcard'), 'creditcard'[Class] = 0)
      ```

- **Step 5**: Create a **Calculated Column** for binning the **Amount** into categories like "$0 - $500", "$500 - $1000", "$1000 - $5000", "$5000 - $10000", and "$10000+".
  
  - **Amount Bin Column**:
    ```DAX
    Amount Bin = 
    SWITCH(TRUE(), 
        'creditcard'[Amount] <= 500, "$0 - $500", 
        'creditcard'[Amount] <= 1000, "$500 - $1000", 
        'creditcard'[Amount] <= 5000, "$1000 - $5000", 
        'creditcard'[Amount] <= 10000, "$5000 - $10000", 
        "$10000+"
    )
    ```

- **Step 6**: Create a **Z-Score Measure** for anomaly detection, which calculates how far each transaction deviates from the average transaction amount.
  ```DAX
  ZScoreM = 
  ( 'creditcard'[Amount] - AVERAGE('creditcard'[Amount]) ) / STDEVX.P('creditcard', 'creditcard'[Amount])
  ```

- **Step 7**: Create **Visuals** such as histograms, scatter plots, and card visuals to represent the key metrics and Z-scores, enabling clear visual identification of patterns and anomalies in the dataset.

  - **Card Visuals**: Represent metrics like Total Fraud Transactions, Mean Amount, StdDevAmount, etc.
  - **Histogram**: Display the distribution of transactions across different **Amount Bins**.
  - **Scatter Plot**: Plot the Z-scores to detect outliers in transaction values.

- **Step 8**: Add slicers to allow interactive filtering of the data by **Class** (fraud vs. normal), **Amount** ranges, and **Time**.

- **Step 9**: Format the report for clarity, and add navigation elements such as buttons for better user interaction.

### Key Measures & Columns Created

1. **Measures**:
   - **Mean Amount**: Average of all transaction amounts.
   - **Standard Deviation of Amount**: Deviation of transaction amounts from the mean.
   - **Total Fraud Transactions**: Count of fraudulent transactions.
   - **Total Normal Transactions**: Count of normal transactions.
   - **Z-Score**: Measures how unusual a transaction is compared to the overall dataset.

2. **Calculated Columns**:
   - **Amount Bin**: Categorizes transaction amounts into "$0 - $500", "$500 - $1000", "$1000 - $5000", "$5000 - $10000", and "$10000+" bins for better visualization and analysis.

### Report Features and Visuals

- **Card Visuals** for displaying key metrics like total fraud and normal transactions.
- **Histogram** for showing the distribution of transactions across different amount bins.
- **Scatter Plot** for displaying the Z-scores to highlight anomalies.
- **Slicers** for filtering by **Class** (Fraud/Normal), **Amount**, and **Time**.
- **Table** to show detailed fraudulent transactions.

### Insights

A single-page report was created in Power BI Desktop and published to Power BI Service.

**Following insights can be drawn from the dashboard:**

1. **Fraud Metrics**:
   - Total fraud transactions and normal transactions are clearly distinguished.
   - Fraudulent transactions often have smaller or larger amounts compared to the normal ones.

2. **Transaction Distribution**:
   - Most transactions fall within the "$0 - $500" and "$500 - $1000" amount bins, with fewer transactions in the "$10000+" bin.
   
3. **Anomaly Detection**:
   - Transactions with high Z-scores are potential outliers and could be fraud.

4. **Visuals**:
   - Users can filter and interact with the report to drill down into specific aspects, such as filtering by fraud type or transaction amount.

### Dashboard Snapshot : ![Credit card fraud detect](https://github.com/user-attachments/assets/34943e48-1875-486f-b1e9-5a82ca91b751)

