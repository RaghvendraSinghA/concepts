# SQL Report: Basics, Joins, and Aggregations

## Table of Contents

1. Introduction to SQL
2. SQL Basics
   - CREATE TABLE
   - INSERT
   - SELECT
   - WHERE
   - ORDER BY
   - LIMIT
   - UPDATE
   - DELETE
3. Sample Database
4. SQL Joins
   - INNER JOIN
   - LEFT JOIN
   - RIGHT JOIN
   - FULL OUTER JOIN
   - CROSS JOIN
   - SELF JOIN
5. SQL Aggregations
   - COUNT()
   - SUM()
   - AVG()
   - MIN()
   - MAX()
   - GROUP BY
   - HAVING
6. Combining Joins and Aggregations
7. References
---

# 1. Introduction to SQL

**SQL (Structured Query Language)** is the standard language used to interact with relational databases.

Using SQL, you can:

- Create databases and tables
- Insert data
- Retrieve data
- Update data
- Delete data
- Analyze data

Popular relational databases include:

- MySQL
- PostgreSQL
- Oracle Database

---

# 2. SQL Basics

## Creating a Table

A table stores data in rows and columns.

```sql

CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2),
    department_id INT,
);
```

Explanation:

- `INT` stores integers.
- `VARCHAR(100)` stores text up to 100 characters.
- `DECIMAL(10,2)` stores numbers with decimal places.
- `PRIMARY KEY` uniquely identifies each row.

---

## Inserting Data

```sql
INSERT INTO Employees
VALUES
(101,'Alice',70000,1),
(102,'Bob',60000,1),
```

---

## Selecting Data

Retrieve every row.

```sql
SELECT *
FROM Employees;
```

Retrieve only specific columns.

```sql
SELECT
    name,
    salary
FROM Employees;
```

---

## WHERE Clause

Filter rows.

```sql
SELECT *
FROM Employees
WHERE salary > 60000;
```

Multiple conditions.

```sql
SELECT *
FROM Employees
WHERE department_id = 1
AND salary > 65000;
```

---

## ORDER BY

Sort records.

Ascending:

```sql
SELECT *
FROM Employees
ORDER BY salary ASC;
```

Descending:

```sql
SELECT *
FROM Employees
ORDER BY salary DESC;
```

---

## LIMIT

Retrieve only a few rows.

```sql
SELECT *
FROM Employees
LIMIT 3;
```

---

## UPDATE

Modify existing rows.

```sql
UPDATE Employees
SET salary = 75000
WHERE employee_id = 101;
```

---

## DELETE

Delete rows.

```sql
DELETE FROM Employees
WHERE employee_id = 105;
```

---

# 3. Sample Database

## Employees

| employee_id | name | salary | department_id |
|------------:|------|--------:|--------------:|
|101|Alice|70000|1|
|102|Bob|60000|1|

---

# 4. SQL Joins

A JOIN combines rows from two or more tables using a related column.

---

## INNER JOIN

Returns only matching rows.

```sql
CREATE TABLE Departments (
    department_id INT PRIMARY KEY,
    department_name VARCHAR(100)
);


INSERT INTO Departments
VALUES
(1, 'Engineering'),
(2, 'HR'),
(3, 'Finance');


CREATE TABLE Employees (
    employee_id INT PRIMARY KEY,
    name VARCHAR(100),
    salary DECIMAL(10,2),
    department_id INT,
    FOREIGN KEY (department_id)
        REFERENCES Departments(department_id)
);

INSERT INTO Employees
VALUES
(101, 'Alice', 70000, 1),
(102, 'Bob', 60000, 1),
(103, 'Charlie', 50000, 2),
(104, 'David', 80000, 3),
(105, 'Eva', 55000, 2);

SELECT
    e.employee_id,
    e.name,
    d.department_name
FROM Employees e
INNER JOIN Departments d
ON e.department_id = d.department_id;
```

Output

| employee_id | name | department_name |
|-------------|------|-----------------|
|101|Alice|Engineering|
|102|Bob|Engineering|
|103|Charlie|HR|
|104|David|Finance|
|105|Eva|HR|

---

## LEFT JOIN

Returns all rows from the left table.

```sql
SELECT
    e.name,
    d.department_name
FROM Employees e
LEFT JOIN Departments d
ON e.department_id = d.department_id;
```

If an employee has no matching department, the department columns contain `NULL`.

---

## RIGHT JOIN

Returns every row from the right table.

```sql
SELECT
    e.name,
    d.department_name
FROM Employees e
RIGHT JOIN Departments d
ON e.department_id = d.department_id;
```

If a department has no employees, employee columns contain `NULL`.

> Note: SQLite does not support `RIGHT JOIN`.

---

## FULL OUTER JOIN

Returns all rows from both tables.

```sql
SELECT
    e.name,
    d.department_name
FROM Employees e
FULL OUTER JOIN Departments d
ON e.department_id = d.department_id;
```

Rows without matches on either side contain `NULL`.

> Note: MySQL does not directly support `FULL OUTER JOIN`. It is commonly simulated using `LEFT JOIN`, `RIGHT JOIN`, and `UNION`.

---

## CROSS JOIN

Creates every possible combination.

```sql
SELECT
    e.name,
    d.department_name
FROM Employees e
CROSS JOIN Departments d;
```

If there are:

- 5 employees
- 3 departments

Result:

```
5 × 3 = 15 rows
```

---

## SELF JOIN

A table joined with itself.

Example:

```sql
CREATE TABLE Employees (
    employee_id INT,
    name VARCHAR(100),
    manager_id INT
);
```

```sql
SELECT
    e.name AS Employee,
    m.name AS Manager
FROM Employees e
LEFT JOIN Employees m
ON e.manager_id = m.employee_id;
```

---

# 5. SQL Aggregations

Aggregate functions perform calculations on a group of rows and return a single result.

---

## COUNT()

Counts rows.

```sql
SELECT COUNT(*)
FROM Employees;
```

Count employees in Engineering.

```sql
SELECT COUNT(*)
FROM Employees
WHERE department_id = 1;
```

---

## SUM()

Calculates total.

```sql
SELECT SUM(salary)
FROM Employees;
```

---

## AVG()

Calculates average.

```sql
SELECT AVG(salary)
FROM Employees;
```

---

## MIN()

Returns smallest value.

```sql
SELECT MIN(salary)
FROM Employees;
```

---

## MAX()

Returns largest value.

```sql
SELECT MAX(salary)
FROM Employees;
```

---

## GROUP BY

GROUP BY groups rows with the same value and applies aggregate functions to each group.

Average salary by department.

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM Employees
GROUP BY department_id;
```

Output

| department_id | average_salary |
|--------------:|---------------:|
|1|65000|
|2|52500|
|3|80000|

---

## HAVING

HAVING filters groups after aggregation.Like after Group-by.

Departments whose average salary exceeds 60,000.

```sql
SELECT
    department_id,
    AVG(salary) AS average_salary
FROM Employees
GROUP BY department_id
HAVING AVG(salary) > 60000;
```

Result

| department_id | average_salary |
|--------------:|---------------:|
|1|65000|
|3|80000|

---

# 6. Combining Joins and Aggregations

Count employees in each department.

```sql
SELECT
    d.department_name,
    COUNT(e.employee_id) AS total_employees
FROM Departments d
LEFT JOIN Employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
```

Output

| Department | Employees |
|------------|----------:|
|Engineering|2|
|HR|2|
|Finance|1|

---

Average salary by department.

```sql
SELECT
    d.department_name,
    AVG(e.salary) AS average_salary
FROM Departments d
INNER JOIN Employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
```

---

Highest-paid employee in each department.

```sql
SELECT
    d.department_name,
    MAX(e.salary) AS highest_salary
FROM Departments d
JOIN Employees e
ON d.department_id = e.department_id
GROUP BY d.department_name;
```

---

Departments with more than one employee.

```sql
SELECT
    d.department_name,
    COUNT(e.employee_id) AS total_employees
FROM Departments d
JOIN Employees e
ON d.department_id = e.department_id
GROUP BY d.department_name
HAVING COUNT(e.employee_id) > 1;
```

---
---

# References

The following official documentation was used as a reference for SQL syntax, joins, aggregate functions, and database concepts.

## General SQL and PostgreSQL

1. [PostgreSQL Documentation — SQL Commands](https://www.postgresql.org/docs/current/sql-commands.html)
2. [PostgreSQL Documentation — SELECT](https://www.postgresql.org/docs/current/sql-select.html)
3. [PostgreSQL Documentation — CREATE TABLE](https://www.postgresql.org/docs/current/sql-createtable.html)
4. [PostgreSQL Documentation — INSERT](https://www.postgresql.org/docs/current/sql-insert.html)
5. [PostgreSQL Documentation — UPDATE](https://www.postgresql.org/docs/current/sql-update.html)
6. [PostgreSQL Documentation — DELETE](https://www.postgresql.org/docs/current/sql-delete.html)

## Keys and Constraints

7. [PostgreSQL Documentation — Constraints, Primary Keys, and Foreign Keys](https://www.postgresql.org/docs/current/ddl-constraints.html)

## SQL Joins

8. [PostgreSQL Documentation — Table Expressions and JOIN Operations](https://www.postgresql.org/docs/current/queries-table-expressions.html)
9. [MySQL Reference Manual — JOIN Clause](https://dev.mysql.com/doc/refman/en/join.html)
10. [SQLite Documentation — SELECT and JOIN Operations](https://www.sqlite.org/lang_select.html)

## Aggregate Functions

11. [PostgreSQL Documentation — Aggregate Functions](https://www.postgresql.org/docs/current/functions-aggregate.html)
12. [PostgreSQL Documentation — GROUP BY and HAVING](https://www.postgresql.org/docs/current/queries-table-expressions.html#QUERIES-GROUP)
13. [MySQL Reference Manual — Aggregate Functions](https://dev.mysql.com/doc/refman/en/aggregate-functions.html)
14. [SQLite Documentation — Aggregate Functions](https://www.sqlite.org/lang_aggfunc.html)
