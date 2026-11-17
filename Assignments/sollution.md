
## Assignment #1

### Question 1

**Show the roll no and name of the students who read B.E.**

```sql
SELECT rollNo, name
FROM student
WHERE degree = 'B.E'
ORDER BY rollNo;
```

**Expected Result:**

| rollNo | name |
| --- | --- |
| 1 | Parag Roy |
| 2 | Rituparna Kashyap |
| 3 | Neha |
| 4 | Raman |
| 8 | Aparajita |

### Question 2

**Show the roll no and name of the students who read M.E.**

```sql
SELECT rollNo, name
FROM student
WHERE degree = 'M.E'
ORDER BY rollNo;
```

**Expected Result:**

| rollNo | name |
| --- | --- |
| 5 | Surja Sanyal |
| 6 | Susahant Satyam |
| 7 | Kamalika Samanta |
| 9 | Sirajul Islam |
| 10 | Manisha Chaudhury |

### Question 3

**Show the roll no and name of the male students.**

```sql
SELECT rollNo, name
FROM student
WHERE sex = 'Male'
ORDER BY rollNo;
```

**Expected Result:**

| rollNo | name |
| --- | --- |
| 1 | Parag Roy |
| 2 | Rituparna Kashyap |
| 4 | Raman |
| 5 | Surja Sanyal |
| 6 | Susahant Satyam |
| 9 | Sirajul Islam |

### Question 4

**Show the roll no and name of the female students.**

```sql
SELECT rollNo, name
FROM student
WHERE sex = 'Female'
ORDER BY rollNo;
```

**Expected Result:**

| rollNo | name |
| --- | --- |
| 3 | Neha |
| 7 | Kamalika Samanta |
| 8 | Aparajita |
| 10 | Manisha Chaudhury |

### Question 5

**Show the department id and phone no of Computer Sc & Engg. Dept.**

```sql
SELECT deptId, phone
FROM department
WHERE name = 'C.S.E';
```

**Expected Result:**

| deptId | phone |
| --- | --- |
| 1 | 2558777 |

### Question 6

**Show the Emp id, name, sex and phone no of the professors who joined before 2000.**

```sql
SELECT empId, name, sex, phone
FROM professor
WHERE startYear < 2000
ORDER BY empId;
```

**Expected Result:**

| empId | name | sex | phone |
| --- | --- | --- | --- |
| CS001 | Dr.Biplab Sarkar | Male | 9434122345 |
| CS006 | Mr.Sripati Mukherjee | Male | 9435675489 |
| EC001 | Dr.B.C.Sarkar | Male | 9456128867 |

### Question 7

**Show the name and phone no of the male professors.**

```sql
SELECT name, phone
FROM professor
WHERE sex = 'Male'
ORDER BY empId;
```

**Expected Result:**

| name | phone |
| --- | --- |
| Dr.Biplab Sarkar | 9434122345 |
| Dr.Souvik Bhattarcharya | 9345134677 |
| Mr.Sanjoy Pratihar | 9332657342 |
| Mr.Biswanath Pal | 9454123876 |
| Mr.Sripati Mukherjee | 9435675489 |
| Dr.B.C.Sarkar | 9456128867 |
| Mr.Somnath pal | 9435129078 |
| Mr.Bivas Paramanik | 9453215789 |

### Question 8

**Show the roll no, course id and grade of top graded students.**

> Top grade is taken as A++.

```sql
SELECT rollNo, courseId, grade
FROM enrollment
WHERE grade = 'A++';
```

**Expected Result:**

| rollNo | courseId | grade |
| --- | --- | --- |
| 7 | PCS001 | A++ |

### Question 9

**Show the roll no and course id of the first year students.**

```sql
SELECT rollNo, courseId
FROM enrollment
WHERE year = 1
ORDER BY rollNo;
```

**Expected Result:**

| rollNo | courseId |
| --- | --- |
| 6 | PEC001 |
| 7 | PCS001 |

### Question 10

**Show the roll no and course id of the other than 1st year students.**

```sql
SELECT rollNo, courseId
FROM enrollment
WHERE year <> 1
ORDER BY rollNo;
```

**Expected Result:**

| rollNo | courseId |
| --- | --- |
| 1 | UCS001 |
| 2 | UCS001 |
| 3 | UCS001 |
| 4 | UEC001 |
| 5 | PCS001 |
| 8 | UEC001 |
| 9 | PEC001 |
| 10 | PEC001 |

### Question 11

**Show the credit point of undergraduate C.S.E course.**

```sql
SELECT credits
FROM course
WHERE cname = 'UG(CSE)';
```

**Expected Result:**

| credits |
| --- |
| 2 |

### Question 12

**Show the course name whose credit points are 4.**

```sql
SELECT cname
FROM course
WHERE credits = 4
ORDER BY courseId;
```

**Expected Result:**

| cname |
| --- |
| PG(CSE) |
| PG(ECE) |

### Question 13

**Show the start year and phone no of the female professors.**

```sql
SELECT startYear, phone
FROM professor
WHERE sex = 'Female'
ORDER BY empId;
```

**Expected Result:**

| startYear | phone |
| --- | --- |
| 2003 | 9414321908 |
| 2002 | 9465123417 |

### Question 14

**Show the roll no and course id of the students who have below B grade.**

> Grade order is A++ > A+ > A > B++ > B+ > B > C... No student in the data has a grade below B (the lowest is B), so the result is empty.

```sql
SELECT rollNo, courseId
FROM enrollment
WHERE grade LIKE 'C%' OR grade LIKE 'D%' OR grade = 'F';
```

**Expected Result:**

| rollNo | courseId |
| --- | --- |
| *Empty set (0 rows)* |  |

### Question 15

**Show the Roll no, year and degree of the student whose name is Aparajita.**

```sql
SELECT rollNo, year, degree
FROM student
WHERE name = 'Aparajita';
```

**Expected Result:**

| rollNo | year | degree |
| --- | --- | --- |
| 8 | 2 | B.E |

---



## Assignment #2

### Question 16

**Display the roll no and name of the students from C.S.E department.**

```sql
SELECT s.rollNo, s.name
FROM student s
JOIN department d ON s.deptNo = d.deptId
WHERE d.name = 'C.S.E'
ORDER BY s.rollNo;
```

**Expected Result:**

| rollNo | name |
| --- | --- |
| 1 | Parag Roy |
| 2 | Rituparna Kashyap |
| 3 | Neha |
| 5 | Surja Sanyal |
| 7 | Kamalika Samanta |

### Question 17

**Display the roll no, name and year of the male students from E.C.E department.**

```sql
SELECT s.rollNo, s.name, s.year
FROM student s
JOIN department d ON s.deptNo = d.deptId
WHERE s.sex = 'Male'
  AND d.name = 'E.C.E'
ORDER BY s.rollNo;
```

**Expected Result:**

| rollNo | name | year |
| --- | --- | --- |
| 4 | Raman | 4 |
| 6 | Susahant Satyam | 1 |
| 9 | Sirajul Islam | 2 |

### Question 18

**Display the rollno, name, degree of the students whose advisor is Mr.Biswanath Pal.**

```sql
SELECT s.rollNo, s.name, s.degree
FROM student s
JOIN professor p ON s.advisor = p.empId
WHERE p.name = 'Mr.Biswanath Pal'
ORDER BY s.rollNo;
```

**Expected Result:**

| rollNo | name | degree |
| --- | --- | --- |
| 1 | Parag Roy | B.E |
| 2 | Rituparna Kashyap | B.E |
| 3 | Neha | B.E |
| 5 | Surja Sanyal | M.E |
| 7 | Kamalika Samanta | M.E |

### Question 19

**Display the rollno, name of the M.E female students whose advisor is Mr.Bivas Paramanik.**

```sql
SELECT s.rollNo, s.name
FROM student s
JOIN professor p ON s.advisor = p.empId
WHERE s.degree = 'M.E'
  AND s.sex = 'Female'
  AND p.name = 'Mr.Bivas Paramanik';
```

**Expected Result:**

| rollNo | name |
| --- | --- |
| 10 | Manisha Chaudhury |

### Question 20

**Display the name and phone no of HOD of CSE department.**

```sql
SELECT p.name, p.phone
FROM department d
JOIN professor p ON d.hod = p.empId
WHERE d.name = 'C.S.E';
```

**Expected Result:**

| name | phone |
| --- | --- |
| Mr.Sripati Mukherjee | 9435675489 |

### Question 21

**Display the name of female Professors of CSE department.**

```sql
SELECT p.name
FROM professor p
JOIN department d ON p.deptNo = d.deptId
WHERE p.sex = 'Female'
  AND d.name = 'C.S.E';
```

**Expected Result:**

| name |
| --- |
| Mrs.Kasturi Dikpati |

### Question 22

**Display the empid, name, start year of HOD of ECE department.**

```sql
SELECT p.empId, p.name, p.startYear
FROM department d
JOIN professor p ON d.hod = p.empId
WHERE d.name = 'E.C.E';
```

**Expected Result:**

| empId | name | startYear |
| --- | --- | --- |
| EC004 | Mr.Bivas Paramanik | 2002 |

### Question 23

**Display rollno and name of 2nd year M.E male students from ECE department.**

```sql
SELECT s.rollNo, s.name
FROM student s
JOIN department d ON s.deptNo = d.deptId
WHERE s.year = 2
  AND s.degree = 'M.E'
  AND s.sex = 'Male'
  AND d.name = 'E.C.E';
```

**Expected Result:**

| rollNo | name |
| --- | --- |
| 9 | Sirajul Islam |

### Question 24

**Display the name, degree, courseid, sem of the student who has rollno 1.**

```sql
SELECT s.name, s.degree, e.courseId, e.sem
FROM student s
JOIN enrollment e ON s.rollNo = e.rollNo
WHERE s.rollNo = 1;
```

**Expected Result:**

| name | degree | courseId | sem |
| --- | --- | --- | --- |
| Parag Roy | B.E | UCS001 | 6 |

### Question 25

**Display the rollno, name and Degree of post graduate students whose Grade is A++.**

```sql
SELECT s.rollNo, s.name, s.degree
FROM student s
JOIN enrollment e ON s.rollNo = e.rollNo
WHERE s.degree = 'M.E'
  AND e.grade = 'A++';
```

**Expected Result:**

| rollNo | name | degree |
| --- | --- | --- |
| 7 | Kamalika Samanta | M.E |

### Question 26

**Display the roll no, Name of students in the CSE department along with their advisor name and his empid.**

```sql
SELECT s.rollNo, s.name, p.name AS advisor_name, p.empId
FROM student s
JOIN department d ON s.deptNo = d.deptId
JOIN professor p ON s.advisor = p.empId
WHERE d.name = 'C.S.E'
ORDER BY s.rollNo;
```

**Expected Result:**

| rollNo | name | advisor_name | empId |
| --- | --- | --- | --- |
| 1 | Parag Roy | Mr.Biswanath Pal | CS005 |
| 2 | Rituparna Kashyap | Mr.Biswanath Pal | CS005 |
| 3 | Neha | Mr.Biswanath Pal | CS005 |
| 5 | Surja Sanyal | Mr.Biswanath Pal | CS005 |
| 7 | Kamalika Samanta | Mr.Biswanath Pal | CS005 |

### Question 27

**Display the name, employee ids, phone nos, in CSE department who have joined before 1995.**

```sql
SELECT p.name, p.empId, p.phone
FROM professor p
JOIN department d ON p.deptNo = d.deptId
WHERE d.name = 'C.S.E'
  AND p.startYear < 1995
ORDER BY p.empId;
```

**Expected Result:**

| name | empId | phone |
| --- | --- | --- |
| Dr.Biplab Sarkar | CS001 | 9434122345 |
| Mr.Sripati Mukherjee | CS006 | 9435675489 |

### Question 28

**Display the empid and Name of professors who teaches post graduate in ECE department.**

> The only ECE professor linked to a PG course is EC003, whose Teaching row uses course id PCE001 (not found in Course). So the result is empty. If PCE001 is corrected to PEC001, the result is EC003, Mr.Somnath pal.

```sql
SELECT DISTINCT p.empId, p.name
FROM professor p
JOIN teaching t ON p.empId = t.empId
JOIN course c ON t.courseId = c.courseId
JOIN department d ON c.deptNo = d.deptId
WHERE c.cname LIKE 'PG%'
  AND d.name = 'E.C.E';
```

**Expected Result:**

| empId | name |
| --- | --- |
| *Empty set (0 rows)* |  |

### Question 29

**Display the name and roll no. of the students who read in second sem post graduate from ECE and grade greater than B++.**

> Grades above B++ are A, A+ and A++.

```sql
SELECT s.name, s.rollNo
FROM student s
JOIN enrollment e ON s.rollNo = e.rollNo
JOIN course c ON e.courseId = c.courseId
JOIN department d ON c.deptNo = d.deptId
WHERE e.sem = 2
  AND s.degree = 'M.E'
  AND d.name = 'E.C.E'
  AND e.grade IN ('A++', 'A+', 'A');
```

**Expected Result:**

| name | rollNo |
| --- | --- |
| Susahant Satyam | 6 |

### Question 30

**Display the names of the professors who teach in undergraduate 6th semester CSE courses.**

```sql
SELECT DISTINCT p.name
FROM professor p
JOIN teaching t ON p.empId = t.empId
JOIN course c ON t.courseId = c.courseId
JOIN department d ON c.deptNo = d.deptId
WHERE c.cname LIKE 'UG%'
  AND t.sem = 6
  AND d.name = 'C.S.E'
ORDER BY p.name;
```

**Expected Result:**

| name |
| --- |
| Mr.Biswanath Pal |
| Mr.Sanjoy Pratihar |
| Mrs.Kasturi Dikpati |

---


## Assignment #3

### Question 1

**Get the empid, name of senior most professors.**

> Senior most means the earliest start year.

```sql
SELECT empId, name
FROM professor
WHERE startYear = (SELECT MIN(startYear) FROM professor);
```

**Expected Result:**

| empId | name |
| --- | --- |
| CS006 | Mr.Sripati Mukherjee |

### Question 2

**Get the rollno, name of the students whose gender is same as their advisor.**

```sql
SELECT s.rollNo, s.name
FROM student s
JOIN professor p ON s.advisor = p.empId
WHERE s.sex = p.sex
ORDER BY s.rollNo;
```

**Expected Result:**

| rollNo | name |
| --- | --- |
| 1 | Parag Roy |
| 2 | Rituparna Kashyap |
| 4 | Raman |
| 5 | Surja Sanyal |
| 6 | Susahant Satyam |
| 9 | Sirajul Islam |

### Question 3

**Get the courseid, coursename, sem taught by advisor of C.S.E dept.**

> The advisor of the C.S.E dept is the professor who advises C.S.E students (CS005).

```sql
SELECT DISTINCT c.courseId, c.cname, t.sem
FROM teaching t
JOIN course c ON t.courseId = c.courseId
WHERE t.empId IN (
  SELECT s.advisor
  FROM student s
  JOIN department d ON s.deptNo = d.deptId
  WHERE d.name = 'C.S.E'
)
ORDER BY c.courseId;
```

**Expected Result:**

| courseId | cname | sem |
| --- | --- | --- |
| PCS001 | PG(CSE) | 2 |
| UCS001 | UG(CSE) | 6 |

### Question 4

**Get the courseid, coursename, sem taught by H.O.D of each dept.**

> The HODs (CS006 and EC004) have no rows in the Teaching table, so the result is empty.

```sql
SELECT c.courseId, c.cname, t.sem
FROM department d
JOIN teaching t ON d.hod = t.empId
JOIN course c ON t.courseId = c.courseId;
```

**Expected Result:**

| courseId | cname | sem |
| --- | --- | --- |
| *Empty set (0 rows)* |  |  |

### Question 5

**Get the post graduate male student and course credit point from C.S.E dept.**

```sql
SELECT s.rollNo, s.name, c.credits
FROM student s
JOIN department d ON s.deptNo = d.deptId
JOIN enrollment e ON s.rollNo = e.rollNo
JOIN course c ON e.courseId = c.courseId
WHERE s.degree = 'M.E'
  AND s.sex = 'Male'
  AND d.name = 'C.S.E';
```

**Expected Result:**

| rollNo | name | credits |
| --- | --- | --- |
| 5 | Surja Sanyal | 4 |

### Question 6

**Get the courseid, coursename, department name which has at least one female student.**

```sql
SELECT DISTINCT c.courseId, c.cname, d.name AS department_name
FROM course c
JOIN department d ON c.deptNo = d.deptId
JOIN enrollment e ON c.courseId = e.courseId
JOIN student s ON e.rollNo = s.rollNo
WHERE s.sex = 'Female'
ORDER BY c.courseId;
```

**Expected Result:**

| courseId | cname | department_name |
| --- | --- | --- |
| PCS001 | PG(CSE) | C.S.E |
| PEC001 | PG(ECE) | E.C.E |
| UCS001 | UG(CSE) | C.S.E |
| UEC001 | UG(ECE) | E.C.E |

### Question 7

**Get the courseid, coursename, department name which is not a 6 point course.**

> All courses have 2 or 4 credits, so every course is returned.

```sql
SELECT c.courseId, c.cname, d.name AS department_name
FROM course c
JOIN department d ON c.deptNo = d.deptId
WHERE c.credits <> 6
ORDER BY c.courseId;
```

**Expected Result:**

| courseId | cname | department_name |
| --- | --- | --- |
| PCS001 | PG(CSE) | C.S.E |
| PEC001 | PG(ECE) | E.C.E |
| UCS001 | UG(CSE) | C.S.E |
| UEC001 | UG(ECE) | E.C.E |

### Question 8

**Get the courseid, coursename which has at least one A++ grade student.**

```sql
SELECT DISTINCT c.courseId, c.cname
FROM course c
JOIN enrollment e ON c.courseId = e.courseId
WHERE e.grade = 'A++';
```

**Expected Result:**

| courseId | cname |
| --- | --- |
| PCS001 | PG(CSE) |

### Question 9

**Get the rollno, name of the female student taught by the advisor of CSE dept.**

```sql
SELECT DISTINCT s.rollNo, s.name
FROM student s
JOIN enrollment e ON s.rollNo = e.rollNo
JOIN teaching t ON e.courseId = t.courseId
WHERE s.sex = 'Female'
  AND t.empId IN (
  SELECT s.advisor
  FROM student s
  JOIN department d ON s.deptNo = d.deptId
  WHERE d.name = 'C.S.E'
)
ORDER BY s.rollNo;
```

**Expected Result:**

| rollNo | name |
| --- | --- |
| 3 | Neha |
| 7 | Kamalika Samanta |

### Question 10

**Get the course id, coursename which have any final year student.**

> Final year means year 4 for B.E and year 2 for M.E.

```sql
SELECT DISTINCT c.courseId, c.cname
FROM course c
JOIN enrollment e ON c.courseId = e.courseId
JOIN student s ON e.rollNo = s.rollNo
WHERE (s.degree = 'B.E' AND s.year = 4)
   OR (s.degree = 'M.E' AND s.year = 2)
ORDER BY c.courseId;
```

**Expected Result:**

| courseId | cname |
| --- | --- |
| PCS001 | PG(CSE) |
| PEC001 | PG(ECE) |
| UEC001 | UG(ECE) |

---

