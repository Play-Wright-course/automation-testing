# Data Query Language (DQL) in SQL

## 🔹 What is DQL?
DQL commands are used to **retrieve data** from database tables.  
It primarily deals with queries to fetch results.

---

## 🔹 Key DQL Command

### 1. SELECT
- Fetches data from tables with conditions, joins, and aggregations.

```sql
-- Get all employees
SELECT * FROM Employee;

-- Get employees with salary > 50k
SELECT Name, Salary FROM Employee WHERE Salary > 50000;

-- Aggregation
SELECT DepartmentID, AVG(Salary) AS AvgSalary
FROM Employee
GROUP BY DepartmentID
HAVING AVG(Salary) > 50000;
```

---

## 🔹 Pros & Cons of DQL

### ✅ Pros
1. **Powerful Retrieval** → Fetch specific or aggregated data.  
2. **Flexible Queries** → Supports joins, subqueries, aggregations.  
3. **Analytics Ready** → Ideal for reporting.  
4. **Safe** → Does not modify data (read-only).

### ❌ Cons
1. **Performance Impact** → Complex queries may be slow.  
2. **Requires Indexes** → To optimize performance.  
3. **Read-only** → Cannot insert/update/delete.  
4. **Locks** → Long-running queries can block resources.

---

## ✅ Summary Table

| Command | Purpose              | Rollback Possible | Example Usage |
|---------|----------------------|------------------|---------------|
| SELECT  | Retrieve data (query)| N/A              | Get employees |

---

## 📊 DQL Command – Feature Comparison

| Command | Rollback | Data Loss | Structure Change | Typical Use Case    |
|---------|----------|-----------|------------------|---------------------|
| SELECT  | N/A      | ❌ No      | ❌ No            | Fetch rows of data  |
