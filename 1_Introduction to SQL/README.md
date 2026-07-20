# Chapter 1: Introduction to SQL

A beginner-friendly guide covering the fundamentals of SQL (Structured Query Language) — terminology, data types, operators, keys, and constraints.

## Table of Contents

- [What is SQL?](#what-is-sql)
- [SQL Related Terminologies](#sql-related-terminologies)
- [SQL Statements](#sql-statements)
- [SQL Data Types](#sql-data-types)
- [SQL Operators](#sql-operators)
  - [Arithmetic Operators](#a-arithmetic-operators)
  - [Comparison (Relational) Operators](#b-comparison-relational-operators)
  - [Logical Operators](#c-logical-operators)
  - [Special Operators](#d-special-operators)
  - [Bitwise Operators (MySQL)](#e-bitwise-operators-mysql)
- [Keys in SQL](#keys-in-sql)
- [SQL Constraints](#sql-constraints)
- [SQL vs NoSQL](#sql-vs-nosql)

---

## What is SQL?

SQL stands for **Structured Query Language**, a computer language used for manipulating and retrieving data stored in a database. SQL was developed by Donald D. Chamberlin and Raymond F. Boyce at IBM in the early 1970s. It was originally called **SEQUEL** (Structured English Query Language).

---

## SQL Related Terminologies

| Terminology | Short Introduction | Example |
|---|---|---|
| **Database** | An organized collection of related data stored electronically. | `CollegeDB` is a database containing Student, Faculty, and Course tables. |
| **Table** | A collection of related data organized into rows and columns. | The `Student` table stores student information such as ID, Name, and Age. |
| **Field (Column/Attribute)** | A single column in a table that stores one type of data. | In the Student table, `ID`, `Name`, and `Age` are fields. |
| **Record (Row/Tuple)** | A single row in a table containing complete information about one entity. | `(101, 'Rahul', 20)` is one record in the Student table. |

### Example Table: `Student`

| ID | Name | Age |
|---|---|---|
| 101 | Rahul | 20 |
| 102 | Priya | 21 |
| 103 | Amit | 19 |

**Explanation:**
- Database: `CollegeDB`
- Table: `Student`
- Fields (Columns): `ID`, `Name`, `Age`
- Records (Rows): `(101, Rahul, 20)`, `(102, Priya, 21)`, `(103, Amit, 19)`

---

## SQL Statements

SQL statements are commands or instructions written in Structured Query Language that tell a database what operations to perform. SQL commands are grouped into the following categories:

- **DDL** — Data Definition Language
- **DML** — Data Manipulation Language
- **DCL** — Data Control Language
- **TCL** — Transaction Control Language
- **DQL** — Data Query Language

---

## SQL Data Types

The data type of a field defines what kind of value will be stored, and is defined when creating a table. Data types are mainly classified into three categories:

- **String** — `char`, `varchar`, etc.
- **Numeric** — `int`, `float`, `bool`, etc.
- **Date and Time** — `date`, `datetime`, etc.

### Commonly Used Data Types in SQL

| Data Type | Purpose | Format / Syntax | Example |
|---|---|---|---|
| **INT** | Stores whole numbers. | `INT` | `Age INT` |
| **VARCHAR(n)** | Stores variable-length text. | `VARCHAR(size)` | `Name VARCHAR(50)` |
| **CHAR(n)** | Stores fixed-length text. | `CHAR(size)` | `Gender CHAR(1)` |
| **FLOAT** | Stores approximate decimal numbers. | `FLOAT` | `Percentage FLOAT` |
| **DECIMAL(p,s)** | Stores exact decimal values (used for money). | `DECIMAL(precision, scale)` | `Salary DECIMAL(10,2)` |
| **DATE** | Stores a date. | `YYYY-MM-DD` | `DOB DATE → 2003-08-15` |
| **TIME** | Stores time. | `HH:MM:SS` | `LoginTime TIME → 10:30:45` |
| **DATETIME** | Stores date and time. | `YYYY-MM-DD HH:MM:SS` | `CreatedAt DATETIME → 2026-07-15 10:30:45` |
| **TIMESTAMP** | Stores date and time (can auto-update). | `YYYY-MM-DD HH:MM:SS` | `UpdatedAt TIMESTAMP` |
| **BOOLEAN (BOOL)** | Stores logical values (TRUE/FALSE). | `BOOLEAN` | `IsActive BOOLEAN (TRUE or FALSE)` |
| **TEXT** | Stores long text. | `TEXT` | `Address TEXT` |

---

## SQL Operators

SQL operators are special symbols or keywords used to perform operations on data, compare values, combine conditions, and manipulate query results.

### A. Arithmetic Operators

Used to perform mathematical calculations.

| Operator | Description | Example | Result |
|---|---|---|---|
| `+` | Addition | `SELECT 10 + 5;` | 15 |
| `-` | Subtraction | `SELECT 10 - 5;` | 5 |
| `*` | Multiplication | `SELECT 10 * 5;` | 50 |
| `/` | Division | `SELECT 10 / 5;` | 2 |
| `%` | Modulus (Remainder) | `SELECT 10 % 3;` | 1 |

### B. Comparison (Relational) Operators

Used to compare two values.

| Operator | Description | Example | Result |
|---|---|---|---|
| `=` | Equal to | `SELECT * FROM Student WHERE Age = 20;` | Returns students with Age = 20 |
| `!=` or `<>` | Not equal to | `SELECT * FROM Student WHERE Age <> 20;` | Returns students whose Age is not 20 |
| `>` | Greater than | `SELECT * FROM Student WHERE Marks > 80;` | Marks greater than 80 |
| `<` | Less than | `SELECT * FROM Student WHERE Age < 18;` | Age less than 18 |
| `>=` | Greater than or equal to | `SELECT * FROM Student WHERE Salary >= 30000;` | Salary ≥ 30000 |
| `<=` | Less than or equal to | `SELECT * FROM Student WHERE Marks <= 50;` | Marks ≤ 50 |

### C. Logical Operators

Used to combine multiple conditions.

| Operator | Description | Example | Result |
|---|---|---|---|
| `AND` | Returns TRUE if both conditions are TRUE. | `SELECT * FROM Student WHERE Age>18 AND Marks>80;` | Students satisfying both conditions |
| `OR` | Returns TRUE if any one condition is TRUE. | `SELECT * FROM Student WHERE City='Kolkata' OR City='Delhi';` | Students from Kolkata or Delhi |
| `NOT` | Reverses the condition. | `SELECT * FROM Student WHERE NOT Age=20;` | Students whose Age is not 20 |

### D. Special Operators

Used for specific search and filtering operations.

| Operator | Description | Example | Result |
|---|---|---|---|
| `BETWEEN` | Selects values within a range. | `SELECT * FROM Student WHERE Marks BETWEEN 60 AND 80;` | Marks between 60 and 80 |
| `IN` | Matches any value in a list. | `SELECT * FROM Student WHERE City IN ('Kolkata','Delhi');` | Students from Kolkata or Delhi |
| `NOT IN` | Excludes values in a list. | `SELECT * FROM Student WHERE City NOT IN ('Kolkata','Delhi');` | Students from other cities |
| `LIKE` | Searches using wildcard patterns. | `SELECT * FROM Student WHERE Name LIKE 'A%';` | Names starting with A |
| `NOT LIKE` | Excludes matching patterns. | `SELECT * FROM Student WHERE Name NOT LIKE 'A%';` | Names not starting with A |
| `IS NULL` | Checks for NULL values. | `SELECT * FROM Student WHERE Phone IS NULL;` | Records with NULL phone |
| `IS NOT NULL` | Checks for non-NULL values. | `SELECT * FROM Student WHERE Phone IS NOT NULL;` | Records with phone numbers |
| `EXISTS` | Returns TRUE if a subquery returns records. | `SELECT * FROM Student WHERE EXISTS (SELECT * FROM Course);` | Returns records if Course table has data |
| `ANY` | Compares with any value returned by a subquery. | `SELECT * FROM Student WHERE Marks > ANY (SELECT Marks FROM Topper);` | Marks greater than any topper's mark |
| `ALL` | Compares with all values returned by a subquery. | `SELECT * FROM Student WHERE Marks > ALL (SELECT Marks FROM Failed);` | Marks greater than all failed students |

### E. Bitwise Operators (MySQL)

| Operator | Description | Example | Result |
|---|---|---|---|
| `&` | Bitwise AND | `SELECT 5 & 3;` | 1 |
| `\|` | Bitwise OR | `SELECT 5 \| 3;` | 7 |
| `^` | Bitwise XOR | `SELECT 5 ^ 3;` | 6 |
| `~` | Bitwise NOT | `SELECT ~5;` | -6 |
| `<<` | Left Shift | `SELECT 5 << 1;` | 10 |
| `>>` | Right Shift | `SELECT 5 >> 1;` | 2 |

---

## Keys in SQL

A **key** in SQL is a field (column) or a combination of fields used to uniquely identify records, establish relationships between tables, and maintain data integrity.

### A. Primary Key (PK)

Uniquely identifies each record in a table. It cannot contain NULL values, and duplicate values are not allowed.

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    Age INT
);
```

| StudentID | Name | Age |
|---|---|---|
| 101 | Rahul | 20 |
| 102 | Priya | 21 |

**Key:** `StudentID` as a primary key

### B. Foreign Key (FK)

A column that refers to the Primary Key of another table. It establishes a relationship between two tables.

```sql
CREATE TABLE Department (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50)
);

CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Name VARCHAR(50),
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

**Relationship:** `Student.DeptID → Department.DeptID`

### C. Candidate Key

Any column (or set of columns) that can uniquely identify a record. A table can have multiple candidate keys.

| StudentID | Email |
|---|---|
| 101 | rahul@gmail.com |
| 102 | priya@gmail.com |

Both `StudentID` and `Email` can uniquely identify a student, so both are Candidate Keys.

### D. Alternate Key

A Candidate Key that is not selected as the Primary Key.

**Example:** If `StudentID` is the Primary Key, then `Email` becomes the Alternate Key.

### E. Super Key

Any column or combination of columns that uniquely identifies a record. It may contain extra attributes.

**Example:**
- `(StudentID)`
- `(StudentID, Name)`
- `(StudentID, Email)`

All of these are Super Keys because they uniquely identify a student.

### F. Composite Key (Compound Key)

A Primary Key formed by two or more columns.

```sql
CREATE TABLE Enrollment (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID)
);
```

Here, `StudentID` and `CourseID` together uniquely identify each record.

### G. Unique Key

Ensures that all values in a column are unique. Unlike a Primary Key, it can allow one NULL value in MySQL.

```sql
CREATE TABLE Student (
    StudentID INT PRIMARY KEY,
    Email VARCHAR(100) UNIQUE
);
```

`Email` cannot contain duplicate values.

---

## SQL Constraints

SQL Constraints are rules applied to table columns to ensure the accuracy, consistency, and integrity of data stored in a database. They prevent invalid data from being inserted, updated, or deleted.

**Types:**
- `NOT NULL`
- `UNIQUE`
- `PRIMARY KEY`
- `FOREIGN KEY`
- `CHECK`
- `DEFAULT`
- `AUTO_INCREMENT` (MySQL-specific)

### NOT NULL Constraint

**Use:** Ensures that a column cannot contain NULL values.

**Syntax:** `column_name datatype NOT NULL`

```sql
CREATE TABLE Student(
    Roll INT,
    Name VARCHAR(50) NOT NULL
);
```

- ✅ Valid: `INSERT INTO Student VALUES(101,'Rahul');`
- ❌ Invalid: `INSERT INTO Student VALUES(102,NULL);` — Reason: `Name` cannot be NULL.

### UNIQUE Constraint

**Use:** Ensures that all values in a column are different.

**Syntax:** `column_name datatype UNIQUE`

```sql
CREATE TABLE Student(
    Roll INT,
    Email VARCHAR(50) UNIQUE
);
```

- ✅ Valid:
  ```sql
  INSERT INTO Student VALUES(101,'a@gmail.com');
  INSERT INTO Student VALUES(102,'b@gmail.com');
  ```
- ❌ Invalid: `INSERT INTO Student VALUES(103,'a@gmail.com');` — Reason: Duplicate value is not allowed.

### PRIMARY KEY Constraint

**Use:** Uniquely identifies each record in a table. It is a combination of **NOT NULL + UNIQUE**.

**Syntax:** `column_name datatype PRIMARY KEY`

```sql
CREATE TABLE Student(
    Roll INT PRIMARY KEY,
    Name VARCHAR(50)
);
```

- ✅ Valid:
  ```sql
  INSERT INTO Student VALUES(101,'Rahul');
  INSERT INTO Student VALUES(102,'Riya');
  ```
- ❌ Invalid (Duplicate): `INSERT INTO Student VALUES(101,'Amit');`
- ❌ Invalid (NULL): `INSERT INTO Student VALUES(NULL,'Riya');` — Reason: Primary key cannot be NULL or duplicate.

### FOREIGN KEY Constraint

**Use:** Creates a relationship between two tables and ensures referential integrity.

**Syntax:**
```sql
FOREIGN KEY(column_name)
REFERENCES ParentTable(parent_column)
```

**Parent Table:**
```sql
CREATE TABLE Department(
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(30)
);
```

**Child Table:**
```sql
CREATE TABLE Student(
    Roll INT PRIMARY KEY,
    Name VARCHAR(50),
    DeptID INT,
    FOREIGN KEY(DeptID) REFERENCES Department(DeptID)
);
```

- ✅ Valid:
  ```sql
  INSERT INTO Department VALUES(1,'CSE');
  INSERT INTO Student VALUES(101,'Rahul',1);
  ```
- ❌ Invalid: `INSERT INTO Student VALUES(102,'Amit',5);` — Reason: Department 5 does not exist.

### CHECK Constraint

**Use:** Allows only values that satisfy a specified condition.

**Syntax:** `column_name datatype CHECK(condition)`

```sql
CREATE TABLE Student(
    Roll INT,
    Age INT CHECK(Age>=18)
);
```

- ✅ Valid: `INSERT INTO Student VALUES(101,20);`
- ❌ Invalid: `INSERT INTO Student VALUES(102,16);` — Reason: Age must be 18 or above.

### DEFAULT Constraint

**Use:** Assigns a default value if no value is provided.

**Syntax:** `column_name datatype DEFAULT value`

```sql
CREATE TABLE Employee(
    ID INT,
    City VARCHAR(30) DEFAULT 'Kolkata'
);
```

- ✅ Valid: `INSERT INTO Employee(ID) VALUES(101);`

  **Result:**

  | ID | City |
  |---|---|
  | 101 | Kolkata |

- ❌ Invalid:
  ```sql
  CREATE TABLE Employee(
      ID INT,
      City VARCHAR(30) DEFAULT
  );
  ```
  Reason: DEFAULT value is missing.

### AUTO_INCREMENT (MySQL)

**Use:** Automatically generates sequential numeric values.

**Syntax:**
```sql
column_name INT AUTO_INCREMENT PRIMARY KEY
```

```sql
CREATE TABLE Student(
    Roll INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(50)
);
```

- ✅ Valid:
  ```sql
  INSERT INTO Student(Name) VALUES('Rahul');
  INSERT INTO Student(Name) VALUES('Riya');
  ```

  **Result:**

  | Roll | Name |
  |---|---|
  | 1 | Rahul |
  | 2 | Riya |

- ❌ Invalid:
  ```sql
  CREATE TABLE Student(
      Roll VARCHAR(20) AUTO_INCREMENT
  );
  ```
  Reason: AUTO_INCREMENT can only be used with integer-type columns.

---

## SQL vs NoSQL

| Feature | SQL | NoSQL |
|---|---|---|
| **Database Type** | Relational Database | Non-Relational Database |
| **Data Storage** | Stores data in tables (rows and columns) | Stores data as documents, key-value pairs, columns, or graphs |
| **Schema** | Fixed (Predefined) Schema | Flexible (Dynamic) Schema |
| **Scalability** | Vertical Scaling (increase server resources) | Horizontal Scaling (add more servers) |
| **Examples** | MySQL, Oracle, PostgreSQL, SQL Server | MongoDB, Cassandra, Redis, CouchDB |

---

## License

This document is provided for educational purposes.
