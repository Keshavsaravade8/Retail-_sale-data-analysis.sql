# Retail-_sale-data-analysis.sql

# 🛒 Retail Sales Analysis SQL Project

## 📌 Project Overview

- **Title**: Retail Sales Analysis  
- **Level**: Beginner  
- **Database**: `sql_pro`

This project demonstrates core SQL skills required for a data analyst role. It includes database setup, data cleaning, and querying techniques on retail sales data using **SQL Server Management Studio (SSMS)**.

---

## 🎯 Objectives

1. Create a retail sales database and table.
2. Load and clean the dataset (remove null or incorrect data).
3. Analyze sales trends, customer behavior, and category performance.
4. Use SQL queries to derive key business insights.

---

## 🗂️ Database Setup

```sql
-- Create a database
CREATE DATABASE sql_pro;

-- Use the database
USE sql_pro;

-- Create retail_sales table
CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
```

---

## 🧼 Data Cleaning

### ✅ Renaming Incorrect Column
```sql
EXEC sp_rename 'retail_sales.quantiy','quantity','COLUMN';
```

### ✅ Checking for NULL Values
```sql
SELECT * FROM retail_sales
WHERE sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```

### ✅ Deleting Rows with NULL Values
```sql
DELETE FROM retail_sales
WHERE sale_date IS NULL
   OR sale_time IS NULL
   OR customer_id IS NULL
   OR gender IS NULL
   OR age IS NULL
   OR category IS NULL
   OR quantity IS NULL
   OR price_per_unit IS NULL
   OR cogs IS NULL
   OR total_sale IS NULL;
```

---

## 📊 SQL Analysis & Insights

### 1. All Sales on 2022-11-05
```sql
SELECT * FROM retail_sales
WHERE sale_date = '2022-11-05';
```

### 2. Clothing Transactions > 4 Units in Nov-2022
```sql
SELECT * FROM retail_sales
WHERE category = 'Clothing'
  AND quantity > 4
  AND sale_date >= '2022-11-01'
  AND sale_date < '2022-12-01';
```

### 3. Total Sales per Category
```sql
SELECT category, SUM(total_sale) AS totalsale
FROM retail_sales
GROUP BY category;
```

### 4. Average Age of Customers (Beauty Category)
```sql
SELECT customer_id, AVG(age) AS avgage
FROM retail_sales
WHERE category = 'Beauty'
GROUP BY customer_id;
```

### 5. High-Value Transactions (> 1000)
```sql
SELECT customer_id, transactions_id, total_sale
FROM retail_sales
WHERE total_sale > 1000
ORDER BY customer_id ASC;
```

### 6. Total Transactions by Gender and Category
```sql
SELECT gender, category, COUNT(transactions_id) AS transaction_count
FROM retail_sales
GROUP BY gender, category
ORDER BY transaction_count ASC;
```

### 7. Average Sale Per Month & Best Month Per Year
```sql
SELECT 
    YEAR(sale_date) AS sale_year,
    MONTH(sale_date) AS sale_month,
    AVG(total_sale) AS avg_monthly_sale
FROM retail_sales
GROUP BY YEAR(sale_date), MONTH(sale_date)
ORDER BY sale_year, avg_monthly_sale DESC;
```

### 8. Top 5 Customers by Total Sales
```sql
SELECT TOP 5 * 
FROM retail_sales
ORDER BY total_sale DESC;
```

### 9. Unique Customers per Category
```sql
SELECT category, COUNT(DISTINCT customer_id) AS numbers_of_customers
FROM retail_sales
GROUP BY category;
```

### 10. Number of Orders per Shift
```sql
SELECT 
  CASE
    WHEN DATEPART(HOUR, sale_time) < 12 THEN 'Morning'
    WHEN DATEPART(HOUR, sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
    ELSE 'Evening'
  END AS shift,
  COUNT(*) AS order_count
FROM retail_sales
GROUP BY 
  CASE
    WHEN DATEPART(HOUR, sale_time) < 12 THEN 'Morning'
    WHEN DATEPART(HOUR, sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
    ELSE 'Evening'
  END;
```

### 11. Monthly Orders per Year
```sql
SELECT 
    YEAR(sale_date) AS sale_year,
    MONTH(sale_date) AS sale_month,
    COUNT(*) AS total_orders
FROM retail_sales
GROUP BY YEAR(sale_date), MONTH(sale_date)
ORDER BY sale_year, sale_month;
```

### 12. Highest Sales Category by Year
```sql
SELECT 
    category,
    YEAR(sale_date) AS sale_year,
    SUM(total_sale) AS total_sales
FROM retail_sales
GROUP BY category, YEAR(sale_date)
ORDER BY total_sales DESC;
```

---

## 🧾 Final Remarks

- ✅ Cleaned the dataset for accurate analysis.
- 📈 Identified top-performing categories and high-value customers.
- 📅 Found peak sales periods and most active sales shifts.

---

## 📂 How to Use

1. Clone the repository.
2. Import the CSV file into SQL Server using SSMS.
3. Run the above queries to analyze the dataset.
4. Modify queries for additional insights or custom analysis.

---

## 🙋‍♂️ Author

**Zero Analyst**  
Showcasing SQL skills for data analytics.

📌 Follow and connect:
- [YouTube](https://www.youtube.com/@zero_analyst)
- [Instagram](https://www.instagram.com/zero_analyst/)
- [LinkedIn](https://www.linkedin.com/in/najirr)
- [Discord Community](https://discord.gg/36h5f2Z5PK)
