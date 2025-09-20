# SQL Practice: Temporary Tables / CTEs (Common Table Expressions) with Explanations

This file contains **15 SQL practice problems** covering:

* WITH clause (CTEs)
* Recursive CTEs

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. Input Table Example

**Table: employees**

| emp\_id | name    | dept  | salary | manager\_id |
| ------- | ------- | ----- | ------ | ----------- |
| 1       | Alice   | HR    | 48000  | NULL        |
| 2       | Bob     | IT    | 60000  | 1           |
| 3       | Charlie | HR    | 55000  | 1           |
| 4       | David   | IT    | 45000  | 2           |
| 5       | Eva     | Sales | 70000  | 1           |

---

## 2. Simple CTEs (WITH clause)

### Q1: List all employees with salary above 50000

```sql
WITH high_salary AS (
    SELECT emp_id, name, salary
    FROM employees
    WHERE salary > 50000
)
SELECT * FROM high_salary;
```

**Output:**

| emp\_id | name    | salary |
| ------- | ------- | ------ |
| 2       | Bob     | 60000  |
| 3       | Charlie | 55000  |
| 5       | Eva     | 70000  |

### Q2: Calculate average salary per department using CTE

```sql
WITH dept_avg AS (
    SELECT dept, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY dept
)
SELECT e.name, e.dept, e.salary, d.avg_salary
FROM employees e
JOIN dept_avg d ON e.dept = d.dept;
```

**Output:**

| name    | dept  | salary | avg\_salary |
| ------- | ----- | ------ | ----------- |
| Alice   | HR    | 48000  | 51500       |
| Charlie | HR    | 55000  | 51500       |
| Bob     | IT    | 60000  | 52500       |
| David   | IT    | 45000  | 52500       |
| Eva     | Sales | 70000  | 70000       |

### Q3: Employees earning more than department average

```sql
WITH dept_avg AS (
    SELECT dept, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY dept
)
SELECT e.name, e.dept, e.salary
FROM employees e
JOIN dept_avg d ON e.dept = d.dept
WHERE e.salary > d.avg_salary;
```

**Output:**

| name    | dept | salary |
| ------- | ---- | ------ |
| Charlie | HR   | 55000  |
| Bob     | IT   | 60000  |

### Q4: Using multiple CTEs

```sql
WITH dept_avg AS (
    SELECT dept, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY dept
),
high_salary AS (
    SELECT * FROM employees WHERE salary > 50000
)
SELECT h.name, h.salary, d.avg_salary
FROM high_salary h
JOIN dept_avg d ON h.dept = d.dept;
```

**Output:**

| name    | salary | avg\_salary |
| ------- | ------ | ----------- |
| Bob     | 60000  | 52500       |
| Charlie | 55000  | 51500       |
| Eva     | 70000  | 70000       |

### Q5: Using CTE for filtering employees with manager

```sql
WITH has_manager AS (
    SELECT emp_id, name, manager_id
    FROM employees
    WHERE manager_id IS NOT NULL
)
SELECT * FROM has_manager;
```

**Output:**

| emp\_id | name    | manager\_id |
| ------- | ------- | ----------- |
| 2       | Bob     | 1           |
| 3       | Charlie | 1           |
| 4       | David   | 2           |
| 5       | Eva     | 1           |

---

## 3. Recursive CTEs

### Q6: Hierarchy - List employees under manager Alice

```sql
WITH RECURSIVE emp_hierarchy AS (
    SELECT emp_id, name, manager_id
    FROM employees
    WHERE manager_id IS NULL  -- top-level manager
    UNION ALL
    SELECT e.emp_id, e.name, e.manager_id
    FROM employees e
    JOIN emp_hierarchy h ON e.manager_id = h.emp_id
)
SELECT * FROM emp_hierarchy;
```

**Output:**

| emp\_id | name    | manager\_id |
| ------- | ------- | ----------- |
| 1       | Alice   | NULL        |
| 2       | Bob     | 1           |
| 3       | Charlie | 1           |
| 5       | Eva     | 1           |
| 4       | David   | 2           |

### Q7: Calculate cumulative salary under each manager

```sql
WITH RECURSIVE emp_hierarchy AS (
    SELECT emp_id, name, salary, manager_id
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.emp_id, e.name, e.salary, e.manager_id
    FROM employees e
    JOIN emp_hierarchy h ON e.manager_id = h.emp_id
)
SELECT manager_id, SUM(salary) AS total_salary
FROM emp_hierarchy
GROUP BY manager_id;
```

**Output:**

| manager\_id | total\_salary |
| ----------- | ------------- |
| NULL        | 48000         |
| 1           | 190000        |
| 2           | 45000         |

### Q8: Depth of hierarchy per employee

```sql
WITH RECURSIVE emp_hierarchy AS (
    SELECT emp_id, name, manager_id, 1 AS level
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.emp_id, e.name, e.manager_id, h.level + 1
    FROM employees e
    JOIN emp_hierarchy h ON e.manager_id = h.emp_id
)
SELECT * FROM emp_hierarchy;
```

**Output:**

| emp\_id | name    | manager\_id | level |
| ------- | ------- | ----------- | ----- |
| 1       | Alice   | NULL        | 1     |
| 2       | Bob     | 1           | 2     |
| 3       | Charlie | 1           | 2     |
| 5       | Eva     | 1           | 2     |
| 4       | David   | 2           | 3     |

### Q9: Employees at level 2 or deeper

```sql
WITH RECURSIVE emp_hierarchy AS (
    SELECT emp_id, name, manager_id, 1 AS level
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.emp_id, e.name, e.manager_id, h.level + 1
    FROM employees e
    JOIN emp_hierarchy h ON e.manager_id = h.emp_id
)
SELECT * FROM emp_hierarchy
WHERE level >= 2;
```

**Output:**

| emp\_id | name    | manager\_id | level |
| ------- | ------- | ----------- | ----- |
| 2       | Bob     | 1           | 2     |
| 3       | Charlie | 1           | 2     |
| 5       | Eva     | 1           | 2     |
| 4       | David   | 2           | 3     |

### Q10: Total salary per hierarchy level

```sql
WITH RECURSIVE emp_hierarchy AS (
    SELECT emp_id, name, salary, manager_id, 1 AS level
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.emp_id, e.name, e.salary, e.manager_id, h.level + 1
    FROM employees e
    JOIN emp_hierarchy h ON e.manager_id = h.emp_id
)
SELECT level, SUM(salary) AS total_salary
FROM emp_hierarchy
GROUP BY level;
```

**Output:**

| level | total\_salary |
| ----- | ------------- |
| 1     | 48000         |
| 2     | 165000        |
| 3     | 45000         |

---

### Explanation:

1. **WITH / CTE** allows creating a temporary result set for easier querying.
2. **Recursive CTE** iterates over hierarchy, useful for tree structures.
3. Break complex transformations into smaller queries to validate each step.

---

**Use case in ETL Testing:**

* Validate intermediate transformations using CTEs.
* Build hierarchical views for aggregation or validation.
* Simplify complex queries into readable step
