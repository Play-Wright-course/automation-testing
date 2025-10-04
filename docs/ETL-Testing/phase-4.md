# ETL Tools and Environments - Phase 4 Guide

## 🧰 Phase 4: ETL Tools and Environments

ETL tools help automate the extraction, transformation, and loading of data. This phase covers hands-on practice, data warehouse environments, and orchestration tools.

---

### 1. Hands-on with ETL Tools

**Popular ETL Tools:**

* Talend Open Studio (Free)
* Informatica PowerCenter (Paid, trial available)
* Pentaho Kettle (PDI)
* Apache NiFi (Open-source)
* SSIS (SQL Server Integration Services)

**Prerequisites:**

* **Talend Open Studio:**

  * Java JDK 8 or above
  * Minimum 4GB RAM
  * Download Talend Open Studio from official site
* **Informatica PowerCenter:**

  * Windows or Linux Server
  * Database for repository (Oracle, SQL Server)
  * Informatica installation files
* **Pentaho Kettle (PDI):**

  * Java JDK 8 or above
  * Pentaho Data Integration installation
* **Apache NiFi:**

  * Java JDK 8 or above
  * Minimum 2GB RAM
  * Download NiFi binary
* **SSIS:**

  * Windows OS
  * SQL Server with Integration Services installed
  * Visual Studio (for creating packages)

**Procedure to Setup Tool (Example: Talend Open Studio):**

1. Download Talend Open Studio.
2. Extract ZIP folder.
3. Set `JAVA_HOME` in environment variables.
4. Open `TOS_DI-win-x86_64.exe` (for Windows) to launch.
5. Create a new project.
6. Explore components: Input, Output, Transform.

**Creating a Simple ETL Job:**

* Input: `customer.csv`
* Transform: Assign Loyalty Status based on Sales
* Output: Load into `customer_dw` table

**Dummy Data (customer.csv):**

| Customer_ID | Name    | Birthdate  | Sales_Amount |
| ----------- | ------- | ---------- | ------------ |
| 101         | Alice   | 12/31/1985 | 250          |
| 102         | Bob     | 11/15/1990 | 300          |
| 103         | Charlie | 02/20/1982 | 150          |

**Transformations:**

* Format `Birthdate` to `YYYY-MM-DD`
* Assign Loyalty Status

  * > = 300 → Gold
  * 200–299 → Silver
  * <200 → Bronze

**Load:**

* Into target table `DW_CUSTOMER`

**Viewing Logs & Error Handling:**

* Each tool provides a console or logs panel.
* Common errors: Missing files, wrong data types, null values.
* Logs help debug and fix ETL jobs.

---

### 2. Data Warehouse Tools

**Popular Data Warehouses:**

* Snowflake
* Amazon Redshift
* Google BigQuery
* Azure Synapse

**Pre-requisites:**

* Cloud account (AWS, GCP, Azure, Snowflake)
* SQL knowledge
* Dataset for loading (e.g., dummy `customer.csv`)

**Procedure Example (Snowflake):**

1. Create free Snowflake trial account.
2. Create database and schema.
3. Create tables:

```sql
CREATE TABLE CUSTOMER_DW (
 Customer_ID INT,
 Name VARCHAR(50),
 Birthdate DATE,
 Sales_Amount INT,
 Loyalty_Status VARCHAR(10)
);
```

4. Load data from CSV using `COPY INTO` command.
5. Query to validate transformations.

---

### 3. Scheduling / Orchestration

**Tools:**

* Apache Airflow
* Oozie
* Control-M

**Purpose:** Schedule and orchestrate ETL jobs in sequence or based on triggers.

**Airflow Example Setup:**
**Prerequisites:**

* Python 3.8+
* Pip
* Minimum 2GB RAM

**Steps:**

1. Install Airflow: `pip install apache-airflow`
2. Initialize DB: `airflow db init`
3. Create DAG folder and Python DAG file
4. Define ETL tasks (Extract, Transform, Load)
5. Start scheduler: `airflow scheduler`
6. Monitor jobs using web UI: `airflow webserver`

**Dummy DAG Example:**

* Task 1: Extract CSV
* Task 2: Transform data (format date, assign loyalty)
* Task 3: Load into Snowflake or Redshift

**Validation:**

* Check logs in Airflow UI
* Confirm data in target tables

---

**Summary:**

1. Choose ETL tool (Talend, Informatica, Pentaho, NiFi, SSIS) for hands-on practice.
2. Load dummy data and apply transformations to simulate business logic.
3. Use Data Warehouses (Snowflake, Redshift, BigQuery, Azure Synapse) for target storage.
4. Schedule and orchestrate ETL jobs with Airflow, Oozie, or Control-M.
5. Practice logs and error handling to debug ETL processes.

This phase ensures you can set up ETL tools, perform hands-on jobs, and manage ETL workflows effectively.
