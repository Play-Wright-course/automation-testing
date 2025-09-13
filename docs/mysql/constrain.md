# 🚦 Why Do We Need Constraints?

Think of constraints as **traffic rules for your database**.  
- Without rules → cars can still move, but accidents happen.  
- With rules → movement is safe, organized, and predictable.  

---

## 🗄️ Example Tables Without Constraints

### Students Table
```sql
CREATE TABLE Students (
    id INT,
    firstname VARCHAR(50),
    lastname VARCHAR(50),
    address VARCHAR(100)
);

INSERT INTO Students (id, firstname, lastname, address) VALUES
(1, 'Rahul', 'Sharma', 'Pune'),
(2, 'Sneha', 'Patil', 'Mumbai'),
(3, 'Amit', 'Verma', 'Delhi'),
(4, 'Priya', 'Nair', 'Bangalore'),
(5, 'Karan', 'Singh', 'Hyderabad'),
(6, 'Neha', 'Kulkarni', 'Chennai');
```

### Marks Table
```sql
CREATE TABLE Marks (
    student_id INT,
    english INT,
    math INT,
    science INT,
    total_marks INT
);

INSERT INTO Marks (student_id, english, math, science, total_marks) VALUES
(1, 78, 85, 90, 253),
(2, 88, 92, 81, 261),
(3, 65, 70, 75, 210),
(4, 90, 95, 89, 274),
(5, 72, 68, 80, 220),
(6, 85, 79, 88, 252);
```

✅ These tables work fine, but without constraints **problems can arise** (duplicates, orphan records, missing data).  

---

## 1. PRIMARY KEY
👉 Makes sure each row is **unique and identifiable**.  

**Without Primary Key**
```sql
INSERT INTO Students (id, firstname, lastname, address)
VALUES (1, 'Rahul', 'Sharma', 'Pune');

INSERT INTO Students (id, firstname, lastname, address)
VALUES (1, 'AnotherRahul', 'Sharma', 'Pune'); -- Duplicate allowed
```
❌ Now two students with same ID exist → confusion in reports.  

**With Primary Key**
```sql
id INT PRIMARY KEY
```
✅ Database stops duplicate rows.  

---

## 2. FOREIGN KEY
👉 Ensures that a value in one table **must exist in another**.  

**Without Foreign Key**
```sql
INSERT INTO Marks (student_id, english, math, science, total_marks)
VALUES (100, 80, 90, 85, 255); -- Student 100 doesn't exist
```
❌ Marks exist for a non-existent student (orphan record).  

**With Foreign Key**
```sql
FOREIGN KEY (student_id) REFERENCES Students(id)
```
✅ Database prevents this.  

---

## 3. UNIQUE
👉 Stops duplicate values in a column that should be unique (like email).  

**Without UNIQUE**
```sql
INSERT INTO Students (id, firstname, lastname, address)
VALUES (7, 'Rohit', 'Sharma', 'Mumbai');

INSERT INTO Students (id, firstname, lastname, address)
VALUES (8, 'Rohit', 'Sharma', 'Mumbai'); -- Duplicate allowed
```

**With UNIQUE**
```sql
email VARCHAR(100) UNIQUE
```
✅ Database blocks duplicate emails.  

---

## 4. NOT NULL
👉 Ensures important data is not left blank.  

**Without NOT NULL**
```sql
INSERT INTO Students (id, firstname, lastname, address)
VALUES (9, NULL, 'Sharma', 'Delhi'); -- Allowed
```

❌ Student without a name → makes no sense.  

**With NOT NULL**
```sql
firstname VARCHAR(50) NOT NULL
```
✅ Database forces valid data.  

---

# ✅ Summary in Easy Words
- **Primary Key** → Every row should have a unique ID → No duplicates.  
- **Foreign Key** → Links two tables → No orphan data.  
- **Unique** → Prevents duplicate values.  
- **Not Null** → Some fields must always have a value.  

👉 Without constraints → data looks fine in the beginning but later causes **duplicates, orphan rows, missing data, wrong ETL reports**.
