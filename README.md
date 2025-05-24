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

## 📌 Key Business Implications from Churn Analysis
### 1. Overall Churn Rate — 26.6%
**Implication:**
A churn rate this high reflects a critical retention problem. Losing over a quarter of customers impacts recurring revenue, raises acquisition costs, and may point to service or support dissatisfaction.

### 2. Contract Type — Monthly Plans Churned Most (40%+)
**Implication:**
Month-to-month customers are more likely to leave due to a lack of commitment.

**Actionable strategies:**
Incentivize longer-term contracts (6–12 months)
Offer loyalty perks or renewal discounts

 ### 3. Support Services — Missing Support Linked to Higher Churn
**Implication:**
Lack of tech support, online backup, or device protection correlates with higher churn.

**Recommendation:**
Bundle essential support services or offer free trials to improve retention.

### 4. Senior Citizens — 41.7% Churn Rate
**Implication:**
Though only ~16% of the base, seniors churned at nearly double the rate of non-seniors.

**Recommendation:**
Introduce senior-friendly plans, simplified billing, and tailored support.

### 5. Tenure Impact — New Users (Under 12 Months) Churned Most (47.7%)
**Implication:**
Nearly half of new users leave within a year, likely due to poor onboarding or unmet expectations.

**Recommendation:**
Strengthen welcome flows, early engagement, and post-signup support.

### 6. Internet Service Type — Fiber Optic Churn Rate: 41.9%
**Implication:**
Fiber users may expect premium quality but churn if dissatisfied.

**Recommendation:**
Audit service quality, support responsiveness, and gather feedback post-installation.

### 7. Payment Method — Electronic Check Users Churned Most (45.3%)
** Implication:**
This group may be higher risk due to demographics or payment issues.

**Recommendation:**
Promote auto-pay with cards or bank transfer; offer switching incentives.

### 8. Gender — No Significant Impact
**Implication:**
Churn was nearly identical across genders.

**Recommendation:**
Focus retention efforts on higher-impact segments (contract, payment, tenure).

### 9. High-Value Churners — 350 Paid $3,000+ Before Leaving
**Implication:**
Losing high-revenue customers is a major business risk.

**Recommendation:**
Develop a VIP retention strategy — proactive support, perks, and satisfaction outreach.
