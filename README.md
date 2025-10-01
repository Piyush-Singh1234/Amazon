
# Amazon USA Sales Analysis Project


---

## Project Summary

This project focuses on analyzing a dataset of over 20,000 sales transactions from an Amazon-like e-commerce platform. The main goal is to explore customer behavior, product performance, and overall sales trends using **MySQL**.

The work involves creating complex SQL queries to address real-world business scenarios such as revenue analysis, customer segmentation, inventory monitoring, and sales forecasting. Data cleaning, handling missing values, and ensuring accurate results are key parts of the process.

An **ERD diagram** is included to illustrate the relationships and structure of the database tables.

---

## Database Design & Setup

### Schema Overview

```sql
CREATE TABLE category (
  category_id INT PRIMARY KEY,
  category_name VARCHAR(20)
);

CREATE TABLE customers (
  customer_id INT PRIMARY KEY,
  first_name VARCHAR(20),
  last_name VARCHAR(20),
  state VARCHAR(20),
  address VARCHAR(5) DEFAULT ('xxxx')
);

CREATE TABLE sellers (
  seller_id INT PRIMARY KEY,
  seller_name VARCHAR(25),
  origin VARCHAR(15)
);

CREATE TABLE products (
  product_id INT PRIMARY KEY,
  product_name VARCHAR(50),
  price FLOAT,
  cogs FLOAT,
  category_id INT,
  CONSTRAINT product_fk_category FOREIGN KEY(category_id) REFERENCES category(category_id)
);

CREATE TABLE orders (
  order_id INT PRIMARY KEY,
  order_date DATE,
  customer_id INT,
  seller_id INT,
  order_status VARCHAR(15),
  CONSTRAINT orders_fk_customers FOREIGN KEY(customer_id) REFERENCES customers(customer_id),
  CONSTRAINT orders_fk_sellers FOREIGN KEY(seller_id) REFERENCES sellers(seller_id)
);

CREATE TABLE order_items (
  order_item_id INT PRIMARY KEY,
  order_id INT,
  product_id INT,
  quantity INT,
  price_per_unit FLOAT,
  CONSTRAINT order_items_fk_orders FOREIGN KEY(order_id) REFERENCES orders(order_id),
  CONSTRAINT order_items_fk_products FOREIGN KEY(product_id) REFERENCES products(product_id)
);

CREATE TABLE payments (
  payment_id INT PRIMARY KEY,
  order_id INT,
  payment_date DATE,
  payment_status VARCHAR(20),
  CONSTRAINT payments_fk_orders FOREIGN KEY(order_id) REFERENCES orders(order_id)
);

CREATE TABLE shippings (
  shipping_id INT PRIMARY KEY,
  order_id INT,
  shipping_date DATE,
  return_date DATE,
  shipping_providers VARCHAR(15),
  delivery_status VARCHAR(15),
  CONSTRAINT shippings_fk_orders FOREIGN KEY(order_id) REFERENCES orders(order_id)
);

CREATE TABLE inventory (
  inventory_id INT PRIMARY KEY,
  product_id INT,
  stock INT,
  warehouse_id INT,
  last_stock_date DATE,
  CONSTRAINT inventory_fk_products FOREIGN KEY(product_id) REFERENCES products(product_id)
);
```

---

## Data Cleaning

Key data preprocessing steps included:

* **Removing duplicates:** Duplicate records in customers and orders tables were eliminated.
* **Handling missing values:** Critical fields such as customer address or payment status were filled with default values or appropriate placeholders.
* **Shipping data:** Return dates that were null were preserved, as not all shipments are returned.

---

## Null Value Handling

* **Customer addresses:** Missing values were replaced with placeholders.
* **Payment status:** Nulls were categorized as “Pending.”
* **Shipping return dates:** Left as null since returns don’t always occur.

---

## Project Goals

This project demonstrates proficiency in SQL for solving practical e-commerce challenges, including:

* Analyzing customer behavior
* Tracking sales trends
* Monitoring inventory levels
* Understanding payment and shipping patterns
* Evaluating product performance

---

## Business Challenges Identified

1. Insufficient product availability due to inconsistent restocking.
2. High return rates in certain product categories.
3. Delays and inconsistencies in shipment deliveries.
4. High costs of customer acquisition with low retention rates.

---

## Solutions Implemented

### Sample SQL Analyses

1. **Top Selling Products:** Ranked products by total sales value and quantity.
2. **Revenue by Category:** Calculated total revenue per category and contribution percentages.
3. **Average Order Value (AOV):** Calculated average order value for customers with more than five orders.
4. **Monthly Sales Trends:** Tracked total sales per month over the past year, including previous month comparisons.
5. **Customers with No Purchases:** Identified registered customers who never placed an order.
6. **Least-Selling Categories by State:** Determined the lowest performing categories in each state.
7. **Customer Lifetime Value (CLTV):** Ranked customers by total lifetime order value.
8. **Inventory Stock Alerts:** Flagged products with low stock and displayed last restock information.
9. **Shipping Delays:** Highlighted orders shipped more than 3 days after the order date.
10. **Payment Success Rate:** Calculated percentages of successful and failed payments.
11. **Top Performing Sellers:** Ranked sellers by total sales and computed successful order percentages.
12. **Product Profit Margin:** Ranked products based on profit margins.
13. **Most Returned Products:** Identified products with the highest return rates.
14. **Inactive Sellers:** Found sellers without sales in the last 6 months.
15. **Customer Classification:** Categorized customers as returning or new based on returns.
16. **Top Customers by State:** Identified top 5 customers per state by order count.
17. **Revenue by Shipping Provider:** Tracked revenue, order volume, and average delivery time per provider.
18. **Revenue Decrease Analysis:** Compared product revenue year-over-year to identify declines.
19. **Stored Procedure for Sales:** Automated adding sales and updating inventory with a PostgreSQL procedure.

---

## Learning Outcomes

By completing this project, I gained the ability to:

* Design and implement normalized relational databases.
* Clean and preprocess real-world datasets for analysis.
* Write advanced SQL queries using window functions, subqueries, and joins.
* Conduct detailed business analysis with large datasets.
* Optimize queries for performance and handle real-world e-commerce scenarios.

---

## Conclusion

This project showcases advanced SQL skills and demonstrates the ability to solve operational challenges in e-commerce. From inventory optimization to customer retention analysis, the work highlights practical insights derived from structured query techniques.

