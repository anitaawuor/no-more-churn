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
- Converted `SeniorCitizen` from binary (`0/1`) to categorical (`No/Yes`) for readability.
- Standardized column names by trimming extra spaces and ensuring consistent formatting.
- Exported the cleaned dataset as `telco_customer_churn.csv`

### 2. Database Setup (MySQL)
- Created a new schema `telco_customer_churn` and a table named `customer_churn_analysis`.
- Defined appropriate data types for each column (e.g., `DECIMAL` for charges, `VARCHAR` for categories).
- Used MySQL’s import wizard to load the cleaned CSV file.

### 3. Exploratory Data Analysis (SQL Queries)
Ran multiple SQL queries to uncover trends and patterns:

```sql
-- 1. Total Customers and Churn Rate
SELECT 
    COUNT(*) AS total_customers,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned_customers,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis;

-- 2. Churn by Contract Type
SELECT 
    Contract,
    COUNT(*) AS total,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis
GROUP BY Contract;

-- 3. Services that Correlate with Churn --
SELECT 
    TechSupport,
    COUNT(*) AS total,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis
GROUP BY TechSupport;

SELECT 
    OnlineBackup,
    COUNT(*) AS total,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis
GROUP BY OnlineBackup;

SELECT 
    DeviceProtection,
    COUNT(*) AS total,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis
GROUP BY DeviceProtection;

-- 4. Churn by Senior Citizen --
SELECT 
    SeniorCitizen,
    COUNT(*) AS total,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis
GROUP BY SeniorCitizen;

-- 5. Churn by Tenure Group --
SELECT 
    CASE 
        WHEN tenure BETWEEN 0 AND 12 THEN '0-12 months'
        WHEN tenure BETWEEN 13 AND 24 THEN '13-24 months'
        WHEN tenure BETWEEN 25 AND 48 THEN '25-48 months'
        ELSE '49+ months'
    END AS tenure_group,
    COUNT(*) AS total,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis
GROUP BY tenure_group;

-- 6. Internet Service Type and Churn --
SELECT 
    InternetService,
    COUNT(*) AS total,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis
GROUP BY InternetService;

-- 7. Churn by Payment Method --
SELECT 
    PaymentMethod,
    COUNT(*) AS total,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis
GROUP BY PaymentMethod;

-- 8. Churn Rate by Gender --
SELECT 
    gender,
    COUNT(*) AS total,
    SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) AS churned,
    ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS churn_rate_percent
FROM customer_churn_analysis
GROUP BY gender;

-- 9. High-Value Churners (TotalCharges > 3000) --
SELECT 
    COUNT(*) AS high_value_churners
FROM customer_churn_analysis
WHERE Churn = 'Yes' AND TotalCharges > 3000;
```

## 📌 Key Insights
- **Churn Rate:** 26.6% of total customers had churned.
- **Contract Type:** Monthly contracts had the highest churn rate (over 40%).
- **Support Services:** Customers without tech support, online backup, or device protection had higher churn rates.
- **Senior Citizens:** Despite being a smaller group (only ~16% of customers), seniors churned at nearly twice the rate of non-seniors (41.7%).
- **Tenure Impact:** New customers (tenure < 12 months) churned at the highest rate (47.7%).
- **Internet Service Type:** Fiber optic customers churned the most, with a 41.9% churn rate.
- **Payment Method:** Electronic check users churned the most, by far, with a 45.3% churn rate.
- **Gender:** Gender had little to no impact on churn, as females churned at a rate of 26.96% and males at 26.20%, a statistically negligible difference of less than 1%.
- **High-value churners:** A total of 350 high-value customers who had paid over $3,000 each in total charges churned — a significant revenue loss, as these long-term or premium users still chose to end their service.

## ✅ Targeted Churn Drivers: Identified Who Left, Why, and What It Cost
### 1. Electronic Check Customers Churned at 45.3%
**Why it mattered:** Electronic check users were the highest-risk segment, with nearly half of them leaving, likely due to demographic or payment-related challenges.

**Recommended Action:** Offer incentives to switch to auto-pay via credit card or bank transfer.

### 2. Monthly Contract Customers Had a Churn Rate Over 40%
**Why it mattered:** Month-to-month contracts provided flexibility, making it easier for customers to leave at any time.

**Recommended Actions:**
- Promote 6–12 month contracts through discounts or bundled offers.
- Target this group with loyalty campaigns or exclusive perks.

### 3. Senior Citizens Churned at Nearly Double the Rate (41.7%)
**Why it mattered:** Though seniors made up only 16% of the base, they churned at twice the rate of non-seniors, representing a significant hidden loss.

**Recommended Actions:**
- Introduce simplified, senior-focused plans.
- Offer personalized support, including live agents or callbacks.
  
### 4. New Customers (Tenure < 12 Months) Churned at 47.7%
**Why it mattered:** Nearly half of new users left within their first year, suggesting poor onboarding or unmet expectations.

**Recommended Actions:**
- Strengthen the onboarding experience.
- Use welcome emails, proactive check-ins, and early support interventions.
  
### 5. Fiber Optic Users Churned at 41.9%
**Why it mattered:** Fiber, typically viewed as a premium offering, had one of the highest churn rates, potentially due to performance or service delivery issues.

**Recommended Actions:**
- Audit installation and network quality.
- Collect feedback within 30 days of installation.

### 6. 350 High-Value Customers (>$3,000 in Charges) Churned
**Why it mattered:** Losing long-term or premium customers posed a serious revenue risk, despite their high lifetime value.

**Recommended Actions:**
- Launch a VIP retention strategy with tailored perks.
- Use proactive outreach and concierge-style support.

### 7. Missing Support Services Were Linked to Higher Churn
**Why it mattered:** Customers lacking tech support, online backup, or device protection churned at noticeably higher rates.

**Recommended Actions:**
- Bundle essential support services into plans.
- Offer free trials or demos to increase adoption.

