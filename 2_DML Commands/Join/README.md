# SQL Joins and Set Operations — Complete Lab Guide

This README explains **SQL selections, projections, joins, and set operations** using simple examples.

> **Note:** The database name is written as `college` (correct spelling of "collage").  
> The examples are written for **MySQL**.

---

## 1. What is a JOIN in SQL?

A **JOIN** is used to combine rows from two or more tables based on a related column.

### Simple Example

Suppose we have two tables:

### `student`

| student_id | student_name | dept_id |
|---:|---|---:|
| 1 | Rahul | 101 |
| 2 | Priya | 102 |

### `depart`

| dept_id | dept_name |
|---:|---|
| 101 | Computer Science |
| 102 | Information Technology |

The common column is `dept_id`.

If we want to display the student name together with the department name:

```sql
SELECT s.student_name, d.dept_name
FROM student AS s
INNER JOIN depart AS d
ON s.dept_id = d.dept_id;
```

### Output

| student_name | dept_name |
|---|---|
| Rahul | Computer Science |
| Priya | Information Technology |

So, **JOIN connects related information stored in different tables.**

---

# 2. Pre-Requisite Setup

## 2.1 Create Database

```sql
CREATE DATABASE IF NOT EXISTS college;
```

Select the database:

```sql
USE college;
```

---

# 2.2 Create the Required Tables

We will create exactly **3 tables**:

1. `student`
2. `faculty`
3. `depart`

Each table contains **5 fields** and **5 records**.

---

## Table 1: `depart`

### Fields

| Field | Data Type | Description |
|---|---|---|
| dept_id | INT | Department ID |
| dept_name | VARCHAR(50) | Department name |
| location | VARCHAR(50) | Department location |
| hod_name | VARCHAR(50) | Head of Department |
| phone | VARCHAR(15) | Department phone |

### Create Table

```sql
CREATE TABLE depart (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL,
    location VARCHAR(50),
    hod_name VARCHAR(50),
    phone VARCHAR(15)
);
```

### Insert 5 Records

```sql
INSERT INTO depart
(dept_id, dept_name, location, hod_name, phone)
VALUES
(101, 'Computer Science', 'Block A', 'Dr. Anil Kumar', '9000000001'),
(102, 'Information Technology', 'Block B', 'Dr. Sunita Roy', '9000000002'),
(103, 'Electronics', 'Block C', 'Dr. Amit Das', '9000000003'),
(104, 'Mechanical', 'Block D', 'Dr. Rina Sen', '9000000004'),
(105, 'Civil', 'Block E', 'Dr. Suman Ghosh', '9000000005');
```

---

## Table 2: `student`

### Fields

| Field | Data Type | Description |
|---|---|---|
| student_id | INT | Student ID |
| student_name | VARCHAR(50) | Student name |
| dept_id | INT | Department ID |
| city | VARCHAR(50) | Student city |
| marks | INT | Student marks |

### Create Table

```sql
CREATE TABLE student (
    student_id INT PRIMARY KEY,
    student_name VARCHAR(50) NOT NULL,
    dept_id INT,
    city VARCHAR(50),
    marks INT
);
```

### Insert 5 Records

```sql
INSERT INTO student
(student_id, student_name, dept_id, city, marks)
VALUES
(1, 'Rahul', 101, 'Kolkata', 85),
(2, 'Priya', 102, 'Durgapur', 78),
(3, 'Amit', 103, 'Kolkata', 92),
(4, 'Sneha', 101, 'Siliguri', 67),
(5, 'Rohan', 105, 'Howrah', 74);
```

---

## Table 3: `faculty`

### Fields

| Field | Data Type | Description |
|---|---|---|
| faculty_id | INT | Faculty ID |
| faculty_name | VARCHAR(50) | Faculty name |
| dept_id | INT | Department ID |
| designation | VARCHAR(50) | Faculty designation |
| salary | DECIMAL(10,2) | Faculty salary |

### Create Table

```sql
CREATE TABLE faculty (
    faculty_id INT PRIMARY KEY,
    faculty_name VARCHAR(50) NOT NULL,
    dept_id INT,
    designation VARCHAR(50),
    salary DECIMAL(10,2)
);
```

### Insert 5 Records

```sql
INSERT INTO faculty
(faculty_id, faculty_name, dept_id, designation, salary)
VALUES
(201, 'Arun Sharma', 101, 'Assistant Professor', 45000.00),
(202, 'Mita Roy', 102, 'Associate Professor', 58000.00),
(203, 'Kamal Das', 103, 'Assistant Professor', 47000.00),
(204, 'Neha Sen', 104, 'Professor', 70000.00),
(205, 'Sourav Paul', 105, 'Assistant Professor', 43000.00);
```

---

# 2.3 Verify the Tables

## Verify Database

```sql
SHOW DATABASES;
```

### Select Database

```sql
USE college;
```

## Verify Tables

```sql
SHOW TABLES;
```

Expected tables:

| Tables |
|---|
| depart |
| faculty |
| student |

---

## Verify Table Structure

```sql
DESC student;
DESC faculty;
DESC depart;
```

---

## Verify All Records

### Student

```sql
SELECT * FROM student;
```

### Output

| student_id | student_name | dept_id | city | marks |
|---:|---|---:|---|---:|
| 1 | Rahul | 101 | Kolkata | 85 |
| 2 | Priya | 102 | Durgapur | 78 |
| 3 | Amit | 103 | Kolkata | 92 |
| 4 | Sneha | 101 | Siliguri | 67 |
| 5 | Rohan | 105 | Howrah | 74 |

### Faculty

```sql
SELECT * FROM faculty;
```

### Output

| faculty_id | faculty_name | dept_id | designation | salary |
|---:|---|---:|---|---:|
| 201 | Arun Sharma | 101 | Assistant Professor | 45000.00 |
| 202 | Mita Roy | 102 | Associate Professor | 58000.00 |
| 203 | Kamal Das | 103 | Assistant Professor | 47000.00 |
| 204 | Neha Sen | 104 | Professor | 70000.00 |
| 205 | Sourav Paul | 105 | Assistant Professor | 43000.00 |

### Department

```sql
SELECT * FROM depart;
```

### Output

| dept_id | dept_name | location | hod_name | phone |
|---:|---|---|---|---|
| 101 | Computer Science | Block A | Dr. Anil Kumar | 9000000001 |
| 102 | Information Technology | Block B | Dr. Sunita Roy | 9000000002 |
| 103 | Electronics | Block C | Dr. Amit Das | 9000000003 |
| 104 | Mechanical | Block D | Dr. Rina Sen | 9000000004 |
| 105 | Civil | Block E | Dr. Suman Ghosh | 9000000005 |

---

# 3. Basic Relational Operations

The main basic operations are:

1. Selection
2. Projection
3. Join
4. Set Operations

---

# 3.1 Selection

## Definition

**Selection** is used to select specific **rows** from a table based on a condition.

In SQL, selection is performed using the `WHERE` clause.

### Syntax

```sql
SELECT *
FROM table_name
WHERE condition;
```

### Example

Find students whose marks are greater than 80:

```sql
SELECT *
FROM student
WHERE marks > 80;
```

### Output

| student_id | student_name | dept_id | city | marks |
|---:|---|---:|---|---:|
| 1 | Rahul | 101 | Kolkata | 85 |
| 3 | Amit | 103 | Kolkata | 92 |

### Important Point

**Selection → selects rows.**

---

# 3.2 Projection

## Definition

**Projection** is used to select specific **columns** from a table.

In SQL, projection is performed by specifying the required columns after `SELECT`.

### Syntax

```sql
SELECT column1, column2
FROM table_name;
```

### Example

Display only student name and marks:

```sql
SELECT student_name, marks
FROM student;
```

### Output

| student_name | marks |
|---|---:|
| Rahul | 85 |
| Priya | 78 |
| Amit | 92 |
| Sneha | 67 |
| Rohan | 74 |

### Important Point

**Projection → selects columns.**

---

# 4. Binary Operation — JOIN

A JOIN is a **binary relational operation** because it combines rows from two relations/tables.

Our common joining column is:

```text
student.dept_id
faculty.dept_id
depart.dept_id
```

---

# 4.1 INNER JOIN

## Definition

An **INNER JOIN** returns only the rows where a matching value exists in both tables.

Only the common/matching part is returned.

### Syntax

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### Example

Display students with their department names:

```sql
SELECT
    s.student_id,
    s.student_name,
    d.dept_name
FROM student AS s
INNER JOIN depart AS d
ON s.dept_id = d.dept_id;
```

### Output

| student_id | student_name | dept_name |
|---:|---|---|
| 1 | Rahul | Computer Science |
| 2 | Priya | Information Technology |
| 3 | Amit | Electronics |
| 4 | Sneha | Computer Science |
| 5 | Rohan | Civil |

---

# 4.2 THETA JOIN

## Definition

A **Theta Join** is a join where the joining condition can use any comparison operator such as:

```text
=
<
>
<=
>=
<>
```

It is called a theta join because the condition can be represented by a general comparison condition.

### Syntax

```sql
SELECT columns
FROM table1
JOIN table2
ON table1.column operator table2.column;
```

### Example

Compare student marks with faculty salary.

To make the comparison meaningful, we convert the salary to thousands:

```sql
SELECT
    s.student_name,
    s.marks,
    f.faculty_name,
    f.salary
FROM student AS s
JOIN faculty AS f
ON s.marks > (f.salary / 1000);
```

### Output

| student_name | marks | faculty_name | salary |
|---|---:|---|---:|
| Rahul | 85 | Arun Sharma | 45000.00 |
| Rahul | 85 | Mita Roy | 58000.00 |
| Rahul | 85 | Kamal Das | 47000.00 |
| Rahul | 85 | Neha Sen | 70000.00 |
| Rahul | 85 | Sourav Paul | 43000.00 |
| Priya | 78 | Arun Sharma | 45000.00 |
| Priya | 78 | Mita Roy | 58000.00 |
| Priya | 78 | Kamal Das | 47000.00 |
| Priya | 78 | Neha Sen | 70000.00 |
| Priya | 78 | Sourav Paul | 43000.00 |
| Amit | 92 | Arun Sharma | 45000.00 |
| Amit | 92 | Mita Roy | 58000.00 |
| Amit | 92 | Kamal Das | 47000.00 |
| Amit | 92 | Neha Sen | 70000.00 |
| Amit | 92 | Sourav Paul | 43000.00 |
| Sneha | 67 | Arun Sharma | 45000.00 |
| Sneha | 67 | Mita Roy | 58000.00 |
| Sneha | 67 | Kamal Das | 47000.00 |
| Sneha | 67 | Sourav Paul | 43000.00 |
| Rohan | 74 | Arun Sharma | 45000.00 |
| Rohan | 74 | Mita Roy | 58000.00 |
| Rohan | 74 | Kamal Das | 47000.00 |
| Rohan | 74 | Neha Sen | 70000.00 |
| Rohan | 74 | Sourav Paul | 43000.00 |

> **Note:** This example intentionally uses a non-equality condition to demonstrate a Theta Join.

---

# 4.3 EQUI JOIN

## Definition

An **Equi Join** is a join where the joining condition uses the equality operator `=`.

### Syntax

```sql
SELECT columns
FROM table1
JOIN table2
ON table1.column = table2.column;
```

### Example

```sql
SELECT
    s.student_name,
    d.dept_name
FROM student AS s
JOIN depart AS d
ON s.dept_id = d.dept_id;
```

### Output

| student_name | dept_name |
|---|---|
| Rahul | Computer Science |
| Priya | Information Technology |
| Amit | Electronics |
| Sneha | Computer Science |
| Rohan | Civil |

### Difference Between Theta Join and Equi Join

| Theta Join | Equi Join |
|---|---|
| Can use `=`, `<`, `>`, `<=`, `>=`, `<>` | Uses `=` |
| More general | Special case of Theta Join |

---

# 4.4 NATURAL JOIN

## Definition

A **Natural Join** automatically joins tables using columns having the **same name**.

Our tables have a common column named `dept_id`.

### Syntax

```sql
SELECT columns
FROM table1
NATURAL JOIN table2;
```

### Example

```sql
SELECT
    student_name,
    dept_name
FROM student
NATURAL JOIN depart;
```

### Output

| student_name | dept_name |
|---|---|
| Rahul | Computer Science |
| Priya | Information Technology |
| Amit | Electronics |
| Sneha | Computer Science |
| Rohan | Civil |

### Important Point

You do not explicitly write:

```sql
ON student.dept_id = depart.dept_id
```

because MySQL automatically uses the common column `dept_id`.

> **Caution:** Natural joins can become risky if tables later contain another column with the same name. Explicit `JOIN ... ON` is generally easier to understand.

---

# 4.5 SEMI JOIN

## Definition

A **Semi Join** returns rows from the **first table only** when a matching row exists in the second table.

SQL does not have a standard `SEMI JOIN` keyword. We commonly implement it using `EXISTS`.

### Syntax

```sql
SELECT columns
FROM table1 AS A
WHERE EXISTS (
    SELECT 1
    FROM table2 AS B
    WHERE A.column = B.column
);
```

### Example

Find students whose department exists in the department table:

```sql
SELECT
    s.student_id,
    s.student_name,
    s.dept_id
FROM student AS s
WHERE EXISTS (
    SELECT 1
    FROM depart AS d
    WHERE s.dept_id = d.dept_id
);
```

### Output

| student_id | student_name | dept_id |
|---:|---|---:|
| 1 | Rahul | 101 |
| 2 | Priya | 102 |
| 3 | Amit | 103 |
| 4 | Sneha | 101 |
| 5 | Rohan | 105 |

### Important Point

A Semi Join returns **only columns/rows from the left table**.

---

# 4.6 ANTI JOIN

## Definition

An **Anti Join** returns rows from the first table for which **no matching row exists** in the second table.

SQL does not have a standard `ANTI JOIN` keyword. It can be implemented using `NOT EXISTS`.

Our current data has a match for every student. To demonstrate Anti Join, add one student with a department that does not exist:

```sql
INSERT INTO student
(student_id, student_name, dept_id, city, marks)
VALUES
(6, 'Kiran', 106, 'Bardhaman', 81);
```

Now execute:

```sql
SELECT
    s.student_id,
    s.student_name,
    s.dept_id
FROM student AS s
WHERE NOT EXISTS (
    SELECT 1
    FROM depart AS d
    WHERE s.dept_id = d.dept_id
);
```

### Output

| student_id | student_name | dept_id |
|---:|---|---:|
| 6 | Kiran | 106 |

### Important

If you want to return to the original 5-student dataset:

```sql
DELETE FROM student
WHERE student_id = 6;
```

---

# 5. OUTER JOIN

Outer joins return matching rows **plus some or all non-matching rows**.

Types:

1. Left Outer Join
2. Right Outer Join
3. Full Outer Join

---

# 5.1 LEFT OUTER JOIN

## Definition

A **LEFT OUTER JOIN** returns:

- All rows from the left table
- Matching rows from the right table
- `NULL` when no matching right-side row exists

### Syntax

```sql
SELECT columns
FROM table1 AS A
LEFT JOIN table2 AS B
ON A.column = B.column;
```

### Example

First add an extra student with no matching department:

```sql
INSERT INTO student
(student_id, student_name, dept_id, city, marks)
VALUES
(6, 'Kiran', 106, 'Bardhaman', 81);
```

Now:

```sql
SELECT
    s.student_id,
    s.student_name,
    s.dept_id,
    d.dept_name
FROM student AS s
LEFT JOIN depart AS d
ON s.dept_id = d.dept_id;
```

### Output

| student_id | student_name | dept_id | dept_name |
|---:|---|---:|---|
| 1 | Rahul | 101 | Computer Science |
| 2 | Priya | 102 | Information Technology |
| 3 | Amit | 103 | Electronics |
| 4 | Sneha | 101 | Computer Science |
| 5 | Rohan | 105 | Civil |
| 6 | Kiran | 106 | NULL |

The `NULL` means no matching department was found.

---

# 5.2 RIGHT OUTER JOIN

## Definition

A **RIGHT OUTER JOIN** returns:

- All rows from the right table
- Matching rows from the left table
- `NULL` when no matching left-side row exists

To demonstrate a non-matching department, insert another department:

```sql
INSERT INTO depart
(dept_id, dept_name, location, hod_name, phone)
VALUES
(106, 'Biotechnology', 'Block F', 'Dr. Arindam Roy', '9000000006');
```

Now execute:

```sql
SELECT
    s.student_name,
    d.dept_id,
    d.dept_name
FROM student AS s
RIGHT JOIN depart AS d
ON s.dept_id = d.dept_id;
```

### Output

| student_name | dept_id | dept_name |
|---|---:|---|
| Rahul | 101 | Computer Science |
| Sneha | 101 | Computer Science |
| Priya | 102 | Information Technology |
| Amit | 103 | Electronics |
| NULL | 104 | Mechanical |
| Rohan | 105 | Civil |
| Kiran | 106 | Biotechnology |

The `NULL` means no matching student was found.

---

# 5.3 FULL OUTER JOIN

## Definition

A **FULL OUTER JOIN** returns:

- All matching rows
- All non-matching rows from the left table
- All non-matching rows from the right table

## Important MySQL Note

MySQL does **not** directly support:

```sql
FULL OUTER JOIN
```

We can simulate it using:

```sql
LEFT JOIN
UNION
RIGHT JOIN
```

### Syntax

```sql
SELECT columns
FROM table1 AS A
LEFT JOIN table2 AS B
ON A.column = B.column

UNION

SELECT columns
FROM table1 AS A
RIGHT JOIN table2 AS B
ON A.column = B.column;
```

### Example

```sql
SELECT
    s.student_name,
    d.dept_id,
    d.dept_name
FROM student AS s
LEFT JOIN depart AS d
ON s.dept_id = d.dept_id

UNION

SELECT
    s.student_name,
    d.dept_id,
    d.dept_name
FROM student AS s
RIGHT JOIN depart AS d
ON s.dept_id = d.dept_id;
```

### Output

| student_name | dept_id | dept_name |
|---|---:|---|
| Rahul | 101 | Computer Science |
| Sneha | 101 | Computer Science |
| Priya | 102 | Information Technology |
| Amit | 103 | Electronics |
| NULL | 104 | Mechanical |
| Rohan | 105 | Civil |
| Kiran | 106 | Biotechnology |

---

# 6. SET OPERATIONS

Set operations combine the results of two `SELECT` statements.

The major set operations are:

1. UNION
2. INTERSECTION
3. DIFFERENCE

## Important Rule

For set operations, the two queries should return:

- The same number of columns
- Compatible data types
- Columns in a compatible order

---

# 6.1 UNION

## Definition

`UNION` combines the results of two queries and **removes duplicate rows**.

### Syntax

```sql
SELECT column1
FROM table1

UNION

SELECT column1
FROM table2;
```

### Example

We need two compatible lists. Find cities of students and department locations:

```sql
SELECT city AS place
FROM student

UNION

SELECT location AS place
FROM depart;
```

### Output

| place |
|---|
| Kolkata |
| Durgapur |
| Siliguri |
| Howrah |
| Block A |
| Block B |
| Block C |
| Block D |
| Block E |

`UNION` removes duplicate values automatically.

---

# 6.2 INTERSECTION

## Definition

`INTERSECT` returns only the rows that are present in **both results**.

## MySQL Note

Modern MySQL versions do not provide the standard `INTERSECT` operator in the same way as some other database systems. A portable approach is to use `INNER JOIN` or `EXISTS`.

### Example Using `EXISTS`

Find cities that appear both as student cities and department locations.

```sql
SELECT DISTINCT s.city AS place
FROM student AS s
WHERE EXISTS (
    SELECT 1
    FROM depart AS d
    WHERE s.city = d.location
);
```

### Output

With the current sample data:

| place |
|---|
| *(No rows)* |

There is no common value because student cities such as `Kolkata` do not match department locations such as `Block A`.

### Better Demonstration

Add a department location named `Kolkata`:

```sql
UPDATE depart
SET location = 'Kolkata'
WHERE dept_id = 101;
```

Now execute:

```sql
SELECT DISTINCT s.city AS place
FROM student AS s
WHERE EXISTS (
    SELECT 1
    FROM depart AS d
    WHERE s.city = d.location
);
```

### Output

| place |
|---|
| Kolkata |

---

# 6.3 DIFFERENCE

## Definition

**Difference** returns rows that are present in the first result but **not present in the second result**.

In relational algebra this is commonly represented as:

```text
A − B
```

## MySQL Implementation

MySQL does not use the standard `EXCEPT` operator in the same way as some database systems.

We can use `NOT EXISTS`.

### Example

Find department IDs that exist in `depart` but have no student:

```sql
SELECT d.dept_id
FROM depart AS d
WHERE NOT EXISTS (
    SELECT 1
    FROM student AS s
    WHERE s.dept_id = d.dept_id
);
```

### Output

Using the demonstration data:

| dept_id |
|---:|
| 104 |

Department `104` (Mechanical) has no student.

---

# 7. Quick Comparison of All Operations

| Operation | Main Purpose | Returns |
|---|---|---|
| Selection | Filter rows | Selected rows |
| Projection | Select columns | Selected columns |
| Inner Join | Match two tables | Matching rows |
| Theta Join | Join using comparison | Rows satisfying condition |
| Equi Join | Join using `=` | Equal matching rows |
| Natural Join | Join using same-named columns | Matching rows |
| Semi Join | Check whether match exists | Rows from first table |
| Anti Join | Check whether match does not exist | Non-matching rows from first table |
| Left Outer Join | Keep all left rows | Left + matching right |
| Right Outer Join | Keep all right rows | Right + matching left |
| Full Outer Join | Keep everything | All left + all right |
| UNION | Combine results | Unique rows from both |
| INTERSECTION | Find common results | Common rows |
| DIFFERENCE | Find unmatched results | Rows in first result only |

---

# 8. JOIN Types at a Glance

```text
JOIN
│
├── INNER JOIN
│   ├── Theta Join
│   ├── Equi Join
│   ├── Natural Join
│   ├── Semi Join
│   └── Anti Join
│
└── OUTER JOIN
    ├── Left Outer Join
    ├── Right Outer Join
    └── Full Outer Join
```

---

# 9. Most Important Syntax Examples

## Inner Join

```sql
SELECT *
FROM student AS s
INNER JOIN depart AS d
ON s.dept_id = d.dept_id;
```

## Left Join

```sql
SELECT *
FROM student AS s
LEFT JOIN depart AS d
ON s.dept_id = d.dept_id;
```

## Right Join

```sql
SELECT *
FROM student AS s
RIGHT JOIN depart AS d
ON s.dept_id = d.dept_id;
```

## Natural Join

```sql
SELECT *
FROM student
NATURAL JOIN depart;
```

## Semi Join

```sql
SELECT *
FROM student AS s
WHERE EXISTS (
    SELECT 1
    FROM depart AS d
    WHERE s.dept_id = d.dept_id
);
```

## Anti Join

```sql
SELECT *
FROM student AS s
WHERE NOT EXISTS (
    SELECT 1
    FROM depart AS d
    WHERE s.dept_id = d.dept_id
);
```

## Full Outer Join in MySQL

```sql
SELECT *
FROM student AS s
LEFT JOIN depart AS d
ON s.dept_id = d.dept_id

UNION

SELECT *
FROM student AS s
RIGHT JOIN depart AS d
ON s.dept_id = d.dept_id;
```

## UNION

```sql
SELECT column_name FROM table1
UNION
SELECT column_name FROM table2;
```

## INTERSECTION Using EXISTS

```sql
SELECT column_name
FROM table1 AS A
WHERE EXISTS (
    SELECT 1
    FROM table2 AS B
    WHERE A.column_name = B.column_name
);
```

## DIFFERENCE Using NOT EXISTS

```sql
SELECT column_name
FROM table1 AS A
WHERE NOT EXISTS (
    SELECT 1
    FROM table2 AS B
    WHERE A.column_name = B.column_name
);
```

---

# 10. Cleanup / Restore Original 5-Record Dataset

Some examples temporarily add records to demonstrate non-matching rows.

Remove the extra student:

```sql
DELETE FROM student
WHERE student_id = 6;
```

Remove the extra department:

```sql
DELETE FROM depart
WHERE dept_id = 106;
```

Restore the original department location if required:

```sql
UPDATE depart
SET location = 'Block A'
WHERE dept_id = 101;
```

After cleanup, verify:

```sql
SELECT COUNT(*) AS total_students
FROM student;

SELECT COUNT(*) AS total_faculty
FROM faculty;

SELECT COUNT(*) AS total_departments
FROM depart;
```

Expected:

| Table | Records |
|---|---:|
| student | 5 |
| faculty | 5 |
| depart | 5 |

---

# 11. Key Points to Remember

1. **Selection → Rows**
2. **Projection → Columns**
3. **JOIN → Combines related tables**
4. **INNER JOIN → Matching rows only**
5. **Theta Join → Any comparison operator**
6. **Equi Join → Equality (`=`)**
7. **Natural Join → Automatically uses same-named columns**
8. **Semi Join → Matching rows from the first table only**
9. **Anti Join → Non-matching rows from the first table only**
10. **LEFT JOIN → All left rows**
11. **RIGHT JOIN → All right rows**
12. **FULL OUTER JOIN → All rows from both tables**
13. **UNION → Combines results and removes duplicates**
14. **INTERSECTION → Common results**
15. **DIFFERENCE → First result minus second result**
16. **MySQL does not directly provide `FULL OUTER JOIN`; use `LEFT JOIN UNION RIGHT JOIN`.**
17. For `INTERSECTION` and `DIFFERENCE`, `EXISTS` and `NOT EXISTS` are simple MySQL-friendly approaches.

---

# 12. Practice Questions

Try these queries yourself:

### Q1. Display all students who scored more than 75.

```sql
-- Write your query here
```

### Q2. Display only student names and cities.

```sql
-- Write your query here
```

### Q3. Display student names with department names.

```sql
-- Write your query here
```

### Q4. Display faculty names with department names.

```sql
-- Write your query here
```

### Q5. Find students belonging to the Computer Science department.

```sql
-- Write your query here
```

### Q6. Display all students even if their department does not exist.

```sql
-- Write your query here
```

### Q7. Display all departments even if they have no students.

```sql
-- Write your query here
```

### Q8. Find departments that have no students.

```sql
-- Write your query here
```

### Q9. Demonstrate UNION using two suitable columns.

```sql
-- Write your query here
```

### Q10. Demonstrate an Anti Join using `NOT EXISTS`.

```sql
-- Write your query here
```

---

# Conclusion

SQL JOINs and set operations are fundamental techniques for retrieving information from multiple tables.

The easiest way to remember them is:

```text
Selection    → Which ROWS do I need?
Projection   → Which COLUMNS do I need?
JOIN         → Which TABLES do I need to combine?
UNION        → Combine two results
INTERSECTION → Find common results
DIFFERENCE   → Find results present in A but not B
```

These operations form the foundation for writing powerful SQL queries in real-world database applications.
