# ETL & ETL Testing - Phase 1 Guide

## 🧩 Phase 1: ETL & Data Basics

### 1. What is ETL?

ETL is a process used to move data from one system to another while cleaning and transforming it.

#### Step 1: Extract

* **Purpose:** Get data from different sources.
* **Sources include:** CSV files, Excel sheets, Databases (SQL Server, Oracle, MySQL), APIs.
* **Example Data (CSV):**

| Customer_ID | Name    | Birthdate  | Sales_Amount |
| ----------- | ------- | ---------- | ------------ |
| 101         | Alice   | 12/31/1985 | 250          |
| 102         | Bob     | 11/15/1990 | 300          |
| 103         | Charlie | 02/20/1982 | 150          |

#### Step 2: Transform

* **Purpose:** Convert data into a usable format according to business logic.
* **Transformations can include:**

  * Cleaning: Remove nulls
  * Standardizing: Convert dates to `YYYY-MM-DD`
  * Aggregating: Total sales per customer
  * Enriching: Add loyalty status based on sales

**Business Logic Examples:**

1. Convert `Birthdate` to standard format.
2. Assign `Loyalty_Status` based on `Sales_Amount`:

   * > = 300 → Gold
   * 200–299 → Silver
   * < 200 → Bronze

**Transformed Data:**

| Customer_ID | Name    | Birthdate  | Sales_Amount | Loyalty_Status |
| ----------- | ------- | ---------- | ------------ | -------------- |
| 101         | Alice   | 1985-12-31 | 250          | Silver         |
| 102         | Bob     | 1990-11-15 | 300          | Gold           |
| 103         | Charlie | 1982-02-20 | 150          | Bronze         |

#### Step 3: Load

* **Purpose:** Move the clean and transformed data into the target system (Data Warehouse, Database, Analytics tool).
* **Ready to Push Data:**

| Customer_ID | Name    | Birthdate  | Sales_Amount | Loyalty_Status |
| ----------- | ------- | ---------- | ------------ | -------------- |
| 101         | Alice   | 1985-12-31 | 250          | Silver         |
| 102         | Bob     | 1990-11-15 | 300          | Gold           |
| 103         | Charlie | 1982-02-20 | 150          | Bronze         |

---

### 2. Why ETL Testing?

* Ensure **data accuracy, completeness, and consistency**
* Validate transformations and business rules
* Catch issues early in data pipelines

### 3. Key ETL Testing Concepts

| Concept                  | Explanation                                                           | Example                                                     |
| ------------------------ | --------------------------------------------------------------------- | ----------------------------------------------------------- |
| Source to Target Mapping | Blueprint showing how data fields move from source → staging → target | Customer Name in source CSV → Customer_Name in target table |
| Data Completeness        | Ensure all records are moved                                          | Source has 3 rows, target should also have 3 rows           |
| Data Accuracy            | Ensure transformations follow business rules                          | Sales >= 300 → Gold, 200–299 → Silver, <200 → Bronze        |
| Data Integrity           | Relationships between tables are maintained                           | Customer_ID in Orders table exists in Customer table        |
| Data Duplication         | No duplicate records                                                  | Customer_ID 101 appears only once                           |
| Reconciliation           | Verify row counts, sums, averages                                     | Total sales in source = total sales in target               |

### 4. Notes for Beginners

* **ETL Testing Tools:** Informatica, Talend, DataStage, SQL scripts, Python, QuerySurge
* **Data Types:** Numeric (int, float), String (varchar, text), Date/Time
* **Common Errors:** Missing data, incorrect transformations, duplicates, mismatched source & target

---

**Summary:**

1. ETL moves and transforms data from sources to targets.
2. ETL Testing ensures data is accurate, complete, and reliable.
3. Use mapping, accuracy, completeness, integrity, and reconciliation to validate data.
