# Telco Customer Churn Analysis
## 📊 Project Overview
This project analyzes customer churn behavior for a fictional telecom company. Using SQL and Power BI, I uncover key factors that contribute to churn and identify actionable insights to improve customer retention.

## 📁 Dataset
- **Source:** [Kaggle - Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- **Description:** The dataset includes demographic info, service usage, and account details for ~7,000 telecom customers.

## 🧰 Tools Used
- **Google Sheets** – Data cleaning and preprocessing
- **MySQL** – Relational database and SQL analysis
- **Power BI** – Interactive visualizations and dashboards

## 🔄 Workflow Summary

### 1. Data Cleaning (Google Sheets)
- Removed rows with missing `TotalCharges` 
- Converted `SeniorCitizen` from `0/1` to `"No"/"Yes"`
- Stripped extra whitespace from column names
- Exported cleaned dataset as `telco_customer_churn.csv`

### 2. Database Setup (MySQL)
- Created schema: `customer_churn`
- Defined table: `customers`
- Loaded data using MySQL Import Wizard
