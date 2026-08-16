# SQL Clauses and SQL Operators — Practical Guide

## 2. Prerequisites — Database and Table Setup

### a. Create the Database

```sql
CREATE DATABASE IF NOT EXISTS School;
USE School;
```

### b. Create the Faculty Table

```sql
CREATE TABLE IF NOT EXISTS Faculty (
  T_id INT PRIMARY KEY,
  Name VARCHAR(50) NOT NULL,
  Department VARCHAR(50) NOT NULL,
  Salary DECIMAL(10,2),
  Date_of_Joining DATE,
  Email VARCHAR(100) UNIQUE
);
```

| Field | Data Type | Description |
|---|---|---|
| T_id | INT | Unique faculty ID / primary key |
| Name | VARCHAR(50) | Faculty name |
| Department | VARCHAR(50) | Department name |
| Salary | DECIMAL(10,2) | Monthly salary |
| Date_of_Joining | DATE | Joining date |
| Email | VARCHAR(100) | Unique email address |

### c. Insert 12 Sample Records

```sql
INSERT INTO Faculty VALUES
(101,'Amit Das','CSE',45000,'2020-06-15','amit.das@school.edu'),
(102,'Priya Roy','IT',52000,'2019-08-10','priya.roy@school.edu'),
(103,'Rahul Sen','ECE',38000,'2021-01-20','rahul.sen@school.edu'),
(104,'Sneha Paul','CSE',60000,'2018-03-12','sneha.paul@school.edu'),
(105,'Arjun Ghosh','ME',42000,'2022-07-05','arjun.ghosh@school.edu'),
(106,'Mita Dutta','IT',55000,'2020-11-25','mita.dutta@school.edu'),
(107,'Sourav Pal','ECE',47000,'2019-02-18','sourav.pal@school.edu'),
(108,'Ananya Bose','CSE',65000,'2017-09-30','ananya.bose@school.edu'),
(109,'Rakesh Roy','ME',35000,'2023-01-15','rakesh.roy@school.edu'),
(110,'Pooja Sen','IT',48000,'2021-05-10','pooja.sen@school.edu'),
(111,'Debasish Das','CSE',58000,'2018-12-01','debasish.das@school.edu'),
(112,'Kavita Pal','ECE',40000,'2022-04-22','kavita.pal@school.edu');
```

### Full Faculty Table (as loaded)

| T_id | Name | Dept | Salary | Joining |
|---|---|---|---|---|
| 101 | Amit Das | CSE | 45000 | 2020-06-15 |
| 102 | Priya Roy | IT | 52000 | 2019-08-10 |
| 103 | Rahul Sen | ECE | 38000 | 2021-01-20 |
| 104 | Sneha Paul | CSE | 60000 | 2018-03-12 |
| 105 | Arjun Ghosh | ME | 42000 | 2022-07-05 |
| 106 | Mita Dutta | IT | 55000 | 2020-11-25 |
| 107 | Sourav Pal | ECE | 47000 | 2019-02-18 |
| 108 | Ananya Bose | CSE | 65000 | 2017-09-30 |
| 109 | Rakesh Roy | ME | 35000 | 2023-01-15 |
| 110 | Pooja Sen | IT | 48000 | 2021-05-10 |
| 111 | Debasish Das | CSE | 58000 | 2018-12-01 |
| 112 | Kavita Pal | ECE | 40000 | 2022-04-22 |

---

## 3. SQL Clauses — Demonstration

### 3.1 WHERE

**About:** Filters rows so that only records satisfying a specified condition are returned. Evaluated before any grouping takes place.

```sql
SELECT column1, column2, ...
FROM Faculty
WHERE condition;
```

**Example:**

```sql
SELECT T_id, Name, Department, Salary
FROM Faculty
WHERE Salary BETWEEN 30000 AND 50000;
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 101 | Amit Das | CSE | 45000 |
| 103 | Rahul Sen | ECE | 38000 |
| 105 | Arjun Ghosh | ME | 42000 |
| 107 | Sourav Pal | ECE | 47000 |
| 109 | Rakesh Roy | ME | 35000 |
| 110 | Pooja Sen | IT | 48000 |
| 112 | Kavita Pal | ECE | 40000 |

### 3.2 LIMIT

**About:** Restricts the number of rows returned by a query, useful for previewing data or pagination.

```sql
SELECT column1, column2, ...
FROM Faculty
LIMIT number;
```

**Example:**

```sql
SELECT T_id, Name, Department, Salary
FROM Faculty
LIMIT 5;
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 101 | Amit Das | CSE | 45000 |
| 102 | Priya Roy | IT | 52000 |
| 103 | Rahul Sen | ECE | 38000 |
| 104 | Sneha Paul | CSE | 60000 |
| 105 | Arjun Ghosh | ME | 42000 |

### 3.3 ORDER BY

**About:** Sorts the result set in ascending (`ASC`, default) or descending (`DESC`) order.

```sql
SELECT column1, column2, ...
FROM Faculty
ORDER BY column_name ASC | DESC;
```

**Example:**

```sql
SELECT T_id, Name, Salary
FROM Faculty
ORDER BY Salary DESC
LIMIT 5;
```

**Output:**

| T_id | Name | Salary |
|---|---|---|
| 108 | Ananya Bose | 65000 |
| 104 | Sneha Paul | 60000 |
| 111 | Debasish Das | 58000 |
| 106 | Mita Dutta | 55000 |
| 102 | Priya Roy | 52000 |

### 3.4 GROUP BY

**About:** Groups rows sharing the same value in one or more columns, typically used with aggregate functions.

```sql
SELECT column, AGG_FUNC(column)
FROM Faculty
GROUP BY column;
```

**Example:**

```sql
SELECT Department, COUNT(*) AS Total_Faculty
FROM Faculty
GROUP BY Department;
```

**Output:**

| Department | Total_Faculty |
|---|---|
| CSE | 4 |
| IT | 3 |
| ECE | 3 |
| ME | 2 |

### 3.5 GROUP BY + COUNT()

**About:** `COUNT(*)` returns the number of records within each group.

```sql
SELECT column, COUNT(*) AS alias
FROM Faculty
GROUP BY column;
```

**Example:**

```sql
SELECT Department, COUNT(*) AS Total_Faculty
FROM Faculty
GROUP BY Department;
```

**Output:**

| Department | COUNT |
|---|---|
| CSE | 4 |
| IT | 3 |
| ECE | 3 |
| ME | 2 |

### 3.6 GROUP BY + MAX()

**About:** `MAX()` returns the highest value of a numeric column within each group.

```sql
SELECT column, MAX(numeric_column) AS alias
FROM Faculty
GROUP BY column;
```

**Example:**

```sql
SELECT Department, MAX(Salary) AS Highest_Salary
FROM Faculty
GROUP BY Department;
```

**Output:**

| Department | MAX(Salary) |
|---|---|
| CSE | 65000 |
| IT | 55000 |
| ECE | 47000 |
| ME | 42000 |

### 3.7 GROUP BY + MIN()

**About:** `MIN()` returns the lowest value of a numeric column within each group.

```sql
SELECT column, MIN(numeric_column) AS alias
FROM Faculty
GROUP BY column;
```

**Example:**

```sql
SELECT Department, MIN(Salary) AS Lowest_Salary
FROM Faculty
GROUP BY Department;
```

**Output:**

| Department | MIN(Salary) |
|---|---|
| CSE | 45000 |
| IT | 48000 |
| ECE | 38000 |
| ME | 35000 |

### 3.8 GROUP BY + SUM()

**About:** `SUM()` adds up all values of a numeric column within each group.

```sql
SELECT column, SUM(numeric_column) AS alias
FROM Faculty
GROUP BY column;
```

**Example:**

```sql
SELECT Department, SUM(Salary) AS Total_Salary
FROM Faculty
GROUP BY Department;
```

**Output:**

| Department | SUM(Salary) |
|---|---|
| CSE | 228000 |
| IT | 155000 |
| ECE | 125000 |
| ME | 77000 |

### 3.9 GROUP BY + AVG()

**About:** `AVG()` calculates the mean value of a numeric column within each group. `ROUND()` keeps the result to two decimal places.

```sql
SELECT column, ROUND(AVG(numeric_column),2) AS alias
FROM Faculty
GROUP BY column;
```

**Example:**

```sql
SELECT Department, ROUND(AVG(Salary),2) AS Average_Salary
FROM Faculty
GROUP BY Department;
```

**Output:**

| Department | AVG(Salary) |
|---|---|
| CSE | 57000.00 |
| IT | 51666.67 |
| ECE | 41666.67 |
| ME | 38500.00 |

### 3.10 HAVING

**About:** Filters groups after `GROUP BY` has been applied — unlike `WHERE`, it can filter on the result of an aggregate function.

```sql
SELECT column, AGG_FUNC(column) AS alias
FROM Faculty
GROUP BY column
HAVING condition;
```

**Example:**

```sql
SELECT Department, AVG(Salary) AS Average_Salary
FROM Faculty
GROUP BY Department
HAVING AVG(Salary) > 50000;
```

**Output:**

| Department | Average_Salary |
|---|---|
| CSE | 57000.00 |
| IT | 51666.67 |

### 3.11 DISTINCT

**About:** Removes duplicate values from the result set, returning only unique values for the selected column(s).

```sql
SELECT DISTINCT column_name
FROM Faculty;
```

**Example:**

```sql
SELECT DISTINCT Department
FROM Faculty;
```

**Output:**

| Department |
|---|
| CSE |
| IT |
| ECE |
| ME |

---

## 4. SQL Operators — Demonstration

### 4.1 Arithmetic Operators

#### 4.1.1 `+` (Addition)

**About:** Adds a numeric value to a column value — e.g., calculating a salary after a raise.

```sql
SELECT column, column + value AS alias
FROM Faculty
WHERE condition;
```

**Example:**

```sql
SELECT Name, Salary, Salary + 5000 AS New_Salary
FROM Faculty
WHERE T_id = 101;
```

**Output:**

| Name | Salary | New_Salary |
|---|---|---|
| Amit Das | 45000 | 50000 |

#### 4.1.2 `-` (Subtraction)

**About:** Deducts a numeric value from a column value — e.g., salary after a deduction.

```sql
SELECT column, column - value AS alias
FROM Faculty
WHERE condition;
```

**Example:**

```sql
SELECT Name, Salary, Salary - 2000 AS New_Salary
FROM Faculty
WHERE T_id = 102;
```

**Output:**

| Name | Salary | New_Salary |
|---|---|---|
| Priya Roy | 52000 | 50000 |

#### 4.1.3 `*` (Multiplication)

**About:** Multiplies a column value by a numeric factor — e.g., projecting monthly salary as an annual figure.

```sql
SELECT column, column * value AS alias
FROM Faculty
WHERE condition;
```

**Example:**

```sql
SELECT Name, Salary, Salary * 12 AS Annual_Salary
FROM Faculty
WHERE T_id = 103;
```

**Output:**

| Name | Salary | Annual_Salary |
|---|---|---|
| Rahul Sen | 38000 | 456000 |

#### 4.1.4 `/` (Division)

**About:** Divides a column value by a numeric value — e.g., computing a half-yearly salary payment.

```sql
SELECT column, column / value AS alias
FROM Faculty
WHERE condition;
```

**Example:**

```sql
SELECT Name, Salary, Salary / 2 AS Half_Salary
FROM Faculty
WHERE T_id = 104;
```

**Output:**

| Name | Salary | Half_Salary |
|---|---|---|
| Sneha Paul | 60000 | 30000 |

#### 4.1.5 `%` (Modulus)

**About:** Returns the remainder after dividing a column value by a numeric value — e.g., isolating the amount above a round-number threshold.

```sql
SELECT column, column % value AS alias
FROM Faculty
WHERE condition;
```

**Example:**

```sql
SELECT Name, Salary, Salary % 10000 AS Remainder
FROM Faculty
WHERE T_id = 105;
```

**Output:**

| Name | Salary | Remainder |
|---|---|---|
| Arjun Ghosh | 42000 | 2000 |

### 4.2 Comparison Operators

#### 4.2.1 `=` (Equal To)

**About:** Returns rows where the column value exactly matches the given value.

```sql
SELECT * FROM Faculty
WHERE column = value;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Department = 'CSE';
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 101 | Amit Das | CSE | 45000 |
| 104 | Sneha Paul | CSE | 60000 |
| 108 | Ananya Bose | CSE | 65000 |
| 111 | Debasish Das | CSE | 58000 |

#### 4.2.2 `>` (Greater Than)

**About:** Returns rows where the column value is strictly greater than the given value.

```sql
SELECT * FROM Faculty
WHERE column > value;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Salary > 55000;
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 104 | Sneha Paul | CSE | 60000 |
| 108 | Ananya Bose | CSE | 65000 |
| 111 | Debasish Das | CSE | 58000 |

#### 4.2.3 `<` (Less Than)

**About:** Returns rows where the column value is strictly less than the given value.

```sql
SELECT * FROM Faculty
WHERE column < value;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Salary < 40000;
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 103 | Rahul Sen | ECE | 38000 |
| 109 | Rakesh Roy | ME | 35000 |

#### 4.2.4 `>=` (Greater Than or Equal To)

**About:** Returns rows where the column value is greater than or equal to the given value.

```sql
SELECT * FROM Faculty
WHERE column >= value;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Salary >= 60000;
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 104 | Sneha Paul | CSE | 60000 |
| 108 | Ananya Bose | CSE | 65000 |

#### 4.2.5 `<=` (Less Than or Equal To)

**About:** Returns rows where the column value is less than or equal to the given value.

```sql
SELECT * FROM Faculty
WHERE column <= value;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Salary <= 40000;
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 103 | Rahul Sen | ECE | 38000 |
| 109 | Rakesh Roy | ME | 35000 |
| 112 | Kavita Pal | ECE | 40000 |

#### 4.2.6 `<>` / `!=` (Not Equal To)

**About:** Returns rows where the column value does not match the given value. Both `<>` and `!=` behave identically in MySQL.

```sql
SELECT * FROM Faculty
WHERE column <> value;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Department <> 'IT';
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 101 | Amit Das | CSE | 45000 |
| 103 | Rahul Sen | ECE | 38000 |
| 104 | Sneha Paul | CSE | 60000 |
| 105 | Arjun Ghosh | ME | 42000 |
| 107 | Sourav Pal | ECE | 47000 |
| 108 | Ananya Bose | CSE | 65000 |
| 109 | Rakesh Roy | ME | 35000 |
| 111 | Debasish Das | CSE | 58000 |
| 112 | Kavita Pal | ECE | 40000 |

### 4.3 Logical Operators

#### 4.3.1 AND

**About:** Returns rows only when all combined conditions are true.

```sql
SELECT * FROM Faculty
WHERE condition1 AND condition2;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Department = 'CSE' AND Salary > 55000;
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 104 | Sneha Paul | CSE | 60000 |
| 108 | Ananya Bose | CSE | 65000 |
| 111 | Debasish Das | CSE | 58000 |

#### 4.3.2 OR

**About:** Returns rows when at least one of the combined conditions is true.

```sql
SELECT * FROM Faculty
WHERE condition1 OR condition2;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Department = 'ME' OR Department = 'ECE';
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 103 | Rahul Sen | ECE | 38000 |
| 105 | Arjun Ghosh | ME | 42000 |
| 107 | Sourav Pal | ECE | 47000 |
| 109 | Rakesh Roy | ME | 35000 |
| 112 | Kavita Pal | ECE | 40000 |

#### 4.3.3 NOT

**About:** Reverses the result of the condition that follows it, returning rows where the condition is false.

```sql
SELECT * FROM Faculty
WHERE NOT condition;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE NOT Department = 'CSE';
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 102 | Priya Roy | IT | 52000 |
| 103 | Rahul Sen | ECE | 38000 |
| 105 | Arjun Ghosh | ME | 42000 |
| 106 | Mita Dutta | IT | 55000 |
| 107 | Sourav Pal | ECE | 47000 |
| 109 | Rakesh Roy | ME | 35000 |
| 110 | Pooja Sen | IT | 48000 |
| 112 | Kavita Pal | ECE | 40000 |

### 4.4 Special Operators

#### 4.4.1 BETWEEN

**About:** Tests whether a column value falls within an inclusive range of two values.

```sql
SELECT * FROM Faculty
WHERE column BETWEEN value1 AND value2;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Salary BETWEEN 40000 AND 50000;
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 101 | Amit Das | CSE | 45000 |
| 105 | Arjun Ghosh | ME | 42000 |
| 107 | Sourav Pal | ECE | 47000 |
| 110 | Pooja Sen | IT | 48000 |
| 112 | Kavita Pal | ECE | 40000 |

#### 4.4.2 IN

**About:** Tests whether a column value matches any value in a specified list, avoiding a chain of `OR` conditions.

```sql
SELECT * FROM Faculty
WHERE column IN (value1, value2, ...);
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Department IN ('CSE','IT');
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 101 | Amit Das | CSE | 45000 |
| 102 | Priya Roy | IT | 52000 |
| 104 | Sneha Paul | CSE | 60000 |
| 106 | Mita Dutta | IT | 55000 |
| 108 | Ananya Bose | CSE | 65000 |
| 110 | Pooja Sen | IT | 48000 |
| 111 | Debasish Das | CSE | 58000 |

#### 4.4.3 NOT IN

**About:** Tests whether a column value does not match any value in a specified list — the inverse of `IN`.

```sql
SELECT * FROM Faculty
WHERE column NOT IN (value1, value2, ...);
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Department NOT IN ('CSE','IT');
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 103 | Rahul Sen | ECE | 38000 |
| 105 | Arjun Ghosh | ME | 42000 |
| 107 | Sourav Pal | ECE | 47000 |
| 109 | Rakesh Roy | ME | 35000 |
| 112 | Kavita Pal | ECE | 40000 |

#### 4.4.4 IS NULL

**About:** Tests whether a column value is `NULL`. Ordinary comparison operators cannot test for NULL, so `IS NULL` is required.

```sql
SELECT * FROM Faculty
WHERE column IS NULL;
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Email IS NULL;
```

#### 4.4.5 EXISTS

**About:** Tests whether a subquery returns at least one row, evaluating to `TRUE`/`FALSE` rather than returning column data.

```sql
SELECT EXISTS (
  SELECT 1 FROM Faculty WHERE condition
) AS alias;
```

**Example:**

```sql
SELECT EXISTS (
  SELECT 1 FROM Faculty WHERE Department = 'CSE'
) AS Dept_Exists;
```

**Output:**

| Dept_Exists |
|---|
| 1 (TRUE — CSE department exists) |

### 4.5 Pattern Matching Operators (LIKE)

The `LIKE` operator matches string patterns using wildcards: `%` represents zero or more characters, and `_` represents exactly one character.

#### 4.5.1 `LIKE 'A%'` (Starts With)

**About:** Matches values that begin with the letter A, followed by any number of characters.

```sql
SELECT * FROM Faculty
WHERE column LIKE 'A%';
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Name LIKE 'A%';
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 101 | Amit Das | CSE | 45000 |
| 105 | Arjun Ghosh | ME | 42000 |
| 108 | Ananya Bose | CSE | 65000 |

#### 4.5.2 `LIKE '%Roy%'` (Contains)

**About:** Matches values that contain the substring 'Roy' anywhere within the value.

```sql
SELECT * FROM Faculty
WHERE column LIKE '%Roy%';
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Name LIKE '%Roy%';
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 102 | Priya Roy | IT | 52000 |
| 109 | Rakesh Roy | ME | 35000 |

#### 4.5.3 `LIKE '_ita%'` (Single-Character Wildcard)

**About:** The underscore (`_`) matches exactly one character. This pattern matches any value whose second, third, and fourth characters are 'i', 't', 'a', regardless of the first character.

```sql
SELECT * FROM Faculty
WHERE column LIKE '_ita%';
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Name LIKE '_ita%';
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 106 | Mita Dutta | IT | 55000 |

#### 4.5.4 `NOT LIKE '%Pal%'` (Does Not Contain)

**About:** Returns rows where the value does NOT contain the substring 'Pal' anywhere within it.

```sql
SELECT * FROM Faculty
WHERE column NOT LIKE '%Pal%';
```

**Example:**

```sql
SELECT * FROM Faculty
WHERE Name NOT LIKE '%Pal%';
```

**Output:**

| T_id | Name | Dept | Salary |
|---|---|---|---|
| 101 | Amit Das | CSE | 45000 |
| 102 | Priya Roy | IT | 52000 |
| 103 | Rahul Sen | ECE | 38000 |
| 104 | Sneha Paul | CSE | 60000 |
| 105 | Arjun Ghosh | ME | 42000 |
| 106 | Mita Dutta | IT | 55000 |
| 108 | Ananya Bose | CSE | 65000 |
| 109 | Rakesh Roy | ME | 35000 |
| 110 | Pooja Sen | IT | 48000 |
| 111 | Debasish Das | CSE | 58000 |

---

