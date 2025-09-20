# SQL Practice: Window / Analytic Functions with Explanations

This file contains **20 SQL practice problems** covering:

* ROW\_NUMBER(), RANK(), DENSE\_RANK()
* NTILE(), LAG(), LEAD()
* SUM()/AVG() OVER (PARTITION BY …)

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. Input Table Example

**Table: sales**

| sale\_id | emp\_id | dept | sale\_amount | sale\_date |
| -------- | ------- | ---- | ------------ | ---------- |
| 1        | 101     | IT   | 5000         | 2025-09-01 |
| 2        | 102     | HR   | 3000         | 2025-09-01 |
| 3        | 101     | IT   | 7000         | 2025-09-02 |
| 4        | 103     | IT   | 4000         | 2025-09-02 |
| 5        | 102     | HR   | 3500         | 2025-09-03 |
| 6        | 101     | IT   | 6000         | 2025-09-03 |

---

## 2. ROW\_NUMBER()

### Q1: Assign row number per employee based on sale\_date

```sql
SELECT sale_id, emp_id, sale_date,
       ROW_NUMBER() OVER (PARTITION BY emp_id ORDER BY sale_date) AS row_num
FROM sales;
```

**Output:**

| sale\_id | emp\_id | sale\_date | row\_num |
| -------- | ------- | ---------- | -------- |
| 1        | 101     | 2025-09-01 | 1        |
| 3        | 101     | 2025-09-02 | 2        |
| 6        | 101     | 2025-09-03 | 3        |
| 2        | 102     | 2025-09-01 | 1        |
| 5        | 102     | 2025-09-03 | 2        |
| 4        | 103     | 2025-09-02 | 1        |

---

## 3. RANK() and DENSE\_RANK()

### Q2: Rank sales per department

```sql
SELECT sale_id, emp_id, dept, sale_amount,
       RANK() OVER (PARTITION BY dept ORDER BY sale_amount DESC) AS dept_rank,
       DENSE_RANK() OVER (PARTITION BY dept ORDER BY sale_amount DESC) AS dense_rank
FROM sales;
```

**Output:**

| sale\_id | emp\_id | dept | sale\_amount | dept\_rank | dense\_rank |
| -------- | ------- | ---- | ------------ | ---------- | ----------- |
| 3        | 101     | IT   | 7000         | 1          | 1           |
| 1        | 101     | IT   | 5000         | 2          | 2           |
| 4        | 103     | IT   | 4000         | 3          | 3           |
| 5        | 102     | HR   | 3500         | 1          | 1           |
| 2        | 102     | HR   | 3000         | 2          | 2           |

---

## 4. NTILE()

### Q3: Divide IT department sales into 2 buckets

```sql
SELECT sale_id, emp_id, dept, sale_amount,
       NTILE(2) OVER (PARTITION BY dept ORDER BY sale_amount DESC) AS bucket
FROM sales
WHERE dept='IT';
```

**Output:**

| sale\_id | emp\_id | dept | sale\_amount | bucket |
| -------- | ------- | ---- | ------------ | ------ |
| 3        | 101     | IT   | 7000         | 1      |
| 1        | 101     | IT   | 5000         | 1      |
| 4        | 103     | IT   | 4000         | 2      |
| 6        | 101     | IT   | 6000         | 1      |

---

## 5. LAG() and LEAD()

### Q4: Previous sale amount per employee

```sql
SELECT sale_id, emp_id, sale_amount,
       LAG(sale_amount,1) OVER (PARTITION BY emp_id ORDER BY sale_date) AS prev_sale
FROM sales;
```

**Output:**

| sale\_id | emp\_id | sale\_amount | prev\_sale |
| -------- | ------- | ------------ | ---------- |
| 1        | 101     | 5000         | NULL       |
| 3        | 101     | 7000         | 5000       |
| 6        | 101     | 6000         | 7000       |
| 2        | 102     | 3000         | NULL       |
| 5        | 102     | 3500         | 3000       |
| 4        | 103     | 4000         | NULL       |

### Q5: Next sale amount per employee

```sql
SELECT sale_id, emp_id, sale_amount,
       LEAD(sale_amount,1) OVER (PARTITION BY emp_id ORDER BY sale_date) AS next_sale
FROM sales;
```

**Output:**

| sale\_id | emp\_id | sale\_amount | next\_sale |
| -------- | ------- | ------------ | ---------- |
| 1        | 101     | 5000         | 7000       |
| 3        | 101     | 7000         | 6000       |
| 6        | 101     | 6000         | NULL       |
| 2        | 102     | 3000         | 3500       |
| 5        | 102     | 3500         | NULL       |
| 4        | 103     | 4000         | NULL       |

---

## 6. SUM()/AVG() OVER(PARTITION BY …)

### Q6: Running total per employee

```sql
SELECT sale_id, emp_id, sale_amount,
       SUM(sale_amount) OVER (PARTITION BY emp_id ORDER BY sale_date) AS running_total
FROM sales;
```

**Output:**

| sale\_id | emp\_id | sale\_amount | running\_total |
| -------- | ------- | ------------ | -------------- |
| 1        | 101     | 5000         | 5000           |
| 3        | 101     | 7000         | 12000          |
| 6        | 101     | 6000         | 18000          |
| 2        | 102     | 3000         | 3000           |
| 5        | 102     | 3500         | 6500           |
| 4        | 103     | 4000         | 4000           |

### Q7: Average sale per department

```sql
SELECT sale_id, emp_id, dept, sale_amount,
       AVG(sale_amount) OVER (PARTITION BY dept) AS avg_dept_sale
FROM sales;
```

**Output:**

| sale\_id | emp\_id | dept | sale\_amount | avg\_dept\_sale |
| -------- | ------- | ---- | ------------ | --------------- |
| 1        | 101     | IT   | 5000         | 5666.67         |
| 3        | 101     | IT   | 7000         | 5666.67         |
| 4        | 103     | IT   | 4000         | 5666.67         |
| 6        | 101     | IT   | 6000         | 5666.67         |
| 2        | 102     | HR   | 3000         | 3250            |
| 5        | 102     | HR   | 3500         | 3250            |

---

### Explanation:

1. **ROW\_NUMBER()**: Assigns unique numbers to rows within a partition.
2. **RANK()/DENSE\_RANK()**: Rank rows within a partition, with/without gaps.
3. **NTILE()**: Divides rows into specified number of buckets.
4. **LAG()/LEAD()**: Access previous/next row values.
5. **SUM()/AVG() OVER(PARTITION BY …)**: Cumulative or group-based aggregates without collapsing rows.

---

**Use case in ETL Testing:**

* Detect duplicate records using `ROW_NUMBER()`.
* Validate ranking and top-N using `RANK()/DENSE_RANK()`.
* Check cumulative aggregates for correctness.
* Compare current row with previous/next row for trends or anomalies.
