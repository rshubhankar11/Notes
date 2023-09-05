# SQL Union Operation

In SQL, the `UNION` operation is used to combine the result sets of two or more `SELECT` queries into a single result set. This operation removes duplicate rows from the combined result set. The `UNION` operation is useful when you want to retrieve rows that satisfy the conditions of any of the involved queries, effectively creating a set union of the results.

## Syntax

The basic syntax of the `UNION` operation in SQL is as follows:

```sql
SELECT column1, column2, ...
FROM table1
WHERE condition1

UNION

SELECT column1, column2, ...
FROM table2
WHERE condition2;
```

- `SELECT`: Specifies the columns you want to retrieve from the tables.
- `FROM`: Specifies the table or tables from which you want to retrieve data.
- `WHERE`: Optional conditions to filter the rows from each table.
- `UNION`: Combines the results of the two `SELECT` queries.

## Example

Suppose you have two tables: `employees` and `contractors`, and you want to retrieve a list of all unique names from both tables. You can use the `UNION` operation as follows:

```sql
SELECT first_name, last_name
FROM employees

UNION

SELECT first_name, last_name
FROM contractors;
```

This query combines the results of the two `SELECT` queries, removing duplicate names and presenting a list of all unique names from both tables.

## `UNION ALL`

It's worth mentioning that there is a related operation called `UNION ALL`. Unlike `UNION`, `UNION ALL` does not remove duplicate rows from the combined result set. It includes all rows from the individual result sets, even if they are duplicates. This can be more efficient than `UNION` when you want to include all rows, including duplicates.

## Conclusion

In SQL, the `UNION` operation is a powerful tool for combining the results of multiple `SELECT` queries into a single result set. It allows you to create a set union of data from different tables or conditions, and it removes duplicate rows by default. Understanding how to use `UNION` can help you write more flexible and efficient SQL queries when dealing with complex data retrieval requirements.
