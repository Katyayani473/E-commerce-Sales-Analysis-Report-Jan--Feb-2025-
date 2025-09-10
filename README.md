# E-commerce_Sales_Analysis
## Project Overview
### project title:E-commerce_Sales_Analysis
### level:Beginner
### Database:p3
This project is a data-driven analysis of a sample e-commerce dataset. The goal is to demonstrate the use of SQL to answer key business questions related to sales performance, customer behavior, and product trends. The entire project is self-contained and is based on a simple, yet representative, database schema.
## Objectives
## 1.Set up a retail sales database: 
Create and populate a retail sales database with the provided sales data.
## 2.Exploratory Data Analysis (EDA): 
Perform basic exploratory data analysis to understand the dataset.
## 3.Business Analysis: 
Use SQL to answer specific business questions and derive insights from the sales data.
## Project Structure
## Database Schema
The analysis is performed on three main tables: customers, products, and orders. The schema is designed to track customer information, product details, and all order transactions.
```
create database p3;
use p3;

CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    city VARCHAR(50),
    country VARCHAR(50)
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price DECIMAL(10, 2),
    stock_quantity INT
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    product_id INT,
    quantity INT,
    total_price DECIMAL(10, 2),
    order_date DATE,
    status VARCHAR(20),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);

## Data Insertion
<pre>INSERT INTO customers (customer_id, first_name, last_name, email, city, country) VALUES
(1, 'Alice', 'Johnson', 'alice.j@email.com', 'New York', 'USA'),
(2, 'Bob', 'Smith', 'bob.s@email.com', 'London', 'UK'),
(3, 'Charlie', 'Davis', 'charlie.d@email.com', 'Paris', 'France'),
(4, 'Diana', 'Miller', 'diana.m@email.com', 'Berlin', 'Germany'),
(5, 'Eva', 'Garcia', 'eva.g@email.com', 'Madrid', 'Spain'),
(6, 'Frank', 'Wilson', 'frank.w@email.com', 'Sydney', 'Australia'),
(7, 'Grace', 'Moore', 'grace.m@email.com', 'Tokyo', 'Japan'),
(8, 'Henry', 'Lee', 'henry.l@email.com', 'Beijing', 'China'),
(9, 'Isla', 'Clark', 'isla.c@email.com', 'New York', 'USA'),
(10, 'Jack', 'Evans', 'jack.e@email.com', 'London', 'UK');

INSERT INTO products (product_id, product_name, category, price, stock_quantity) VALUES
(101, 'Laptop', 'Electronics', 1200.00, 50),
(102, 'Mouse', 'Electronics', 25.00, 200),
(103, 'Keyboard', 'Electronics', 75.00, 150),
(104, 'Desk Chair', 'Furniture', 150.00, 75),
(105, 'Coffee Table', 'Furniture', 220.00, 40),
(106, 'T-shirt', 'Apparel', 20.00, 500),
(107, 'Jeans', 'Apparel', 60.00, 300),
(108, 'Running Shoes', 'Apparel', 85.00, 100),
(109, 'Cookbook', 'Books', 30.00, 90),
(110, 'Novel', 'Books', 15.00, 120);


INSERT INTO orders (order_id, customer_id, product_id, quantity, total_price, order_date, status) VALUES
(1001, 1, 101, 1, 1200.00, '2025-01-15', 'Shipped'),
(1002, 2, 106, 2, 40.00, '2025-01-16', 'Shipped'),
(1003, 3, 109, 1, 30.00, '2025-01-17', 'Shipped'),
(1004, 4, 104, 1, 150.00, '2025-01-18', 'Shipped'),
(1005, 5, 102, 3, 75.00, '2025-01-19', 'Shipped'),
(1006, 6, 105, 1, 220.00, '2025-02-01', 'Shipped'),
(1007, 7, 101, 1, 1200.00, '2025-02-02', 'Shipped'),
(1008, 8, 108, 2, 170.00, '2025-02-03', 'Shipped'),
(1009, 9, 107, 1, 60.00, '2025-02-04', 'Shipped'),
(1010, 10, 103, 1, 75.00, '2025-02-05', 'Shipped'),
(1011, 1, 102, 1, 25.00, '2025-02-05', 'Pending'),
(1012, 2, 106, 1, 20.00, '2025-02-06', 'Pending');</pre>
## Data Analysis And Findings
## Question 1: What are the total sales, total orders, and average order value?
<pre>
  select sum(total_price)as total_sales,
count(*)as total_orders,
sum(total_price)/count(*) as avg_order_value  from orders
</pre>
## Question 2: What are the monthly and daily sales trends?
<pre>select month(order_date),day(order_date),sum(total_price) from orders group by month(order_date),day(order_date)</pre>

