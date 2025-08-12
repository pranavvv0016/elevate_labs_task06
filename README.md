# Task 6 - Sales Trend Analysis Using Aggregations

## 📌 Objective
Analyze **monthly revenue** and **monthly order volume** from the Olist Brazilian E-Commerce dataset using SQL.

---

## 📂 Dataset
Dataset Source: [Olist Brazilian E-Commerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

For this task, we used:
- **olist_orders_dataset.csv** → contains order details including `order_id` and `order_purchase_timestamp`
- **olist_order_payments_dataset.csv** → contains payment details including `order_id` and `payment_value`

---

## 🛠 Tools Used
- **SQLite** (via DB Browser for SQLite)
- SQL for data aggregation and analysis

---

## 🗂 Steps Performed
1. **Loaded Data**: Imported both CSV files into SQLite as tables:
   - `olist_orders_dataset`
   - `olist_order_payments_dataset`

2. **Joined Tables**: Used `order_id` to join orders and payments tables.

3. **Extracted Year & Month**: Applied `strftime('%Y', ...)` and `strftime('%m', ...)` to get year and month from `order_purchase_timestamp`.

4. **Aggregated Data**:
   - **Monthly Revenue**: `SUM(payment_value)`
   - **Monthly Order Volume**: `COUNT(DISTINCT order_id)`

5. **Sorted Output**: Ordered results by year and month.

---

# 🖥 SQL Query
```sql
SELECT
  CAST(strftime('%Y', o.order_purchase_timestamp) AS INTEGER) AS year,
  CAST(strftime('%m', o.order_purchase_timestamp) AS INTEGER) AS month,
  SUM(COALESCE(p.payment_value, 0)) AS total_revenue,
  COUNT(DISTINCT o.order_id) AS total_orders
FROM olist_orders_dataset o
JOIN olist_order_payments_dataset p
  ON o.order_id = p.order_id
WHERE o.order_purchase_timestamp IS NOT NULL
GROUP BY year, month
ORDER BY year, month;
```

##📁 Files in This Repository
```
task6_results.csv → Output CSV of monthly revenue and order volume.

task6.sql → SQL query used to produce the results.

README.md → Task documentation (this file).
```
#📌 How to Run
```
Open DB Browser for SQLite.

Import both CSVs into tables named:

olist_orders_dataset

olist_order_payments_dataset

Paste and run the SQL query from task6.sql.

Export the results as task6_results.csv.
```
