# All the Basic DML Commands : 

A quick reference guide to the core **Data Manipulation Language (DML)** commands in SQL — `INSERT`, `SELECT`, `UPDATE`, `DELETE`, and `MERGE`.

---

## 1. INSERT Command

**Purpose:** Used to add new records into a table.

**Syntax:**
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```
or
```sql
INSERT INTO table_name
VALUES (value1, value2, ...);
```

**Example:**
```sql
INSERT INTO Student VALUES (3, 'Amit', 22);
```

**Result:**

| StudentID | Name  | Age |
|-----------|-------|-----|
| 1         | Rahul | 20  |
| 2         | Priya | 21  |
| 3         | Amit  | 22  |

---

## 2. SELECT Command

**Purpose:** Used to retrieve (display) data from one or more tables.

**Syntax:**
```sql
-- Retrieve all columns
SELECT * FROM table_name;

-- Retrieve specific columns
SELECT column1, column2 FROM table_name;
```

**Example 1:**
```sql
SELECT * FROM Student;
```

**Result:**

| StudentID | Name  | Age |
|-----------|-------|-----|
| 1         | Rahul | 20  |
| 2         | Priya | 21  |
| 3         | Amit  | 22  |

**Example 2:**
```sql
SELECT Name, Age FROM Student;
```

**Result:**

| Name  | Age |
|-------|-----|
| Rahul | 20  |
| Priya | 21  |
| Amit  | 22  |

---

## 3. UPDATE Command

**Purpose:** Used to modify existing records in a table.

**Syntax:**
```sql
UPDATE table_name
SET column_name = value
WHERE condition;
```

> **Note:** If the `WHERE` clause is omitted, all rows in the table will be updated.

**Example:**
```sql
UPDATE Student SET Age = 23 WHERE StudentID = 3;
```

**Result:**

| StudentID | Name  | Age |
|-----------|-------|-----|
| 1         | Rahul | 20  |
| 2         | Priya | 21  |
| 3         | Amit  | 23  |

---

## 4. DELETE Command

**Purpose:** Used to remove existing records from a table.

**Syntax:**
```sql
DELETE FROM table_name
WHERE condition;
```

> **Note:** If the `WHERE` clause is omitted, all records in the table will be deleted, but the table structure remains unchanged.

**Example:**
```sql
DELETE FROM Student
WHERE StudentID = 2;
```

**Result:**

| StudentID | Name  | Age |
|-----------|-------|-----|
| 1         | Rahul | 20  |
| 3         | Amit  | 23  |

---

## 5. MERGE Command

**Purpose:** Used to insert, update, or delete records in a target table based on matching records from a source table. It combines the functionality of `INSERT`, `UPDATE`, and `DELETE` into a single statement.

**Syntax:**
```sql
MERGE INTO target_table AS T
USING source_table AS S
ON (T.primary_key = S.primary_key)
WHEN MATCHED THEN
    UPDATE SET
        T.column1 = S.column1,
        T.column2 = S.column2
WHEN NOT MATCHED THEN
    INSERT (column1, column2, ...)
    VALUES (S.column1, S.column2, ...);
```

**Example:**

**Target Table (Student)**

| StudentID | Name  | Age |
|-----------|-------|-----|
| 1         | Rahul | 20  |
| 2         | Priya | 21  |

**Source Table (NewStudent)**

| StudentID | Name  | Age |
|-----------|-------|-----|
| 2         | Priya | 22  |
| 3         | Amit  | 23  |

**MERGE Statement:**
```sql
MERGE INTO Student AS T
USING NewStudent AS S
ON (T.StudentID = S.StudentID)
WHEN MATCHED THEN
    UPDATE SET
        T.Name = S.Name,
        T.Age = S.Age
WHEN NOT MATCHED THEN
    INSERT (StudentID, Name, Age)
    VALUES (S.StudentID, S.Name, S.Age);
```

**Result:**

| StudentID | Name  | Age |
|-----------|-------|-----|
| 1         | Rahul | 20  |
| 2         | Priya | 22  |
| 3         | Amit  | 23  |

**Explanation:**
- `StudentID` 2 already exists → **Updated** (Age changed from 21 to 22).
- `StudentID` 3 does not exist → **Inserted** as a new record.

---

## Summary Table

| Command | Purpose                                      |
|---------|-----------------------------------------------|
| INSERT  | Add new records to a table                    |
| SELECT  | Retrieve data from a table                    |
| UPDATE  | Modify existing records                       |
| DELETE  | Remove existing records                       |
| MERGE   | Insert, update, or delete based on a match     |
