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

## 🔹 Advantages Explained with Examples

### 1. Schema Control
DDL lets you define strong structures with relationships.

```sql
CREATE TABLE Department (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50) UNIQUE
);

CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Salary DECIMAL(10,2),
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

👉 Employees must belong to a valid department.

---

### 2. Integrity Enforcement
Constraints enforce data accuracy.

```sql
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Salary DECIMAL(10,2) CHECK (Salary > 0),
    DeptID INT NOT NULL,
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

👉 Prevents negative salaries and missing departments.

---

### 3. Performance (Indexes & Partitions)
Indexes and partitions improve query speed.

```sql
-- Index for faster salary searches
CREATE INDEX idx_salary ON Employee(Salary);

-- Partition sales table by year
CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    SaleDate DATE,
    Amount DECIMAL(10,2)
)
PARTITION BY RANGE (YEAR(SaleDate)) (
    PARTITION p2023 VALUES LESS THAN (2024),
    PARTITION p2024 VALUES LESS THAN (2025)
);
```

👉 Queries on salaries or specific years run faster.

---

### 4. Automation Friendly (CI/CD)
DDL scripts can be stored and executed in deployments.

```sql
-- migration_v2.sql
ALTER TABLE Employee ADD COLUMN Email VARCHAR(100);
```

👉 Keeps dev, test, and prod in sync automatically.

---

### 5. Flexibility (Evolving Structures)
Easily adapt schema to new business needs.

```sql
ALTER TABLE Employee ADD COLUMN PhoneNumber VARCHAR(15);
ALTER TABLE Employee RENAME COLUMN Name TO FullName;
```

👉 Business changes are easily handled.

---

## ✅ Summary Table

| Advantage | What it Means | Example |
|-----------|---------------|---------|
| **Schema Control** | Strong control over tables, keys, relationships | Employee → Department with foreign key |
| **Integrity Enforcement** | Constraints ensure only valid data | CHECK (Salary > 0), NOT NULL |
| **Performance** | Indexes & partitions speed up queries | `CREATE INDEX idx_salary` |
| **Automation Friendly** | DDL scripts can be versioned in Git & run in CI/CD | Migration scripts for deployments |
| **Flexibility** | Schema can evolve with business needs | `ALTER TABLE Employee ADD PhoneNumber` |

## 📊 DDL Commands – Feature Comparison

| Command       | Rollback Possible | Data Loss | Structure Change | Typical Use Case |
|---------------|------------------|-----------|------------------|------------------|
| **CREATE**    | ✅ Yes (before commit) | ❌ No | ✅ Creates new object | Create tables, views, indexes |
| **ALTER**     | ✅ Yes (before commit) | ❌ No | ✅ Modifies structure | Add/modify columns, constraints |
| **DROP**      | ✅ Yes (before commit) | ✅ Yes (all data lost) | ✅ Removes object completely | Delete table/schema permanently |
| **TRUNCATE**  | ✅ Yes (before commit) | ✅ Yes (all rows deleted) | ❌ No (structure remains) | Quickly remove all records |
| **RENAME**    | ✅ Yes (before commit) | ❌ No | ✅ Only name changes | Rename table/column |
| **COMMENT**   | ✅ Yes (before commit) | ❌ No | ❌ No (metadata only) | Add description to objects |
| **CREATE INDEX** | ✅ Yes (before commit) | ❌ No | ✅ Creates performance structure | Improve query performance |
| **DROP INDEX**   | ✅ Yes (before commit) | ❌ No (only index removed) | ✅ Removes performance structure | Free up space, remove unused index |

---

### 🔑 Key Notes
- **Rollback** → Possible only until you `COMMIT` (some DBs auto-commit DDL, e.g., Oracle).  
- **Data Loss** → `DROP` & `TRUNCATE` cause data removal; `ALTER`/`RENAME` don’t.  
- **Structure Change** → All DDL affects schema except `COMMENT`.  
- **Performance Impact** → `TRUNCATE` is faster than `DELETE`; indexes speed queries but slow inserts/updates.  

