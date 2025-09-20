# SQL Practice: Stored Procedures / Functions with Explanations

This file contains **10 SQL practice problems** covering:

* Stored Procedures
* User Defined Functions (UDFs)

Each question includes:

* Input Table(s)
* Question
* SQL Query / Procedure / Function
* Explanation
* Output Table

---

## 1. Input Table Example

**Table: employees**

| emp\_id | name    | salary | dept  |
| ------- | ------- | ------ | ----- |
| 1       | Alice   | 48000  | HR    |
| 2       | Bob     | 60000  | IT    |
| 3       | Charlie | 55000  | HR    |
| 4       | David   | 45000  | IT    |
| 5       | Eva     | 70000  | Sales |

---

## 2. Stored Procedure Examples

### Q1: Create procedure to give 10% bonus to employee

```sql
CREATE PROCEDURE give_bonus(IN emp INT, OUT bonus_amt DECIMAL(10,2))
BEGIN
    SELECT salary*0.10 INTO bonus_amt FROM employees WHERE emp_id=emp;
END;
```

**Usage:**

```sql
CALL give_bonus(2, @b);
SELECT @b;
```

**Output:**

| @b   |
| ---- |
| 6000 |

### Q2: Procedure to increase salary by % for a department

```sql
CREATE PROCEDURE increase_salary(IN dept_name VARCHAR(20), IN increment DECIMAL(5,2))
BEGIN
    UPDATE employees
    SET salary = salary + (salary * increment/100)
    WHERE dept = dept_name;
END;
```

**Usage:**

```sql
CALL increase_salary('HR', 5);
SELECT * FROM employees WHERE dept='HR';
```

**Output:**

| emp\_id | name    | salary | dept |
| ------- | ------- | ------ | ---- |
| 1       | Alice   | 50400  | HR   |
| 3       | Charlie | 57750  | HR   |

### Q3: Procedure to get total salary of department

```sql
CREATE PROCEDURE dept_total_salary(IN dept_name VARCHAR(20), OUT total_salary DECIMAL(10,2))
BEGIN
    SELECT SUM(salary) INTO total_salary FROM employees WHERE dept=dept_name;
END;
```

**Usage:**

```sql
CALL dept_total_salary('IT', @ts);
SELECT @ts;
```

**Output:**

| @ts    |
| ------ |
| 105000 |

### Q4: Procedure to get employee details by ID

```sql
CREATE PROCEDURE emp_details(IN emp INT)
BEGIN
    SELECT * FROM employees WHERE emp_id = emp;
END;
```

**Usage:**

```sql
CALL emp_details(5);
```

**Output:**

| emp\_id | name | salary | dept  |
| ------- | ---- | ------ | ----- |
| 5       | Eva  | 70000  | Sales |

---

## 3. User Defined Function Examples

### Q5: Function to calculate bonus

```sql
CREATE FUNCTION calc_bonus(sal DECIMAL(10,2)) RETURNS DECIMAL(10,2)
BEGIN
    RETURN sal * 0.10;
END;
```

**Usage:**

```sql
SELECT name, calc_bonus(salary) AS bonus FROM employees;
```

**Output:**

| name    | bonus |
| ------- | ----- |
| Alice   | 5040  |
| Bob     | 6000  |
| Charlie | 5775  |
| David   | 4500  |
| Eva     | 7000  |

### Q6: Function to check if salary > threshold

```sql
CREATE FUNCTION is_high_salary(sal DECIMAL(10,2)) RETURNS VARCHAR(3)
BEGIN
    RETURN IF(sal>60000,'YES','NO');
END;
```

**Usage:**

```sql
SELECT name, is_high_salary(salary) AS high_sal FROM employees;
```

**Output:**

| name    | high\_sal |
| ------- | --------- |
| Alice   | NO        |
| Bob     | NO        |
| Charlie | NO        |
| David   | NO        |
| Eva     | YES       |

### Q7: Procedure to insert new employee

```sql
CREATE PROCEDURE add_employee(IN ename VARCHAR(50), IN esal DECIMAL(10,2), IN edept VARCHAR(20))
BEGIN
    INSERT INTO employees(name,salary,dept) VALUES(ename,esal,edept);
END;
```

**Usage:**

```sql
CALL add_employee('Frank', 48000, 'IT');
SELECT * FROM employees WHERE name='Frank';
```

**Output:**

| emp\_id | name  | salary | dept |
| ------- | ----- | ------ | ---- |
| 6       | Frank | 48000  | IT   |

### Q8: Function to convert salary to string with currency

```sql
CREATE FUNCTION salary_str(sal DECIMAL(10,2)) RETURNS VARCHAR(20)
BEGIN
    RETURN CONCAT('$', CAST(sal AS CHAR));
END;
```

**Usage:**

```sql
SELECT name, salary_str(salary) AS salary_display FROM employees;
```

**Output:**

| name    | salary\_display |
| ------- | --------------- |
| Alice   | \$50400         |
| Bob     | \$60000         |
| Charlie | \$57750         |
| David   | \$45000         |
| Eva     | \$70000         |

### Q9: Procedure to delete employee by ID

```sql
CREATE PROCEDURE delete_employee(IN emp INT)
BEGIN
    DELETE FROM employees WHERE emp_id = emp;
END;
```

**Usage:**

```sql
CALL delete_employee(6);
SELECT * FROM employees WHERE emp_id=6;
```

**Output:**
\| -- No rows -- |

### Q10: Function to calculate tax at 10%

```sql
CREATE FUNCTION calc_tax(sal DECIMAL(10,2)) RETURNS DECIMAL(10,2)
BEGIN
    RETURN sal * 0.10;
END;
```

**Usage:**

```sql
SELECT name, calc_tax(salary) AS tax FROM employees;
```

**Output:**

| name    | tax  |
| ------- | ---- |
| Alice   | 5040 |
| Bob     | 6000 |
| Charlie | 5775 |
| David   | 4500 |
| Eva     | 7000 |

---

### Explanation:

1. **Stored Procedures**: Encapsulate SQL logic; can take input/output parameters.
2. **Functions**: Return a value; can be used inside SELECT statements.
3. Useful for ETL testing when transformations are done via procedural logic.

---

**Use case in ETL Testing:**

* Validate bonus calculations, salary increments, or other business rules.
* Check the correctness of procedural logic applied on data.
* Ensure outputs match expected results before moving to production.
