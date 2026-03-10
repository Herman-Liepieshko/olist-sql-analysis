# Brazilian E-Commerce SQL Analysis

An end-to-end SQL analysis of the **Olist Brazilian E-Commerce dataset**, exploring ~100,000 orders through 15 progressively complex SQL queries — from basic aggregations to window functions and RFM customer segmentation. All analysis is performed in a Jupyter Notebook using an **in-memory SQLite database** powered by Python.

---

## Skills Demonstrated

| Skill | Details |
|---|---|
| SQL Joins | Multi-table JOINs across 5+ tables |
| Aggregations | GROUP BY, COUNT, SUM, AVG, ROUND |
| Subqueries | Scalar subqueries, correlated subqueries |
| Window Functions | RANK(), SUM() OVER, AVG() OVER, NTILE() |
| CTEs | WITH clauses for readable multi-step logic |
| Data Visualization | Matplotlib & Seaborn charts with business context |
| Business Analysis | RFM segmentation, delivery SLA analysis, revenue trends |

---

## Dataset

**Brazilian E-Commerce Public Dataset by Olist**
Source: [Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

~100,000 orders placed between 2016 and 2018 on the Olist marketplace, spanning 9 relational CSV files.

---

## Database Schema

```
customers ─────────────────────────────────────────┐
  customer_id (PK)                                 │
  customer_unique_id                               │
  customer_city, customer_state                    │
                                                   │
orders ────────────────────────────────────────────┘
  order_id (PK)                        customer_id (FK)
  order_status
  order_purchase_timestamp
  order_delivered_customer_date
  order_estimated_delivery_date
        │
        ├──── order_items ─────────────────── products
        │       order_id (FK)                  product_id (PK)
        │       product_id (FK)                product_category_name (FK)
        │       seller_id  (FK)                       │
        │       price, freight_value       category_translation
        │                │                   product_category_name
        │                └──────── sellers    product_category_name_english
        │                          seller_id (PK)
        │                          seller_city, seller_state
        │
        ├──── order_payments
        │       order_id (FK)
        │       payment_type, payment_value, payment_installments
        │
        └──── order_reviews
                order_id (FK)
                review_score (1–5)
```

---

## Business Questions Covered

**Block 1 — Basic Aggregations**
1. How many orders were placed each month? What is the overall trend?
2. Which are the top 10 product categories by number of sales?
3. What is the average order value and average freight cost?
4. How are review scores distributed across all orders?

**Block 2 — JOINs and Table Relationships**
5. Which top 10 cities generate the most revenue?
6. Which product categories receive the best and worst customer ratings?
7. Is there a relationship between freight cost and customer satisfaction?

**Block 3 — Subqueries**
8. What percentage of orders were delivered late?
9. Which sellers generate revenue above the platform average?
10. Which product categories have an above-average late delivery rate?

**Block 4 — Window Functions**
11. What does cumulative revenue growth look like month over month?
12. Who are the top 3 sellers by revenue in each of the 5 largest states?
13. What does a 3-month rolling average of order value reveal?

**Block 5 — Advanced Analysis**
14. How can we segment customers using RFM analysis?
15. How does the average delivery time vary by product category, and which categories have the longest delays?

---

## Key Findings

- **Strong Growth**: Platform revenue was on track to double from 2017 to 2018, with a major Black Friday spike in November 2017.
- **Delivery = Satisfaction**: Late deliveries and high freight costs are the strongest drivers of negative (1-star) reviews.
- **One-Time Buyers**: RFM analysis shows most customers buy once and don't return — customer retention is the biggest untapped opportunity.
- **Geographic Concentration**: São Paulo and the Southeast region dominate both revenue and seller activity.

---

## SQL Techniques Used

| Technique | Used in Queries |
|---|---|
| GROUP BY + COUNT/SUM/AVG | Q1, Q2, Q3, Q4, Q15 |
| Multi-table JOIN | Q2, Q5, Q6, Q7, Q15 |
| CASE WHEN | Q8, Q10, Q14 |
| Scalar Subquery | Q9 |
| Nested Subquery with aggregation | Q10 |
| SUM() OVER (running total) | Q11 |
| RANK() OVER (PARTITION BY) | Q12 |
| AVG() OVER (ROWS BETWEEN) | Q13 |
| NTILE() window function | Q14 |
| CTE (WITH clause) | Q12, Q14, Q15 |
| Date functions (strftime, julianday) | Q1, Q8, Q11, Q13, Q14, Q15 |
| COALESCE for null handling | Q2, Q6, Q10 |

---

## Project Structure

```
olist-sql-analysis/
├── data/
│   └── raw/
│       ├── olist_customers_dataset.csv
│       ├── olist_geolocation_dataset.csv
│       ├── olist_order_items_dataset.csv
│       ├── olist_order_payments_dataset.csv
│       ├── olist_order_reviews_dataset.csv
│       ├── olist_orders_dataset.csv
│       ├── olist_products_dataset.csv
│       ├── olist_sellers_dataset.csv
│       └── product_category_name_translation.csv
├── notebooks/
│   └── sql_analysis.ipynb
├── README.md
└── requirements.txt
```

---

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/Herman-Liepieshko/olist-sql-analysis.git
cd olist-sql-analysis

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch Jupyter
jupyter notebook

# 4. Open notebooks/sql_analysis.ipynb and run all cells
```

The notebook uses an **in-memory SQLite database** — no database server required. All CSV files are loaded automatically from `data/raw/`.
