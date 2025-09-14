# SQL Commands: DDL, DML, DQL, TCL, DCL

## 📌 Types of SQL Commands  

SQL commands are divided into **5 main categories**:  

---

## 1. DDL (Data Definition Language)  
👉 Used to define and manage the structure of the database (tables, schemas, indexes).  

### Commands:  
- `CREATE` → Create new objects (table, view, database, etc.)  
- `ALTER` → Modify structure of existing objects  
- `DROP` → Delete objects  
- `TRUNCATE` → Remove all rows from a table (faster than DELETE, no rollback in some DBs)  
- `COMMENT` → Add comments to schema objects  
- `RENAME` → Rename objects  

### Example  
```sql
-- Create a new table
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(50),
    Salary DECIMAL(10,2),
    Department VARCHAR(30)
);

-- Alter the table
ALTER TABLE Employee ADD Age INT;

-- Drop the table
DROP TABLE Employee;

-- Remove all records but keep structure
TRUNCATE TABLE Employee;
```

---

## 2. DML (Data Manipulation Language)  
👉 Used to manage and modify the data inside tables.  

### Commands:  
- `INSERT` → Insert new records  
- `UPDATE` → Modify existing records  
- `DELETE` → Remove records  
- `MERGE` (in some DBs) → Insert/Update simultaneously  

### Example  
```sql
-- Insert data
INSERT INTO Employee (EmpID, Name, Salary, Department, Age)
VALUES (101, 'John Doe', 55000, 'IT', 28);

-- Update data
UPDATE Employee
SET Salary = 60000
WHERE EmpID = 101;

-- Delete a record
DELETE FROM Employee WHERE EmpID = 101;
```

---

## 3. DQL (Data Query Language)  
👉 Used to fetch/query data from database.  

### Command:  
- `SELECT`  

### Example  
```sql
-- Select all data
SELECT * FROM Employee;

-- Select specific columns
SELECT Name, Salary FROM Employee;

-- Select with condition
SELECT * FROM Employee WHERE Department = 'IT';
```

---

## 4. TCL (Transaction Control Language)  
👉 Used to manage transactions (groups of SQL statements).  

### Commands:  
- `COMMIT` → Save changes permanently  
- `ROLLBACK` → Undo changes  
- `SAVEPOINT` → Set a point to rollback later  
- `SET TRANSACTION` → Set transaction properties  

### Example  
```sql
BEGIN TRANSACTION;

UPDATE Employee SET Salary = Salary + 5000 WHERE Department = 'IT';

-- If everything is fine
COMMIT;

-- If error, rollback
ROLLBACK;
```

---

## 5. DCL (Data Control Language)  
👉 Used to control access (security/permissions).  

### Commands:  
- `GRANT` → Give permissions  
- `REVOKE` → Take back permissions  

### Example  
```sql
-- Grant permission
GRANT SELECT, INSERT ON Employee TO user1;

-- Revoke permission
REVOKE INSERT ON Employee FROM user1;
```

---

## ✅ Quick Summary Table  

| Type | Full Form | Purpose | Examples |
|------|-----------|---------|----------|
| **DDL** | Data Definition Language | Define database objects | CREATE, ALTER, DROP, TRUNCATE |
| **DML** | Data Manipulation Language | Modify data | INSERT, UPDATE, DELETE |
| **DQL** | Data Query Language | Query data | SELECT |
| **TCL** | Transaction Control Language | Manage transactions | COMMIT, ROLLBACK, SAVEPOINT |
| **DCL** | Data Control Language | Control access | GRANT, REVOKE |
