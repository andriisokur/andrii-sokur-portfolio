# SQL Sales Analysis

## Overview

This is a small SQL project focused on analysing sales data.

The goal was to practise common business analysis tasks using SQL: checking revenue, identifying top customers, reviewing product performance, and looking at monthly trends.

## Business questions

- Which customers generated the most revenue?
- Which products sold the most units?
- Which products generated the most revenue?
- How did revenue change month by month?
- What was the month-over-month revenue growth?

## Tools used

- SQL
- Aggregations
- Common table expressions
- Basic window functions

## Example table

The queries are based on a simple `orders` table with fields like:

- `order_date`
- `customer_id`
- `product_name`
- `quantity`
- `amount`

## Example queries

### Top customers by revenue

```sql
SELECT
    customer_id,
    SUM(amount) AS total_spent
FROM orders
GROUP BY customer_id
ORDER BY total_spent DESC;
```

Monthly revenue
```sql
SELECT
    DATE_TRUNC('month', order_date) AS month,
    SUM(amount) AS revenue
FROM orders
GROUP BY month
ORDER BY month;
```

Revenue growth by month
```sql
WITH monthly_revenue AS (
    SELECT
        DATE_TRUNC('month', order_date) AS month,
        SUM(amount) AS revenue
    FROM orders
    GROUP BY month
),
revenue_with_previous_month AS (
    SELECT
        month,
        revenue,
        LAG(revenue) OVER (ORDER BY month) AS previous_month
    FROM monthly_revenue
)
SELECT
    month,
    revenue,
    previous_month,
    ROUND(
        (revenue - previous_month) * 100.0 / previous_month,
        2
    ) AS growth_percentage
FROM revenue_with_previous_month
WHERE previous_month IS NOT NULL;
```

Top products by quantity
```sql
SELECT
    product_name,
    SUM(quantity) AS total_sold
FROM orders
GROUP BY product_name
ORDER BY total_sold DESC;
```

Top products by revenue
```sql
SELECT
    product_name,
    SUM(amount) AS total_revenue
FROM orders
GROUP BY product_name
ORDER BY total_revenue DESC;
```

## What this project shows

This project shows how I use SQL to answer basic business questions, such as finding top customers, checking product performance, and reviewing revenue trends.

Before using this type of analysis in a real report, I would also check the data for missing values, duplicates, and inconsistent product or customer names.
