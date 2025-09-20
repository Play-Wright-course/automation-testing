# SQL Practice: Joins with Explanations

This file contains **20 SQL practice problems** covering:

* INNER JOIN
* LEFT JOIN
* RIGHT JOIN
* FULL OUTER JOIN
* SELF JOIN

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. INNER JOIN

### Q1: Employees with their department names

**Input Tables:**
**employees**

| emp\_id | name    | dept\_id |
| ------- | ------- | -------- |
| 1       | Alice   | 10       |
| 2       | Bob     | 20       |
| 3       | Charlie | 30       |

**departments**

| dept\_id | dept\_name |
| -------- | ---------- |
| 10       | HR         |
| 20       | IT         |
| 30       | Sales      |
| 40       | Marketing  |

**Query:**

```sql
SELECT e.emp_id, e.name, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```

**Explanation:**
INNER JOIN returns rows where there is a match in both tables.

**Output:**

| emp\_id | name    | dept\_name |
| ------- | ------- | ---------- |
| 1       | Alice   | HR         |
| 2       | Bob     | IT         |
| 3       | Charlie | Sales      |

---

### Q2: Employees with salary > 50000 and their departments

**Input Table: salaries**

| emp\_id | salary |
| ------- | ------ |
| 1       | 50000  |
| 2       | 60000  |
| 3       | 55000  |

```sql
SELECT e.name, s.salary, d.dept_name
FROM employees e
INNER JOIN salaries s ON e.emp_id = s.emp_id
INNER JOIN departments d ON e.dept_id = d.dept_id
WHERE s.salary > 50000;
```

**Output:**

| name    | salary | dept\_name |
| ------- | ------ | ---------- |
| Bob     | 60000  | IT         |
| Charlie | 55000  | Sales      |

---

### Q3: Employees who have a project assigned

**Input Table: projects**

| project\_id | emp\_id | project\_name |
| ----------- | ------- | ------------- |
| 101         | 1       | Alpha         |
| 102         | 3       | Beta          |

```sql
SELECT e.name, p.project_name
FROM employees e
INNER JOIN projects p ON e.emp_id = p.emp_id;
```

**Output:**

| name    | project\_name |
| ------- | ------------- |
| Alice   | Alpha         |
| Charlie | Beta          |

---

### Q4: Employees with matching departments (example with missing dept)

**Input Table:**
employees same as above, departments without dept\_id 30

| dept\_id | dept\_name |
| -------- | ---------- |
| 10       | HR         |
| 20       | IT         |
| 40       | Marketing  |

```sql
SELECT e.name, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```

**Output:**

| name  | dept\_name |
| ----- | ---------- |
| Alice | HR         |
| Bob   | IT         |

---

### Q5: Inner join on multiple conditions

**Input Table: employee\_projects**

| emp\_id | project\_id | role      |
| ------- | ----------- | --------- |
| 1       | 101         | Developer |
| 2       | 102         | Manager   |

```sql
SELECT e.name, ep.role, p.project_name
FROM employees e
INNER JOIN employee_projects ep ON e.emp_id = ep.emp_id
INNER JOIN projects p ON ep.project_id = p.project_id;
```

**Output:**

| name  | role      | project\_name |
| ----- | --------- | ------------- |
| Alice | Developer | Alpha         |
| Bob   | Manager   | Beta          |

---

## 2. LEFT JOIN

### Q6: All employees and their departments (include those without dept)

**Input Tables:** employees and departments

```sql
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id;
```

**Explanation:**
LEFT JOIN returns all rows from left table (employees), NULL if no match in right table.

**Output:**

| name    | dept\_name |
| ------- | ---------- |
| Alice   | HR         |
| Bob     | IT         |
| Charlie | Sales      |

---

### Q7: Employees with projects (include those without projects)

**Query:**

```sql
SELECT e.name, p.project_name
FROM employees e
LEFT JOIN projects p ON e.emp_id = p.emp_id;
```

**Output:**

| name    | project\_name |
| ------- | ------------- |
| Alice   | Alpha         |
| Bob     | NULL          |
| Charlie | Beta          |

---

### Q8: Left join with condition

```sql
SELECT e.name, s.salary
FROM employees e
LEFT JOIN salaries s ON e.emp_id = s.emp_id
WHERE s.salary > 50000 OR s.salary IS NULL;
```

**Output:**

| name    | salary |
| ------- | ------ |
| Alice   | 50000  |
| Bob     | 60000  |
| Charlie | 55000  |

---

### Q9: Left join multiple tables

```sql
SELECT e.name, d.dept_name, p.project_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id
LEFT JOIN projects p ON e.emp_id = p.emp_id;
```

**Output:**

| name    | dept\_name | project\_name |
| ------- | ---------- | ------------- |
| Alice   | HR         | Alpha         |
| Bob     | IT         | NULL          |
| Charlie | Sales      | Beta          |

---

### Q10: Left join with filtering

```sql
SELECT e.name, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id
WHERE d.dept_name IS NULL;
```

**Output:**

| name                  | dept\_name |
| --------------------- | ---------- |
| (none if all matched) |            |

---

## 3. RIGHT JOIN

### Q11: All departments and employees (include depts without employees)

```sql
SELECT e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.dept_id;
```

**Output:**

| name    | dept\_name |
| ------- | ---------- |
| Alice   | HR         |
| Bob     | IT         |
| Charlie | Sales      |
| NULL    | Marketing  |

---

### Q12: Right join with projects

```sql
SELECT e.name, p.project_name
FROM employees e
RIGHT JOIN projects p ON e.emp_id = p.emp_id;
```

**Output:**

| name    | project\_name |
| ------- | ------------- |
| Alice   | Alpha         |
| Charlie | Beta          |

---

### Q13: Right join multiple tables

```sql
SELECT e.name, s.salary, d.dept_name
FROM employees e
RIGHT JOIN salaries s ON e.emp_id = s.emp_id
RIGHT JOIN departments d ON e.dept_id = d.dept_id;
```

**Output:**

| name    | salary | dept\_name |
| ------- | ------ | ---------- |
| Alice   | 50000  | HR         |
| Bob     | 60000  | IT         |
| Charlie | 55000  | Sales      |
| NULL    | NULL   | Marketing  |

---

### Q14: Right join with condition

```sql
SELECT e.name, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.dept_id
WHERE e.name IS NULL;
```

**Output:**

| name | dept\_name |
| ---- | ---------- |
| NULL | Marketing  |

---

### Q15: Right join with filtering on NULL

```sql
SELECT e.name, p.project_name
FROM employees e
RIGHT JOIN projects p ON e.emp_id = p.emp_id
WHERE e.name IS NULL;
```

**Output:**

| name   | project\_name |
| ------ | ------------- |
| (none) |               |

---

## 4. FULL OUTER JOIN

### Q16: Employees and departments (all records)

```sql
SELECT e.name, d.dept_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.dept_id;
```

**Output:**

| name    | dept\_name |
| ------- | ---------- |
| Alice   | HR         |
| Bob     | IT         |
| Charlie | Sales      |
| NULL    | Marketing  |

---

### Q17: Employees and projects (all records)

```sql
SELECT e.name, p.project_name
FROM employees e
FULL OUTER JOIN projects p ON e.emp_id = p.emp_id;
```

**Output:**

| name    | project\_name |
| ------- | ------------- |
| Alice   | Alpha         |
| Bob     | NULL          |
| Charlie | Beta          |

---

### Q18: Full join with multiple tables

```sql
SELECT e.name, d.dept_name, p.project_name
FROM employees e
FULL OUTER JOIN departments d ON e.dept_id = d.dept_id
FULL OUTER JOIN projects p ON e.emp_id = p.emp_id;
```

**Output:**

| name    | dept\_name | project\_name |
| ------- | ---------- | ------------- |
| Alice   | HR         | Alpha         |
| Bob     | IT         | NULL          |
| Charlie | Sales      | Beta          |
| NULL    | Marketing  | NULL          |

---

## 5. SELF JOIN

### Q19: Employees and their manager (self join)

**Input Table: employees**

| emp\_id | name    | manager\_id |
| ------- | ------- | ----------- |
| 1       | Alice   | NULL        |
| 2       | Bob     | 1           |
| 3       | Charlie | 1           |

```sql
SELECT e1.name AS employee, e2.name AS manager
FROM employees e1
LEFT JOIN employees e2 ON e1.manager_id = e2.emp_id;
```

**Output:**

| employee | manager |
| -------- | ------- |
| Alice    | NULL    |
| Bob      | Alice   |
| Charlie  | Alice   |

---

### Q20: Employees reporting to the same manager

```sql
SELECT e1.name AS emp1, e2.name AS emp2, e1.manager_id
FROM employees e1
INNER JOIN employees e2 ON e1.manager_id = e2.manager_id
WHERE e1.emp_id < e2.emp_id;
```

**Output:**

| emp1 | emp2    | manager\_id |
| ---- | ------- | ----------- |
| Bob  | Charlie | 1           |
