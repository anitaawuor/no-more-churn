# Telco Customer Churn Analysis
## 📊 Project Overview
This project analyzed customer churn behavior for a fictional telecom company. Using SQL and Power BI, I uncovered key factors that contributed to churn and identified actionable insights to improve customer retention.

## 📁 Dataset
- **Source:** [Kaggle - Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- **Description:** The dataset includes demographic info, service usage, and account details for ~7,000 telecom customers.

## 🧰 Tools Used
- **Google Sheets** – Data cleaning and preprocessing
- **MySQL** – Data storage and analysis using SQL
- **Power BI** – Interactive dashboards and visual storytelling

## 🔄 Project Workflow 
### 1. Data Cleaning (Google Sheets)
- Removed rows with empty `TotalCharges` (less than 1% of data).
- Converted `SeniorCitizen` from binary (0/1) to categorical (`"No"/"Yes"`) for readability.
- Standardized column names by trimming extra spaces and ensuring consistent formatting.
- Exported the cleaned dataset as `telco_customer_churn.csv`

### 2. Database Setup (MySQL)
- Created a new schema: `telco_customer_churn` and a table named `customer_churn_analysis`.
- Defined appropriate data types for each column.
- Used MySQL’s table data import wizard to load the cleaned CSV file.

### 3. Exploratory Data Analysis (SQL Queries)
Ran multiple SQL queries to uncover trends and patterns:
- Churn Rate: 26.6% of total customers had churned.
- Contract Type: Monthly contracts had the highest churn rate (over 40%).
- Support Services: Customers without tech support, online backup, or device protection had higher churn rates.
- Senior Citizens: Despite being a smaller group (only ~16% of customers), seniors churned at nearly twice the rate of non-seniors (41.7%).
- Tenure Impact: New customers (tenure < 12 months) churned at the highest rate (47.7%).
- Internet Service Type: Fiber optic customers churned the most, with a 41.9% churn rate.
- Payment Method: Electronic check users churned the most, by far, with a 45.3% churn rate.
- Gender: Gender had little to no impact on churn, as females churned at a rate of 26.96% and males at 26.20%, a statistically negligible difference of less than 1%.
- High-value churners: A total of 350 high-value customers who had paid over $3,000 each in total charges churned — a significant revenue loss, as these long-term or premium users still chose to end their service.
