# SQLite JOIN - Overview

SQL JOIN is used to combine rows from two or more tables based on a related column between them. There are several types of JOINs, each serving different purposes.


1. `INNER JOIN`: Returns only the rows that have matching values in both tables.
```sql
SELECT employees.name, departments.department_name
FROM employees
INNER JOIN departments ON employees.department_id = departments.department_id;
```

2. `LEFT JOIN`: Returns all rows from the left table, and the matching rows from the right table. If there's no match, NULL is returned.
```sql
SELECT employees.name, departments.department_name
FROM employees
LEFT JOIN departments ON employees.department_id = departments.department_id;
```

3. `RIGHT JOIN`: Returns all rows from the right table, and the matching rows from the left table. If there's no match, NULL is returned.
```sql
SELECT employees.name, departments.department_name
FROM employees
RIGHT JOIN departments ON employees.department_id = departments.department_id;
```

4. `FULL OUTER JOIN`: Returns all rows when there is a match in either table. If no match, NULL is returned for missing columns.
```sql
SELECT employees.name, departments.department_name
FROM employees
FULL OUTER JOIN departments ON employees.department_id = departments.department_id;
```

5. `CROSS JOIN`: Returns the Cartesian product of both tables (all possible combinations of rows).
```sql
SELECT employees.name, departments.department_name
FROM employees
CROSS JOIN departments;
```

6. `SELF JOIN`: Joins a table with itself. Useful for hierarchical or relational data within the same table.
```sql
SELECT e1.name AS employee, e2.name AS manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.employee_id;
```
 
## Key Points:

- INNER JOIN: Matches in both tables.

- LEFT JOIN: All from the left, matches from the right.

- RIGHT JOIN: All from the right, matches from the left.

- FULL OUTER JOIN: All records from both sides.

- CROSS JOIN: All combinations.

- SELF JOIN: Table joins itself.



# TEAMWORK
1. Calculate total Sales by City
```sql
SELECT Owners.City, SUM(Procedures.Price) AS total_sales
FROM Sales
JOIN Pets ON Sales.PetID = Pets.PetID
JOIN Owners ON Pets.OwnerID = Owners.OwnerID
JOIN Procedures ON Sales.ProcedureCode = Procedures.ProcedureCode
GROUP BY Owners.City
ORDER BY total_sales DESC;
```

2. Calculate total Sales by Pet Kind
```sql
SELECT Pets.Kind, SUM(Procedures.Price) AS total_sales
FROM Sales
JOIN Pets ON Sales.PetID = Pets.PetID
JOIN Procedures ON Sales.ProcedureCode = Procedures.ProcedureCode
GROUP BY Pets.Kind;
```

3. Calculate total Sales by City and Pet Kind
```sql
SELECT Owners.City, Pets.Kind, SUM(Procedures.Price) AS total_sales
FROM Sales
JOIN Pets ON Sales.PetID = Pets.PetID
JOIN Owners ON Pets.OwnerID = Owners.OwnerID
JOIN Procedures ON Sales.ProcedureCode = Procedures.ProcedureCode
GROUP BY Owners.City, Pets.Kind;
```

4. Calculate Average Sales by City
```sql
SELECT Owners.City, AVG(Procedures.Price) AS average_sales
FROM Sales
JOIN Pets ON Sales.PetID = Pets.PetID
JOIN Owners ON Pets.OwnerID = Owners.OwnerID
JOIN Procedures ON Sales.ProcedureCode = Procedures.ProcedureCode
GROUP BY Owners.City;
```





