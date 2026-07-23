# Chapter II — SQL DDL (Data Definition Language)

## A. Introduction to DDL (Data Definition Language) in SQL

DDL (Data Definition Language) is a category of SQL commands used to create, modify, and manage the structure of database objects such as databases, tables, indexes, and views.

**Key points:**

1. DDL stands for Data Definition Language.
2. It is used to define and manage the structure (schema) of a database.
3. DDL commands create, modify, rename, or remove database objects.
4. These commands affect the database schema, not the actual data stored in tables.
5. Most DDL operations are auto-committed, meaning changes are saved immediately.
6. DDL is mainly used by database administrators (DBAs) and developers while designing databases.
7. It helps maintain the organization and structure of database objects.
8. Common database objects managed by DDL include:
   - Database
   - Table
   - View
   - Index
   - Schema

## B. SQL DDL Commands

### 1. `SHOW DATABASES` *(Utility Command)*

**Purpose:** Displays all databases available on the MySQL server.

**Syntax:**
```sql
SHOW DATABASES;
```

**Example:**
```sql
SHOW DATABASES;
```

**Result:**

| Database |
|---|
| information_schema |
| mysql |
| performance_schema |
| sys |
| CollegeDB |

---

### 2. `CREATE DATABASE` *(DDL Command)*

**Purpose:** Creates a new database.

**Syntax:**
```sql
CREATE DATABASE database_name;
```

**Example:**
```sql
CREATE DATABASE CollegeDB;
```

**Result:** `Query OK, 1 row affected`

---

### 3. `SHOW DATABASES` *(Utility Command)*

**Purpose:** Verifies that the new database has been created successfully.

**Syntax:**
```sql
SHOW DATABASES;
```

**Example:**
```sql
SHOW DATABASES;
```

**Result:**

| Database |
|---|
| information_schema |
| mysql |
| CollegeDB |

---

### 4. `USE DATABASE` *(Utility Command)*

**Purpose:** Selects the database that you want to work with.

**Syntax:**
```sql
USE database_name;
```

**Example:**
```sql
USE CollegeDB;
```

**Result:** `Database changed`

---

### 5. `CREATE TABLE` *(DDL Command)*

**Purpose:** Creates a new table inside the selected database.

**Syntax:**
```sql
CREATE TABLE table_name (
    column_name datatype constraint,
    column_name datatype constraint
);
```

**Example:**
```sql
CREATE TABLE Student(
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);
```

**Result:** `Query OK, 0 rows affected`

---

### 6. `SHOW TABLES` *(Utility Command)*

**Purpose:** Displays all tables in the current database.

**Syntax:**
```sql
SHOW TABLES;
```

**Example:**
```sql
SHOW TABLES;
```

**Result:**

| Tables_in_CollegeDB |
|---|
| Student |

---

### 7. `DESCRIBE` / `DESC` *(Utility Command)*

**Purpose:** Displays the structure of a table, including column names, data types, keys, and NULL information.

**Syntax:**
```sql
DESC table_name;
-- or
DESCRIBE table_name;
```

**Example:**
```sql
DESC Student;
```

**Result:**

| Field | Type | Null | Key | Default |
|---|---|---|---|---|
| StudentID | int | NO | PRI | NULL |
| Name | varchar(50) | YES | | NULL |
| Age | int | YES | | NULL |

---

### 8. `SHOW CREATE TABLE` *(Utility Command)*

**Purpose:** Displays the SQL statement used to create a table.

**Syntax:**
```sql
SHOW CREATE TABLE table_name;
```

**Example:**
```sql
SHOW CREATE TABLE Student;
```

**Result:**
```sql
CREATE TABLE Student(
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);
```

---

### 9. `ALTER TABLE` *(DDL Command)*

**Definition:** The `ALTER TABLE` command is used to modify the structure of an existing table without deleting the table or its data.

**Common Uses:**
- Add a new column
- Modify a column's data type
- Rename a column
- Drop (delete) a column

#### 9.1 ADD COLUMN

**Purpose:** Adds a new column to an existing table.

**Syntax:**
```sql
ALTER TABLE table_name ADD column_name datatype;
```

**Example:**
```sql
ALTER TABLE Student ADD Email VARCHAR(100);
```

**Result:** `Query OK, Table altered successfully.`

**Updated Table Structure:**

| StudentID | Name | Age | Email |
|---|---|---|---|

#### 9.2 MODIFY COLUMN DATATYPE

**Purpose:** Changes the data type or size of an existing column.

**Syntax:**
```sql
ALTER TABLE table_name MODIFY column_name new_datatype;
```

**Example:**
```sql
ALTER TABLE Student MODIFY Name VARCHAR(100);
```

**Result:** `Query OK, Table altered successfully.`

**Updated Structure:**

| Column | Old Data Type | New Data Type |
|---|---|---|
| Name | VARCHAR(50) | VARCHAR(100) |

#### 9.3 RENAME COLUMN

**Purpose:** Changes the name of an existing column.

**Syntax** *(MySQL 8.0+)*:
```sql
ALTER TABLE table_name RENAME COLUMN old_column_name TO new_column_name;
```

**Example:**
```sql
ALTER TABLE Student RENAME COLUMN Age TO StudentAge;
```

**Result:** `Query OK, Table altered successfully.`

**Updated Structure:**

| StudentID | Name | StudentAge | Email |
|---|---|---|---|

#### 9.4 DROP COLUMN

**Purpose:** Removes an existing column permanently from the table.

**Syntax:**
```sql
ALTER TABLE table_name DROP COLUMN column_name;
```

**Example:**
```sql
ALTER TABLE Student DROP COLUMN Email;
```

**Result:** `Query OK, Table altered successfully.`

**Updated Structure:**

| StudentID | Name | StudentAge |
|---|---|---|

---

### 10. `DESC` *(Utility Command)*

**Purpose:** Displays the updated table structure after `ALTER` operations.

**Syntax:**
```sql
DESC table_name;
```

**Example:**
```sql
DESC Student;
```

**Result:**

| Field | Type | Key |
|---|---|---|
| StudentID | INT | PRI |
| Name | VARCHAR(100) | |
| StudentAge | INT | |

---

### 11. `TRUNCATE TABLE` *(DDL Command)*

**Purpose:** Deletes all records from a table while keeping its structure.

**Syntax:**
```sql
TRUNCATE TABLE table_name;
```

**Example:**
```sql
TRUNCATE TABLE Student;
```

**Result:** `Query OK, 0 rows affected` — table structure remains unchanged.

---

### 12. `RENAME TABLE` *(DDL Command)*

**Purpose:** Changes the name of an existing table.

**Syntax:**
```sql
RENAME TABLE old_table_name TO new_table_name;
```

**Example:**
```sql
RENAME TABLE Student TO Students;
```

**Result:** `Query OK, Table renamed successfully.`

---

### 13. `SHOW TABLES` *(Utility Command)*

**Purpose:** Verifies that the table has been renamed successfully.

**Syntax:**
```sql
SHOW TABLES;
```

**Example:**
```sql
SHOW TABLES;
```

**Result:**

| Tables_in_CollegeDB |
|---|
| Students |

---

### 14. `DROP TABLE` *(DDL Command)*

**Purpose:** Deletes a table permanently from the database.

**Syntax:**
```sql
DROP TABLE table_name;
```

**Example:**
```sql
DROP TABLE Students;
```

**Result:** `Query OK, Table dropped.`

---

### 15. `SHOW TABLES` *(Utility Command)*

**Purpose:** Verifies that the table has been deleted.

**Syntax:**
```sql
SHOW TABLES;
```

**Example:**
```sql
SHOW TABLES;
```

**Result:** `Empty set`

---

### 16. `SHOW CREATE DATABASE` *(Utility Command)*

**Purpose:** Displays the SQL statement used to create the database.

**Syntax:**
```sql
SHOW CREATE DATABASE database_name;
```

**Example:**
```sql
SHOW CREATE DATABASE CollegeDB;
```

**Result:**
```sql
CREATE DATABASE CollegeDB;
```

---

### 17. `DROP DATABASE` *(DDL Command)*

**Purpose:** Deletes the database permanently.

**Syntax:**
```sql
DROP DATABASE database_name;
```

**Example:**
```sql
DROP DATABASE CollegeDB;
```

**Result:** `Query OK, Database dropped.`

---

### 18. `SHOW DATABASES` *(Utility Command)*

**Purpose:** Verifies that the database has been deleted.

**Syntax:**
```sql
SHOW DATABASES;
```

**Example:**
```sql
SHOW DATABASES;
```

**Result:**

| Database |
|---|
| information_schema |
| mysql |
| performance_schema |
| sys |
