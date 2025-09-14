# Data Manipulation Language (DML) in SQL

## 🔹 What is DML?
DML commands are used to **manipulate and manage the data** stored inside database tables.  
Unlike DDL, which defines the schema, **DML works on the actual rows (records)** inside the tables.

---

## 🔹 Key DML Commands (in depth)

### 1. INSERT
- Adds new records into a table.
```sql
INSERT INTO Employee (EmpID, Name, Salary)
VALUES (101, 'Amit Sharma', 55000.00);
```

### 2. UPDATE
- Modifies existing records.
```sql
UPDATE Employee
SET Salary = Salary + 5000
WHERE EmpID = 101;
```

### 3. DELETE
- Removes records from a table.
```sql
DELETE FROM Employee WHERE EmpID = 101;
```

### 4. MERGE (UPSERT)
- Combines INSERT + UPDATE + DELETE in one.
```sql
MERGE INTO Employee AS E
USING NewEmployee AS N
ON (E.EmpID = N.EmpID)
WHEN MATCHED THEN
    UPDATE SET E.Salary = N.Salary
WHEN NOT MATCHED THEN
    INSERT (EmpID, Name, Salary) VALUES (N.EmpID, N.Name, N.Salary);
```

---

## 🔹 Pros & Cons of DML

### ✅ Pros
1. **Direct Data Control** → Can manipulate specific rows.  
2. **Flexible** → SELECT with filters, joins, aggregations.  
3. **Transaction Safe** → Rollback possible.  
4. **Granular** → Row-level operations.

### ❌ Cons
1. **Data Loss Risk** → UPDATE/DELETE without WHERE affects all rows.  
2. **Performance Issues** → Large queries slow performance.  
3. **Locking Problems** → Concurrent transactions may cause locks.  
4. **Index Dependency** → Without indexes, queries may be slow.

---

## ✅ Summary Table

| Command   | Purpose                     | Rollback Possible | Example Usage            |
|-----------|-----------------------------|------------------|--------------------------|
| INSERT    | Add new records              | ✅ Yes           | Add employee             |
| UPDATE    | Modify existing records      | ✅ Yes           | Increase salary          |
| DELETE    | Remove records               | ✅ Yes           | Delete inactive employee |
| MERGE     | Insert/Update/Delete in one  | ✅ Yes           | Sync staging & prod data |

---

## 📊 DML Commands – Feature Comparison

| Command   | Rollback | Data Loss Risk | Structure Change | Typical Use Case          |
|-----------|----------|----------------|------------------|---------------------------|
| INSERT    | ✅ Yes   | ❌ No           | ❌ No            | Add new data              |
| UPDATE    | ✅ Yes   | ⚠️ Yes          | ❌ No            | Modify existing data      |
| DELETE    | ✅ Yes   | ⚠️ Yes          | ❌ No            | Remove rows               |
| MERGE     | ✅ Yes   | ⚠️ Possible     | ❌ No            | Sync datasets efficiently |
