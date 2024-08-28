# ORM (Object-Relational Mapping)
Is a technique that allows working with databases through objects without writing SQL queries directly. ORM automatically maps database tables to objects in the code.

### Key Points:

- **SQL Abstraction:** Allows performing CRUD operations using objects instead of SQL.
- **Mapping Tables to Objects:** Database tables map to classes, rows to objects.
- **Compatibility:** Easily switch between different databases (MySQL, PostgreSQL, etc.).
- **Popular ORMs:** SQLAlchemy, Django ORM, Hibernate, Sequelize.

### Benefits:
- Simplifies database interaction.
- Increases security (protection from SQL injections).
- Speeds up development.

However, it may be less efficient for complex queries compared to direct SQL.


# TEAMWORK 

1. Read about SQL, learn insert, delete, update, select on this page  https://sqliteonline.com/

   Download dbBrowser for sqlite  https://sqlitebrowser.org/dl/

   A lot of resources is here https://www.w3schools.com/sql/default.asp

2. Create 3 tables with some non-complex data, populate them with values, you will be able to use this database later on, but this is just for you to practise and understand db a bit better.

3. Try to open the database that you created in your project (you can see the my.db in files on the left side)



## SQL: insert, delete, update, select: 

1. `INSERT`: This statement is used to add new rows to a table.
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```

2. `UPDATE`: This command modifies existing data in a table.
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

3. `DELETE`: Removes data from a table.
```sql
DELETE FROM table_name
WHERE condition;
```

4. `SELECT`: Retrieves data from a database.

```sql
SELECT * FROM table_name;
```

To retrieve specific data with a condition:
```sql
SELECT * FROM Customers WHERE City = 'New York';
```


## Create 3 tables with some non-complex data, populate them with values 

1. CUSTOMERS TABLE

This table stores customer details.
```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(100),
    City VARCHAR(50),
    Email VARCHAR(100)
);

INSERT INTO Customers (CustomerID, CustomerName, City, Email) 
VALUES
(1, 'John Doe', 'New York', 'john@example.com'),
(2, 'Jane Smith', 'Los Angeles', 'jane@example.com'),
(3, 'Emily Davis', 'Chicago', 'emily@example.com');
```

2. PRUDCTION TABLE

This table stores product details.
```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(100),
    Price DECIMAL(10, 2)
);

INSERT INTO Products (ProductID, ProductName, Price)
VALUES
(1, 'Laptop', 999.99),
(2, 'Smartphone', 599.99),
(3, 'Tablet', 299.99);
```

3. ORDERS TABLE

This table stores order details and relates to both Customers and Products.

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    ProductID INT,
    OrderDate DATE,
    Quantity INT,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);

INSERT INTO Orders (OrderID, CustomerID, ProductID, OrderDate, Quantity)
VALUES
(1, 1, 1, '2024-08-28', 1),
(2, 2, 2, '2024-08-27', 2),
(3, 3, 3, '2024-08-26', 1);
```


## Examples with the tables with using INSERT, UPDATE, DELETE, and SELECT functions:

1. `INSERT`

Adding a new customer and a new order.

```sql
INSERT INTO Customers (CustomerID, CustomerName, City, Email) 
VALUES (5, 'Michael Johnson', 'Houston', 'michael@example.com');

INSERT INTO Orders (OrderID, CustomerID, ProductID, OrderDate, Quantity) 
VALUES (5, 4, 2, '2024-08-29', 1);
```

2. `UPDATE`

Updating a product's price and changing a customer’s city.
```sql
UPDATE Products
SET Price = 1099.99
WHERE ProductID = 1;

UPDATE Customers
SET City = 'San Francisco'
WHERE CustomerID = 1;
```

3. `DELETE`

Removing a customer and deleting their corresponding order.

```sql
DELETE FROM Customers
WHERE CustomerID = 3;

DELETE FROM Orders
WHERE CustomerID = 3;
```

4. `SELECT`

Fetching information from multiple tables using JOIN.

```sql
SELECT Customers.CustomerName, Products.ProductName, Orders.Quantity, Orders.OrderDate
FROM Orders
JOIN Customers ON Orders.CustomerID = Customers.CustomerID
JOIN Products ON Orders.ProductID = Products.ProductID;
```

## OPEN DataBase in INTELLiJ IDEA:

1. Open the Database Tool Window: Go to View > Tool Windows > Database.
2. Add Data Source:
3. Click the + button to add a new data source.
4. Select SQLite.
5. In the "File" field, browse to your my.db file.
   
View Tables: You can now explore the structure and data in your database directly within IntelliJ.

<img width="1321" alt="Screenshot 2024-08-28 at 23 52 16" src="https://github.com/user-attachments/assets/af3a3656-a5de-4506-871a-12e6f621a926">

