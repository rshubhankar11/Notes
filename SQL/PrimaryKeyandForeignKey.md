# Primary Key and Foreign Key in Relational Databases

## Table of Contents

1. [Introduction](#introduction)
2. [Primary Key](#primary-key)
   - [Explanation](#explanation-of-primary-key)
   - [Example](#example-of-primary-key)
3. [Foreign Key](#foreign-key)
   - [Explanation](#explanation-of-foreign-key)
   - [Example](#example-of-foreign-key)
4. [Comparison Table](#comparison-table)
5. [Conclusion](#conclusion)

---

## Introduction

In relational databases, primary keys and foreign keys play crucial roles in establishing relationships between tables and maintaining data integrity. They ensure accurate data retrieval, data linkage, and overall database organization.

## Primary Key

### Explanation of Primary Key

A primary key is a unique identifier for each record in a table. It ensures that each row in the table is distinct and can be uniquely identified. Primary keys are used to uniquely identify records and enforce data integrity rules, as they prevent duplicate or null values. A primary key can consist of one or multiple columns.

### Example of Primary Key

Consider a `students` table where each student is assigned a unique student ID as the primary key:

```sql
CREATE TABLE students (
    student_id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    age INT
);
```

In this example, the `student_id` column acts as the primary key for the `students` table, ensuring that each student has a unique identifier.

## Foreign Key

### Explanation of Foreign Key

A foreign key is a column or a set of columns in a table that refers to the primary key of another table. It establishes a relationship between two tables by ensuring referential integrity. Foreign keys maintain the relationships between tables and help maintain data consistency.

### Example of Foreign Key

Consider an `orders` table that references the `customers` table using a foreign key:

```sql
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    email VARCHAR(100)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    order_date DATE,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

In this example, the `customer_id` column in the `orders` table is a foreign key that references the primary key of the `customers` table. This establishes a relationship between the `orders` and `customers` tables, ensuring that orders are associated with valid customers.

## Comparison Table

| Aspect           | Primary Key                                     | Foreign Key                                         |
| ---------------- | ----------------------------------------------- | --------------------------------------------------- |
| Purpose          | Uniquely identifies each record in a table      | Establishes relationships between two tables        |
| Uniqueness       | Must be unique within the table                 | Doesn't have to be unique; references a primary key |
| Nullable         | Not nullable                                    | Can be nullable                                     |
| Columns          | Typically consists of one or more columns       | Typically a single column or a set of columns       |
| Referenced Table | Same table or a different table                 | Typically references a primary key in another table |
| Data Integrity   | Enforces data integrity and prevents duplicates | Ensures referential integrity and data consistency  |

## Conclusion

Primary keys and foreign keys are fundamental concepts in relational databases that help establish relationships between tables and maintain data integrity. Primary keys uniquely identify records, while foreign keys establish relationships between tables and ensure data consistency. Understanding these concepts is essential for designing well-structured databases and performing accurate data operations.

---
