# SQL Practice: Subqueries (Single-row, Multi-row, Correlated) with Explanations

This file contains **20 SQL practice problems** covering:

* Single-row subquery (=, <, >)
* Multi-row subquery (IN, ANY, ALL)
* Correlated subquery

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. Single-row Subqueries

### Q1: Find employees with salary equal to the highest salary

**Input Table: employees**

| emp\_id | name    | salary |
| ------- | ------- | ------ |
| 1       | Alice   | 48000  |
| 2       | Bob     | 60000  |
| 3       | Charlie | 55000  |
| 4       | David   | 45000  |
| 5       | Eva     | 70000  |

```sql
SELECT emp_id, name, salary
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees);
```

**Explanation:**
Single-row subquery returns MAX(salary). The outer query selects employee(s) with that salary.

**Output:**

| emp\_id | name | salary |
| ------- | ---- | ------ |
| 5       | Eva  | 70000  |

---

### Q2: Employees with salary less than the average salary

```sql
SELECT emp_id, name, salary
FROM employees
WHERE salary < (SELECT AVG(salary) FROM employees);
```

**Output:**

| emp\_id | name  | salary |
| ------- | ----- | ------ |
| 1       | Alice | 48000  |
| 4       | David | 45000  |

---

### Q3: Employee(s) with minimum salary

```sql
SELECT emp_id, name, salary
FROM employees
WHERE salary = (SELECT MIN(salary) FROM employees);
```

**Output:**

| emp\_id | name  | salary |
| ------- | ----- | ------ |
| 4       | David | 45000  |

---

### Q4: Employee(s) with salary just above 50000

```sql
SELECT emp_id, name, salary
FROM employees
WHERE salary = (SELECT MIN(salary) FROM employees WHERE salary > 50000);
```

**Output:**

| emp\_id | name    | salary |
| ------- | ------- | ------ |
| 3       | Charlie | 55000  |

---

### Q5: Employee(s) having salary greater than 60000

```sql
SELECT emp_id, name, salary
FROM employees
WHERE salary > (SELECT MAX(salary) - 10000 FROM employees);
```

**Output:**

| emp\_id | name | salary |
| ------- | ---- | ------ |
| 2       | Bob  | 60000  |
| 5       | Eva  | 70000  |

---

## 2. Multi-row Subqueries

### Q6: Employees in departments with more than one employee

**Input Table: employees**

| emp\_id | name    | dept  |
| ------- | ------- | ----- |
| 1       | Alice   | HR    |
| 2       | Bob     | IT    |
| 3       | Charlie | HR    |
| 4       | David   | IT    |
| 5       | Eva     | Sales |

```sql
SELECT emp_id, name, dept
FROM employees
WHERE dept IN (
    SELECT dept
    FROM employees
    GROUP BY dept
    HAVING COUNT(*) > 1
);
```

**Explanation:**
Multi-row subquery returns departments with more than 1 employee. Outer query selects employees in those departments.

**Output:**

| emp\_id | name    | dept |
| ------- | ------- | ---- |
| 1       | Alice   | HR   |
| 2       | Bob     | IT   |
| 3       | Charlie | HR   |
| 4       | David   | IT   |

---

### Q7: Employees with salary in top 3 salaries

```sql
SELECT emp_id, name, salary
FROM employees
WHERE salary IN (
    SELECT DISTINCT salary
    FROM employees
    ORDER BY salary DESC
    LIMIT 3
);
```

**Output:**

| emp\_id | name    | salary |
| ------- | ------- | ------ |
| 2       | Bob     | 60000  |
| 3       | Charlie | 55000  |
| 5       | Eva     | 70000  |

---

### Q8: Employees in departments 'HR' or 'IT'

```sql
SELECT emp_id, name, dept
FROM employees
WHERE dept IN ('HR','IT');
```

**Output:**

| emp\_id | name    | dept |
| ------- | ------- | ---- |
| 1       | Alice   | HR   |
| 2       | Bob     | IT   |
| 3       | Charlie | HR   |
| 4       | David   | IT   |

---

### Q9: Employees not in department with only one employee

```sql
SELECT emp_id, name, dept
FROM employees
WHERE dept NOT IN (
    SELECT dept
    FROM employees
    GROUP BY dept
    HAVING COUNT(*) = 1
);
```

**Output:**

| emp\_id | name    | dept |
| ------- | ------- | ---- |
| 1       | Alice   | HR   |
| 2       | Bob     | IT   |
| 3       | Charlie | HR   |
| 4       | David   | IT   |

---

### Q10: Employees with salary greater than any employee in HR

```sql
SELECT emp_id, name, salary
FROM employees
WHERE salary > ANY (
    SELECT salary
    FROM employees
    WHERE dept='HR'
);
```

**Output:**

| emp\_id | name | salary |
| ------- | ---- | ------ |
| 2       | Bob  | 60000  |
| 5       | Eva  | 70000  |

---

## 3. Correlated Subqueries

### Q11: Employees with salary greater than average salary of their department

```sql
SELECT e1.emp_id, e1.name, e1.salary, e1.dept
FROM employees e1
WHERE e1.salary > (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.dept = e1.dept
);
```

**Output:**

| emp\_id | name    | salary | dept |
| ------- | ------- | ------ | ---- |
| 3       | Charlie | 55000  | HR   |
| 2       | Bob     | 60000  | IT   |

---

### Q12: Employees who earn the maximum salary in their department

```sql
SELECT e1.emp_id, e1.name, e1.salary, e1.dept
FROM employees e1
WHERE e1.salary = (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.dept = e1.dept
);
```

**Output:**

| emp\_id | name    | salary | dept  |
| ------- | ------- | ------ | ----- |
| 3       | Charlie | 55000  | HR    |
| 2       | Bob     | 60000  | IT    |
| 5       | Eva     | 70000  | Sales |

---

### Q13: Employees whose salary is greater than all employees in HR

```sql
SELECT emp_id, name, salary
FROM employees e
WHERE salary > ALL (
    SELECT salary
    FROM employees
    WHERE dept='HR'
);
```

**Output:**

| emp\_id | name | salary |
| ------- | ---- | ------ |
| 2       | Bob  | 60000  |
| 5       | Eva  | 70000  |

---

### Q14: Employees with salary less than the maximum salary of IT department

```sql
SELECT emp_id, name, salary
FROM employees e
WHERE salary < (
    SELECT MAX(salary)
    FROM employees
    WHERE dept='IT'
);
```

**Output:**

| emp\_id | name    | salary |
| ------- | ------- | ------ |
| 1       | Alice   | 48000  |
| 3       | Charlie | 55000  |
| 4       | David   | 45000  |

---

### Q15: Employees earning below average salary of Sales department

```sql
SELECT emp_id, name, salary
FROM employees e
WHERE salary < (
    SELECT AVG(salary)
    FROM employees
    WHERE dept='Sales'
);
```

**Output:**

| emp\_id | name | salary |
| ------- | ---- | ------ |
| (none)  |      |        |

---

### Q16: Employees who earn more than any employee in Sales

```sql
SELECT emp_id, name, salary
FROM employees e
WHERE salary > ANY (
    SELECT salary
    FROM employees
    WHERE dept='Sales'
);
```

**Output:**

| emp\_id | name    | salary |
| ------- | ------- | ------ |
| 1       | Alice   | 48000  |
| 2       | Bob     | 60000  |
| 3       | Charlie | 55000  |
| 4       | David   | 45000  |

---

### Q17: Employees who earn less than any employee in IT

```sql
SELECT emp_id, name, salary
FROM employees e
WHERE salary < ANY (
    SELECT salary
    FROM employees
    WHERE dept='IT'
);
```

**Output:**

| emp\_id | name  | salary |
| ------- | ----- | ------ |
| 1       | Alice | 48000  |
| 4       | David | 45000  |

---

### Q18: Employees earning equal to average of their department

```sql
SELECT e1.emp_id, e1.name, e1.salary, e1.dept
FROM employees e1
WHERE e1.salary = (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.dept = e1.dept
);
```

**Output:**

| emp\_id | name | salary | dept |
| ------- | ---- | ------ | ---- |
| (none)  |      |        |      |

---

### Q19: Employees earning less than maximum salary in their department

```sql
SELECT e1.emp_id, e1.name, e1.salary, e1.dept
FROM employees e1
WHERE e1.salary < (
    SELECT MAX(e2.salary)
    FROM employees e2
    WHERE e2.dept = e1.dept
);
```

**Output:**

| emp\_id | name  | salary | dept |
| ------- | ----- | ------ | ---- |
| 1       | Alice | 48000  | HR   |
| 4       | David | 45000  | IT   |

---

### Q20: Employees earning more than minimum salary in their department

```sql
SELECT e1.emp_id, e1.name, e1.salary, e1.dept
FROM employees e1
WHERE e1.salary > (
    SELECT MIN(e2.salary)
    FROM employees e2
    WHERE e2.dept = e1.dept
);
```

**Output:**

| emp\_id | name    | salary | dept |
| ------- | ------- | ------ | ---- |
| 1       | Alice   | 48000  | HR   |
| 3       | Charlie | 55000  | HR   |
| 2       | Bob     | 60000  | IT   |
