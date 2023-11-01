# All Important questions for Interview

**1. What is SQL?**

**Answer:** SQL (Structured Query Language) is a domain-specific language used for managing and manipulating relational databases. It allows users to create, retrieve, update, and delete data from databases.

**2. What are the different types of SQL joins?**

**Answer:** There are five main types of SQL joins:

- **INNER JOIN:** Retrieves matching records from both tables.
- **LEFT JOIN:** Retrieves all records from the left table and matching records from the right table.
- **RIGHT JOIN:** Retrieves all records from the right table and matching records from the left table.
- **FULL OUTER JOIN:** Retrieves all records when there is a match in either left or right table.
- **CROSS JOIN:** Generates all possible combinations of records from both tables.

**3. What is the difference between WHERE and HAVING clauses?**

**Answer:** The `WHERE` clause is used to filter rows before grouping in a query, while the `HAVING` clause is used to filter groups after grouping in a query that includes a `GROUP BY` clause.

**4. Explain the concept of normalization in databases.**

**Answer:** Normalization is the process of organizing data in a database to reduce data redundancy and dependency. It involves dividing large tables into smaller tables and defining relationships between them to ensure data integrity and optimize storage.

**5. What is an index in a database?**

**Answer:** An index is a database object that improves data retrieval performance by providing a faster way to look up rows based on the values in one or more columns. Indexes are similar to the index of a book, allowing the database to quickly locate specific data.

**6. What are primary keys and foreign keys?**

**Answer:** A primary key is a unique identifier for a record in a table, ensuring each record is distinct. A foreign key is a column that establishes a link between two tables, typically referring to the primary key of another table. It enforces referential integrity and maintains relationships between tables.

**7. What are stored procedures?**

**Answer:** Stored procedures are precompiled sets of one or more SQL statements that are stored in the database and can be executed later. They provide code reusability, security, and performance improvements by reducing the need to send multiple individual queries to the database server.

**8. What is normalization and denormalization?**

**Answer:** Normalization is the process of designing a database schema to minimize data redundancy and ensure data integrity. Denormalization, on the other hand, involves intentionally introducing redundancy for performance optimization. It can lead to faster data retrieval at the cost of increased storage.

**9. Explain ACID properties in the context of database transactions.**

**Answer:** ACID stands for Atomicity, Consistency, Isolation, and Durability. These properties ensure the reliability of database transactions:

- **Atomicity:** Ensures that a transaction is treated as a single unit of work, either entirely completed or entirely rolled back.
- **Consistency:** Ensures that a transaction takes the database from one consistent state to another.
- **Isolation:** Ensures that concurrent transactions do not interfere with each other.
- **Durability:** Ensures that once a transaction is committed, its changes are permanent and survive system failures.

**10. What is a subquery?**

**Answer:** A subquery, also known as an inner query or nested query, is a query nested within another query. It can be used to retrieve data that will be used in the main query's condition or to calculate aggregate functions.

## Queries :

### 1. Give the query to select highest salaried employee in the table ?

**Ans :**

```sql
SELECT *
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);
```

In this query, we use a subquery to find the maximum salary in the `employees` table, and then we use that value in the main query's `WHERE` clause to retrieve the employee(s) with that maximum salary. The `*` in the `SELECT` statement selects all columns for the employee(s) with the highest salary.

### 2. Get 4th Highest salaried

```sql
SELECT DISTINCT salary
FROM employee
ORDER BY salary DESC
LIMIT 1 OFFSET 3;
```

In this SQL query:

1. We select the `salary` column from the `employee` table.
2. We use the `ORDER BY` clause to sort the salaries in descending order (from highest to lowest).
3. The `LIMIT 1` clause is used to limit the result to only one row.
4. The `OFFSET 3` clause skips the first three rows (which are the highest three salaries), effectively giving you the 4th highest salary.

Make sure to replace `employee` with the actual name of your employee table in your database.
