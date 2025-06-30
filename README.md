# SQL_task5

-- DROP TABLES IF THEY EXIST (to avoid errors on re-run)
DROP TABLE IF EXISTS Orders;
DROP TABLE IF EXISTS Customers;

-- 1. Create Customers table
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(50)
);

-- 2. Create Orders table
CREATE TABLE Orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    amount DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES Customers(customer_id)
);

-- 3. Insert sample data into Customers
INSERT INTO Customers (customer_id, name, city) VALUES
(1, 'Alice', 'New York'),
(2, 'Bob', 'Chicago'),
(3, 'Charlie', 'Los Angeles'),
(4, 'David', 'Houston');

-- 4. Insert sample data into Orders
INSERT INTO Orders (order_id, customer_id, order_date, amount) VALUES
(101, 1, '2024-06-01', 250.00),
(102, 1, '2024-06-05', 180.00),
(103, 2, '2024-06-10', 340.00),
(104, 5, '2024-06-15', 90.00);  -- This order references a non-existing customer

-- 5. INNER JOIN - Only matching records
SELECT c.name AS customer_name, o.order_id, o.amount
FROM Customers c
INNER JOIN Orders o ON c.customer_id = o.customer_id;

-- 6. LEFT JOIN - All customers, even if no orders
SELECT c.name AS customer_name, o.order_id, o.amount
FROM Customers c
LEFT JOIN Orders o ON c.customer_id = o.customer_id;

-- 7. RIGHT JOIN - All orders, even if customer doesn't exist
SELECT c.name AS customer_name, o.order_id, o.amount
FROM Customers c
RIGHT JOIN Orders o ON c.customer_id = o.customer_id;

-- 8. FULL JOIN - All customers and orders, matched and unmatched
SELECT c.name AS customer_name, o.order_id, o.amount
FROM Customers c
FULL JOIN Orders o ON c.customer_id = o.customer_id;
