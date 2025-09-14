# Data Query Language (DQL) – Part 2: Joins

In this section, we will learn **INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN** with clear inputs and outputs.
We’ll use four sample tables: **Employees, Departments, Projects, EmployeeProject**.

---

## Sample Tables

### Employees
|   EmpID | Name        |   DeptID |
|--------:|:------------|---------:|
|     101 | Amit Sharma |        1 |
|     102 | Riya Mehta  |        2 |
|     103 | Arjun Rao   |        3 |
|     104 | Neha Singh  |        2 |
|     105 | Rohit Verma |      nan |
|     106 | Priya Nair  |        5 |

### Departments
|   DeptID | DeptName   |
|---------:|:-----------|
|        1 | HR         |
|        2 | IT         |
|        3 | Finance    |
|        4 | Marketing  |

### Projects
|   ProjID | ProjName        |   DeptID |
|---------:|:----------------|---------:|
|      201 | Portal Revamp   |        2 |
|      202 | Payroll Cleanup |        3 |
|      203 | Hiring Sprint   |        1 |
|      204 | Brand Campaign  |        4 |

### EmployeeProject (many-to-many + hours)
|   EmpID |   ProjID |   Hours |
|--------:|---------:|--------:|
|     101 |      203 |      20 |
|     102 |      201 |      40 |
|     104 |      201 |      35 |
|     103 |      202 |      25 |
|     105 |      204 |      10 |
|     106 |      201 |      15 |

---

## 1) INNER JOIN – Only matching rows in both tables
Get each employee’s department name (employees without department are excluded).

```sql
SELECT e.EmpID, e.Name, d.DeptName
FROM Employees e
INNER JOIN Departments d ON e.DeptID = d.DeptID
ORDER BY e.EmpID;
```

**Output**
|   EmpID | Name        | DeptName   |
|--------:|:------------|:-----------|
|     101 | Amit Sharma | HR         |
|     102 | Riya Mehta  | IT         |
|     103 | Arjun Rao   | Finance    |
|     104 | Neha Singh  | IT         |

---

## 2) LEFT JOIN – All rows from left (Employees), matched Departments if any
Shows all employees; missing departments appear as NULL.

```sql
SELECT e.EmpID, e.Name, d.DeptName
FROM Employees e
LEFT JOIN Departments d ON e.DeptID = d.DeptID
ORDER BY e.EmpID;
```

**Output**
|   EmpID | Name        | DeptName   |
|--------:|:------------|:-----------|
|     101 | Amit Sharma | HR         |
|     102 | Riya Mehta  | IT         |
|     103 | Arjun Rao   | Finance    |
|     104 | Neha Singh  | IT         |
|     105 | Rohit Verma | nan        |
|     106 | Priya Nair  | nan        |

---

## 3) RIGHT JOIN – All rows from right (Departments), matched Employees if any
Shows all departments; departments without employees show NULLs for employee columns.

```sql
SELECT d.DeptID, d.DeptName, e.EmpID, e.Name
FROM Employees e
RIGHT JOIN Departments d ON e.DeptID = d.DeptID
ORDER BY d.DeptID, e.EmpID;
```

**Output**
|   DeptID | DeptName   |   EmpID | Name        |
|---------:|:-----------|--------:|:------------|
|        1 | HR         |     101 | Amit Sharma |
|        2 | IT         |     102 | Riya Mehta  |
|        2 | IT         |     104 | Neha Singh  |
|        3 | Finance    |     103 | Arjun Rao   |
|        4 | Marketing  |     nan | nan         |

---

## 4) FULL OUTER JOIN – All rows from both sides
Includes employees without departments and departments without employees.

> Note: Some databases (e.g., MySQL) don’t support `FULL JOIN`. You can emulate it using `LEFT JOIN UNION RIGHT JOIN`.

```sql
-- Standard syntax (supported in SQL Server, PostgreSQL, etc.)
SELECT e.EmpID, e.Name, e.DeptID, d.DeptName
FROM Employees e
FULL OUTER JOIN Departments d ON e.DeptID = d.DeptID
ORDER BY e.DeptID, e.EmpID;

-- MySQL-compatible workaround
SELECT e.EmpID, e.Name, e.DeptID, d.DeptName
FROM Employees e
LEFT JOIN Departments d ON e.DeptID = d.DeptID
UNION
SELECT e.EmpID, e.Name, e.DeptID, d.DeptName
FROM Employees e
RIGHT JOIN Departments d ON e.DeptID = d.DeptID
ORDER BY DeptID, EmpID;
```

**Output**
|   EmpID | Name        |   DeptID | DeptName   |
|--------:|:------------|---------:|:-----------|
|     101 | Amit Sharma |        1 | HR         |
|     102 | Riya Mehta  |        2 | IT         |
|     104 | Neha Singh  |        2 | IT         |
|     103 | Arjun Rao   |        3 | Finance    |
|     nan | nan         |        4 | Marketing  |
|     106 | Priya Nair  |        5 | nan        |
|     105 | Rohit Verma |      nan | nan        |

---

## 5) INNER JOIN with filter + ordering
Employees in **IT** or **Finance**, sorted by department then name.

```sql
SELECT e.Name, d.DeptName, e.EmpID
FROM Employees e
INNER JOIN Departments d ON e.DeptID = d.DeptID
WHERE d.DeptName IN ('IT','Finance')
ORDER BY d.DeptName, e.Name;
```

**Output**
| Name       | DeptName   |   EmpID |
|:-----------|:-----------|--------:|
| Arjun Rao  | Finance    |     103 |
| Neha Singh | IT         |     104 |
| Riya Mehta | IT         |     102 |

---

# Complex Examples

## Complex A) Multi-join + Aggregation
Total hours and unique contributors per **project** and **department**.

```sql
SELECT d.DeptName,
       p.ProjName,
       SUM(ep.Hours)    AS TotalHours,
       COUNT(DISTINCT e.EmpID) AS Contributors
FROM EmployeeProject ep
JOIN Employees e   ON ep.EmpID = e.EmpID
JOIN Projects  p   ON ep.ProjID = p.ProjID
LEFT JOIN Departments d ON p.DeptID = d.DeptID
GROUP BY d.DeptName, p.ProjName
ORDER BY d.DeptName, p.ProjName;
```

**Output**
| DeptName   | ProjName        |   TotalHours |   Contributors |
|:-----------|:----------------|-------------:|---------------:|
| Finance    | Payroll Cleanup |           25 |              1 |
| HR         | Hiring Sprint   |           20 |              1 |
| IT         | Portal Revamp   |           90 |              3 |
| Marketing  | Brand Campaign  |           10 |              1 |

---

## Complex B) Self-join – Coworker pairs in the same department
List all unique **pairs of employees** who are in the same department (NULL departments excluded).

```sql
SELECT a.DeptID, a.Name AS EmployeeA, b.Name AS EmployeeB
FROM Employees a
JOIN Employees b ON a.DeptID = b.DeptID AND a.EmpID < b.EmpID
WHERE a.DeptID IS NOT NULL
ORDER BY a.DeptID, EmployeeA, EmployeeB;
```

**Output**
|   DeptID | EmployeeA   | EmployeeB   |
|---------:|:------------|:------------|
|        2 | Riya Mehta  | Neha Singh  |

---

✅ In this part, we covered:
- `INNER JOIN` → Only matching rows
- `LEFT JOIN` → All left rows + matches
- `RIGHT JOIN` → All right rows + matches
- `FULL JOIN` → All rows from both sides (with MySQL workaround)
- **Complex joins** → Multi-table joins with aggregation; Self-join for peer relationships
