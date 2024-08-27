# TEAMWORK
# Explore different filters and their combinations with SQL

1. Use our Pet clinics files
2. Use online free SQLight platform https://sqliteonline.com/

https://www.sqlite.org/optoverview.html

```sql
SELECT * FROM Pets WHERE LENGTH(Name) = 5;
SELECT * FROM Pets WHERE Name LIKE '%er';
SELECT DISTINCT Kind FROM Pets;
```

## SQLite Filtering Methods (Summary):

1. `WHERE` – Basic filtering.
- Equality/Inequality: =, !=
- Comparisons: >, <, >=, <=
2. `LIKE` – Pattern matching.
- Starts with: LIKE 'S%'
- Ends with: LIKE '%a'
- Contains: LIKE '%abc%'
3. `IN` – Matches a value from a list.
```sql
WHERE column_name IN ('value1', 'value2')
```
4. `BETWEEN` – Filters within a range.
```sql
WHERE column_name BETWEEN 10 AND 20
```
5. `IS NULL/IS NOT NULL` – Filters NULL values.
```sql
WHERE column_name IS NULL
```
7. `NOT` – Negates conditions.
```sql
WHERE column_name NOT LIKE 'S%'
```
8. `AND / OR` – Combines conditions.
```sql
WHERE condition1 AND condition2
```
9. `EXISTS` – Checks if a subquery returns rows.
```sql
WHERE EXISTS (subquery)
```
10. `GLOB` – Advanced pattern matching.
```sql
WHERE column_name GLOB 'S*'
```
11. `LIMIT` – Limits the number of results.
```sql
SELECT * FROM table LIMIT 5
```
12. **Aggregates +** `HAVING` – Filtering grouped data.
```sql
HAVING COUNT(*) > 10
```












