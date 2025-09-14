# Data Query Language (DQL) – Part 4: Subqueries & CTE (WITH)

This part dives into **Subqueries** and **CTEs (Common Table Expressions)** with 6 core examples and 3 complex cases.  
Each example shows **input tables**, the **SQL query**, and the **expected output**.

---

## Sample Tables

### Employees
|   EmpID | Name        |   DeptID |   Salary |   ManagerID |
|--------:|:------------|---------:|---------:|------------:|
|     101 | Amit Sharma |        1 |    50000 |         nan |
|     102 | Riya Mehta  |        2 |    70000 |         101 |
|     103 | Arjun Rao   |        3 |    55000 |         101 |
|     104 | Neha Singh  |        2 |    80000 |         102 |
|     105 | Rohit Verma |        1 |    48000 |         101 |
|     106 | Priya Nair  |        2 |    65000 |         102 |

### Departments
|   DeptID | DeptName   |
|---------:|:-----------|
|        1 | HR         |
|        2 | IT         |
|        3 | Finance    |
|        4 | Marketing  |

### Orders
|   OrderID |   EmpID | Customer   | OrderDate   |
|----------:|--------:|:-----------|:------------|
|         1 |     102 | Acme       | 2023-01-10  |
|         2 |     104 | Bolt       | 2023-01-15  |
|         3 |     102 | Crown      | 2023-02-02  |
|         4 |     106 | Acme       | 2023-02-18  |
|         5 |     103 | Delta      | 2023-03-05  |
|         6 |     106 | Acme       | 2023-03-12  |

### OrderItems
|   OrderID | Product   |   Qty |   UnitPrice |
|----------:|:----------|------:|------------:|
|         1 | Laptop    |     1 |       60000 |
|         1 | Mouse     |     2 |        1000 |
|         2 | Tablet    |     3 |       15000 |
|         3 | Laptop    |     1 |       60000 |
|         3 | Phone     |     2 |       20000 |
|         4 | Phone     |     1 |       20000 |
|         5 | Laptop    |     1 |       60000 |
|         6 | Mouse     |     5 |        1000 |

---

## 1) Scalar Subquery – Employees earning above company average
```sql
SELECT EmpID, Name, Salary
FROM Employees
WHERE Salary > (SELECT AVG(Salary) FROM Employees)
ORDER BY Salary DESC;
```
**Output**
|   EmpID | Name       |   Salary |
|--------:|:-----------|---------:|
|     104 | Neha Singh |    80000 |
|     102 | Riya Mehta |    70000 |
|     106 | Priya Nair |    65000 |

---

## 2) IN Subquery – Employees in departments having more than 1 employee
```sql
SELECT e.EmpID, e.Name, e.DeptID, d.DeptName
FROM Employees e
JOIN Departments d ON e.DeptID = d.DeptID
WHERE e.DeptID IN (
  SELECT DeptID
  FROM Employees
  GROUP BY DeptID
  HAVING COUNT(*) > 1
)
ORDER BY e.DeptID, e.Name;
```
**Output**
|   EmpID | Name        |   DeptID | DeptName   |
|--------:|:------------|---------:|:-----------|
|     101 | Amit Sharma |        1 | HR         |
|     105 | Rohit Verma |        1 | HR         |
|     104 | Neha Singh  |        2 | IT         |
|     106 | Priya Nair  |        2 | IT         |
|     102 | Riya Mehta  |        2 | IT         |

---

## 3) EXISTS (Correlated) – Employees who have placed at least one order
```sql
SELECT e.EmpID, e.Name
FROM Employees e
WHERE EXISTS (
  SELECT 1
  FROM Orders o
  WHERE o.EmpID = e.EmpID
)
ORDER BY e.EmpID;
```
**Output**
|   EmpID | Name       |
|--------:|:-----------|
|     102 | Riya Mehta |
|     103 | Arjun Rao  |
|     104 | Neha Singh |
|     106 | Priya Nair |

---

## 4) NOT EXISTS – Departments with no employees
```sql
SELECT d.DeptID, d.DeptName
FROM Departments d
WHERE NOT EXISTS (
  SELECT 1
  FROM Employees e
  WHERE e.DeptID = d.DeptID
)
ORDER BY d.DeptID;
```
**Output**
|   DeptID | DeptName   |
|---------:|:-----------|
|        4 | Marketing  |

---

## 5) Subquery in FROM (Derived Table) – Revenue by product
```sql
SELECT t.Product, t.TotalRevenue
FROM (
  SELECT oi.Product,
         SUM(oi.Qty * oi.UnitPrice) AS TotalRevenue
  FROM OrderItems oi
  GROUP BY oi.Product
) AS t
ORDER BY t.TotalRevenue DESC;
```
**Output**
| Product   |   TotalRevenue |
|:----------|---------------:|
| Laptop    |         180000 |
| Phone     |          60000 |
| Tablet    |          45000 |
| Mouse     |           7000 |

---

## 6) ANY/ALL – Salary greater than ALL salaries in HR
```sql
SELECT Name, Salary
FROM Employees
WHERE Salary > ALL (
  SELECT Salary FROM Employees WHERE DeptID = 1
)
ORDER BY Salary DESC;
```
**Output**
| Name       |   Salary |
|:-----------|---------:|
| Neha Singh |    80000 |
| Riya Mehta |    70000 |
| Priya Nair |    65000 |
| Arjun Rao  |    55000 |

---

# CTEs (WITH clause)

## 7) CTE – Revenue per employee
```sql
WITH OrderTotals AS (
  SELECT oi.OrderID, SUM(oi.Qty * oi.UnitPrice) AS OrderTotal
  FROM OrderItems oi
  GROUP BY oi.OrderID
)
SELECT e.Name, SUM(ot.OrderTotal) AS Revenue
FROM Orders o
JOIN OrderTotals ot ON o.OrderID = ot.OrderID
JOIN Employees e ON o.EmpID = e.EmpID
GROUP BY e.Name
ORDER BY Revenue DESC;
```
**Output**
| Name       |   Revenue |
|:-----------|----------:|
| Riya Mehta |    162000 |
| Arjun Rao  |     60000 |
| Neha Singh |     45000 |
| Priya Nair |     25000 |

---

## 8) Multiple CTEs – Per-customer orders & revenue
```sql
WITH OrderTotals AS (
  SELECT oi.OrderID, SUM(oi.Qty * oi.UnitPrice) AS OrderTotal
  FROM OrderItems oi
  GROUP BY oi.OrderID
),
CustomerOrders AS (
  SELECT o.Customer, o.OrderID, ot.OrderTotal
  FROM Orders o
  JOIN OrderTotals ot ON o.OrderID = ot.OrderID
)
SELECT Customer,
       COUNT(DISTINCT OrderID) AS Orders,
       SUM(OrderTotal)         AS Revenue
FROM CustomerOrders
GROUP BY Customer
ORDER BY Revenue DESC;
```
**Output**
| Customer   |   Orders |   Revenue |
|:-----------|---------:|----------:|
| Crown      |        1 |    100000 |
| Acme       |        3 |     87000 |
| Delta      |        1 |     60000 |
| Bolt       |        1 |     45000 |

---

## 9) Recursive CTE – Organization levels
```sql
WITH RECURSIVE Org AS (
  SELECT EmpID, Name, ManagerID, 0 AS Level
  FROM Employees
  WHERE ManagerID IS NULL
  UNION ALL
  SELECT e.EmpID, e.Name, e.ManagerID, o.Level + 1
  FROM Employees e
  JOIN Org o ON e.ManagerID = o.EmpID
)
SELECT EmpID, Name, Level
FROM Org
ORDER BY Level, EmpID;
```
**Output**
|   EmpID | Name        |   Level |
|--------:|:------------|--------:|
|     101 | Amit Sharma |       0 |
|     102 | Riya Mehta  |       1 |
|     103 | Arjun Rao   |       1 |
|     105 | Rohit Verma |       1 |
|     104 | Neha Singh  |       2 |
|     106 | Priya Nair  |       2 |

---

# Complex Examples

## Complex A) Top 2 earners per department (CTE + window function)
```sql
WITH Ranked AS (
  SELECT d.DeptName, e.Name, e.Salary,
         ROW_NUMBER() OVER (PARTITION BY e.DeptID ORDER BY e.Salary DESC) AS rn
  FROM Employees e
  LEFT JOIN Departments d ON e.DeptID = d.DeptID
)
SELECT DeptName, Name, Salary, rn AS Rank
FROM Ranked
WHERE rn <= 2
ORDER BY DeptName, Rank, Name;
```
**Output**
| DeptName   | Name        |   Salary |   Rank |
|:-----------|:------------|---------:|-------:|
| Finance    | Arjun Rao   |    55000 |      1 |
| HR         | Amit Sharma |    50000 |      1 |
| HR         | Rohit Verma |    48000 |      2 |
| IT         | Neha Singh  |    80000 |      1 |
| IT         | Riya Mehta  |    70000 |      2 |

---

## Complex B) Highest revenue product per customer (CTE + ranking)
```sql
WITH CustProd AS (
  SELECT o.Customer, oi.Product,
         SUM(oi.Qty * oi.UnitPrice) AS Revenue
  FROM Orders o
  JOIN OrderItems oi ON o.OrderID = oi.OrderID
  GROUP BY o.Customer, oi.Product
),
Ranked AS (
  SELECT Customer, Product, Revenue,
         ROW_NUMBER() OVER (PARTITION BY Customer ORDER BY Revenue DESC) AS rk
  FROM CustProd
)
SELECT Customer, Product, Revenue
FROM Ranked
WHERE rk = 1
ORDER BY Customer;
```
**Output**
| Customer   | Product   |   Revenue |
|:-----------|:----------|----------:|
| Acme       | Laptop    |     60000 |
| Bolt       | Tablet    |     45000 |
| Crown      | Laptop    |     60000 |
| Delta      | Laptop    |     60000 |

---

## Complex C) Manager → Employee pairs (recursive CTE for relationships)
```sql
WITH RECURSIVE Tree AS (
  SELECT EmpID, Name, ManagerID, CAST(Name AS VARCHAR(200)) AS Path
  FROM Employees
  WHERE ManagerID IS NULL
  UNION ALL
  SELECT e.EmpID, e.Name, e.ManagerID, CAST(t.Path || ' > ' || e.Name AS VARCHAR(200))
  FROM Employees e
  JOIN Tree t ON e.ManagerID = t.EmpID
)
SELECT * FROM Tree ORDER BY Path;
```
**Output**
| Manager     | Employee    |
|:------------|:------------|
| Amit Sharma | Arjun Rao   |
| Amit Sharma | Riya Mehta  |
| Amit Sharma | Rohit Verma |
| Riya Mehta  | Neha Singh  |
| Riya Mehta  | Priya Nair  |

---

✅ In this part, you learned:
- Scalar, IN, EXISTS/NOT EXISTS, ANY/ALL subqueries
- Derived tables (subquery in FROM)
- CTEs (single, multiple) and **recursive CTEs** for hierarchies
- Complex patterns using **window functions** + CTEs
