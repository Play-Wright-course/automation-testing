# ETL Testing Process - Phase 3 Guide

## ⚙️ Phase 3: ETL Testing Process

ETL Testing Process ensures that your ETL pipeline correctly extracts, transforms, and loads data while following business rules. Here’s a detailed breakdown with examples.

---

### 1. Understanding ETL Workflow

* **Purpose:** Visualize and understand the flow of data from source to target.
* **Workflow:**

  * **Source Systems:** Original data (CSV, DBs, APIs)
  * **Staging Area:** Temporary storage for raw data before transformations
  * **Data Warehouse (Target):** Final storage after ETL transformations
  * **Reports/Analytics:** Business dashboards or reporting systems consuming the data

**Example Workflow:**

```
Source Systems (Customer.csv, Sales DB) → Staging Tables → Data Warehouse (DW_CUSTOMER, DW_SALES) → Reports (Power BI / Tableau)
```

* **Identify transformations:**

  * Date formatting
  * Calculating total sales
  * Assigning loyalty status based on sales

**Example:**

* Customer CSV has `Birthdate` as `12/31/1985`
* Transformation: Convert to `YYYY-MM-DD` → `1985-12-31`
* Load into `DW_CUSTOMER` table

---

### 2. Test Planning

* **Purpose:** Plan all ETL test cases before execution
* **Steps:**

  1. Read **Source to Target (S2T) mapping documents**
  2. Identify test cases based on data flows and transformations

**Common Test Cases:**

| Test Case                       | Description                             | Example                                             |
| ------------------------------- | --------------------------------------- | --------------------------------------------------- |
| Row Count Validation            | Ensure all records are loaded           | Source = 3 rows, Target = 3 rows                    |
| Data Truncation Check           | Ensure no data is truncated             | Name `Alexander` stored as `Alex` → Fail            |
| Transformation Logic Validation | Check business rules                    | Sales >= 300 → Gold, <200 → Bronze                  |
| Incremental Load Testing        | Verify only new/changed rows are loaded | Add Customer_ID 104 → Target should reflect new row |

---

### 3. Test Execution

* **Purpose:** Execute test cases using SQL queries or testing tools
* **Steps:**

  1. Query **Source and Target tables**
  2. Validate:

     * Row counts match
     * Transformation rules applied correctly
     * Data types are consistent
     * Primary and foreign keys maintained

**Example SQL Checks:**

```sql
-- Row Count Validation
SELECT COUNT(*) FROM source_customer;
SELECT COUNT(*) FROM dw_customer;

-- Transformation Validation (Loyalty Status)
SELECT Customer_ID, Sales_Amount, Loyalty_Status FROM dw_customer;
-- Check if rules applied correctly

-- Data Type Validation
SELECT COLUMN_NAME, DATA_TYPE FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME='dw_customer';
```

**Validation Points:**

* Counts should match
* Loyalty status and calculations should follow business rules
* Birthdates and numeric fields consistent
* Keys maintained and not broken

---

**Summary:**

1. **Understanding Workflow:** Identify flow and transformations from source → staging → target → reports
2. **Test Planning:** Read mapping documents, create test cases
3. **Test Execution:** Run SQL or tools to validate row counts, transformations, data types, and keys

This structured process ensures ETL pipelines produce accurate and reliable data for analytics and reporting.
