# SQL Practice: Exception / Error Handling with Explanations

This file contains **15 SQL practice problems** covering:

* Detecting NULLs and invalid data
* Handling negative values
* Identifying orphan records (foreign key violations)

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. Input Table Examples

**Table: employees**

| emp\_id | name    | salary | dept\_id |
| ------- | ------- | ------ | -------- |
| 1       | Alice   | 48000  | 10       |
| 2       | Bob     | NULL   | 20       |
| 3       | Charlie | 55000  | NULL     |
| 4       | David   | -45000 | 10       |
| 5       | Eva     | 70000  | 30       |

**Table: departments**

| dept\_id | dept\_name |
| -------- | ---------- |
| 10       | HR         |
| 20       | IT         |
| 30       | Sales      |

---

## 2. Detect NULLs

### Q1: Employees with NULL salary

```sql
SELECT * FROM employees WHERE salary IS NULL;
```

**Output:**

| emp\_id | name | salary | dept\_id |
| ------- | ---- | ------ | -------- |
| 2       | Bob  | NULL   | 20       |

### Q2: Employees with NULL department

```sql
SELECT * FROM employees WHERE dept_id IS NULL;
```

**Output:**

| emp\_id | name    | salary | dept\_id |
| ------- | ------- | ------ | -------- |
| 3       | Charlie | 55000  | NULL     |

### Q3: Employees with NULL name or salary

```sql
SELECT * FROM employees WHERE name IS NULL OR salary IS NULL;
```

**Output:**

| emp\_id | name | salary | dept\_id |
| ------- | ---- | ------ | -------- |
| 2       | Bob  | NULL   | 20       |

---

## 3. Detect invalid or negative values

### Q4: Employees with negative salary

```sql
SELECT * FROM employees WHERE salary < 0;
```

**Output:**

| emp\_id | name  | salary | dept\_id |
| ------- | ----- | ------ | -------- |
| 4       | David | -45000 | 10       |

### Q5: Employees with salary outside valid range (e.g., <0 or >100000)

```sql
SELECT * FROM employees WHERE salary < 0 OR salary > 100000;
```

**Output:**

| emp\_id | name  | salary | dept\_id |
| ------- | ----- | ------ | -------- |
| 4       | David | -45000 | 10       |

---

## 4. Identify orphan records (FK violations)

### Q6: Employees with invalid department

```sql
SELECT * FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id
WHERE d.dept_id IS NULL;
```

**Output:**

| emp\_id | name    | salary | dept\_id |
| ------- | ------- | ------ | -------- |
| 3       | Charlie | 55000  | NULL     |

### Q7: Employees not assigned to a valid department

```sql
SELECT * FROM employees WHERE dept_id NOT IN (SELECT dept_id FROM departments);
```

**Output:**

| emp\_id | name    | salary | dept\_id |
| ------- | ------- | ------ | -------- |
| 3       | Charlie | 55000  | NULL     |

---

## 5. Combined checks

### Q8: Detect NULLs or negative salaries

```sql
SELECT * FROM employees WHERE salary IS NULL OR salary < 0;
```

**Output:**

| emp\_id | name  | salary | dept\_id |
| ------- | ----- | ------ | -------- |
| 2       | Bob   | NULL   | 20       |
| 4       | David | -45000 | 10       |

### Q9: Employees with NULL dept\_id or invalid department

```sql
SELECT * FROM employees e
WHERE dept_id IS NULL OR dept_id NOT IN (SELECT dept_id FROM departments);
```

**Output:**

| emp\_id | name    | salary | dept\_id |
| ------- | ------- | ------ | -------- |
| 3       | Charlie | 55000  | NULL     |

### Q10: Detect all data issues

```sql
SELECT * FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id
WHERE salary IS NULL OR salary < 0 OR d.dept_id IS NULL;
```

**Output:**

| emp\_id | name    | salary | dept\_id |
| ------- | ------- | ------ | -------- |
| 2       | Bob     | NULL   | 20       |
| 3       | Charlie | 55000  | NULL     |
| 4       | David   | -45000 | 10       |

---

### Explanation:

1. **NULL checks**: Detect missing values.
2. **Negative or invalid values**: Ensure business rules for numeric fields.
3. **Orphan records**: Detect foreign key violations (departments missing).

---

**Use case in ETL Testing:**

* Ensures data quality and integrity before loading into target.
* Detects anomalies like missing keys, invalid values, or broken relationships.
* Helps prevent downstream errors in analytics or reporting.
