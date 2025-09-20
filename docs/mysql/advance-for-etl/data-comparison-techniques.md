# SQL Practice: Validation Queries / Data Comparison Techniques with Explanations

This file contains **15 SQL practice problems** covering:

* Check for missing or extra records between source and target
* Validate record counts per key or per group
* Identify duplicates
* Compare aggregates (SUM, AVG) between source and target

Each question includes:

* Input Table(s)
* Question
* SQL Query
* Explanation
* Output Table

---

## 1. Input Table Examples

**Table: source\_orders**

| order\_id | customer\_id | amount |
| --------- | ------------ | ------ |
| 101       | 1            | 500    |
| 102       | 2            | 600    |
| 103       | 3            | 700    |
| 104       | 4            | 800    |

**Table: target\_orders**

| order\_id | customer\_id | amount |
| --------- | ------------ | ------ |
| 101       | 1            | 500    |
| 102       | 2            | 600    |
| 104       | 4            | 800    |
| 105       | 5            | 900    |

---

## 2. Check for missing records in target

### Q1: Identify source orders missing in target

```sql
SELECT *
FROM source_orders s
WHERE NOT EXISTS (
    SELECT 1 FROM target_orders t WHERE s.order_id = t.order_id
);
```

**Output:**

| order\_id | customer\_id | amount |
| --------- | ------------ | ------ |
| 103       | 3            | 700    |

### Q2: Identify extra records in target

```sql
SELECT *
FROM target_orders t
WHERE NOT EXISTS (
    SELECT 1 FROM source_orders s WHERE t.order_id = s.order_id
);
```

**Output:**

| order\_id | customer\_id | amount |
| --------- | ------------ | ------ |
| 105       | 5            | 900    |

---

## 3. Validate record counts per key/group

### Q3: Count orders per customer in source

```sql
SELECT customer_id, COUNT(*) AS order_count
FROM source_orders
GROUP BY customer_id;
```

**Output:**

| customer\_id | order\_count |
| ------------ | ------------ |
| 1            | 1            |
| 2            | 1            |
| 3            | 1            |
| 4            | 1            |

### Q4: Compare counts between source and target

```sql
SELECT s.customer_id, COUNT(s.order_id) AS src_count, COUNT(t.order_id) AS tgt_count
FROM source_orders s
LEFT JOIN target_orders t ON s.order_id = t.order_id
GROUP BY s.customer_id;
```

**Output:**

| customer\_id | src\_count | tgt\_count |
| ------------ | ---------- | ---------- |
| 1            | 1          | 1          |
| 2            | 1          | 1          |
| 3            | 1          | 0          |
| 4            | 1          | 1          |

---

## 4. Identify duplicates

### Q5: Find duplicate orders in source

```sql
SELECT order_id, COUNT(*) AS cnt
FROM source_orders
GROUP BY order_id
HAVING COUNT(*) > 1;
```

**Output:**

| order\_id           | cnt |
| ------------------- | --- |
| -- No duplicates -- |     |

### Q6: Find duplicate customer entries in target

```sql
SELECT customer_id, COUNT(*) AS cnt
FROM target_orders
GROUP BY customer_id
HAVING COUNT(*) > 1;
```

**Output:**

| customer\_id        | cnt |
| ------------------- | --- |
| -- No duplicates -- |     |

---

## 5. Compare aggregates (SUM, AVG)

### Q7: Total sales amount source vs target

```sql
SELECT SUM(amount) AS source_total FROM source_orders;
SELECT SUM(amount) AS target_total FROM target_orders;
```

**Output:**

| source\_total | target\_total |
| ------------- | ------------- |
| 2600          | 2300          |

### Q8: Average order amount comparison

```sql
SELECT AVG(amount) AS avg_source FROM source_orders;
SELECT AVG(amount) AS avg_target FROM target_orders;
```

**Output:**

| avg\_source | avg\_target |
| ----------- | ----------- |
| 650         | 766.67      |

### Q9: Compare per customer amount

```sql
SELECT s.customer_id, s.amount AS source_amount, t.amount AS target_amount
FROM source_orders s
LEFT JOIN target_orders t ON s.order_id = t.order_id;
```

**Output:**

| customer\_id | source\_amount | target\_amount |
| ------------ | -------------- | -------------- |
| 1            | 500            | 500            |
| 2            | 600            | 600            |
| 3            | 700            | NULL           |
| 4            | 800            | 800            |

### Q10: Validate sum per customer group

```sql
SELECT s.customer_id, SUM(s.amount) AS src_sum, SUM(t.amount) AS tgt_sum
FROM source_orders s
LEFT JOIN target_orders t ON s.order_id = t.order_id
GROUP BY s.customer_id;
```

**Output:**

| customer\_id | src\_sum | tgt\_sum |
| ------------ | -------- | -------- |
| 1            | 500      | 500      |
| 2            | 600      | 600      |
| 3            | 700      | NULL     |
| 4            | 800      | 800      |

---

### Explanation:

1. **Missing/Extra Records:** Identifies discrepancies between source and target.
2. **Record Counts:** Ensures no loss or duplication in ETL.
3. **Duplicates:** Detects incorrect multiple entries.
4. **Aggregate Comparisons:** Checks that sums and averages match expectations.

---

**Use case in ETL Testing:**

* Core ETL validation: ensure completeness, accuracy, and consistency of transformed data.
* Compare source and target tables for all key metrics.
* Detect and resolve anomalies before loading
