# 📊 SQL Sales Analysis

## 📌 Overview
This project demonstrates SQL-based analysis of sales data to uncover key business insights such as revenue trends, customer behavior, and product performance.

The goal is to transform raw transactional data into meaningful business insights.

---

## 🎯 Objectives
- Identify top customers by revenue
- Analyze monthly sales trends
- Track revenue growth over time
- Determine best-selling products
- Understand overall business performance

---

## 🛠 Tools
- SQL
- Relational Databases
- Aggregate Functions
- Basic Window Functions

---

## 📊 Key Queries

### 🔹 Top Customers
```sql
SELECT customer_id, SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id
ORDER BY total_spent DESC;
```

🔹 Monthly Revenue
```sql
SELECT DATE_TRUNC('month', order_date) AS month,
       SUM(amount) AS revenue
FROM orders
GROUP BY month
ORDER BY month;
```

### 🔹 Revenue Growth
```sql
WITH monthly_revenue AS (
    SELECT DATE_TRUNC('month', order_date) AS month,
           SUM(amount) AS revenue
    FROM orders
    GROUP BY month
)
SELECT month,
       revenue,
       LAG(revenue) OVER (ORDER BY month) AS previous_month,
       ROUND(
           (revenue - LAG(revenue) OVER (ORDER BY month)) 
           * 100.0 / LAG(revenue) OVER (ORDER BY month), 
           2
       ) AS growth_percentage
FROM monthly_revenue;
```

🔹 Top Products
```sql
SELECT product_name,
       SUM(quantity) AS total_sold
FROM orders
GROUP BY product_name
ORDER BY total_sold DESC;
```

🔹 Top Products by Revenue
```sql
SELECT product_name,
       SUM(amount) AS total_revenue
FROM orders
GROUP BY product_name
ORDER BY total_revenue DESC;
```


