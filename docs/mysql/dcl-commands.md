# Data Control Language (DCL) in SQL

## 🔹 What is DCL?
DCL commands are used to **control access and permissions** in a database.  
They define who can access, modify, or manage database objects.

---

## 🔹 Key DCL Commands (in depth)

### 1. GRANT
- Provides privileges to a user.
```sql
GRANT SELECT, INSERT ON Employee TO user1;
```

### 2. REVOKE
- Removes previously granted privileges.
```sql
REVOKE INSERT ON Employee FROM user1;
```

### 3. DENY (SQL Server)
- Explicitly denies permission to users.
```sql
DENY DELETE ON Employee TO user1;
```

---

## 🔹 Pros & Cons of DCL

### ✅ Pros
1. **Security** → Ensures only authorized users access data.  
2. **Granularity** → Assign specific privileges per object.  
3. **Control** → Manage roles and user access.  
4. **Scalability** → Assign privileges to roles for teams.

### ❌ Cons
1. **Mismanagement Risk** → Wrong grants expose sensitive data.  
2. **Complexity** → Hard to manage in large organizations.  
3. **Performance Overhead** → Checking permissions for each query.  
4. **Inconsistency** → Syntax varies across databases.

---

## ✅ Summary Table

| Command | Purpose                 | Rollback Possible | Example Usage             |
|---------|-------------------------|------------------|---------------------------|
| GRANT   | Give permissions         | ✅ Yes           | Allow SELECT on Employee  |
| REVOKE  | Remove permissions       | ✅ Yes           | Remove INSERT privilege   |
| DENY    | Explicitly block access  | ✅ Yes           | Prevent DELETE on Employee|

---

## 📊 DCL Commands – Feature Comparison

| Command | Rollback | Data Loss | Structure Change | Typical Use Case        |
|---------|----------|-----------|------------------|-------------------------|
| GRANT   | ✅ Yes   | ❌ No      | ❌ No            | Provide privileges      |
| REVOKE  | ✅ Yes   | ❌ No      | ❌ No            | Remove privileges       |
| DENY    | ✅ Yes   | ❌ No      | ❌ No            | Restrict user actions   |
