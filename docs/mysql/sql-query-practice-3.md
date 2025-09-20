# SQL Practice: Functions (String, Date, Numeric) with Explanations

This file contains **20 SQL practice problems** covering:

* String functions: TRIM, SUBSTR, CONCAT, LENGTH, UPPER, LOWER
* Date functions: NOW, GETDATE, DATEADD, DATEDIFF, TO\_DATE
* Numeric functions: ROUND, CEIL, FLOOR, ABS

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. String Functions

### Q1: Remove spaces from names using TRIM

**Input Table: employees**

| emp\_id | name        |
| ------- | ----------- |
| 1       | ' Alice '   |
| 2       | ' Bob '     |
| 3       | ' Charlie ' |

**Query:**

```sql
SELECT emp_id, TRIM(name) AS name_clean
FROM employees;
```

**Explanation:**
`TRIM` removes leading and trailing spaces.

**Output:**

| emp\_id | name\_clean |
| ------- | ----------- |
| 1       | Alice       |
| 2       | Bob         |
| 3       | Charlie     |

---

### Q2: Extract first 3 letters of name using SUBSTR

**Input Table: employees**

| emp\_id | name    |
| ------- | ------- |
| 1       | Alice   |
| 2       | Bob     |
| 3       | Charlie |

```sql
SELECT emp_id, SUBSTR(name,1,3) AS short_name
FROM employees;
```

**Output:**

| emp\_id | short\_name |
| ------- | ----------- |
| 1       | Ali         |
| 2       | Bob         |
| 3       | Cha         |

---

### Q3: Concatenate name with department

**Input Table: employees**

| emp\_id | name    | dept  |
| ------- | ------- | ----- |
| 1       | Alice   | HR    |
| 2       | Bob     | IT    |
| 3       | Charlie | Sales |

```sql
SELECT emp_id, CONCAT(name, ' - ', dept) AS name_dept
FROM employees;
```

**Output:**

| emp\_id | name\_dept      |
| ------- | --------------- |
| 1       | Alice - HR      |
| 2       | Bob - IT        |
| 3       | Charlie - Sales |

---

### Q4: Get length of each name

**Input Table: employees**

| emp\_id | name    |
| ------- | ------- |
| 1       | Alice   |
| 2       | Bob     |
| 3       | Charlie |

```sql
SELECT emp_id, LENGTH(name) AS name_length
FROM employees;
```

**Output:**

| emp\_id | name\_length |
| ------- | ------------ |
| 1       | 5            |
| 2       | 3            |
| 3       | 7            |

---

### Q5: Convert name to uppercase and lowercase

**Input Table: employees**

| emp\_id | name    |
| ------- | ------- |
| 1       | Alice   |
| 2       | Bob     |
| 3       | Charlie |

```sql
SELECT emp_id, UPPER(name) AS upper_name, LOWER(name) AS lower_name
FROM employees;
```

**Output:**

| emp\_id | upper\_name | lower\_name |
| ------- | ----------- | ----------- |
| 1       | ALICE       | alice       |
| 2       | BOB         | bob         |
| 3       | CHARLIE     | charlie     |

---

## 2. Date Functions

### Q6: Get current date using NOW (MySQL) / GETDATE (SQL Server)

```sql
SELECT NOW() AS current_date; -- MySQL
-- SELECT GETDATE() AS current_date; -- SQL Server
```

**Output Example:**

| current\_date    |
| ---------------- |
| 2025-09-20 11:00 |

---

### Q7: Add 5 days to current date

```sql
SELECT DATEADD(day, 5, GETDATE()) AS future_date; -- SQL Server
```

**Output Example:**

| future\_date     |
| ---------------- |
| 2025-09-25 11:00 |

---

### Q8: Difference between two dates (in days)

**Input Table: projects**

| project\_id | start\_date | end\_date  |
| ----------- | ----------- | ---------- |
| 1           | 2025-09-01  | 2025-09-10 |
| 2           | 2025-09-05  | 2025-09-20 |

```sql
SELECT project_id, DATEDIFF(day, start_date, end_date) AS duration_days
FROM projects; -- SQL Server
```

**Output:**

| project\_id | duration\_days |
| ----------- | -------------- |
| 1           | 9              |
| 2           | 15             |

---

### Q9: Convert string to date using TO\_DATE (Oracle)

```sql
SELECT TO_DATE('20-09-2025','DD-MM-YYYY') AS date_val FROM dual;
```

**Output:**

| date\_val |
| --------- |
| 20-SEP-25 |

---

### Q10: Extract year, month from date

**Input Table: employees**

| emp\_id | name    | joining\_date |
| ------- | ------- | ------------- |
| 1       | Alice   | 2020-05-10    |
| 2       | Bob     | 2021-08-15    |
| 3       | Charlie | 2022-01-20    |

```sql
SELECT emp_id, YEAR(joining_date) AS year_joined, MONTH(joining_date) AS month_joined
FROM employees;
```

**Output:**

| emp\_id | year\_joined | month\_joined |
| ------- | ------------ | ------------- |
| 1       | 2020         | 5             |
| 2       | 2021         | 8             |
| 3       | 2022         | 1             |

---

## 3. Numeric Functions

### Q11: Round salary to nearest 1000

**Input Table: employees**

| emp\_id | salary |
| ------- | ------ |
| 1       | 52345  |
| 2       | 60789  |
| 3       | 55432  |

```sql
SELECT emp_id, ROUND(salary, -3) AS rounded_salary
FROM employees;
```

**Output:**

| emp\_id | rounded\_salary |
| ------- | --------------- |
| 1       | 52000           |
| 2       | 61000           |
| 3       | 55000           |

---

### Q12: Ceiling function

```sql
SELECT emp_id, CEIL(salary/1000.0) AS ceil_k_salary
FROM employees;
```

**Output:**

| emp\_id | ceil\_k\_salary |
| ------- | --------------- |
| 1       | 53              |
| 2       | 61              |
| 3       | 56              |

---

### Q13: Floor function

```sql
SELECT emp_id, FLOOR(salary/1000.0) AS floor_k_salary
FROM employees;
```

**Output:**

| emp\_id | floor\_k\_salary |
| ------- | ---------------- |
| 1       | 52               |
| 2       | 60               |
| 3       | 55               |

---

### Q14: Absolute value

**Input Table: transactions**

| trans\_id | amount |
| --------- | ------ |
| 1         | -500   |
| 2         | 300    |
| 3         | -1000  |

```sql
SELECT trans_id, ABS(amount) AS abs_amount
FROM transactions;
```

**Output:**

| trans\_id | abs\_amount |
| --------- | ----------- |
| 1         | 500         |
| 2         | 300         |
| 3         | 1000        |

---

### Q15: Multiply salary by 1.1 and round

```sql
SELECT emp_id, ROUND(salary*1.1,0) AS increased_salary
FROM employees;
```

**Output:**

| emp\_id | increased\_salary |
| ------- | ----------------- |
| 1       | 57579             |
| 2       | 66868             |
| 3       | 60975             |

---

### Q16: Add 7 days to date using DATEADD

```sql
SELECT emp_id, DATEADD(day,7,joining_date) AS next_week
FROM employees;
```

**Output:**

| emp\_id | next\_week |
| ------- | ---------- |
| 1       | 2020-05-17 |
| 2       | 2021-08-22 |
| 3       | 2022-01-27 |

---

### Q17: Difference in years from today

```sql
SELECT emp_id, DATEDIFF(year, joining_date, GETDATE()) AS years_with_company
FROM employees;
```

**Output Example:**

| emp\_id | years\_with\_company |
| ------- | -------------------- |
| 1       | 5                    |
| 2       | 4                    |
| 3       | 3                    |

---

### Q18: Concatenate numeric and string

```sql
SELECT emp_id, CONCAT('Salary: ', salary) AS salary_text
FROM employees;
```

**Output:**

| emp\_id | salary\_text  |
| ------- | ------------- |
| 1       | Salary: 52345 |
| 2       | Salary: 60789 |
| 3       | Salary: 55432 |

---

### Q19: Lowercase department

**Input Table: employees**

| emp\_id | dept  |
| ------- | ----- |
| 1       | HR    |
| 2       | IT    |
| 3       | Sales |

```sql
SELECT emp_id, LOWER(dept) AS lower_dept
FROM employees;
```

**Output:**

| emp\_id | lower\_dept |
| ------- | ----------- |
| 1       | hr          |
| 2       | it          |
| 3       | sales       |

---

### Q20: Uppercase department

```sql
SELECT emp_id, UPPER(dept) AS upper_dept
FROM employees;
```

**Output:**

| emp\_id | upper\_dept |
| ------- | ----------- |
| 1       | HR          |
| 2       | IT          |
| 3       | SALES       |
