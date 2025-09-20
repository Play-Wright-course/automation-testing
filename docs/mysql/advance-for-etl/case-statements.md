# SQL Practice: CASE Statements / Conditional Logic with Explanations

This file contains **15 SQL practice problems** covering:

* CASE WHEN ... THEN ... ELSE ... END
* Using CASE inside aggregations

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. Input Table Example

**Table: employees**

| emp\_id | name    | dept  | salary |
| ------- | ------- | ----- | ------ |
| 1       | Alice   | HR    | 48000  |
| 2       | Bob     | IT    | 60000  |
| 3       | Charlie | HR    | 55000  |
| 4       | David   | IT    | 45000  |
| 5       | Eva     | Sales | 70000  |

---

## 2. Simple CASE Statements

### Q1: Assign salary grade based on salary

```sql
SELECT emp_id, name, salary,
       CASE
           WHEN salary < 50000 THEN 'Low'
           WHEN salary BETWEEN 50000 AND 60000 THEN 'Medium'
           ELSE 'High'
       END AS salary_grade
FROM employees;
```

**Output:**

| emp\_id | name    | salary | salary\_grade |
| ------- | ------- | ------ | ------------- |
| 1       | Alice   | 48000  | Low           |
| 2       | Bob     | 60000  | Medium        |
| 3       | Charlie | 55000  | Medium        |
| 4       | David   | 45000  | Low           |
| 5       | Eva     | 70000  | High          |

### Q2: Mark department type

```sql
SELECT emp_id, name, dept,
       CASE dept
           WHEN 'HR' THEN 'Admin'
           WHEN 'IT' THEN 'Technical'
           ELSE 'Business'
       END AS dept_type
FROM employees;
```

**Output:**

| emp\_id | name    | dept  | dept\_type |
| ------- | ------- | ----- | ---------- |
| 1       | Alice   | HR    | Admin      |
| 2       | Bob     | IT    | Technical  |
| 3       | Charlie | HR    | Admin      |
| 4       | David   | IT    | Technical  |
| 5       | Eva     | Sales | Business   |

### Q3: Flag high earners

```sql
SELECT emp_id, name, salary,
       CASE WHEN salary > 60000 THEN 'Yes' ELSE 'No' END AS high_earner
FROM employees;
```

**Output:**

| emp\_id | name    | salary | high\_earner |
| ------- | ------- | ------ | ------------ |
| 1       | Alice   | 48000  | No           |
| 2       | Bob     | 60000  | No           |
| 3       | Charlie | 55000  | No           |
| 4       | David   | 45000  | No           |
| 5       | Eva     | 70000  | Yes          |

### Q4: Combine multiple conditions

```sql
SELECT emp_id, name, dept, salary,
       CASE
           WHEN dept='IT' AND salary > 50000 THEN 'Tech High'
           WHEN dept='IT' THEN 'Tech Low'
           ELSE 'Other'
       END AS category
FROM employees;
```

**Output:**

| emp\_id | name    | dept  | salary | category  |
| ------- | ------- | ----- | ------ | --------- |
| 1       | Alice   | HR    | 48000  | Other     |
| 2       | Bob     | IT    | 60000  | Tech High |
| 3       | Charlie | HR    | 55000  | Other     |
| 4       | David   | IT    | 45000  | Tech Low  |
| 5       | Eva     | Sales | 70000  | Other     |

### Q5: CASE with NULL check

```sql
SELECT emp_id, name, dept, salary,
       CASE WHEN salary IS NULL THEN 'Missing' ELSE 'Available' END AS salary_status
FROM employees;
```

**Output:**

| emp\_id | name    | dept  | salary | salary\_status |
| ------- | ------- | ----- | ------ | -------------- |
| 1       | Alice   | HR    | 48000  | Available      |
| 2       | Bob     | IT    | 60000  | Available      |
| 3       | Charlie | HR    | 55000  | Available      |
| 4       | David   | IT    | 45000  | Available      |
| 5       | Eva     | Sales | 70000  | Available      |

---

## 3. Using CASE inside Aggregations

### Q6: Count high and low salary employees

```sql
SELECT
       SUM(CASE WHEN salary > 60000 THEN 1 ELSE 0 END) AS high_salary_count,
       SUM(CASE WHEN salary <= 60000 THEN 1 ELSE 0 END) AS low_salary_count
FROM employees;
```

**Output:**

| high\_salary\_count | low\_salary\_count |
| ------------------- | ------------------ |
| 1                   | 4                  |

### Q7: Total salary per dept with conditional bonus

```sql
SELECT dept,
       SUM(salary + CASE WHEN salary > 50000 THEN 500 ELSE 200 END) AS total_with_bonus
FROM employees
GROUP BY dept;
```

**Output:**

| dept  | total\_with\_bonus |
| ----- | ------------------ |
| HR    | 108700             |
| IT    | 105700             |
| Sales | 70500              |

### Q8: Average salary grade calculation

```sql
SELECT dept,
       AVG(CASE WHEN salary > 60000 THEN 3
                WHEN salary BETWEEN 50000 AND 60000 THEN 2
                ELSE 1 END) AS avg_salary_grade
FROM employees
GROUP BY dept;
```

**Output:**

| dept  | avg\_salary\_grade |
| ----- | ------------------ |
| HR    | 1.5                |
| IT    | 2.5                |
| Sales | 3                  |

### Q9: Count employees by category using CASE

```sql
SELECT
       SUM(CASE WHEN dept='IT' THEN 1 ELSE 0 END) AS IT_count,
       SUM(CASE WHEN dept='HR' THEN 1 ELSE 0 END) AS HR_count,
       SUM(CASE WHEN dept='Sales' THEN 1 ELSE 0 END) AS Sales_count
FROM employees;
```

**Output:**

| IT\_count | HR\_count | Sales\_count |
| --------- | --------- | ------------ |
| 2         | 2         | 1            |

### Q10: Conditional MAX salary per dept

```sql
SELECT dept,
       MAX(CASE WHEN salary > 50000 THEN salary ELSE 0 END) AS max_high_salary
FROM employees
GROUP BY dept;
```

**Output:**

| dept  | max\_high\_salary |
| ----- | ----------------- |
| HR    | 55000             |
| IT    | 60000             |
| Sales | 70000             |

---

### Explanation:

1. **CASE WHEN ... THEN ... ELSE ... END** lets you apply conditional logic in SELECT.
2. Inside **aggregations**, CASE allows counting, summing, or calculating values conditionally.

---

**Use case in ETL Testing:**

* Transform raw data values based on conditions.
* Validate that business rules (e.g., salary grade, bonus) are applied correctly.
* Count or sum values based on conditional logic.
