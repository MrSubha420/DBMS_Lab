# MySQL Functions – Complete Practical Guide

## 1. Prerequisites

Before studying MySQL functions, create a database and an employee table containing sample records.

### Step 1: Create Database

```sql
CREATE DATABASE employee;
```

### Step 2: Select Database

```sql
USE employee;
```

### Step 3: Create `emp_details` Table

The following table contains 10 relevant employee fields.

```sql
CREATE TABLE emp_details (
    emp_id INT PRIMARY KEY,
    first_name VARCHAR(30),
    last_name VARCHAR(30),
    department VARCHAR(30),
    job_title VARCHAR(40),
    salary DECIMAL(10,2),
    hire_date DATE,
    city VARCHAR(30),
    email VARCHAR(80),
    status VARCHAR(15)
);
```

### Step 4: Insert at Least 20 Employees

```sql
INSERT INTO emp_details
(emp_id, first_name, last_name, department, job_title, salary, hire_date, city, email, status)
VALUES
(101, 'Rahul', 'Sharma', 'IT', 'Software Engineer', 55000, '2021-01-15', 'Kolkata', 'rahul@company.com', 'Active'),
(102, 'Priya', 'Das', 'HR', 'HR Executive', 42000, '2020-03-20', 'Delhi', 'priya@company.com', 'Active'),
(103, 'Amit', 'Roy', 'IT', 'Senior Developer', 72000, '2019-07-10', 'Kolkata', 'amit@company.com', 'Active'),
(104, 'Sneha', 'Sen', 'Finance', 'Accountant', 48000, '2022-02-18', 'Mumbai', 'sneha@company.com', 'Active'),
(105, 'Rohan', 'Gupta', 'Sales', 'Sales Executive', 39000, '2023-04-12', 'Delhi', 'rohan@company.com', 'Active'),
(106, 'Ananya', 'Ghosh', 'IT', 'Data Analyst', 61000, '2021-08-25', 'Kolkata', 'ananya@company.com', 'Active'),
(107, 'Sourav', 'Dutta', 'HR', 'Recruiter', 45000, '2022-06-14', 'Kolkata', 'sourav@company.com', 'Active'),
(108, 'Neha', 'Verma', 'Finance', 'Financial Analyst', 67000, '2018-11-05', 'Pune', 'neha@company.com', 'Active'),
(109, 'Arjun', 'Mehta', 'Sales', 'Sales Manager', 75000, '2017-09-22', 'Mumbai', 'arjun@company.com', 'Active'),
(110, 'Moumita', 'Paul', 'IT', 'Web Developer', 58000, '2023-01-09', 'Kolkata', 'moumita@company.com', 'Active'),
(111, 'Kunal', 'Singh', 'Operations', 'Operations Executive', 46000, '2020-12-17', 'Delhi', 'kunal@company.com', 'Active'),
(112, 'Tania', 'Bose', 'Finance', 'Senior Accountant', 62000, '2019-05-30', 'Kolkata', 'tania@company.com', 'Active'),
(113, 'Vikram', 'Patel', 'IT', 'System Administrator', 64000, '2021-10-11', 'Ahmedabad', 'vikram@company.com', 'Active'),
(114, 'Puja', 'Nair', 'HR', 'HR Manager', 70000, '2016-04-08', 'Kochi', 'puja@company.com', 'Active'),
(115, 'Sayan', 'Chakraborty', 'Sales', 'Marketing Executive', 43000, '2024-01-16', 'Kolkata', 'sayan@company.com', 'Active'),
(116, 'Ishita', 'Roy', 'Operations', 'Operations Manager', 68000, '2018-07-19', 'Pune', 'ishita@company.com', 'Active'),
(117, 'Deb', 'Mukherjee', 'IT', 'Software Tester', 52000, '2022-09-27', 'Kolkata', 'deb@company.com', 'Inactive'),
(118, 'Riya', 'Khan', 'Finance', 'Finance Executive', 51000, '2023-06-05', 'Delhi', 'riya@company.com', 'Active'),
(119, 'Aditya', 'Roy', 'Sales', 'Business Analyst', 59000, '2020-02-13', 'Mumbai', 'aditya@company.com', 'Active'),
(120, 'Nandini', 'Saha', 'IT', 'Project Manager', 85000, '2015-12-01', 'Kolkata', 'nandini@company.com', 'Active');
```

Verify the records:

```sql
SELECT * FROM emp_details;
```

---

# 2. What is a Function in SQL?

A **function in SQL** is a predefined or user-created operation that accepts one or more input values, performs a specific task, and returns a value.

Functions are useful for:

- Performing calculations
- Processing strings
- Working with dates and times
- Summarizing records
- Handling NULL values
- Applying conditions
- Converting data types
- Performing customized operations

General idea:

```text
Input → Function → Output
```

Example:

```sql
SELECT UPPER(first_name)
FROM emp_details;
```

If the input is:

```text
Rahul
```

the function returns:

```text
RAHUL
```

---

# 3. Types of SQL Functions

SQL functions can broadly be divided into:

```text
SQL Functions
│
├── A. Built-in Functions
│   │
│   ├── 1. Aggregate Functions
│   ├── 2. String Functions
│   ├── 3. Numeric / Mathematical Functions
│   ├── 4. Date and Time Functions
│   ├── 5. Conditional / Control-Flow Functions
│   ├── 6. Conversion Functions
│   └── 7. Other Common Utility Functions
│
└── B. User-Defined Functions
```

---

# A. Built-in Functions

## Definition

**Built-in functions** are functions already provided by MySQL. The programmer does not need to create them before using them.

Examples:

```sql
COUNT()
SUM()
AVG()
MAX()
MIN()
UPPER()
LOWER()
ROUND()
NOW()
IF()
COALESCE()
```

---

# 4. Aggregate Functions

## Definition

**Aggregate functions** perform calculations on a group of rows and return a single result.

The most commonly used aggregate functions are:

1. `COUNT()`
2. `SUM()`
3. `AVG()`
4. `MAX()`
5. `MIN()`

> Aggregate functions are frequently used with `GROUP BY`.

---

## 4.1 COUNT()

### About

`COUNT()` counts rows or non-NULL values.

### Syntax

```sql
COUNT(expression)
```

### Example

```sql
SELECT COUNT(*) AS total_employees
FROM emp_details;
```

### Output

| total_employees |
|---:|
| 20 |

### Another Example

Count employees in the IT department:

```sql
SELECT COUNT(*) AS IT_Employees
FROM emp_details
WHERE department = 'IT';
```

### Output

| IT_Employees |
|---:|
| 7 |

---

## 4.2 SUM()

### About

`SUM()` calculates the total of a numeric column.

### Syntax

```sql
SUM(column_name)
```

### Example

```sql
SELECT SUM(salary) AS total_salary
FROM emp_details;
```

### Output

| total_salary |
|---:|
| 1161000.00 |

---

## 4.3 AVG()

### About

`AVG()` calculates the average value of a numeric column.

### Syntax

```sql
AVG(column_name)
```

### Example

```sql
SELECT ROUND(AVG(salary), 2) AS average_salary
FROM emp_details;
```

### Output

| average_salary |
|---:|
| 58050.00 |

---

## 4.4 MAX()

### About

`MAX()` returns the highest value.

### Syntax

```sql
MAX(column_name)
```

### Example

```sql
SELECT MAX(salary) AS highest_salary
FROM emp_details;
```

### Output

| highest_salary |
|---:|
| 85000.00 |

---

## 4.5 MIN()

### About

`MIN()` returns the lowest value.

### Syntax

```sql
MIN(column_name)
```

### Example

```sql
SELECT MIN(salary) AS lowest_salary
FROM emp_details;
```

### Output

| lowest_salary |
|---:|
| 39000.00 |

---

## 4.6 Aggregate Functions with GROUP BY

Example:

```sql
SELECT
    department,
    COUNT(*) AS employees,
    ROUND(AVG(salary), 2) AS average_salary,
    MAX(salary) AS maximum_salary,
    MIN(salary) AS minimum_salary
FROM emp_details
GROUP BY department;
```

### Output

| department | employees | average_salary | maximum_salary | minimum_salary |
|---|---:|---:|---:|---:|
| Finance | 4 | 57000.00 | 67000.00 | 48000.00 |
| HR | 3 | 52333.33 | 70000.00 | 42000.00 |
| IT | 7 | 63857.14 | 85000.00 | 52000.00 |
| Operations | 2 | 57000.00 | 68000.00 | 46000.00 |
| Sales | 4 | 54000.00 | 75000.00 | 39000.00 |

---

# 5. String Functions

String functions are used to manipulate character/text data.

Important string functions:

- `UPPER()`
- `LOWER()`
- `CONCAT()`
- `LENGTH()`
- `CHAR_LENGTH()`
- `SUBSTRING()`
- `LEFT()`
- `RIGHT()`
- `TRIM()`
- `REPLACE()`
- `REVERSE()`

---

## 5.1 UPPER()

### About

Converts text into uppercase.

### Syntax

```sql
UPPER(string)
```

### Example

```sql
SELECT first_name, UPPER(first_name) AS uppercase_name
FROM emp_details
LIMIT 5;
```

### Output

| first_name | uppercase_name |
|---|---|
| Rahul | RAHUL |
| Priya | PRIYA |
| Amit | AMIT |
| Sneha | SNEHA |
| Rohan | ROHAN |

---

## 5.2 LOWER()

### About

Converts text into lowercase.

### Syntax

```sql
LOWER(string)
```

### Example

```sql
SELECT first_name, LOWER(first_name) AS lowercase_name
FROM emp_details
LIMIT 5;
```

### Output

| first_name | lowercase_name |
|---|---|
| Rahul | rahul |
| Priya | priya |
| Amit | amit |
| Sneha | sneha |
| Rohan | rohan |

---

## 5.3 CONCAT()

### About

Combines two or more strings.

### Syntax

```sql
CONCAT(string1, string2, ...)
```

### Example

```sql
SELECT
    emp_id,
    CONCAT(first_name, ' ', last_name) AS full_name
FROM emp_details
LIMIT 5;
```

### Output

| emp_id | full_name |
|---:|---|
| 101 | Rahul Sharma |
| 102 | Priya Das |
| 103 | Amit Roy |
| 104 | Sneha Sen |
| 105 | Rohan Gupta |

---

## 5.4 LENGTH()

### About

Returns the length of a string in bytes.

### Syntax

```sql
LENGTH(string)
```

### Example

```sql
SELECT
    first_name,
    LENGTH(first_name) AS name_length
FROM emp_details
LIMIT 5;
```

### Output

| first_name | name_length |
|---|---:|
| Rahul | 5 |
| Priya | 5 |
| Amit | 4 |
| Sneha | 5 |
| Rohan | 5 |

---

## 5.5 CHAR_LENGTH()

### About

Returns the number of characters in a string.

### Syntax

```sql
CHAR_LENGTH(string)
```

### Example

```sql
SELECT
    first_name,
    CHAR_LENGTH(first_name) AS character_count
FROM emp_details
LIMIT 5;
```

### Output

| first_name | character_count |
|---|---:|
| Rahul | 5 |
| Priya | 5 |
| Amit | 4 |
| Sneha | 5 |
| Rohan | 5 |

---

## 5.6 SUBSTRING()

### About

Extracts a portion of a string.

### Syntax

```sql
SUBSTRING(string, start_position, length)
```

### Example

```sql
SELECT
    first_name,
    SUBSTRING(first_name, 1, 3) AS short_name
FROM emp_details
LIMIT 5;
```

### Output

| first_name | short_name |
|---|---|
| Rahul | Rah |
| Priya | Pri |
| Amit | Ami |
| Sneha | Sne |
| Rohan | Roh |

---

## 5.7 LEFT()

### About

Returns a specified number of characters from the left side.

### Syntax

```sql
LEFT(string, number_of_characters)
```

### Example

```sql
SELECT first_name, LEFT(first_name, 2) AS first_two
FROM emp_details
LIMIT 5;
```

### Output

| first_name | first_two |
|---|---|
| Rahul | Ra |
| Priya | Pr |
| Amit | Am |
| Sneha | Sn |
| Rohan | Ro |

---

## 5.8 RIGHT()

### About

Returns a specified number of characters from the right side.

### Syntax

```sql
RIGHT(string, number_of_characters)
```

### Example

```sql
SELECT first_name, RIGHT(first_name, 2) AS last_two
FROM emp_details
LIMIT 5;
```

### Output

| first_name | last_two |
|---|---|
| Rahul | ul |
| Priya | ya |
| Amit | it |
| Sneha | ha |
| Rohan | an |

---

## 5.9 TRIM()

### About

Removes leading and trailing spaces.

### Syntax

```sql
TRIM(string)
```

### Example

```sql
SELECT TRIM('   MySQL Functions   ') AS cleaned_text;
```

### Output

| cleaned_text |
|---|
| MySQL Functions |

---

## 5.10 REPLACE()

### About

Replaces a portion of a string with another string.

### Syntax

```sql
REPLACE(string, old_string, new_string)
```

### Example

```sql
SELECT
    email,
    REPLACE(email, '@company.com', '@example.com') AS new_email
FROM emp_details
LIMIT 3;
```

### Output

| email | new_email |
|---|---|
| rahul@company.com | rahul@example.com |
| priya@company.com | priya@example.com |
| amit@company.com | amit@example.com |

---

## 5.11 REVERSE()

### About

Reverses a string.

### Syntax

```sql
REVERSE(string)
```

### Example

```sql
SELECT first_name, REVERSE(first_name) AS reversed_name
FROM emp_details
LIMIT 5;
```

### Output

| first_name | reversed_name |
|---|---|
| Rahul | luhaR |
| Priya | ayirP |
| Amit | timA |
| Sneha | ahenS |
| Rohan | nahoR |

---

# 6. Numeric / Mathematical Functions

Important numeric functions:

- `ROUND()`
- `CEIL()`
- `FLOOR()`
- `ABS()`
- `MOD()`
- `POWER()`
- `SQRT()`
- `TRUNCATE()`

---

## 6.1 ROUND()

### About

Rounds a number to the specified number of decimal places.

### Syntax

```sql
ROUND(number, decimal_places)
```

### Example

```sql
SELECT
    ROUND(AVG(salary), 2) AS average_salary
FROM emp_details;
```

### Output

| average_salary |
|---:|
| 58050.00 |

---

## 6.2 CEIL()

### About

Returns the smallest integer greater than or equal to a number.

### Syntax

```sql
CEIL(number)
```

### Example

```sql
SELECT CEIL(1250.35) AS result;
```

### Output

| result |
|---:|
| 1251 |

---

## 6.3 FLOOR()

### About

Returns the largest integer less than or equal to a number.

### Syntax

```sql
FLOOR(number)
```

### Example

```sql
SELECT FLOOR(1250.99) AS result;
```

### Output

| result |
|---:|
| 1250 |

---

## 6.4 ABS()

### About

Returns the absolute/positive value.

### Syntax

```sql
ABS(number)
```

### Example

```sql
SELECT ABS(-5000) AS result;
```

### Output

| result |
|---:|
| 5000 |

---

## 6.5 MOD()

### About

Returns the remainder after division.

### Syntax

```sql
MOD(number, divisor)
```

### Example

```sql
SELECT MOD(100, 7) AS remainder;
```

### Output

| remainder |
|---:|
| 2 |

---

## 6.6 POWER()

### About

Returns a number raised to a specified power.

### Syntax

```sql
POWER(number, power)
```

### Example

```sql
SELECT POWER(5, 2) AS result;
```

### Output

| result |
|---:|
| 25 |

---

## 6.7 SQRT()

### About

Returns the square root.

### Syntax

```sql
SQRT(number)
```

### Example

```sql
SELECT SQRT(144) AS result;
```

### Output

| result |
|---:|
| 12 |

---

## 6.8 TRUNCATE()

### About

Removes decimal digits without rounding.

### Syntax

```sql
TRUNCATE(number, decimal_places)
```

### Example

```sql
SELECT TRUNCATE(1250.9876, 2) AS result;
```

### Output

| result |
|---:|
| 1250.98 |

---

# 7. Date and Time Functions

Important date/time functions:

- `NOW()`
- `CURDATE()`
- `CURTIME()`
- `YEAR()`
- `MONTH()`
- `MONTHNAME()`
- `DAY()`
- `DAYNAME()`
- `DATE_FORMAT()`
- `DATEDIFF()`
- `DATE_ADD()`
- `DATE_SUB()`
- `LAST_DAY()`

---

## 7.1 NOW()

### About

Returns the current date and time.

### Syntax

```sql
NOW()
```

### Example

```sql
SELECT NOW() AS current_datetime;
```

### Output

The exact value depends on the time when the query is executed.

| current_datetime |
|---|
| Current date and time |

---

## 7.2 CURDATE()

### About

Returns the current date.

### Syntax

```sql
CURDATE()
```

### Example

```sql
SELECT CURDATE() AS current_date;
```

### Output

| current_date |
|---|
| Current system date |

---

## 7.3 CURTIME()

### About

Returns the current time.

### Syntax

```sql
CURTIME()
```

### Example

```sql
SELECT CURTIME() AS current_time;
```

### Output

| current_time |
|---|
| Current system time |

---

## 7.4 YEAR()

### About

Extracts the year from a date.

### Syntax

```sql
YEAR(date)
```

### Example

```sql
SELECT
    first_name,
    hire_date,
    YEAR(hire_date) AS hire_year
FROM emp_details
LIMIT 5;
```

### Output

| first_name | hire_date | hire_year |
|---|---|---:|
| Rahul | 2021-01-15 | 2021 |
| Priya | 2020-03-20 | 2020 |
| Amit | 2019-07-10 | 2019 |
| Sneha | 2022-02-18 | 2022 |
| Rohan | 2023-04-12 | 2023 |

---

## 7.5 MONTH()

### About

Extracts the month number.

### Syntax

```sql
MONTH(date)
```

### Example

```sql
SELECT first_name, MONTH(hire_date) AS hire_month
FROM emp_details
LIMIT 5;
```

### Output

| first_name | hire_month |
|---|---:|
| Rahul | 1 |
| Priya | 3 |
| Amit | 7 |
| Sneha | 2 |
| Rohan | 4 |

---

## 7.6 MONTHNAME()

### About

Returns the name of the month.

### Syntax

```sql
MONTHNAME(date)
```

### Example

```sql
SELECT first_name, MONTHNAME(hire_date) AS hire_month
FROM emp_details
LIMIT 5;
```

### Output

| first_name | hire_month |
|---|---|
| Rahul | January |
| Priya | March |
| Amit | July |
| Sneha | February |
| Rohan | April |

---

## 7.7 DAY()

### About

Extracts the day of the month.

### Syntax

```sql
DAY(date)
```

### Example

```sql
SELECT first_name, DAY(hire_date) AS hire_day
FROM emp_details
LIMIT 5;
```

### Output

| first_name | hire_day |
|---|---:|
| Rahul | 15 |
| Priya | 20 |
| Amit | 10 |
| Sneha | 18 |
| Rohan | 12 |

---

## 7.8 DAYNAME()

### About

Returns the weekday name.

### Syntax

```sql
DAYNAME(date)
```

### Example

```sql
SELECT first_name, DAYNAME(hire_date) AS weekday
FROM emp_details
LIMIT 5;
```

### Output

| first_name | weekday |
|---|---|
| Rahul | Friday |
| Priya | Friday |
| Amit | Wednesday |
| Sneha | Friday |
| Rohan | Wednesday |

---

## 7.9 DATE_FORMAT()

### About

Formats a date according to a specified pattern.

### Syntax

```sql
DATE_FORMAT(date, format)
```

### Example

```sql
SELECT
    first_name,
    DATE_FORMAT(hire_date, '%d-%m-%Y') AS formatted_date
FROM emp_details
LIMIT 5;
```

### Output

| first_name | formatted_date |
|---|---|
| Rahul | 15-01-2021 |
| Priya | 20-03-2020 |
| Amit | 10-07-2019 |
| Sneha | 18-02-2022 |
| Rohan | 12-04-2023 |

Common format specifiers:

| Specifier | Meaning |
|---|---|
| `%Y` | 4-digit year |
| `%y` | 2-digit year |
| `%m` | Month number |
| `%M` | Month name |
| `%d` | Day |
| `%H` | Hour |
| `%i` | Minute |
| `%s` | Second |

---

## 7.10 DATEDIFF()

### About

Returns the number of days between two dates.

### Syntax

```sql
DATEDIFF(date1, date2)
```

### Example

```sql
SELECT
    first_name,
    DATEDIFF(CURDATE(), hire_date) AS days_in_company
FROM emp_details
LIMIT 5;
```

### Output

The exact number changes according to the execution date.

| first_name | days_in_company |
|---|---:|
| Rahul | Calculated by MySQL |
| Priya | Calculated by MySQL |
| Amit | Calculated by MySQL |
| Sneha | Calculated by MySQL |
| Rohan | Calculated by MySQL |

---

## 7.11 DATE_ADD()

### About

Adds an interval to a date.

### Syntax

```sql
DATE_ADD(date, INTERVAL value unit)
```

### Example

```sql
SELECT
    first_name,
    hire_date,
    DATE_ADD(hire_date, INTERVAL 1 YEAR) AS anniversary
FROM emp_details
LIMIT 5;
```

### Output

| first_name | hire_date | anniversary |
|---|---|---|
| Rahul | 2021-01-15 | 2022-01-15 |
| Priya | 2020-03-20 | 2021-03-20 |
| Amit | 2019-07-10 | 2020-07-10 |
| Sneha | 2022-02-18 | 2023-02-18 |
| Rohan | 2023-04-12 | 2024-04-12 |

---

## 7.12 DATE_SUB()

### About

Subtracts an interval from a date.

### Syntax

```sql
DATE_SUB(date, INTERVAL value unit)
```

### Example

```sql
SELECT
    first_name,
    hire_date,
    DATE_SUB(hire_date, INTERVAL 1 YEAR) AS previous_year
FROM emp_details
LIMIT 5;
```

### Output

| first_name | hire_date | previous_year |
|---|---|---|
| Rahul | 2021-01-15 | 2020-01-15 |
| Priya | 2020-03-20 | 2019-03-20 |
| Amit | 2019-07-10 | 2018-07-10 |
| Sneha | 2022-02-18 | 2021-02-18 |
| Rohan | 2023-04-12 | 2022-04-12 |

---

## 7.13 LAST_DAY()

### About

Returns the last day of the month.

### Syntax

```sql
LAST_DAY(date)
```

### Example

```sql
SELECT
    first_name,
    hire_date,
    LAST_DAY(hire_date) AS month_end
FROM emp_details
LIMIT 5;
```

### Output

| first_name | hire_date | month_end |
|---|---|---|
| Rahul | 2021-01-15 | 2021-01-31 |
| Priya | 2020-03-20 | 2020-03-31 |
| Amit | 2019-07-10 | 2019-07-31 |
| Sneha | 2022-02-18 | 2022-02-28 |
| Rohan | 2023-04-12 | 2023-04-30 |

---

# 8. Conditional / Control-Flow Functions

Important functions/expressions:

- `IF()`
- `IFNULL()`
- `NULLIF()`
- `COALESCE()`
- `CASE`

---

## 8.1 IF()

### About

`IF()` returns one value when a condition is true and another value when it is false.

### Syntax

```sql
IF(condition, value_if_true, value_if_false)
```

### Example

```sql
SELECT
    first_name,
    salary,
    IF(salary >= 60000, 'High Salary', 'Normal Salary') AS salary_category
FROM emp_details
LIMIT 8;
```

### Output

| first_name | salary | salary_category |
|---|---:|---|
| Rahul | 55000.00 | Normal Salary |
| Priya | 42000.00 | Normal Salary |
| Amit | 72000.00 | High Salary |
| Sneha | 48000.00 | Normal Salary |
| Rohan | 39000.00 | Normal Salary |
| Ananya | 61000.00 | High Salary |
| Sourav | 45000.00 | Normal Salary |
| Neha | 67000.00 | High Salary |

---

## 8.2 IFNULL()

### About

Returns an alternative value when the first expression is `NULL`.

### Syntax

```sql
IFNULL(expression, replacement_value)
```

### Example

```sql
SELECT
    first_name,
    IFNULL(city, 'Not Available') AS city
FROM emp_details;
```

### Output

Since the sample data contains no NULL city values, the original city values are returned.

| first_name | city |
|---|---|
| Rahul | Kolkata |
| Priya | Delhi |
| Amit | Kolkata |
| Sneha | Mumbai |
| Rohan | Delhi |

---

## 8.3 NULLIF()

### About

Returns `NULL` if two expressions are equal; otherwise returns the first expression.

### Syntax

```sql
NULLIF(expression1, expression2)
```

### Example

```sql
SELECT NULLIF(100, 100) AS result;
```

### Output

| result |
|---|
| NULL |

---

## 8.4 COALESCE()

### About

Returns the first non-NULL value.

### Syntax

```sql
COALESCE(value1, value2, value3, ...)
```

### Example

```sql
SELECT
    COALESCE(NULL, NULL, 'Kolkata', 'Delhi') AS first_available_city;
```

### Output

| first_available_city |
|---|
| Kolkata |

---

## 8.5 CASE

### About

`CASE` allows multiple conditions and is commonly used to classify data.

### Syntax

```sql
CASE
    WHEN condition1 THEN result1
    WHEN condition2 THEN result2
    ELSE result
END
```

### Example

```sql
SELECT
    first_name,
    salary,
    CASE
        WHEN salary >= 70000 THEN 'Very High'
        WHEN salary >= 60000 THEN 'High'
        WHEN salary >= 50000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_level
FROM emp_details
LIMIT 10;
```

### Output

| first_name | salary | salary_level |
|---|---:|---|
| Rahul | 55000.00 | Medium |
| Priya | 42000.00 | Low |
| Amit | 72000.00 | Very High |
| Sneha | 48000.00 | Low |
| Rohan | 39000.00 | Low |
| Ananya | 61000.00 | High |
| Sourav | 45000.00 | Low |
| Neha | 67000.00 | High |
| Arjun | 75000.00 | Very High |
| Moumita | 58000.00 | Medium |

---

# 9. Conversion Functions

Conversion functions are used to convert one data type into another.

Important functions:

- `CAST()`
- `CONVERT()`

---

## 9.1 CAST()

### About

Converts an expression into a specified data type.

### Syntax

```sql
CAST(expression AS data_type)
```

### Example

```sql
SELECT CAST(salary AS SIGNED) AS salary_integer
FROM emp_details
LIMIT 5;
```

### Output

| salary_integer |
|---:|
| 55000 |
| 42000 |
| 72000 |
| 48000 |
| 39000 |

---

## 9.2 CONVERT()

### About

Converts an expression into another data type.

### Syntax

```sql
CONVERT(expression, data_type)
```

### Example

```sql
SELECT CONVERT('2026-08-25', DATE) AS converted_date;
```

### Output

| converted_date |
|---|
| 2026-08-25 |

---

# 10. Other Common Utility Functions

## 10.1 GREATEST()

### About

Returns the greatest value among the supplied arguments.

### Syntax

```sql
GREATEST(value1, value2, ...)
```

### Example

```sql
SELECT GREATEST(50000, 65000, 45000) AS highest_value;
```

### Output

| highest_value |
|---:|
| 65000 |

---

## 10.2 LEAST()

### About

Returns the smallest value among the supplied arguments.

### Syntax

```sql
LEAST(value1, value2, ...)
```

### Example

```sql
SELECT LEAST(50000, 65000, 45000) AS lowest_value;
```

### Output

| lowest_value |
|---:|
| 45000 |

---

## 10.3 GROUP_CONCAT()

### About

Combines values from multiple rows into a single string.

### Syntax

```sql
GROUP_CONCAT(expression)
```

### Example

```sql
SELECT
    department,
    GROUP_CONCAT(first_name ORDER BY first_name SEPARATOR ', ') AS employees
FROM emp_details
GROUP BY department;
```

### Output

| department | employees |
|---|---|
| Finance | Neha, Riya, Sneha, Tania |
| HR | Priya, Puja, Sourav |
| IT | Amit, Ananya, Deb, Moumita, Nandini, Rahul, Vikram |
| Operations | Ishita, Kunal |
| Sales | Aditya, Arjun, Rohan, Sayan |

---

# B. User-Defined Functions

## 11. What is a User-Defined Function?

A **User-Defined Function (UDF)** in MySQL is a stored function created by the programmer to perform a customized operation.

A user-defined stored function:

- Has a user-defined name
- Accepts zero or more parameters
- Performs SQL or expression-based operations
- Returns exactly one value
- Can be called inside SQL statements

---

# 12. Syntax for Creating a User-Defined Function

```sql
DELIMITER //

CREATE FUNCTION function_name(parameter_name DATA_TYPE)
RETURNS return_data_type
DETERMINISTIC
BEGIN
    DECLARE variable_name DATA_TYPE;

    -- statements

    RETURN value;
END //

DELIMITER ;
```

### Important Terms

| Term | Meaning |
|---|---|
| `DELIMITER` | Changes the statement delimiter temporarily |
| `CREATE FUNCTION` | Creates a stored function |
| `parameter` | Input supplied to the function |
| `RETURNS` | Specifies the return data type |
| `DETERMINISTIC` | Same input produces the same output |
| `BEGIN...END` | Contains function statements |
| `RETURN` | Returns the final value |

---

# 13. User-Defined Function Example 1

## Create a Function to Calculate Annual Salary

### Function

```sql
DELIMITER //

CREATE FUNCTION annual_salary(monthly_salary DECIMAL(10,2))
RETURNS DECIMAL(12,2)
DETERMINISTIC
BEGIN
    RETURN monthly_salary * 12;
END //

DELIMITER ;
```

### Test the Function

```sql
SELECT annual_salary(50000) AS annual_salary;
```

### Output

| annual_salary |
|---:|
| 600000.00 |

---

# 14. Apply User-Defined Function on `emp_details`

```sql
SELECT
    emp_id,
    first_name,
    department,
    salary AS monthly_salary,
    annual_salary(salary) AS annual_salary
FROM emp_details
LIMIT 10;
```

### Output

| emp_id | first_name | department | monthly_salary | annual_salary |
|---:|---|---|---:|---:|
| 101 | Rahul | IT | 55000.00 | 660000.00 |
| 102 | Priya | HR | 42000.00 | 504000.00 |
| 103 | Amit | IT | 72000.00 | 864000.00 |
| 104 | Sneha | Finance | 48000.00 | 576000.00 |
| 105 | Rohan | Sales | 39000.00 | 468000.00 |
| 106 | Ananya | IT | 61000.00 | 732000.00 |
| 107 | Sourav | HR | 45000.00 | 540000.00 |
| 108 | Neha | Finance | 67000.00 | 804000.00 |
| 109 | Arjun | Sales | 75000.00 | 900000.00 |
| 110 | Moumita | IT | 58000.00 | 696000.00 |

---

# 15. User-Defined Function Example 2

## Create a Function to Categorize Salary

```sql
DELIMITER //

CREATE FUNCTION salary_category(emp_salary DECIMAL(10,2))
RETURNS VARCHAR(20)
DETERMINISTIC
BEGIN
    DECLARE category VARCHAR(20);

    IF emp_salary >= 70000 THEN
        SET category = 'Very High';
    ELSEIF emp_salary >= 60000 THEN
        SET category = 'High';
    ELSEIF emp_salary >= 50000 THEN
        SET category = 'Medium';
    ELSE
        SET category = 'Low';
    END IF;

    RETURN category;
END //

DELIMITER ;
```

### Test the Function

```sql
SELECT salary_category(75000) AS category;
```

### Output

| category |
|---|
| Very High |

---

# 16. Apply User-Defined Function on Employee Table

```sql
SELECT
    emp_id,
    first_name,
    salary,
    salary_category(salary) AS salary_level
FROM emp_details;
```

### Output

| emp_id | first_name | salary | salary_level |
|---:|---|---:|---|
| 101 | Rahul | 55000.00 | Medium |
| 102 | Priya | 42000.00 | Low |
| 103 | Amit | 72000.00 | Very High |
| 104 | Sneha | 48000.00 | Low |
| 105 | Rohan | 39000.00 | Low |
| 106 | Ananya | 61000.00 | High |
| 107 | Sourav | 45000.00 | Low |
| 108 | Neha | 67000.00 | High |
| 109 | Arjun | 75000.00 | Very High |
| 110 | Moumita | 58000.00 | Medium |
| 111 | Kunal | 46000.00 | Low |
| 112 | Tania | 62000.00 | High |
| 113 | Vikram | 64000.00 | High |
| 114 | Puja | 70000.00 | Very High |
| 115 | Sayan | 43000.00 | Low |
| 116 | Ishita | 68000.00 | High |
| 117 | Deb | 52000.00 | Medium |
| 118 | Riya | 51000.00 | Medium |
| 119 | Aditya | 59000.00 | Medium |
| 120 | Nandini | 85000.00 | Very High |

---

# 17. View Created User-Defined Functions

To view functions created in the current database:

```sql
SHOW FUNCTION STATUS
WHERE Db = 'employee';
```

You can also inspect a particular function:

```sql
SHOW CREATE FUNCTION annual_salary;
```

---

# 18. Delete a User-Defined Function

If a function is no longer required:

```sql
DROP FUNCTION annual_salary;
```

Similarly:

```sql
DROP FUNCTION salary_category;
```

---

