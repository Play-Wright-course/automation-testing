# Data Query Language (DQL) – Part 3: Aggregations

In this section, we will learn about **aggregate functions** in SQL: COUNT, SUM, AVG, GROUP BY, and HAVING.

---

## Sample Table: Orders

| OrderID | Customer   | Product     | Quantity | Price | OrderDate  |
|---------|------------|-------------|----------|-------|------------|
| 1       | Amit       | Laptop      | 1        | 60000 | 2023-01-15 |
| 2       | Riya       | Phone       | 2        | 20000 | 2023-01-20 |
| 3       | Neha       | Laptop      | 1        | 60000 | 2023-02-05 |
| 4       | Arjun      | Tablet      | 3        | 15000 | 2023-02-10 |
| 5       | Priya      | Phone       | 1        | 20000 | 2023-02-18 |
| 6       | Amit       | Tablet      | 2        | 15000 | 2023-03-01 |
| 7       | Riya       | Laptop      | 1        | 60000 | 2023-03-12 |
| 8       | Priya      | Phone       | 3        | 20000 | 2023-03-25 |
| 9       | Arjun      | Laptop      | 2        | 60000 | 2023-04-02 |

---

## 1. COUNT – Number of Records
```sql
SELECT COUNT(*) AS TotalOrders
FROM Orders;
```
**Output**
| TotalOrders |
|-------------|
| 9           |

---

## 2. SUM – Total Value
```sql
SELECT SUM(Price * Quantity) AS TotalRevenue
FROM Orders;
```
**Output**
| TotalRevenue |
|--------------|
| 310000       |

---

## 3. AVG – Average Value
```sql
SELECT AVG(Price) AS AvgPrice
FROM Orders;
```
**Output**
| AvgPrice |
|----------|
| 30000    |

---

## 4. GROUP BY – Aggregate Per Customer
```sql
SELECT Customer, COUNT(OrderID) AS OrdersPlaced
FROM Orders
GROUP BY Customer;
```
**Output**
| Customer | OrdersPlaced |
|----------|--------------|
| Amit     | 2            |
| Riya     | 2            |
| Neha     | 1            |
| Arjun    | 2            |
| Priya    | 2            |

---

## 5. GROUP BY with SUM
```sql
SELECT Product, SUM(Quantity) AS TotalSold
FROM Orders
GROUP BY Product;
```
**Output**
| Product | TotalSold |
|---------|-----------|
| Laptop  | 4         |
| Phone   | 6         |
| Tablet  | 5         |

---

## 6. HAVING – Filter Groups
```sql
SELECT Customer, SUM(Price * Quantity) AS TotalSpent
FROM Orders
GROUP BY Customer
HAVING SUM(Price * Quantity) > 50000;
```
**Output**
| Customer | TotalSpent |
|----------|------------|
| Amit     | 90000      |
| Riya     | 100000     |
| Arjun    | 150000     |

---

## 7. Complex Example 1 – Multiple Aggregates
```sql
SELECT Customer,
       COUNT(OrderID) AS OrdersCount,
       SUM(Price * Quantity) AS TotalSpent,
       AVG(Price) AS AvgProductPrice
FROM Orders
GROUP BY Customer;
```
**Output**
| Customer | OrdersCount | TotalSpent | AvgProductPrice |
|----------|-------------|------------|-----------------|
| Amit     | 2           | 90000      | 37500           |
| Riya     | 2           | 100000     | 40000           |
| Neha     | 1           | 60000      | 60000           |
| Arjun    | 2           | 150000     | 37500           |
| Priya    | 2           | 80000      | 20000           |

---

## 8. Complex Example 2 – Aggregation with Date Filtering
```sql
SELECT Product,
       SUM(Quantity) AS SoldInFeb,
       SUM(Price * Quantity) AS RevenueInFeb
FROM Orders
WHERE OrderDate BETWEEN '2023-02-01' AND '2023-02-28'
GROUP BY Product;
```
**Output**
| Product | SoldInFeb | RevenueInFeb |
|---------|-----------|--------------|
| Laptop  | 1         | 60000        |
| Tablet  | 3         | 45000        |
| Phone   | 1         | 20000        |

---

✅ In this part, we covered:
- `COUNT` → Number of rows  
- `SUM` → Total values  
- `AVG` → Average values  
- `GROUP BY` → Aggregates per group  
- `HAVING` → Filter groups based on aggregate condition  
- **Complex Queries** → Multiple aggregates + filtering by date  
