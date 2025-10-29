
# 🧾 SQL Sales Database Project
## 📊 Project Overview

This project demonstrates how to create and manage a sales database system using SQL.
It includes multiple related tables — Customers, Products, Orders, and OrderDetails — and explores how to use joins and aggregate functions to analyze and retrieve data.

The goal is to understand data relationships and perform real-world database operations like calculating total revenue, linking customers to their orders, and practicing inner, left, right, and full joins.

## 🧠 Objective

To design a mini relational database and perform SQL operations to:

Create and link multiple tables using Primary and Foreign Keys

Perform JOIN operations (INNER, LEFT, RIGHT, FULL OUTER)

Calculate total revenue generated from customer orders

## ⚙️ Tools Used
Tool	Purpose
SQL Server / MySQL	Database creation and query execution

## 🗂️ Database Structure
##🧍 Customer Table

Stores basic customer details.

CREATE TABLE Customer (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(50)
);

INSERT INTO Customer VALUES
(1, 'Priya Desai', 'Mumbai'),
(2, 'Rohan Joshi', 'Pune'),
(3, 'Vidhak Joshi', 'Dhule');

## 💻 Products Table

Contains product information and pricing.

CREATE TABLE Products (
    product_id INT PRIMARY KEY,
    name VARCHAR(100),
    price DECIMAL(10, 2)
);

INSERT INTO Products VALUES
(10, 'Laptop', 50000.00),
(11, 'Mouse', 500.00),
(12, 'Headphones', 1500.00);

## 📦 Orders Table

Links customers to their purchase orders.

CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES Customer(customer_id)
);

INSERT INTO Orders VALUES
(100, 1, '2025-07-15'),
(101, 2, '2025-07-16');

## 🧾 OrderDetails Table

Connects orders to products and quantities.

CREATE TABLE OrderDetails (
    detail_id INT PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    FOREIGN KEY (order_id) REFERENCES Orders(order_id),
    FOREIGN KEY (product_id) REFERENCES Products(product_id)
);

INSERT INTO OrderDetails VALUES
(1, 100, 10, 1),
(2, 100, 11, 2),
(3, 101, 12, 1);

## 🔍 SQL Queries & Operations
1. View all tables
SELECT * FROM Customer;
SELECT * FROM Products;
SELECT * FROM Orders;
SELECT * FROM OrderDetails;

2. Calculate total revenue per order
SELECT 
    (OrderDetails.quantity * Products.price) AS total_revenue,
    Products.name,
    Products.price,
    OrderDetails.order_id,
    OrderDetails.quantity
FROM OrderDetails
LEFT JOIN Products 
ON Products.product_id = OrderDetails.product_id;

3. Calculate total overall revenue
SELECT SUM(OrderDetails.quantity * Products.price) AS total_revenue
FROM OrderDetails
LEFT JOIN Products 
ON Products.product_id = OrderDetails.product_id;

4. INNER JOIN
SELECT * 
FROM Customer
INNER JOIN Products 
ON Products.name = Customer.name;

5. LEFT JOIN
SELECT * 
FROM Customer
LEFT JOIN Orders 
ON Orders.customer_id = Customer.customer_id;

6. RIGHT JOIN
SELECT * 
FROM Products
RIGHT JOIN Customer 
ON Products.name = Customer.name;

7. FULL OUTER JOIN
SELECT * 
FROM Products
FULL OUTER JOIN Customer 
ON Products.name = Customer.name;

## 📈 Output Insights

The project calculates total revenue per product and per order.

Demonstrates the use of all types of SQL joins.

Shows the relationship between customers, orders, and products in a structured manner.

