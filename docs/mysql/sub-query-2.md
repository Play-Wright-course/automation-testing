# SQL Practice: Filtering & Conditions with Explanations

This file contains **20 SQL practice problems** covering filtering and conditional operators:

* Comparison operators: =, <>, >, <, >=, <=
* Logical operators: AND, OR, NOT
* BETWEEN, IN, LIKE
* IS NULL / IS NOT NULL

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. Comparison Operators

### Q1: Employees with salary = 50000

**Input Table: employees**

| emp\_id | name    | dept  | salary |
| ------- | ------- | ----- | ------ |
| 1       | Alice   | HR    | 50000  |
| 2       | Bob     | IT    | 60000  |
| 3       | Charlie | HR    | 55000  |
| 4       | David   | Sales | 45000  |

**Query:**

```sql
SELECT *
FROM employees
WHERE salary = 50000;
```

**Explanation:**
`=` operator selects rows where salary equals 50000.

**Output:**

| emp\_id | name  | dept | salary |
| ------- | ----- | ---- | ------ |
| 1       | Alice | HR   | 50000  |

---

### Q2: Employees with salary <> 60000

```sql
SELECT *
FROM employees
WHERE salary <> 60000;
```

**Explanation:**
`<>` selects rows not equal to 60000.

**Output:**

| emp\_id | name    | dept  | salary |
| ------- | ------- | ----- | ------ |
| 1       | Alice   | HR    | 50000  |
| 3       | Charlie | HR    | 55000  |
| 4       | David   | Sales | 45000  |

---

### Q3: Employees with salary > 50000

```sql
SELECT name, salary
FROM employees
WHERE salary > 50000;
```

**Explanation:**
`>` selects rows with salary greater than 50000.

**Output:**

| name    | salary |
| ------- | ------ |
| Bob     | 60000  |
| Charlie | 55000  |

---

### Q4: Employees with salary <= 50000

```sql
SELECT name, salary
FROM employees
WHERE salary <= 50000;
```

**Explanation:**
`<=` selects salaries less than or equal to 50000.

**Output:**

| name  | salary |
| ----- | ------ |
| Alice | 50000  |
| David | 45000  |

---

### Q5: Employees with salary >= 55000

```sql
SELECT *
FROM employees
WHERE salary >= 55000;
```

**Explanation:**
`>=` selects salaries 55000 or more.

**Output:**

| emp\_id | name    | dept | salary |
| ------- | ------- | ---- | ------ |
| 2       | Bob     | IT   | 60000  |
| 3       | Charlie | HR   | 55000  |

---

## 2. Logical Operators (AND, OR, NOT)

### Q6: Employees in HR AND salary > 50000

```sql
SELECT *
FROM employees
WHERE dept = 'HR' AND salary > 50000;
```

**Explanation:**
`AND` ensures both conditions are true.

**Output:**

| emp\_id | name    | dept | salary |
| ------- | ------- | ---- | ------ |
| 3       | Charlie | HR   | 55000  |

---

### Q7: Employees in HR OR salary > 55000

```sql
SELECT *
FROM employees
WHERE dept = 'HR' OR salary > 55000;
```

**Explanation:**
`OR` selects rows matching either condition.

**Output:**

| emp\_id | name    | dept | salary |
| ------- | ------- | ---- | ------ |
| 1       | Alice   | HR   | 50000  |
| 2       | Bob     | IT   | 60000  |
| 3       | Charlie | HR   | 55000  |

---

### Q8: Employees NOT in HR

```sql
SELECT *
FROM employees
WHERE NOT dept = 'HR';
```

**Explanation:**
`NOT` inverts the condition.

**Output:**

| emp\_id | name  | dept  | salary |
| ------- | ----- | ----- | ------ |
| 2       | Bob   | IT    | 60000  |
| 4       | David | Sales | 45000  |

---

### Q9: Employees in IT AND salary >= 60000

```sql
SELECT name, dept, salary
FROM employees
WHERE dept = 'IT' AND salary >= 60000;
```

**Explanation:**
Both conditions must be true.

**Output:**

| name | dept | salary |
| ---- | ---- | ------ |
| Bob  | IT   | 60000  |

---

### Q10: Employees in Sales OR HR with salary < 50000

```sql
SELECT *
FROM employees
WHERE (dept = 'Sales' OR dept = 'HR') AND salary < 50000;
```

**Explanation:**
Parentheses control precedence: OR is evaluated first.

**Output:**

| emp\_id | name  | dept  | salary |
| ------- | ----- | ----- | ------ |
| 4       | David | Sales | 45000  |

---

## 3. BETWEEN, IN, LIKE

### Q11: Employees with salary BETWEEN 50000 AND 60000

```sql
SELECT *
FROM employees
WHERE salary BETWEEN 50000 AND 60000;
```

**Explanation:**
`BETWEEN` includes the boundary values.

**Output:**

| emp\_id | name    | dept | salary |
| ------- | ------- | ---- | ------ |
| 1       | Alice   | HR   | 50000  |
| 3       | Charlie | HR   | 55000  |
| 2       | Bob     | IT   | 60000  |

---

### Q12: Employees in specific departments (IN)

```sql
SELECT *
FROM employees
WHERE dept IN ('HR', 'Sales');
```

**Explanation:**
`IN` filters multiple discrete values.

**Output:**

| emp\_id | name    | dept  | salary |
| ------- | ------- | ----- | ------ |
| 1       | Alice   | HR    | 50000  |
| 3       | Charlie | HR    | 55000  |
| 4       | David   | Sales | 45000  |

---

### Q13: Employees whose name starts with 'A' (LIKE)

```sql
SELECT *
FROM employees
WHERE name LIKE 'A%';
```

**Explanation:**
`%` is wildcard for any number of characters.

**Output:**

| emp\_id | name  | dept | salary |
| ------- | ----- | ---- | ------ |
| 1       | Alice | HR   | 50000  |

---

### Q14: Employees whose name contains 'a' (LIKE)

```sql
SELECT *
FROM employees
WHERE name LIKE '%a%';
```

**Explanation:**
`%` before and after 'a' matches any string containing 'a'.

**Output:**

| emp\_id | name    | dept  | salary |
| ------- | ------- | ----- | ------ |
| 1       | Alice   | HR    | 50000  |
| 2       | Bob     | IT    | 60000  |
| 3       | Charlie | HR    | 55000  |
| 4       | David   | Sales | 45000  |

---

### Q15: Employees whose name ends with 'e'

```sql
SELECT *
FROM employees
WHERE name LIKE '%e';
```

**Output:**

| emp\_id | name    | dept | salary |
| ------- | ------- | ---- | ------ |
| 1       | Alice   | HR   | 50000  |
| 3       | Charlie | HR   | 55000  |

---

## 4. IS NULL / IS NOT NULL

### Q16: Employees with NULL salary

**Input Table: employees**

| emp\_id | name    | dept  | salary |
| ------- | ------- | ----- | ------ |
| 1       | Alice   | HR    | 50000  |
| 2       | Bob     | IT    | NULL   |
| 3       | Charlie | HR    | 55000  |
| 4       | David   | Sales | NULL   |

**Query:**

```sql
SELECT *
FROM employees
WHERE salary IS NULL;
```

**Explanation:**
`IS NULL` selects rows where value is NULL.

**Output:**

| emp\_id | name  | dept  | salary |
| ------- | ----- | ----- | ------ |
| 2       | Bob   | IT    | NULL   |
| 4       | David | Sales | NULL   |

---

### Q17: Employees with NOT NULL salary

```sql
SELECT *
FROM employees
WHERE salary IS NOT NULL;
```

**Output:**

| emp\_id | name    | dept | salary |
| ------- | ------- | ---- | ------ |
| 1       | Alice   | HR   | 50000  |
| 3       | Charlie | HR   | 55000  |

---

### Q18: Employees with salary NULL or less than 50000

```sql
SELECT *
FROM employees
WHERE salary IS NULL OR salary < 50000;
```

**Output:**

| emp\_id | name  | dept  | salary |
| ------- | ----- | ----- | ------ |
| 2       | Bob   | IT    | NULL   |
| 4       | David | Sales | NULL   |

---

### Q19: Employees with salary NOT NULL AND > 50000

```sql
SELECT *
FROM employees
WHERE salary IS NOT NULL AND salary > 50000;
```

**Output:**

| emp\_id | name    | dept | salary |
| ------- | ------- | ---- | ------ |
| 2       | Bob     | IT   | 60000  |
| 3       | Charlie | HR   | 55000  |

---

### Q20: Employees with salary IS NULL OR department = 'HR'

```sql
SELECT *
FROM employees
WHERE salary IS NULL OR dept = 'HR';
```

**Output:**

| emp\_id | name    | dept | salary |
| ------- | ------- | ---- | ------ |
| 1       | Alice   | HR   | 50000  |
| 2       | Bob     | IT   | NULL   |
| 3       | Charlie | HR   | 55000  |

```
```
