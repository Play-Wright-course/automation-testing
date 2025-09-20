# Basic SQL Practice with Explanations

This file contains **20 SQL practice problems** covering:
- SELECT, FROM, WHERE
- ORDER BY
- DISTINCT
- LIMIT / TOP / ROWNUM

Each question includes:
- Input Table(s)
- Question
- SQL Query
- Explanation
- Output Table

---

## 1. SELECT, FROM, WHERE

### Q1: Fetch employees from department `HR`
**Input Table: employees**
| emp_id | name    | dept  | salary |
|--------|---------|-------|--------|
| 1      | Alice   | HR    | 50000  |
| 2      | Bob     | IT    | 60000  |
| 3      | Charlie | HR    | 55000  |
| 4      | David   | Sales | 45000  |

**Query:**
```sql
SELECT emp_id, name, dept, salary
FROM employees
WHERE dept = 'HR';
```

**Explanation:**
We used `WHERE dept = 'HR'` to filter only HR employees.

**Output:**
| emp_id | name    | dept | salary |
|--------|---------|------|--------|
| 1      | Alice   | HR   | 50000  |
| 3      | Charlie | HR   | 55000  |

---

### Q2: Fetch employees earning more than 55,000
**Query:**
```sql
SELECT name, salary
FROM employees
WHERE salary > 55000;
```

**Explanation:**
`>` operator filters salaries above 55,000.

**Output:**
| name | salary |
|------|--------|
| Bob  | 60000  |

---

### Q3: Employees from IT or Sales department
**Query:**
```sql
SELECT * 
FROM employees
WHERE dept IN ('IT', 'Sales');
```

**Explanation:**
The `IN` operator checks if dept is one of the listed values.

**Output:**
| emp_id | name  | dept  | salary |
|--------|-------|-------|--------|
| 2      | Bob   | IT    | 60000  |
| 4      | David | Sales | 45000  |

---

### Q4: Employees not in HR
**Query:**
```sql
SELECT name, dept
FROM employees
WHERE dept <> 'HR';
```

**Explanation:**
`<>` means NOT EQUAL.

**Output:**
| name  | dept  |
|-------|-------|
| Bob   | IT    |
| David | Sales |

---

### Q5: Fetch employee with emp_id = 2
**Query:**
```sql
SELECT * 
FROM employees
WHERE emp_id = 2;
```

**Explanation:**
Simple filter on primary key.

**Output:**
| emp_id | name | dept | salary |
|--------|------|------|--------|
| 2      | Bob  | IT   | 60000  |

---

## 2. ORDER BY

### Q6: Sort employees by salary ascending
**Query:**
```sql
SELECT name, salary
FROM employees
ORDER BY salary ASC;
```

**Explanation:**
Default is ascending. Employees ordered by lowest salary first.

**Output:**
| name    | salary |
|---------|--------|
| David   | 45000  |
| Alice   | 50000  |
| Charlie | 55000  |
| Bob     | 60000  |

---

### Q7: Sort employees by salary descending
**Query:**
```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC;
```

**Explanation:**
`DESC` shows highest salary first.

**Output:**
| name    | salary |
|---------|--------|
| Bob     | 60000  |
| Charlie | 55000  |
| Alice   | 50000  |
| David   | 45000  |

---

### Q8: Sort employees by department, then salary
**Query:**
```sql
SELECT name, dept, salary
FROM employees
ORDER BY dept ASC, salary DESC;
```

**Explanation:**
First sort alphabetically by dept, then within dept sort by salary high-to-low.

**Output:**
| name    | dept  | salary |
|---------|-------|--------|
| Alice   | HR    | 50000  |
| Charlie | HR    | 55000  |
| Bob     | IT    | 60000  |
| David   | Sales | 45000  |

---

### Q9: Sort by name alphabetically
**Query:**
```sql
SELECT * 
FROM employees
ORDER BY name;
```

**Explanation:**
Alphabetical sort on `name` column.

**Output:**
| emp_id | name    | dept  | salary |
|--------|---------|-------|--------|
| 1      | Alice   | HR    | 50000  |
| 2      | Bob     | IT    | 60000  |
| 3      | Charlie | HR    | 55000  |
| 4      | David   | Sales | 45000  |

---

### Q10: Sort by length of name
**Query:**
```sql
SELECT name, LENGTH(name) AS name_length
FROM employees
ORDER BY name_length;
```

**Explanation:**
We calculated length of name, then ordered by it.

**Output:**
| name    | name_length |
|---------|-------------|
| Bob     | 3           |
| Alice   | 5           |
| David   | 5           |
| Charlie | 7           |

---

## 3. DISTINCT

### Q11: List unique departments
**Query:**
```sql
SELECT DISTINCT dept
FROM employees;
```

**Explanation:**
Removes duplicate department names.

**Output:**
| dept  |
|-------|
| HR    |
| IT    |
| Sales |

---

### Q12: Unique salary values
**Query:**
```sql
SELECT DISTINCT salary
FROM employees;
```

**Explanation:**
Shows only unique salary numbers.

**Output:**
| salary |
|--------|
| 50000  |
| 60000  |
| 55000  |
| 45000  |

---

### Q13: Unique combinations of dept and salary
**Query:**
```sql
SELECT DISTINCT dept, salary
FROM employees;
```

**Explanation:**
Checks uniqueness across multiple columns.

**Output:**
| dept  | salary |
|-------|--------|
| HR    | 50000  |
| HR    | 55000  |
| IT    | 60000  |
| Sales | 45000  |

---

### Q14: Unique first letters of names
**Query:**
```sql
SELECT DISTINCT SUBSTR(name,1,1) AS first_letter
FROM employees;
```

**Explanation:**
Takes the first character from each name and removes duplicates.

**Output:**
| first_letter |
|--------------|
| A            |
| B            |
| C            |
| D            |

---

### Q15: Unique job roles (assume another column exists)
**Input Table with job column:**
| emp_id | name    | dept  | salary | job        |
|--------|---------|-------|--------|------------|
| 1      | Alice   | HR    | 50000  | Analyst    |
| 2      | Bob     | IT    | 60000  | Developer  |
| 3      | Charlie | HR    | 55000  | Analyst    |
| 4      | David   | Sales | 45000  | Sales Rep  |

**Query:**
```sql
SELECT DISTINCT job
FROM employees;
```

**Output:**
| job       |
|-----------|
| Analyst   |
| Developer |
| Sales Rep |

---

## 4. LIMIT / TOP / ROWNUM

### Q16: Get first 2 employees
**Query (MySQL/Postgres):**
```sql
SELECT * 
FROM employees
LIMIT 2;
```

**Explanation:**
Fetches only first 2 rows.

**Output:**
| emp_id | name  | dept | salary |
|--------|-------|------|--------|
| 1      | Alice | HR   | 50000  |
| 2      | Bob   | IT   | 60000  |

---

### Q17: Get top 1 highest salary employee (SQL Server)
**Query:**
```sql
SELECT TOP 1 name, salary
FROM employees
ORDER BY salary DESC;
```

**Explanation:**
SQL Server uses `TOP` instead of LIMIT.

**Output:**
| name | salary |
|------|--------|
| Bob  | 60000  |

---

### Q18: Get employees with ROWNUM <= 3 (Oracle)
**Query:**
```sql
SELECT * 
FROM employees
WHERE ROWNUM <= 3;
```

**Explanation:**
Oracle uses `ROWNUM` pseudo column.

**Output:**
| emp_id | name    | dept | salary |
|--------|---------|------|--------|
| 1      | Alice   | HR   | 50000  |
| 2      | Bob     | IT   | 60000  |
| 3      | Charlie | HR   | 55000  |

---

### Q19: Get top 2 employees by salary (Postgres)
**Query:**
```sql
SELECT name, salary
FROM employees
ORDER BY salary DESC
LIMIT 2;
```

**Explanation:**
Orders by salary then limits to 2.

**Output:**
| name    | salary |
|---------|--------|
| Bob     | 60000  |
| Charlie | 55000  |

---

### Q20: Skip first 1 row and fetch next 2 (OFFSET)
**Query (Postgres):**
```sql
SELECT name, salary
FROM employees
ORDER BY emp_id
OFFSET 1 ROWS FETCH NEXT 2 ROWS ONLY;
```

**Explanation:**
Skips first record and fetches next 2.

**Output:**
| name    | salary |
|---------|--------|
| Bob     | 60000  |
| Charlie | 55000  |
