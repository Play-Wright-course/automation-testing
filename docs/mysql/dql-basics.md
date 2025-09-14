# Data Query Language (DQL) – Part 1: Basics

In this section, we will learn the **basics of SELECT**: filtering, pattern matching, sorting, distinct values, and aliases.

---

## Sample Table: Employee

| EmpID | Name         | Department | Salary  | HireDate   |
|-------|--------------|------------|---------|------------|
| 101   | Amit Sharma  | HR         | 50000   | 2020-01-15 |
| 102   | Riya Mehta   | IT         | 65000   | 2021-03-22 |
| 103   | Arjun Rao    | Finance    | 55000   | 2019-07-09 |
| 104   | Neha Singh   | IT         | 75000   | 2022-05-01 |
| 105   | Rohit Verma  | HR         | 48000   | 2023-02-10 |
| 106   | Priya Nair   | IT         | 65000   | 2020-12-11 |

---

## 1. SELECT – Fetch All Columns
```sql
SELECT * FROM Employee;
```

**Output**
| EmpID | Name        | Department | Salary | HireDate   |
|-------|-------------|------------|--------|------------|
| 101   | Amit Sharma | HR         | 50000  | 2020-01-15 |
| 102   | Riya Mehta  | IT         | 65000  | 2021-03-22 |
| 103   | Arjun Rao   | Finance    | 55000  | 2019-07-09 |
| 104   | Neha Singh  | IT         | 75000  | 2022-05-01 |
| 105   | Rohit Verma | HR         | 48000  | 2023-02-10 |
| 106   | Priya Nair  | IT         | 65000  | 2020-12-11 |

---

## 2. WHERE – Filter Rows
```sql
SELECT Name, Department, Salary
FROM Employee
WHERE Department = 'IT';
```

**Output**
| Name       | Department | Salary |
|------------|------------|--------|
| Riya Mehta | IT         | 65000  |
| Neha Singh | IT         | 75000  |
| Priya Nair | IT         | 65000  |

---

## 3. LIKE – Pattern Matching

### a) Starts With Pattern
```sql
SELECT Name FROM Employee
WHERE Name LIKE 'R%';
```
**Output**
| Name        |
|-------------|
| Riya Mehta  |
| Rohit Verma |

---

### b) Ends With Pattern
```sql
SELECT Name FROM Employee
WHERE Name LIKE '%a';
```
**Output**
| Name       |
|------------|
| Riya Mehta |
| Priya Nair |

---

### c) Contains Substring
```sql
SELECT Name FROM Employee
WHERE Name LIKE '%Singh%';
```
**Output**
| Name       |
|------------|
| Neha Singh |

---

### d) Single Character Wildcard (_)
```sql
SELECT Name FROM Employee
WHERE Name LIKE '_mit%';
```
**Output**
| Name        |
|-------------|
| Amit Sharma |

---

### e) Combined Pattern
```sql
SELECT Name FROM Employee
WHERE Name LIKE 'R%a';
```
**Output**
| Name       |
|------------|
| Riya Mehta |
| Priya Nair |

---

## 4. ORDER BY – Sort Results
```sql
SELECT Name, Salary
FROM Employee
ORDER BY Salary DESC;
```

**Output**
| Name       | Salary |
|------------|--------|
| Neha Singh | 75000  |
| Riya Mehta | 65000  |
| Priya Nair | 65000  |
| Arjun Rao  | 55000  |
| Amit Sharma| 50000  |
| Rohit Verma| 48000  |

---

## 5. DISTINCT – Unique Values
```sql
SELECT DISTINCT Department
FROM Employee;
```

**Output**
| Department |
|------------|
| HR         |
| IT         |
| Finance    |

---

## 6. ALIASES – Renaming Columns
```sql
SELECT Name AS EmployeeName,
       Salary AS MonthlySalary
FROM Employee;
```

**Output**
| EmployeeName | MonthlySalary |
|--------------|---------------|
| Amit Sharma  | 50000         |
| Riya Mehta   | 65000         |
| Arjun Rao    | 55000         |
| Neha Singh   | 75000         |
| Rohit Verma  | 48000         |
| Priya Nair   | 65000         |

---

✅ In this part, we covered:
- `SELECT *` → Fetch all columns  
- `WHERE` → Filter rows  
- `LIKE` → Pattern matching (starts, ends, contains, single char, combined)  
- `ORDER BY` → Sort results  
- `DISTINCT` → Get unique values  
- `ALIASES` → Rename output columns  

Next: **Part 2 (Joins)** – Learn INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN with multiple tables.
