# Transaction Control Language (TCL) in SQL

## 🔹 What is TCL?
TCL commands manage **transactions** in the database.  
They ensure data integrity and control how changes are saved or undone.

---

## 🔹 Key TCL Commands (in depth)

### 1. COMMIT
- Saves changes permanently.
```sql
COMMIT;
```

### 2. ROLLBACK
- Undo changes since last commit.
```sql
ROLLBACK;
```

### 3. SAVEPOINT
- Creates a point to rollback partially.
```sql
SAVEPOINT sp1;
ROLLBACK TO sp1;
```

### 4. SET TRANSACTION
- Sets transaction properties like isolation level.
```sql
SET TRANSACTION READ ONLY;
```

---

## 🔹 Pros & Cons of TCL

### ✅ Pros
1. **Transaction Safety** → Prevents accidental data loss.  
2. **Consistency** → Maintains ACID properties.  
3. **Flexibility** → Can rollback fully or partially.  
4. **Control** → Developers control when to save changes.

### ❌ Cons
1. **Complexity** → Misuse can cause locks.  
2. **Performance** → Frequent rollbacks may reduce speed.  
3. **Overhead** → Managing multiple savepoints may be costly.  
4. **Limited Scope** → Works only with DML changes.

---

## ✅ Summary Table

| Command       | Purpose                       | Rollback Possible | Example Usage            |
|---------------|-------------------------------|------------------|--------------------------|
| COMMIT        | Save all changes permanently  | ❌ No            | End transaction          |
| ROLLBACK      | Undo changes                  | ✅ Yes           | Revert mistaken updates  |
| SAVEPOINT     | Partial rollback              | ✅ Yes           | Rollback to checkpoint   |
| SET TRANSACTION | Define transaction behavior | N/A              | Read-only transaction    |

---

## 📊 TCL Commands – Feature Comparison

| Command       | Rollback | Data Loss | Structure Change | Typical Use Case         |
|---------------|----------|-----------|------------------|--------------------------|
| COMMIT        | ❌ No    | ❌ No      | ❌ No            | Save all operations      |
| ROLLBACK      | ✅ Yes   | ❌ No      | ❌ No            | Undo operations          |
| SAVEPOINT     | ✅ Yes   | ❌ No      | ❌ No            | Rollback to savepoint    |
| SET TRANSACTION | N/A    | ❌ No      | ❌ No            | Define isolation level   |
