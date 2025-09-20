# SQL Practice: Advanced / Complex Joins for ETL Testing

This file contains **10 SQL practice problems** covering:

* Cross Join (Cartesian product)
* Self-join with multiple conditions
* Join with subqueries
* Join multiple tables (3–4 tables)

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. CROSS JOIN

### Q1: Generate all combinations of employees and projects

**Input Tables:**

**employees**

| emp\_id | name  |
| ------- | ----- |
| 1       | Alice |
| 2       | Bob   |

**projects**

| project\_id | project\_name |
| ----------- | ------------- |
| 101         | Alpha         |
| 102         | Beta          |

**Query:**

```sql
SELECT e.name, p.project_name
FROM employees e
CROSS JOIN projects p;
```

**Explanation:**

* `CROSS JOIN` generates all possible combinations between two tables.
* Useful in ETL testing when validating assignment of employees to all possible project slots.

**Output:**

| name  | project\_name |
| ----- | ------------- |
| Alice | Alpha         |
| Alice | Beta          |
| Bob   | Alpha         |
| Bob   | Beta          |

---

## 2. SELF JOIN (single condition)

### Q2: Find employees with the same department

**Input Table: employees**

| emp\_id | name    | dept\_id |
| ------- | ------- | -------- |
| 1       | Alice   | 10       |
| 2       | Bob     | 10       |
| 3       | Charlie | 20       |
| 4       | David   | 10       |

**Query:**

```sql
SELECT e1.name AS emp1, e2.name AS emp2, e1.dept_id
FROM employees e1
JOIN employees e2
  ON e1.dept_id = e2.dept_id
  AND e1.emp_id < e2.emp_id;
```

**Explanation:**

* Self-join compares a table with itself.
* `e1.emp_id < e2.emp_id` avoids duplicate pairs and self-pairing.
* ETL use case: Validate **peer relationships** in the same group.

**Output:**

| emp1  | emp2  | dept\_id |
| ----- | ----- | -------- |
| Alice | Bob   | 10       |
| Alice | David | 10       |
| Bob   | David | 10       |

---

## 3. SELF JOIN (multiple conditions)

### Q3: Employees reporting to same manager and in same department

**Input Table: employees**

| emp\_id | name    | dept\_id | manager\_id |
| ------- | ------- | -------- | ----------- |
| 1       | Alice   | 10       | 100         |
| 2       | Bob     | 10       | 100         |
| 3       | Charlie | 20       | 200         |
| 4       | David   | 10       | 100         |

**Query:**

```sql
SELECT e1.name AS emp1, e2.name AS emp2, e1.dept_id, e1.manager_id
FROM employees e1
JOIN employees e2
  ON e1.dept_id = e2.dept_id
  AND e1.manager_id = e2.manager_id
  AND e1.emp_id < e2.emp_id;
```

**Output:**

| emp1  | emp2  | dept\_id | manager\_id |
| ----- | ----- | -------- | ----------- |
| Alice | Bob   | 10       | 100         |
| Alice | David | 10       | 100         |
| Bob   | David | 10       | 100         |

---

## 4. JOIN WITH SUBQUERY

### Q4: Select employees working on highest salary projects

**Input Tables:**

**employees**

| emp\_id | name    | project\_id |
| ------- | ------- | ----------- |
| 1       | Alice   | 101         |
| 2       | Bob     | 102         |
| 3       | Charlie | 101         |

**projects**

| project\_id | project\_name | budget |
| ----------- | ------------- | ------ |
| 101         | Alpha         | 5000   |
| 102         | Beta          | 10000  |

**Query:**

```sql
SELECT e.name, p.project_name, p.budget
FROM employees e
JOIN projects p
  ON e.project_id = p.project_id
WHERE p.budget = (SELECT MAX(budget) FROM projects);
```

**Explanation:**

* Subquery `(SELECT MAX(budget) FROM projects)` returns the largest project budget.
* ETL use case: Validate transformation logic based on derived values from another table.

**Output:**

| name | project\_name | budget |
| ---- | ------------- | ------ |
| Bob  | Beta          | 10000  |

---

## 5. JOIN MULTIPLE TABLES (3 tables)

### Q5: Employee assignments with department and project names

**Input Tables:**

**employees**

| emp\_id | name  | dept\_id | project\_id |
| ------- | ----- | -------- | ----------- |
| 1       | Alice | 10       | 101         |
| 2       | Bob   | 20       | 102         |

**departments**

| dept\_id | dept\_name |
| -------- | ---------- |
| 10       | HR         |
| 20       | IT         |

**projects**

| project\_id | project\_name |
| ----------- | ------------- |
| 101         | Alpha         |
| 102         | Beta          |

**Query:**

```sql
SELECT e.name, d.dept_name, p.project_name
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
JOIN projects p ON e.project_id = p.project_id;
```

**Explanation:**

* Joining 3 tables to get full contextual information
* ETL use case: Validate final transformed fact table combining multiple sources

**Output:**

| name  | dept\_name | project\_name |
| ----- | ---------- | ------------- |
| Alice | HR         | Alpha         |
| Bob   | IT         | Beta          |

---

## 6. JOIN MULTIPLE TABLES WITH CONDITIONS

### Q6: Employees in HR department working on budget > 5000 projects

**Query:**

```sql
SELECT e.name, d.dept_name, p.project_name, p.budget
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id
JOIN projects p ON e.project_id = p.project_id
WHERE d.dept_name = 'HR' AND p.budget > 5000;
```

**Output:**

| name  | dept\_name | project\_name | budget |
| ----- | ---------- | ------------- | ------ |
| Alice | HR         | Alpha         | 5000   |
