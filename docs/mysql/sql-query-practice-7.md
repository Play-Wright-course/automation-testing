# SQL Practice: Aggregations (GROUP BY, Aggregate Functions, HAVING) with Explanations

This file contains **20 SQL practice problems** covering:

* GROUP BY
* Aggregate functions: COUNT, SUM, AVG, MIN, MAX
* HAVING clause

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. GROUP BY and COUNT

### Q1: Count employees in each department

**Input Table: employees**

| emp\_id | name    | dept  |
| ------- | ------- | ----- |
| 1       | Alice   | HR    |
| 2       | Bob     | IT    |
| 3       | Charlie | HR    |
| 4       | David   | IT    |
| 5       | Eva     | Sales |

```sql
SELECT dept, COUNT(*) AS emp_count
FROM employees
GROUP BY dept;
```

**Explanation:**
`COUNT(*)` counts rows in each department.

**Output:**

| dept  | emp\_count |
| ----- | ---------- |
| HR    | 2          |
| IT    | 2          |
| Sales | 1          |

---

### Q2: Count employees with salary > 50000 in each department

**Input Table: employees**

| emp\_id | name    | dept  | salary |
| ------- | ------- | ----- | ------ |
| 1       | Alice   | HR    | 48000  |
| 2       | Bob     | IT    | 60000  |
| 3       | Charlie | HR    | 55000  |
| 4       | David   | IT    | 45000  |
| 5       | Eva     | Sales | 70000  |

```sql
SELECT dept, COUNT(*) AS emp_count_high_salary
FROM employees
WHERE salary > 50000
GROUP BY dept;
```

**Output:**

| dept  | emp\_count\_high\_salary |
| ----- | ------------------------ |
| HR    | 1                        |
| IT    | 1                        |
| Sales | 1                        |

---

### Q3: Count distinct departments

```sql
SELECT COUNT(DISTINCT dept) AS distinct_departments
FROM employees;
```

**Output:**

| distinct\_departments |
| --------------------- |
| 3                     |

---

### Q4: Count employees per department having more than 1 employee

```sql
SELECT dept, COUNT(*) AS emp_count
FROM employees
GROUP BY dept
HAVING COUNT(*) > 1;
```

**Output:**

| dept | emp\_count |
| ---- | ---------- |
| HR   | 2          |
| IT   | 2          |

---

### Q5: Count employees whose name starts with 'A' per department

```sql
SELECT dept, COUNT(*) AS count_A
FROM employees
WHERE name LIKE 'A%'
GROUP BY dept;
```

**Output:**

| dept | count\_A |
| ---- | -------- |
| HR   | 1        |

---

## 2. SUM

### Q6: Total salary per department

```sql
SELECT dept, SUM(salary) AS total_salary
FROM employees
GROUP BY dept;
```

**Output:**

| dept  | total\_salary |
| ----- | ------------- |
| HR    | 103000        |
| IT    | 105000        |
| Sales | 70000         |

---

### Q7: Total salary of employees with salary > 50000 per department

```sql
SELECT dept, SUM(salary) AS high_salary_sum
FROM employees
WHERE salary > 50000
GROUP BY dept;
```

**Output:**

| dept  | high\_salary\_sum |
| ----- | ----------------- |
| HR    | 55000             |
| IT    | 60000             |
| Sales | 70000             |

---

### Q8: Total salary across company

```sql
SELECT SUM(salary) AS total_company_salary
FROM employees;
```

**Output:**

| total\_company\_salary |
| ---------------------- |
| 278000                 |

---

### Q9: Sum of salary per department having sum > 100000

```sql
SELECT dept, SUM(salary) AS total_salary
FROM employees
GROUP BY dept
HAVING SUM(salary) > 100000;
```

**Output:**

| dept | total\_salary |
| ---- | ------------- |
| HR   | 103000        |
| IT   | 105000        |

---

### Q10: Sum salary where employee name contains 'a'

```sql
SELECT SUM(salary) AS total_a_salary
FROM employees
WHERE name LIKE '%a%';
```

**Output:**

| total\_a\_salary |
| ---------------- |
| 178000           |

---

## 3. AVG

### Q11: Average salary per department

```sql
SELECT dept, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept;
```

**Output:**

| dept  | avg\_salary |
| ----- | ----------- |
| HR    | 51500       |
| IT    | 52500       |
| Sales | 70000       |

---

### Q12: Average salary of employees with salary > 50000

```sql
SELECT AVG(salary) AS avg_high_salary
FROM employees
WHERE salary > 50000;
```

**Output:**

| avg\_high\_salary |
| ----------------- |
| 61666.67          |

---

### Q13: Average salary per department having more than 1 employee

```sql
SELECT dept, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept
HAVING COUNT(*) > 1;
```

**Output:**

| dept | avg\_salary |
| ---- | ----------- |
| HR   | 51500       |
| IT   | 52500       |

---

### Q14: Average salary of employees whose name starts with 'C'

```sql
SELECT AVG(salary) AS avg_C_salary
FROM employees
WHERE name LIKE 'C%';
```

**Output:**

| avg\_C\_salary |
| -------------- |
| 55000          |

---

### Q15: Average salary across company

```sql
SELECT AVG(salary) AS avg_salary_company
FROM employees;
```

**Output:**

| avg\_salary\_company |
| -------------------- |
| 55600                |

---

## 4. MIN/MAX

### Q16: Minimum and Maximum salary per department

```sql
SELECT dept, MIN(salary) AS min_salary, MAX(salary) AS max_salary
FROM employees
GROUP BY dept;
```

**Output:**

| dept  | min\_salary | max\_salary |
| ----- | ----------- | ----------- |
| HR    | 48000       | 55000       |
| IT    | 45000       | 60000       |
| Sales | 70000       | 70000       |

---

### Q17: Minimum salary in company

```sql
SELECT MIN(salary) AS min_salary_company
FROM employees;
```

**Output:**

| min\_salary\_company |
| -------------------- |
| 45000                |

---

### Q18: Maximum salary in company

```sql
SELECT MAX(salary) AS max_salary_company
FROM employees;
```

**Output:**

| max\_salary\_company |
| -------------------- |
| 70000                |

---

### Q19: Maximum salary per department having more than 1 employee

```sql
SELECT dept, MAX(salary) AS max_salary
FROM employees
GROUP BY dept
HAVING COUNT(*) > 1;
```

**Output:**

| dept | max\_salary |
| ---- | ----------- |
| HR   | 55000       |
| IT   | 60000       |

---

### Q20: Minimum salary for employees with salary > 50000

```sql
SELECT MIN(salary) AS min_high_salary
FROM employees
WHERE salary > 50000;
```

**Output:**

| min\_high\_salary |
| ----------------- |
| 55000             |
