# SQL Practice: Data Type Conversions with Explanations

This file contains **15 SQL practice problems** covering:

* CAST() and CONVERT()
* Implicit vs Explicit conversion

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. Input Table Example

**Table: employees**

| emp\_id | name    | salary | join\_date |
| ------- | ------- | ------ | ---------- |
| 1       | Alice   | 48000  | 2025-01-10 |
| 2       | Bob     | 60000  | 2024-12-15 |
| 3       | Charlie | 55000  | 2025-03-01 |
| 4       | David   | 45000  | 2025-02-20 |
| 5       | Eva     | 70000  | 2024-11-05 |

---

## 2. CAST() / CONVERT() Examples

### Q1: Convert salary to string

```sql
SELECT emp_id, name, CAST(salary AS VARCHAR(10)) AS salary_str
FROM employees;
```

**Output:**

| emp\_id | name    | salary\_str |
| ------- | ------- | ----------- |
| 1       | Alice   | 48000       |
| 2       | Bob     | 60000       |
| 3       | Charlie | 55000       |
| 4       | David   | 45000       |
| 5       | Eva     | 70000       |

### Q2: Convert join\_date to string

```sql
SELECT emp_id, name, CONVERT(VARCHAR(10), join_date, 120) AS join_date_str
FROM employees;
```

**Output:**

| emp\_id | name    | join\_date\_str |
| ------- | ------- | --------------- |
| 1       | Alice   | 2025-01-10      |
| 2       | Bob     | 2024-12-15      |
| 3       | Charlie | 2025-03-01      |
| 4       | David   | 2025-02-20      |
| 5       | Eva     | 2024-11-05      |

### Q3: Convert string to date

```sql
SELECT emp_id, name, CAST('2025-09-20' AS DATE) AS example_date
FROM employees;
```

**Output:**

| emp\_id | name    | example\_date |
| ------- | ------- | ------------- |
| 1       | Alice   | 2025-09-20    |
| 2       | Bob     | 2025-09-20    |
| 3       | Charlie | 2025-09-20    |
| 4       | David   | 2025-09-20    |
| 5       | Eva     | 2025-09-20    |

### Q4: Convert salary to float and calculate bonus

```sql
SELECT emp_id, name, CAST(salary AS FLOAT) * 0.10 AS bonus
FROM employees;
```

**Output:**

| emp\_id | name    | bonus |
| ------- | ------- | ----- |
| 1       | Alice   | 4800  |
| 2       | Bob     | 6000  |
| 3       | Charlie | 5500  |
| 4       | David   | 4500  |
| 5       | Eva     | 7000  |

### Q5: Implicit conversion in concatenation

```sql
SELECT emp_id, name + ' earns ' + salary AS description
FROM employees;
```

**Output:**

| emp\_id | description         |
| ------- | ------------------- |
| 1       | Alice earns 48000   |
| 2       | Bob earns 60000     |
| 3       | Charlie earns 55000 |
| 4       | David earns 45000   |
| 5       | Eva earns 70000     |

---

### Q6: Convert numeric string to integer

```sql
SELECT emp_id, name, CAST('12345' AS INT) AS num_value
FROM employees;
```

**Output:**

| emp\_id | name    | num\_value |
| ------- | ------- | ---------- |
| 1       | Alice   | 12345      |
| 2       | Bob     | 12345      |
| 3       | Charlie | 12345      |
| 4       | David   | 12345      |
| 5       | Eva     | 12345      |

### Q7: Convert date to datetime

```sql
SELECT emp_id, name, CAST(join_date AS DATETIME) AS join_datetime
FROM employees;
```

**Output:**

| emp\_id | name    | join\_datetime      |
| ------- | ------- | ------------------- |
| 1       | Alice   | 2025-01-10 00:00:00 |
| 2       | Bob     | 2024-12-15 00:00:00 |
| 3       | Charlie | 2025-03-01 00:00:00 |
| 4       | David   | 2025-02-20 00:00:00 |
| 5       | Eva     | 2024-11-05 00:00:00 |

### Q8: Convert integer to decimal

```sql
SELECT emp_id, name, CONVERT(DECIMAL(10,2), salary) AS salary_decimal
FROM employees;
```

**Output:**

| emp\_id | name    | salary\_decimal |
| ------- | ------- | --------------- |
| 1       | Alice   | 48000.00        |
| 2       | Bob     | 60000.00        |
| 3       | Charlie | 55000.00        |
| 4       | David   | 45000.00        |
| 5       | Eva     | 70000.00        |

### Q9: Implicit conversion in comparison

```sql
SELECT emp_id, name
FROM employees
WHERE salary > '50000';
```

**Output:**

| emp\_id | name    |
| ------- | ------- |
| 2       | Bob     |
| 3       | Charlie |
| 5       | Eva     |

### Q10: Convert string date to different format

```sql
SELECT emp_id, name, CONVERT(VARCHAR(10), join_date, 101) AS join_date_us
FROM employees;
```

**Output:**

| emp\_id | name    | join\_date\_us |
| ------- | ------- | -------------- |
| 1       | Alice   | 01/10/2025     |
| 2       | Bob     | 12/15/2024     |
| 3       | Charlie | 03/01/2025     |
| 4       | David   | 02/20/2025     |
| 5       | Eva     | 11/05/2024     |

---

### Explanation:

1. **CAST()** explicitly converts data from one type to another.
2. **CONVERT()** can change types and formats (especially for dates).
3. **Implicit conversion** happens automatically when data types are compatible.
4. **Explicit conversion** is safer and avoids errors in ETL.

---

**Use case in ETL Testing:**

* Verify numeric → string conversions for reporting.
* Ensure string → date conversions match target format.
* Validate ETL handles type changes correctly during t
