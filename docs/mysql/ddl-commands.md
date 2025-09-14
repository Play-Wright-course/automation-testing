# Data Definition Language (DDL) in SQL

## 🔹 What is DDL?
DDL commands are used to **define, modify, and manage the structure** of database objects (like tables, views, schemas, indexes).  

These commands **work at the schema level** (structure), not on individual rows of data.  

---

## 🔹 Key DDL Commands (in depth)

### 1. CREATE
- Used to create **database objects** such as tables, schemas, views, or indexes.  
- You must define the structure (columns, data types, constraints).  

**Example**  
```sql
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Salary DECIMAL(10,2) CHECK (Salary > 0),
    DepartmentID INT,
    HireDate DATE DEFAULT CURRENT_DATE
);
```

---

### 2. ALTER
- Used to **modify existing objects** (add/remove/rename columns, change data types, add constraints).  

**Example**  
```sql
-- Add a new column
ALTER TABLE Employee ADD Age INT;

-- Modify column type
ALTER TABLE Employee MODIFY Salary DECIMAL(12,2);

-- Drop a column
ALTER TABLE Employee DROP COLUMN Age;

-- Add a foreign key
ALTER TABLE Employee
ADD CONSTRAINT fk_dept FOREIGN KEY (DepartmentID) REFERENCES Department(DeptID);
```

---

### 3. DROP
- Deletes a database object completely (table, view, database, index).  
- ⚠️ Removes structure **and** all data.  

**Example**  
```sql
DROP TABLE Employee;
DROP DATABASE HR;
```

---

### 4. TRUNCATE
- Removes **all rows** from a table, but keeps the structure.  
- Much faster than `DELETE` (no logging of each row).  
- Cannot be rolled back in some DBs.  

**Example**  
```sql
TRUNCATE TABLE Employee;
```

---

### 5. RENAME
- Renames a database object (varies slightly across RDBMS).  

**Example** (MySQL / Oracle)  
```sql
RENAME TABLE Employee TO Staff;
```

---

### 6. COMMENT
- Add descriptions to database objects. (Supported in Oracle, PostgreSQL, etc.)  

**Example**  
```sql
COMMENT ON TABLE Employee IS 'Stores employee details';
COMMENT ON COLUMN Employee.Salary IS 'Monthly Salary in INR';
```

---

## 🔹 Pros & Cons of DDL

### ✅ Pros
1. **Schema Control** → DDL provides strong control over database design (tables, keys, indexes).  
2. **Integrity Enforcement** → Constraints (`PRIMARY KEY`, `FOREIGN KEY`, `CHECK`) ensure data accuracy.  
3. **Performance** → With indexes and partitions defined via DDL, queries become faster.  
4. **Automation Friendly** → You can version-control DDL scripts for CI/CD pipelines.  
5. **Flexibility** → Easily modify structures as business needs evolve.  

---

### ❌ Cons
1. **Destructive Nature**  
   - `DROP` and `TRUNCATE` permanently remove data (can’t easily rollback).  
   - Small mistake → huge data loss.  

2. **Locking Issues**  
   - Some DDL operations lock tables (no read/write allowed until completed).  

3. **Dependent Objects**  
   - Dropping/altering tables can break views, stored procedures, or queries that depend on them.  

4. **Environment Differences**  
   - Syntax varies across RDBMS (MySQL, Oracle, PostgreSQL). Example: `ALTER` column syntax differs.  

5. **Not Transaction-Safe (in some DBs)**  
   - In MySQL, some DDL operations auto-commit → cannot be rolled back.  

---

## ✅ Summary Table

| Command  | Purpose | Notes |
|----------|---------|-------|
| **CREATE** | Define new objects (tables, views, indexes) | Requires schema definition |
| **ALTER** | Modify structure of objects | Add/remove/modify columns & constraints |
| **DROP** | Delete objects permanently | Removes both structure & data |
| **TRUNCATE** | Delete all rows but keep structure | Faster than DELETE, limited rollback |
| **RENAME** | Rename objects | Syntax varies by DB |
| **COMMENT** | Add documentation | Useful for metadata |
