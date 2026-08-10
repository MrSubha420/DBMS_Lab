# MySQL Complete Tutorial: Database, Table & DML Operations Using a Student Table — Step by Step with Description, Syntax, Example & Output

## PART 1: BASIC SETUP

### Step 1: Create Database

**Description:** Creates a new database named School if it doesn't already exist.

**Syntax:**
```sql
CREATE DATABASE database_name;
```

**Example:**
```sql
CREATE DATABASE School;
```

**Verify:**
```sql
SHOW DATABASES;
```

**Output:**
```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| School              |
| sys                |
+--------------------+
```

### Step 2: Select (Use) the Database

**Description:** Tells MySQL which database to work in for all following commands.

**Syntax:**
```sql
USE database_name;
```

**Example:**
```sql
USE School;
```

**Verify:**
```sql
SELECT DATABASE();
```

**Output:**
```
+------------+
| DATABASE() |
+------------+
| School     |
+------------+
```

### Step 3: Create Table

**Description:** Creates a Student table with 6 fields: stu_id, Name, Father_Name, Email, City, HS_Marks.

**Syntax:**
```sql
CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ...
);
```

**Example:**
```sql
CREATE TABLE Student (
    stu_id INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Father_Name VARCHAR(50),
    Email VARCHAR(100),
    City VARCHAR(50),
    HS_Marks DECIMAL(5,2)
);
```

**Verify:**
```sql
DESCRIBE Student;
```

**Output:**
```
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| stu_id      | int          | NO   | PRI | NULL    |       |
| Name        | varchar(50)  | NO   |     | NULL    |       |
| Father_Name | varchar(50)  | YES  |     | NULL    |       |
| Email       | varchar(100) | YES  |     | NULL    |       |
| City        | varchar(50)  | YES  |     | NULL    |       |
| HS_Marks    | decimal(5,2) | YES  |     | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
```

## PART 2: DML OPERATIONS

### (a) INSERT — Insert 12 Students at a Time

**Description:** Adds multiple rows into the table in a single statement (bulk insert).

**Syntax:**
```sql
INSERT INTO table_name (col1, col2, ...)
VALUES (val1, val2, ...), (val1, val2, ...);
```

**Example:**
```sql
INSERT INTO Student (stu_id, Name, Father_Name, Email, City, HS_Marks) VALUES
(1, 'Aarav Sharma', 'Rakesh Sharma', 'aarav.sharma@email.com', 'Delhi', 85.50),
(2, 'Priya Patel', 'Manoj Patel', 'priya.patel@email.com', 'Ahmedabad', 78.25),
(3, 'Rohan Verma', 'Suresh Verma', 'rohan.verma@email.com', 'Lucknow', 92.00),
(4, 'Sneha Reddy', 'Kiran Reddy', 'sneha.reddy@email.com', 'Hyderabad', 88.75),
(5, 'Karan Singh', 'Devendra Singh', 'karan.singh@email.com', 'Jaipur', 65.40),
(6, 'Ananya Iyer', 'Ramesh Iyer', 'ananya.iyer@email.com', 'Chennai', 91.20),
(7, 'Vikram Nair', 'Sunil Nair', 'vikram.nair@email.com', 'Kochi', 73.60),
(8, 'Divya Menon', 'Anil Menon', 'divya.menon@email.com', 'Kochi', 80.00),
(9, 'Arjun Gupta', 'Ravi Gupta', 'arjun.gupta@email.com', 'Kanpur', 68.90),
(10, 'Kavya Rao', 'Prakash Rao', 'kavya.rao@email.com', 'Bangalore', 95.30),
(11, 'Aditya Joshi', 'Mahesh Joshi', 'aditya.joshi@email.com', 'Pune', 77.85),
(12, 'Meera Desai', 'Nitin Desai', 'meera.desai@email.com', 'Surat', 83.15);
```

**Output:**
```
Query OK, 12 rows affected (0.02 sec)
Records: 12  Duplicates: 0  Warnings: 0
```

### (b) SELECT — Verify All Data Was Inserted

**Description:** Retrieves and displays all rows/columns from the table to confirm the insert worked.

**Syntax:**
```sql
SELECT * FROM table_name;
```

**Example:**
```sql
SELECT * FROM Student;
```

**Output:**
```
+--------+---------------+-----------------+---------------------------+------------+----------+
| stu_id | Name          | Father_Name     | Email                     | City       | HS_Marks |
+--------+---------------+-----------------+---------------------------+------------+----------+
| 1      | Aarav Sharma  | Rakesh Sharma   | aarav.sharma@email.com    | Delhi      | 85.50    |
| 2      | Priya Patel   | Manoj Patel     | priya.patel@email.com     | Ahmedabad  | 78.25    |
| 3      | Rohan Verma   | Suresh Verma    | rohan.verma@email.com     | Lucknow    | 92.00    |
| 4      | Sneha Reddy   | Kiran Reddy     | sneha.reddy@email.com     | Hyderabad  | 88.75    |
| 5      | Karan Singh   | Devendra Singh  | karan.singh@email.com     | Jaipur     | 65.40    |
| 6      | Ananya Iyer   | Ramesh Iyer     | ananya.iyer@email.com     | Chennai    | 91.20    |
| 7      | Vikram Nair   | Sunil Nair      | vikram.nair@email.com     | Kochi      | 73.60    |
| 8      | Divya Menon   | Anil Menon      | divya.menon@email.com     | Kochi      | 80.00    |
| 9      | Arjun Gupta   | Ravi Gupta      | arjun.gupta@email.com     | Kanpur     | 68.90    |
| 10     | Kavya Rao     | Prakash Rao     | kavya.rao@email.com       | Bangalore  | 95.30    |
| 11     | Aditya Joshi  | Mahesh Joshi    | aditya.joshi@email.com    | Pune       | 77.85    |
| 12     | Meera Desai   | Nitin Desai     | meera.desai@email.com     | Surat      | 83.15    |
+--------+---------------+-----------------+---------------------------+------------+----------+
12 rows in set (0.00 sec)
```

**Check row count directly:**
```sql
SELECT COUNT(*) FROM Student;
```
```
+----------+
| COUNT(*) |
+----------+
| 12       |
+----------+
```

### (c) INSERT — Data on Specific Fields Only

**Description:** Inserts a new row while providing values for only some columns (other columns become NULL). This is done by explicitly listing which columns you're filling.

**Syntax:**
```sql
INSERT INTO table_name (col1, col2) VALUES (val1, val2);
```

**Example:**
```sql
INSERT INTO Student (stu_id, Name, City) VALUES (13, 'Rahul Mehta', 'Mumbai');
```

**Verify:**
```sql
SELECT * FROM Student WHERE stu_id = 13;
```

**Output:**
```
+--------+-------------+-------------+-------+--------+----------+
| stu_id | Name        | Father_Name | Email | City   | HS_Marks |
+--------+-------------+-------------+-------+--------+----------+
| 13     | Rahul Mehta | NULL        | NULL  | Mumbai | NULL     |
+--------+-------------+-------------+-------+--------+----------+
```

Notice Father_Name, Email, and HS_Marks are NULL because we didn't provide values for them.

### (d) SELECT — Specific Columns Only

**Description:** Retrieves only chosen columns instead of the entire table — useful when you don't need every field.

**Syntax:**
```sql
SELECT col1, col2 FROM table_name;
```

**Example:**
```sql
SELECT Name, City, HS_Marks FROM Student;
```

**Output:**
```
+---------------+------------+----------+
| Name          | City       | HS_Marks |
+---------------+------------+----------+
| Aarav Sharma  | Delhi      | 85.50    |
| Priya Patel   | Ahmedabad  | 78.25    |
| Rohan Verma   | Lucknow    | 92.00    |
| Sneha Reddy   | Hyderabad  | 88.75    |
| Karan Singh   | Jaipur     | 65.40    |
| Ananya Iyer   | Chennai    | 91.20    |
| Vikram Nair   | Kochi      | 73.60    |
| Divya Menon   | Kochi      | 80.00    |
| Arjun Gupta   | Kanpur     | 68.90    |
| Kavya Rao     | Bangalore  | 95.30    |
| Aditya Joshi  | Pune       | 77.85    |
| Meera Desai   | Surat      | 83.15    |
| Rahul Mehta   | Mumbai     | NULL     |
+---------------+------------+----------+
13 rows in set (0.00 sec)
```

### (e) ALTER TABLE — Add a New Column, Insert Data, and Verify

**Description:** Adds a new column (Phone) to the existing table structure, then fills it in for a record.

**Step 1 — Add the column:**
```sql
ALTER TABLE Student ADD Phone VARCHAR(15);
```

**Verify structure:**
```sql
DESCRIBE Student;
```
```
+-------------+--------------+------+-----+---------+-------+
| Field       | Type         | Null | Key | Default | Extra |
+-------------+--------------+------+-----+---------+-------+
| stu_id      | int          | NO   | PRI | NULL    |       |
| Name        | varchar(50)  | NO   |     | NULL    |       |
| Father_Name | varchar(50)  | YES  |     | NULL    |       |
| Email       | varchar(100) | YES  |     | NULL    |       |
| City        | varchar(50)  | YES  |     | NULL    |       |
| HS_Marks    | decimal(5,2) | YES  |     | NULL    |       |
| Phone       | varchar(15)  | YES  |     | NULL    |       |
+-------------+--------------+------+-----+---------+-------+
```

**Step 2 — Insert/update data into the new column:**
```sql
UPDATE Student SET Phone = '9876543210' WHERE stu_id = 1;
```

**Verify:**
```sql
SELECT stu_id, Name, Phone FROM Student WHERE stu_id = 1;
```
```
+--------+--------------+------------+
| stu_id | Name         | Phone      |
+--------+--------------+------------+
| 1      | Aarav Sharma | 9876543210 |
+--------+--------------+------------+
```

### (f) UPDATE — Updating Existing Data

**Description:** Modifies values in existing rows based on a condition.

**Syntax:**
```sql
UPDATE table_name SET column = value WHERE condition;
```

**Example:**
```sql
UPDATE Student SET HS_Marks = 90.00 WHERE stu_id = 5;
```

**Verify:**
```sql
SELECT stu_id, Name, HS_Marks FROM Student WHERE stu_id = 5;
```

**Output:**
```
+--------+-------------+----------+
| stu_id | Name        | HS_Marks |
+--------+-------------+----------+
| 5      | Karan Singh | 90.00    |
+--------+-------------+----------+
```

⚠️ Always use WHERE with UPDATE — omitting it updates every row in the table.

### (g) DELETE — Deleting Data

**Description:** Removes one or more rows from the table based on a condition.

**Syntax:**
```sql
DELETE FROM table_name WHERE condition;
```

**Example:**
```sql
DELETE FROM Student WHERE stu_id = 13;
```

**Verify:**
```sql
SELECT * FROM Student WHERE stu_id = 13;
```

**Output:**
```
Empty set (0.00 sec)
```

The row for stu_id = 13 (Rahul Mehta) is gone.

⚠️ Always use WHERE with DELETE — omitting it deletes all rows in the table.

### (h) MERGING DATA — Upsert in MySQL

**Description:** Standard SQL has a MERGE statement, but MySQL does not support MERGE. Instead, MySQL provides INSERT ... ON DUPLICATE KEY UPDATE — this inserts a new row, but if a row with the same primary/unique key already exists, it updates that row instead. This is called an "upsert" (update + insert).

**Syntax:**
```sql
INSERT INTO table_name (col1, col2, ...)
VALUES (val1, val2, ...)
ON DUPLICATE KEY UPDATE col2 = val2, ...;
```

**Example — Case 1: Key doesn't exist yet (acts as INSERT)**
```sql
INSERT INTO Student (stu_id, Name, City, HS_Marks)
VALUES (14, 'Isha Kapoor', 'Indore', 89.00)
ON DUPLICATE KEY UPDATE City = 'Indore', HS_Marks = 89.00;
```

**Output:**
```
Query OK, 1 row affected (0.01 sec)
```

**Example — Case 2: Key already exists (acts as UPDATE)**
```sql
INSERT INTO Student (stu_id, Name, City, HS_Marks)
VALUES (14, 'Isha Kapoor', 'Bhopal', 93.50)
ON DUPLICATE KEY UPDATE City = 'Bhopal', HS_Marks = 93.50;
```

**Output:**
```
Query OK, 2 rows affected (0.01 sec)
```

2 rows affected is MySQL's way of confirming it took the UPDATE path (1 for delete-equivalent + 1 for insert-equivalent), not a fresh insert.

**Verify:**
```sql
SELECT * FROM Student WHERE stu_id = 14;
```

**Output:**
```
+--------+-------------+-------------+-------+--------+----------+-------+
| stu_id | Name        | Father_Name | Email | City   | HS_Marks | Phone |
+--------+-------------+-------------+-------+--------+----------+-------+
| 14     | Isha Kapoor | NULL        | NULL  | Bhopal | 93.50    | NULL  |
+--------+-------------+-------------+-------+--------+----------+-------+
```

**Alternative (MySQL-specific) — REPLACE:** REPLACE fully deletes the old row and inserts a brand-new one (so any unlisted columns reset to their defaults, unlike ON DUPLICATE KEY UPDATE which only touches the columns you specify).

```sql
REPLACE INTO Student (stu_id, Name, City, HS_Marks)
VALUES (14, 'Isha Kapoor', 'Bhopal', 93.50);
```
