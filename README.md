# Data-Science
This repository contains the code for Customer Analysis

## Software Requirements

* Python

## Installation

Setup and configuration for running the code.

### Windows

1. Download and install python 3.12.x for windows (64 bit). <https://www.python.org/downloads/>.
2. Create a work folder, `c:\workspace`.
3. Copy and paste the folder, `Data-Science` into work folder.
4. In the `Data-Science` project run the following commands.

    ```ps
        python -m venv venv
        venv/Scripts/activate
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    ```
5. Press `Ctrl+Shift+P` to open the Command Palette in VSCode.
6. Search for and select `Python: Select Interpreter`, then choose: `Enter interpreter path...`.
7. Click `Find.. ` and browse your file system to find a Python interpreter.
8. Navigate to `c:\workspace\Data-Science\venv\Scripts`.
9. Select `python.exe`.
10. If no kernel selected, click `Select kernel` and select `venv\Scripts\python.exe`.

# Take-Home Assessment: Customer Analysis

## Part 1: Data Analysis 

### 1. Data Exploration & Cleansing

**(a) Are there any data quality issues in the dataset? What steps would you take to clean or refine the data?**

*The dataset in `.txt` format, which can be addressed by loading the file with proper delimiters using `pandas.read_csv()`. Duplicate rows exist, so we can detect them with `df.duplicated()` and drop them with `df.drop_duplicates()`. Missing values in columns like `chn`, `cus_no`, `gndr`, and `age` occur due to incomplete records. To handle this, we can fill missing values `cus_no`,`gndr`, and `age` using a mapping from `acc_no` (since they are related), fill missing `chn` values based on transaction types (e.g., filling 'IB' for `trn_desc` values like 'IBK', 'FUND TRANSFER' and 'SALARY'). By applying these refinements, we can clean the dataset for analysis.*

**(b) What are the key characteristics of the dataset? Summarise the distribution of transactions, key statistics, and any anomalies you notice?**

*The dataset consists of 20,639 transactions with key columns including `trn_no`, `acc_no`, `cus_no`, `brn_cd`, `trn_type`, `trn_dt`, `trn_time`, `amt`, `trn_desc`, `chn`, `gndr` and `age`. The `trn_desc` column shows that the majority of transactions are labeled as "FUND TRANSFER" (15,145 occurrences), followed by "PAYMENT" (3,835) and smaller numbers for other transaction types. Gender distribution reveals a predominance of male (13,335) over female (7,301) participants. In terms of channels, "IB" is the most common (16,982), with smaller occurrences of other channels like "MEPS" (1,189) and "POS" (1,113). The transaction amount (`amt`) ranges from 0.1 to 10,000, with a mean of 857.54 and a high standard deviation of 1,635.89, indicating significant variability. The age of customers ranges from 25 to 73, with a mean of 51.49 years. Missing values are present in the `cus_no`, `chn`, `gndr`, and `age` columns, with `chn` having the most significant missing data (419 nulls). There are also some duplicates in the dataset, particularly in customer-related fields, which need to be addressed to ensure accurate analysis. The dataset will benefit from handling the missing values and duplicates before further analysis.*

### 2. Transaction Volume & Trends 

**(a) What is the average transaction amount? How many transactions do customers make per month on average?**

*Average Transaction Amount: 841.69*

*Average Transaction per Customer per Month: 55.54*

**(b) Visualise transaction volume across different time periods. Are there any patterns in spending behaviour during specific times of the day or week?**

*Transactions peak between 10 AM and 3 PM, with the busiest hours being 11 AM and 12 PM. After 3 PM, the number of transactions gradually declines, remaining steady through the evening until around 9 PM, followed by a sharp drop after 9 PM, with the least activity observed around 3 AM and 4 AM when most people are likely inactive.*

### 3. Banking Context: Malaysia-Specific Transactions  

**(a) What aspects of the dataset reflect banking transactions unique to Malaysia?** 

*The dataset reflects Malaysia-specific banking transactions in several ways. For example, the branch code (brn_cd) follows a format typical of Malaysian banks, which use standardized numbering to identify branches. Additionally, the transaction channel (chn) field includes values like FPX (Financial Process Exchange) and MEPS (Malaysia Electronic Payment System), which are systems specific to Malaysia for processing interbank transactions and ATM/POS operations. These local channels, alongside transaction descriptions such as "FUND TRANSFER" and "PAYMENT," indicate that the dataset is aligned with the Malaysian banking framework and regulatory environment, a detail that is crucial for ensuring compliance, tailoring local banking products, and strengthening cybersecurity measures in the region.*

**(b) If you could add one more column to better represent banking transactions in Malaysia, what would it be and why?** 

*It would be useful to add a column called **Merchant Category (`mcht_ct`)** that categorizes the merchant or service provider involved in the transaction (for example, retail, utilities, entertainment, online services, groceries, etc.). This enhancement is beneficial because it allows for deeper insight into consumer spending habits and helps banks and financial institutions tailor their services, marketing strategies, and risk assessments more effectively.*

## Part 2: Dataset Analysis 

### 1. Customer Behaviour Analysis 

**(a) Which transaction channel is used the most, and why do you think that is?**

*The most used transaction channel in the dataset is **IB (Internet Banking)**, with 12,423 transactions. This is likely due to its convenience, allowing users to perform transactions anytime and anywhere without visiting a physical branch. In Malaysia, the push toward digital banking supported by initiatives from Bank Negara Malaysia and platforms like FPX has significantly increased the adoption of online banking services. Customers are also drawn to IB because it often offers lower fees, faster processing, and enhanced security features. This widespread usage reflects the country’s broader shift toward digital financial services and customer preference for efficient, accessible, and secure transaction methods.*

**(b) Identify one key transaction trend or pattern in your dataset. Why is this trend important?**

*One key transaction pattern in the dataset is the movement of funds through multiple accounts without clear justification. This behavior can indicate an attempt to obscure the origin and destination of money. Rapid and repeated transfers between different accounts, particularly across branches or regions, are often associated with layering—a stage in the money laundering process designed to hide the source of illicit funds. Detecting such patterns is crucial for cybersecurity and financial institutions to prevent illegal activities and ensure regulatory compliance.*

### 2. Transaction Insights 

**(a) If you were asked to forecast transaction trends for the next quarter, what factors would you consider, and what approach would you take?**

*To forecast transaction trends for the next quarter, I would consider factors like historical transaction volumes, seasonal patterns, promotional campaigns, economic conditions, and shifts in customer behavior. It's essential to assess the impact of holidays, marketing initiatives, and events, as these could drive spikes or declines in transactions. Additionally, market conditions like inflation or consumer confidence should be taken into account, as they can influence spending behavior.*

**(b) Describe the methodology you would use (e.g., statistical methods, machine learning, business intuition).** 

*The methodology would involve a combination of statistical models and machine learning techniques. Time series analysis methods like ARIMA or SARIMA would help capture trends, seasonality, and cyclical patterns in the data. Random Forests or other ensemble models could be employed to handle high-dimensional data and identify non-linear interactions, such as the impact of campaigns vs economic factors. Business intuition would also play a role, working with domain experts to interpret model outputs, adjust predictions based on qualitative insights (e.g., competitor actions), and validate predictions with real-time data to ensure accuracy.*

### 3. Technical Considerations & Data Quality 

**(a) What are some potential data quality issues that could arise when collecting transaction data? How would you address them?**

*Firstly, human errors, system integration issues, or outdated data can lead to discrepancies, such as misspelled or incorrect transaction amounts. To address this, automated validation checks should be implemented during data entry to catch these errors early. Secondly, the presence of missing critical fields, often due to insufficient entry requirements, can lead to incomplete records. This can be mitigated by enforcing mandatory fields in data collection forms and flagging any incomplete entries. Lastly, overlapping entries from multiple systems can create redundancy and confusion. To prevent this, deduplication algorithms and Master Data Management (MDM) strategies should be employed to maintain a single, accurate source of truth across systems.*

**(b) Write one SQL query to gain insight from your dataset (e.g., finding the most active customers, detecting large transactions). Explain what your query does and why it is useful.**

*This query identifies the top 5 customers with the most transaction, helping businesses focus on high-value customers for targeted strategies and promotions.*

### 4. SQL Challenge

**(a) Write an SQL query to find all accounts that have at least three consecutive withdrawal transactions exceeding RM 5,000, ordered by transaction date.** 

*This code queries to find customers with three consecutive withdrawals over 5000 units, ordered by transaction date. It uses a CTE with `ROW_NUMBER()` to identify consecutive transactions. This query is useful for detecting customers who make consecutive large withdrawals, which could indicate suspicious activity, such as money laundering or financial distress.*

**(b) Modify your query to detect four or more consecutive withdrawals instead of three.**

*This code retrieves transactions where customers made 4 or more consecutive large debit withdrawals (over 5000). It uses window functions(ROW_NUMBER) to group consecutive transactions by account, then filters groups with 4 or more withdrawals. The results, including account number and transaction dates.* 
