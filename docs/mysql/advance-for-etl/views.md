# SQL Practice: Performance / Index Considerations for ETL Testing

This file contains **5 SQL practice problems** covering:

* Using EXPLAIN PLAN to understand query execution
* Identify heavy queries
* Index usage

Each question includes:

* Input Table(s)
* Question
* SQL Query / Commands
* Explanation
* Output / Expected Result

---

## 1. EXPLAIN PLAN for simple SELECT

### Q1: Analyze query execution for employee selection

**Input Table: employees**

| emp\_id | name    | dept\_id | salary |
| ------- | ------- | -------- | ------ |
| 1       | Alice   | 10       | 50000  |
| 2       | Bob     | 20       | 60000  |
| 3       | Charlie | 10       | 55000  |

**Query:**

```sql
EXPLAIN PLAN FOR
SELECT * FROM employees WHERE dept_id = 10;
```

**Explanation:**

* `EXPLAIN PLAN` shows how the database executes a query.
* Helps identify if indexes are being used.
* ETL use case: Ensure queries on large staging tables are optimized.

**Output / Result:**

* Shows full table scan or index usage depending on table structure.

---

## 2. Create Index and Test Performance

### Q2: Add index on dept\_id to improve query

**Query:**

```sql
CREATE INDEX idx_dept_id ON employees(dept_id);
SELECT * FROM employees WHERE dept_id = 10;
```

**Explanation:**

* Index improves performance on WHERE filters.
* ETL use case: Optimized queries in large source/target tables.

**Output:**

* Faster execution compared to full table scan.

---

## 3. Identify Heavy Query Using EXPLAIN PLAN

### Q3: Join query on large tables

**Input Tables:**

* employees (1M rows)
* departments (100 rows)

**Query:**

```sql
EXPLAIN PLAN FOR
SELECT e.name, d.dept_name
FROM employees e
JOIN departments d ON e.dept_id = d.dept_id;
```

**Explanation:**

* EXPLAIN PLAN shows estimated rows, join type, cost.
* Helps detect if query is heavy before running in ETL.

**Output / Result:**

* Details of join order, estimated cost, potential need for indexes.

---

## 4. Detect Queries Without Indexes

### Q4: Check if a query uses index

**Query:**

```sql
SELECT * FROM employees WHERE salary > 50000;
```

**Explanation:**

* If no index on salary, query may perform full table scan.
* ETL use case: Avoid heavy queries in large data loads.

**Output / Result:**

* Execution plan indicates full table scan.
* Recommendation: Create index if this query is frequent.

---

## 5. Identify and Optimize Heavy Queries

### Q5: Aggregation on large table

**Query:**

```sql
EXPLAIN PLAN FOR
SELECT dept_id, COUNT(*) AS emp_count, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept_id;
```

**Explanation:**

* EXPLAIN PLAN shows aggregation cost.
* Using indexes or partitioning may improve performance.
* ETL use case: Validate that aggregate queries are efficient for staging to target comparisons.

**Output / Result:**

* Execution plan with row estimates, table access type, and cost.
* Helps ETL testers identify bottlen
