# SQL Practice: Set Operators with Explanations

This file contains **15 SQL practice problems** covering:

* UNION / UNION ALL
* INTERSECT
* MINUS / EXCEPT

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. UNION

### Q1: Combine employees from two departments

**Input Tables:**
**dept\_hr**

| emp\_id | name  |
| ------- | ----- |
| 1       | Alice |
| 2       | Bob   |

**dept\_it**

| emp\_id | name    |
| ------- | ------- |
| 3       | Charlie |
| 4       | David   |

**Query:**

```sql
SELECT name FROM dept_hr
UNION
SELECT name FROM dept_it;
```

**Explanation:**
UNION combines results and removes duplicates.

**Output:**

| name    |
| ------- |
| Alice   |
| Bob     |
| Charlie |
| David   |

---

### Q2: UNION ALL (keep duplicates)

**Input Tables:**
**dept\_sales**

| emp\_id | name  |
| ------- | ----- |
| 5       | Eve   |
| 6       | Frank |

**dept\_marketing**

| emp\_id | name  |
| ------- | ----- |
| 6       | Frank |
| 7       | Grace |

```sql
SELECT name FROM dept_sales
UNION ALL
SELECT name FROM dept_marketing;
```

**Output:**

| name  |
| ----- |
| Eve   |
| Frank |
| Frank |
| Grace |

---

## 2. INTERSECT

### Q3: Employees present in both departments

**Input Tables:**
**dept\_a**

| emp\_id | name    |
| ------- | ------- |
| 1       | Alice   |
| 2       | Bob     |
| 3       | Charlie |

**dept\_b**

| emp\_id | name    |
| ------- | ------- |
| 2       | Bob     |
| 3       | Charlie |
| 4       | David   |

```sql
SELECT name FROM dept_a
INTERSECT
SELECT name FROM dept_b;
```

**Explanation:**
INTERSECT returns only rows present in both tables.

**Output:**

| name    |
| ------- |
| Bob     |
| Charlie |

---

### Q4: INTERSECT multiple conditions

```sql
SELECT emp_id, name FROM dept_a
INTERSECT
SELECT emp_id, name FROM dept_b;
```

**Output:**

| emp\_id | name    |
| ------- | ------- |
| 2       | Bob     |
| 3       | Charlie |

---

## 3. MINUS / EXCEPT

### Q5: Employees in dept\_a but not in dept\_b

```sql
SELECT name FROM dept_a
MINUS
SELECT name FROM dept_b; -- Oracle
-- EXCEPT in SQL Server
```

**Output:**

| name  |
| ----- |
| Alice |

---

### Q6: Employees in dept\_b but not in dept\_a

```sql
SELECT name FROM dept_b
MINUS
SELECT name FROM dept_a;
```

**Output:**

| name  |
| ----- |
| David |

---

### Q7: UNION and MINUS combined

**Input Tables:**
**dept\_x**

| emp\_id | name  |
| ------- | ----- |
| 1       | Alice |
| 2       | Bob   |

**dept\_y**

| emp\_id | name    |
| ------- | ------- |
| 2       | Bob     |
| 3       | Charlie |

```sql
SELECT name FROM (
  SELECT name FROM dept_x
  UNION
  SELECT name FROM dept_y
) combined
MINUS
SELECT name FROM dept_x;
```

**Explanation:**
Combine both tables, then remove names already in dept\_x.

**Output:**

| name    |
| ------- |
| Charlie |

---

### Q8: Check mismatched records between source and target

**Input Tables:**
**source\_employees**

| emp\_id | name    |
| ------- | ------- |
| 1       | Alice   |
| 2       | Bob     |
| 3       | Charlie |

**target\_employees**

| emp\_id | name    |
| ------- | ------- |
| 2       | Bob     |
| 3       | Charlie |
| 4       | David   |

```sql
SELECT name FROM source_employees
MINUS
SELECT name FROM target_employees;
```

**Output:**

| name  |
| ----- |
| Alice |

---

### Q9: EXCEPT example (SQL Server)

```sql
SELECT name FROM target_employees
EXCEPT
SELECT name FROM source_employees;
```

**Output:**

| name  |
| ----- |
| David |

---

### Q10: Find common employees and unique employees in one query

```sql
SELECT name FROM source_employees
INTERSECT
SELECT name FROM target_employees; -- common

SELECT name FROM source_employees
MINUS
SELECT name FROM target_employees; -- in source only

SELECT name FROM target_employees
MINUS
SELECT name FROM source_employees; -- in target only
```

**Output:**
**Common:**

| name    |
| ------- |
| Bob     |
| Charlie |

**Source only:**

| name  |
| ----- |
| Alice |

**Target only:**

| name  |
| ----- |
| David |
