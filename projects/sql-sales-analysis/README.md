# 📊 SQL Sales Analysis

## 📌 Overview
This project demonstrates SQL-based analysis of sales data to uncover key business insights such as revenue trends, customer behavior, and product performance.

---

## 🎯 Objectives
- Identify top customers by revenue
- Analyze monthly sales trends
- Determine best-selling products
- Understand business performance

---

## 🛠 Tools
- SQL
- Relational Databases

---

## 📊 Key Queries

### 🔹 Top Customers
Find customers who generate the most revenue.

```sql
SELECT customer_id, SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id
ORDER BY total_spent DESC;
```

---

### 🔹 Monthly Revenue
Analyze how revenue changes over time.

```sql
SELECT DATE_TRUNC('month', order_date) AS month, SUM(amount) AS revenue
FROM orders
GROUP BY month
ORDER BY month;
```

---

### 🔹 Top Products
Identify the most popular products.

```sql
SELECT product_name, SUM(quantity) AS total_sold
FROM orders
GROUP BY product_name
ORDER BY total_sold DESC;
```

---

## 💡 Insights
- A small number of customers generate most of the revenue
- Sales show clear monthly trends and seasonality
- Certain products consistently outperform others

---

## 🚀 Impact
This project demonstrates:
- Strong SQL querying skills
- Ability to extract business insights from data
- Understanding of real-world analytical tasks
