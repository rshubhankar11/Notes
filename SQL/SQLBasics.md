# SQL Complete Reference Guide

## Table of Contents

1. [Introduction to SQL](#introduction-to-sql)
2. [Basic SQL Commands](#basic-sql-commands)
3. [SQL Joins](#sql-joins)
   - [INNER JOIN](#inner-join)
   - [LEFT JOIN](#left-join)
   - [RIGHT JOIN](#right-join)
   - [FULL OUTER JOIN](#full-outer-join)
   - [CROSS JOIN](#cross-join)
4. [SQL Built-in Functions](#sql-built-in-functions)
   - [Aggregate Functions](#aggregate-functions)
   - [String Functions](#string-functions)
   - [Date and Time Functions](#date-and-time-functions)
   - [Numeric Functions](#numeric-functions)
5. [Important Features](#important-features)
6. [Advantages and Disadvantages](#advantages-and-disadvantages)

---

## Introduction to SQL

Structured Query Language (SQL) is a domain-specific language used for managing and manipulating relational databases. It is used to perform tasks such as querying data, updating data, creating tables, and defining relationships between tables.

## Basic SQL Commands

- `SELECT`: Retrieve data from one or more tables.
- `INSERT`: Insert new records into a table.
- `UPDATE`: Modify existing records in a table.
- `DELETE`: Remove records from a table.
- `CREATE TABLE`: Create a new table.
- `ALTER TABLE`: Modify an existing table's structure.
- `DROP TABLE`: Delete a table.
- `CREATE INDEX`: Create an index for faster data retrieval.

## SQL Joins

### INNER JOIN

Retrieve matching records from both tables.

```sql
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.id;
```

### LEFT JOIN

Retrieve all records from the left table and matching records from the right table.

```sql
SELECT customers.customer_name, orders.order_date
FROM customers
LEFT JOIN orders ON customers.customer_id = orders.customer_id;
```

### RIGHT JOIN

Retrieve all records from the right table and matching records from the left table.

```sql
SELECT orders.order_id, products.product_name
FROM orders
RIGHT JOIN products ON orders.product_id = products.id;
```

### FULL OUTER JOIN

Retrieve all records when there is a match in either left or right table.

```sql
SELECT students.student_name, courses.course_name
FROM students
FULL OUTER JOIN courses ON students.course_id = courses.id;
```

### CROSS JOIN

Generate all possible combinations of records from both tables.

```sql
SELECT employees.name, departments.department_name
FROM employees
CROSS JOIN departments;
```

## SQL Built-in Functions

### Aggregate Functions

- `COUNT()`: Count the number of rows.

```sql
SELECT COUNT(*) FROM orders;
```

- `SUM()`: Calculate the sum of values.

```sql
SELECT SUM(total_price) FROM invoices;
```

- `AVG()`: Calculate the average of values.

```sql
SELECT AVG(salary) FROM employees;
```

- `MIN()`: Get the minimum value.

```sql
SELECT MIN(price) FROM products;
```

- `MAX()`: Get the maximum value.

```sql
SELECT MAX(score) FROM test_scores;
```

### String Functions

- `CONCAT()`: Concatenate strings.

```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM users;
```

- `SUBSTRING()`: Extract a substring.

```sql
SELECT SUBSTRING(description, 1, 10) AS short_desc FROM articles;
```

- `UPPER()`: Convert to uppercase.

```sql
SELECT UPPER(product_name) FROM products;
```

- `LOWER()`: Convert to lowercase.

```sql
SELECT LOWER(city) FROM customers;
```

- `LENGTH()`: Get the length of a string.

```sql
SELECT LENGTH(email) FROM contacts;
```

### Date and Time Functions

- `NOW()`: Current date and time.

```sql
SELECT NOW();
```

- `DATE()`: Extract date from a datetime.

```sql
SELECT DATE(created_at) FROM orders;
```

- `TIME()`: Extract time from a datetime.

```sql
SELECT TIME(order_time) FROM orders;
```

- `YEAR()`, `MONTH()`, `DAY()`: Extract parts of a date.

```sql
SELECT YEAR(birthdate), MONTH(birthdate), DAY(birthdate) FROM users;
```

### Numeric Functions

- `ROUND()`: Round to the nearest integer.

```sql
SELECT ROUND(price, 2) FROM products;
```

- `FLOOR()`: Round down to the nearest integer.

```sql
SELECT FLOOR(quantity) FROM inventory;
```

- `CEIL()`: Round up to the nearest integer.

```sql
SELECT CEIL(total_distance) FROM trips;
```

- `ABS()`: Absolute value.

```sql
SELECT ABS(balance) FROM accounts;
```

## Important Features

- **Transactions**: Ensure data consistency and integrity using ACID properties.
- **Indexes**: Improve data retrieval performance by creating indexes on columns.
- **Views**: Create virtual tables based on existing tables.
- **Stored Procedures**: Store a set of SQL statements for reuse.
- **Triggers**: Automatically execute SQL statements on certain events.

## Advantages and Disadvantages

### Advantages

- Provides a standardized way to interact with databases.
- Offers powerful querying capabilities for data retrieval and manipulation.
- Supports complex operations like joins and subqueries.
- Enables data integrity through constraints and relationships.
- Widely used and supported in various database management systems.

### Disadvantages

- Can be complex for beginners due to its syntax and capabilities.
- Not suitable for unstructured or semi-structured data.
- Performance can degrade on large datasets without proper optimization.
- Different database systems may have variations in SQL syntax.

---
