# SQL Practice: Pivot / Unpivot with Explanations

This file contains **15 SQL practice problems** covering:

* PIVOT (convert rows to columns)
* UNPIVOT (convert columns to rows)

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. Input Table Example

**Table: sales\_data**

| emp\_id | dept | month | sales\_amount |
| ------- | ---- | ----- | ------------- |
| 101     | IT   | Jan   | 5000          |
| 101     | IT   | Feb   | 6000          |
| 102     | HR   | Jan   | 3000          |
| 102     | HR   | Feb   | 3500          |
| 103     | IT   | Jan   | 4000          |
| 103     | IT   | Feb   | 4500          |

---

## 2. PIVOT Examples

### Q1: Pivot sales per employee for each month

```sql
SELECT emp_id, [Jan], [Feb]
FROM (
    SELECT emp_id, month, sales_amount
    FROM sales_data
) src
PIVOT (
    SUM(sales_amount) FOR month IN ([Jan], [Feb])
) pvt;
```

**Output:**

| emp\_id | Jan  | Feb  |
| ------- | ---- | ---- |
| 101     | 5000 | 6000 |
| 102     | 3000 | 3500 |
| 103     | 4000 | 4500 |

### Q2: Pivot sales per department per month

```sql
SELECT dept, [Jan], [Feb]
FROM (
    SELECT dept, month, sales_amount
    FROM sales_data
) src
PIVOT (
    SUM(sales_amount) FOR month IN ([Jan], [Feb])
) pvt;
```

**Output:**

| dept | Jan  | Feb   |
| ---- | ---- | ----- |
| IT   | 9000 | 10500 |
| HR   | 3000 | 3500  |

### Q3: Pivot using CASE for months (alternative)

```sql
SELECT emp_id,
       SUM(CASE WHEN month='Jan' THEN sales_amount ELSE 0 END) AS Jan,
       SUM(CASE WHEN month='Feb' THEN sales_amount ELSE 0 END) AS Feb
FROM sales_data
GROUP BY emp_id;
```

**Output:**

| emp\_id | Jan  | Feb  |
| ------- | ---- | ---- |
| 101     | 5000 | 6000 |
| 102     | 3000 | 3500 |
| 103     | 4000 | 4500 |

### Q4: Pivot sales for IT department only

```sql
SELECT emp_id, [Jan], [Feb]
FROM (
    SELECT emp_id, month, sales_amount
    FROM sales_data
    WHERE dept='IT'
) src
PIVOT (
    SUM(sales_amount) FOR month IN ([Jan], [Feb])
) pvt;
```

**Output:**

| emp\_id | Jan  | Feb  |
| ------- | ---- | ---- |
| 101     | 5000 | 6000 |
| 103     | 4000 | 4500 |

### Q5: Pivot with dynamic aggregation by department and month

```sql
SELECT dept, [Jan], [Feb]
FROM (
    SELECT dept, month, sales_amount
    FROM sales_data
) src
PIVOT (
    SUM(sales_amount) FOR month IN ([Jan], [Feb])
) pvt;
```

**Output:**

| dept | Jan  | Feb   |
| ---- | ---- | ----- |
| IT   | 9000 | 10500 |
| HR   | 3000 | 3500  |

---

## 3. UNPIVOT Examples

### Q6: Unpivot columns Jan and Feb into rows

```sql
SELECT emp_id, month, sales_amount
FROM (
    SELECT emp_id, [Jan], [Feb]
    FROM (
        SELECT emp_id, month, sales_amount
        FROM sales_data
    ) src
    PIVOT (
        SUM(sales_amount) FOR month IN ([Jan], [Feb])
    ) pvt
) unpvt
UNPIVOT (
    sales_amount FOR month IN ([Jan], [Feb])
) AS unp;
```

**Output:**

| emp\_id | month | sales\_amount |
| ------- | ----- | ------------- |
| 101     | Jan   | 5000          |
| 101     | Feb   | 6000          |
| 102     | Jan   | 3000          |
| 102     | Feb   | 3500          |
| 103     | Jan   | 4000          |
| 103     | Feb   | 4500          |

### Q7: Unpivot department sales per month

```sql
SELECT month, dept, sales_amount
FROM (
    SELECT dept, [Jan], [Feb]
    FROM (
        SELECT dept, month, sales_amount FROM sales_data
    ) src
    PIVOT (SUM(sales_amount) FOR month IN ([Jan], [Feb])) pvt
) unpvt
UNPIVOT (
    sales_amount FOR month IN ([Jan], [Feb])
) AS u;
```

**Output:**

| month | dept | sales\_amount |
| ----- | ---- | ------------- |
| Jan   | IT   | 9000          |
| Feb   | IT   | 10500         |
| Jan   | HR   | 3000          |
| Feb   | HR   | 3500          |

### Q8: Unpivot for a single employee

```sql
SELECT emp_id, month, sales_amount
FROM (
    SELECT emp_id, [Jan], [Feb]
    FROM (
        SELECT emp_id, month, sales_amount FROM sales_data
        WHERE emp_id=101
    ) src
    PIVOT (SUM(sales_amount) FOR month IN ([Jan], [Feb])) pvt
) unpvt
UNPIVOT (
    sales_amount FOR month IN ([Jan], [Feb])
) AS u;
```

**Output:**

| emp\_id | month | sales\_amount |
| ------- | ----- | ------------- |
| 101     | Jan   | 5000          |
| 101     | Feb   | 6000          |

### Q9: Unpivot to calculate monthly totals

```sql
SELECT month, SUM(sales_amount) AS total_sales
FROM (
    SELECT emp_id, [Jan], [Feb]
    FROM (
        SELECT emp_id, month, sales_amount FROM sales_data
    ) src
    PIVOT (SUM(sales_amount) FOR month IN ([Jan], [Feb])) pvt
) unpvt
UNPIVOT (
    sales_amount FOR month IN ([Jan], [Feb])
) AS u
GROUP BY month;
```

**Output:**

| month | total\_sales |
| ----- | ------------ |
| Jan   | 12000        |
| Feb   | 14000        |

### Q10: Alternative UNPIVOT using UNION ALL

```sql
SELECT emp_id, 'Jan' AS month, [Jan] AS sales_amount FROM (
    SELECT emp_id, month, sales_amount FROM sales_data
) src
PIVOT (SUM(sales_amount) FOR month IN ([Jan], [Feb])) pvt
UNION ALL
SELECT emp_id, 'Feb', [Feb] FROM (
    SELECT emp_id, month, sales_amount FROM sales_data
) src
PIVOT (SUM(sales_amount) FOR month IN ([Jan], [Feb])) pvt;
```

**Output:** Same as previous unpivot examples.

---

### Explanation:

1. **PIVOT** transforms rows into columns, useful to reshape data for reporting.
2. **UNPIVOT** transforms columns into rows, useful for normalization or comparison.
3. Both are helpful in **ETL testing** to validate reshaped warehouse data matches source data.

---

**Use case in ETL Testing:**

* Validate that monthly sales totals pivot correctly per employee or department.
* Compare reshaped data with raw transactional data.
* Transform wide tables to long tables or vice versa for reporting or downstream processing.
