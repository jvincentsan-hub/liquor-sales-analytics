# 🔍 BigQuery Data Analysis Walkthrough

This document outlines the step-by-step SQL analysis performed on 10 years of liquor sales data inside Google BigQuery.

---

## Step 1: Data Cleaning & Handling Missing Values

Before analyzing trends, I checked for null values in the sales data and ensured the date columns were properly formatted.

```sql
-- Checking for null values in critical columns
SELECT 
  COUNTIF(invoice_id IS NULL) AS missing_invoices,
  COUNTIF(sale_dollars IS NULL) AS missing_sales
FROM `your_project.liquor_sales.sales_history`;
```
## Step 2: Aggregating 10-Year Sales Trends

To find the overall trajectory of liquor sales over the last decade, I aggregated total revenue and volume sold by year.

```sql
-- Extracting year and summing total sales
SELECT 
  EXTRACT(YEAR FROM date) AS sales_year,
  ROUND(SUM(sale_dollars), 2) AS total_revenue,
  SUM(volume_sold_liters) AS total_liters_sold
FROM `your_project.liquor_sales.sales_history`
GROUP BY sales_year
ORDER BY sales_year DESC;
```
## Step 3: Identifying Top Performing Product Categories
Next, I isolated which categories (e.g., Bourbon, Vodka, Tequila) drove the most revenue over the 10-year span.

```sql
SELECT 
  category_name,
  ROUND(SUM(sale_dollars), 2) AS total_revenue
FROM `your_project.liquor_sales.sales_history`
GROUP BY category_name
ORDER BY total_revenue DESC
LIMIT 5;
```
