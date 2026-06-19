# Iowa Liquor Sales: 10-Year Monthly Trend Analysis

## 📌 Project Overview
This project analyzes a massive, real-world public dataset containing millions of liquor sales transactions in Iowa spanning from 2016 to 2025. The goal of this analysis is to uncover macro-level seasonal purchasing patterns, evaluate year-over-year growth, and identify cyclical demand fluctuations to help retailers optimize inventory management and predict supply chain demand.

---

## 📊 Business Objectives & Questions
* **Seasonality:** Which months historically experience the highest surge in liquor sales volume?
* **Growth Trends:** How have total sales evolved over the last decade? Is the market expanding, or has it plateaued?
* **Predictive Value:** Can historical buying behavior accurately forecast which quarters require aggressive stocking and staffing?

---

## 🗄️ Dataset Used
* **Source:** Google BigQuery Public Data
* **Table:** `bigquery-public-data.iowa_liquor_sales.sales`
* **Scope:** Time-series filtering from **January 1, 2016, to December 31, 2025**.

---

## 💻 SQL Implementation

The analysis aggregates total dollar sales by year and month while ensuring the final output is sequentially ordered chronologically.

```sql
SELECT 
    EXTRACT(YEAR FROM date) as sales_year, 
    FORMAT_DATE('%b', date) as calendar_month, 
    SUM(sale_dollars) as total_sales
FROM 
    `bigquery-public-data.iowa_liquor_sales.sales`
WHERE 
    date BETWEEN '2016-01-01' AND '2025-12-31'
GROUP BY 
    sales_year, 
    calendar_month, 
    EXTRACT(MONTH FROM date)
ORDER BY 
    sales_year ASC, 
    EXTRACT(MONTH FROM date) ASC;
