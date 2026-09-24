
## Pre-requistic 
-- ============================================
-- 1. CREATE DATABASE
-- ============================================

CREATE DATABASE IF NOT EXISTS university1;

USE university1;


-- ============================================
-- 2. CREATE DEPARTMENT TABLE
-- ============================================

CREATE TABLE department (
    deptId INT PRIMARY KEY,
    name VARCHAR(50),
    hod VARCHAR(10),
    phone VARCHAR(15)
);


-- ============================================
-- 3. INSERT DEPARTMENT DATA
-- ============================================

INSERT INTO department (deptId, name, hod, phone)
VALUES
(1, 'C.S.E', 'CS006', '2558777'),
(2, 'E.C.E', 'EC004', '2558776');


-- ============================================
-- 4. CREATE PROFESSOR TABLE
-- ============================================

CREATE TABLE professor (
    empId VARCHAR(10) PRIMARY KEY,
    name VARCHAR(100),
    sex VARCHAR(10),
    startYear INT,
    deptNo INT,
    phone VARCHAR(15)
);


-- ============================================
-- 5. INSERT PROFESSOR DATA
-- ============================================

INSERT INTO professor
(empId, name, sex, startYear, deptNo, phone)
VALUES
('CS001', 'Dr. Biplab Sarkar', 'Male', 1982, 1, '9434122345'),
('CS002', 'Dr. Supriya Bhattacharya', 'Male', 2000, 1, '9345134677'),
('CS003', 'M. Sanjoy Pratihar', 'Male', 2003, 1, '9332657342'),
('CS004', 'Ms. Kasturi Dikpati', 'Female', 2003, 1, '9414321908'),
('CS005', 'M. Biswantu Pal', 'Male', 2004, 1, '9544123876'),
('EC001', 'Dr. B. C. Sarkar', 'Male', 1986, 2, '9456128867'),
('EC002', 'Ms. Smita Hazra', 'Female', 2002, 2, '9465123417'),
('EC003', 'M. Somnath Pal', 'Male', 2005, 2, '9435129078'),
('CS006', 'M. Sripati Mukherjee', 'Male', 1977, 1, '9435675489'),
('EC004', 'M. Bivas Paramanik', 'Male', 2002, 2, '9453215789');


-- ============================================
-- 6. CREATE STUDENT TABLE
-- ============================================

CREATE TABLE student (
    rollNo INT,
    name VARCHAR(100),
    degree VARCHAR(10),
    year INT,
    sex VARCHAR(10),
    deptNo INT,
    advisor VARCHAR(10)
);


-- ============================================
-- 7. INSERT STUDENT DATA
-- ============================================

INSERT INTO student
(rollNo, name, degree, year, sex, deptNo, advisor)
VALUES
(1, 'Parag Roy', 'B.E', 3, 'Male', 1, 'CS005'),
(2, 'Riturna Kashyap', 'B.E', 3, 'Male', 1, 'CS005'),
(3, 'Neha', 'B.E', 3, 'Female', 1, 'CS005'),
(4, 'Raman', 'B.E', 4, 'Male', 2, 'EC004'),
(5, 'Surja Sanyal', 'M.E', 2, 'Male', 1, 'CS005'),
(6, 'Susahant Satyam', 'M.E', 1, 'Male', 2, 'EC004'),
(7, 'Kamalika Samanta', 'M.E', 1, 'Female', 1, 'CS005'),
(8, 'Aparajita', 'B.E', 2, 'Female', 2, 'EC004'),
(9, 'Sirajul Islam', 'M.E', 2, 'Male', 2, 'EC004'),
(10, 'Manisha Chaudhury', 'M.E', 2, 'Female', 2, 'EC004'),
(7, 'Kamalika Samanta', 'M.E', 1, 'Female', 1, 'CS005');


-- ============================================
-- 8. CREATE COURSE TABLE
-- ============================================

CREATE TABLE course (
    courseId VARCHAR(10) PRIMARY KEY,
    name VARCHAR(50),
    credits INT,
    deptNo INT
);


-- ============================================
-- 9. INSERT COURSE DATA
-- ============================================

INSERT INTO course
(courseId, name, credits, deptNo)
VALUES
('UCS001', 'UG CSE', 2, 1),
('PCS001', 'PG CSE', 4, 1),
('UEC001', 'UG ECE', 2, 2),
('PEC001', 'PG ECE', 4, 2);


-- ============================================
-- 10. CREATE ENROLLMENT TABLE
-- ============================================

CREATE TABLE enrollment (
    rollNo INT,
    courseId VARCHAR(10),
    sem INT,
    year INT,
    grade VARCHAR(5)
);


-- ============================================
-- 11. INSERT ENROLLMENT DATA
-- ============================================

INSERT INTO enrollment
(rollNo, courseId, sem, year, grade)
VALUES
(1, 'UCS001', 6, 3, 'A'),
(2, 'UCS001', 6, 3, 'B'),
(3, 'UCS001', 6, 3, 'A+'),
(4, 'UEC001', 8, 4, 'A'),
(5, 'PCS001', 4, 2, 'A+'),
(6, 'PEC001', 2, 1, 'A+'),
(7, 'PCS001', 2, 1, 'A++'),
(8, 'UEC001', 4, 2, 'B++'),
(9, 'PEC001', 4, 2, 'A'),
(10, 'PEC001', 4, 2, 'B++');


-- ============================================
-- 12. CREATE TEACHING TABLE
-- ============================================

CREATE TABLE teaching (
    empId VARCHAR(10),
    courseId VARCHAR(10),
    sem INT,
    year INT,
    classroom VARCHAR(10)
);


-- ============================================
-- 13. INSERT TEACHING DATA
-- ============================================

INSERT INTO teaching
(empId, courseId, sem, year, classroom)
VALUES
('CS001', 'PCS001', 2, 1, 'PC-1'),
('CS001', 'PCS001', 4, 2, 'PC-2'),
('CS002', 'PCS001', 2, 1, 'PC-1'),
('CS003', 'UCS001', 6, 3, 'UC-1'),
('CS004', 'UCS001', 6, 3, 'UC-1'),
('CS005', 'PCS001', 2, 1, 'PC-1'),
('CS005', 'UCS001', 6, 3, 'UC-1'),
('EC001', 'UEC001', 4, 2, 'UE-1'),
('EC002', 'UEC001', 4, 2, 'UE-1'),
('EC003', 'PEC001', 4, 2, 'PE-1'),
('EC003', 'UEC001', 6, 3, 'UE-1');


-- ============================================
-- 14. CREATE PREREQUISITE TABLE
-- ============================================

CREATE TABLE prerequisite (
    preReqCourse VARCHAR(20),
    courseId VARCHAR(10)
);


-- ============================================
-- 15. INSERT PREREQUISITE DATA
-- ============================================

INSERT INTO prerequisite
(preReqCourse, courseId)
VALUES
('H.S', 'UCS001'),
('B.E', 'PCS001'),
('H.S', 'UEC001'),
('B.E', 'PEC001');


-- ============================================
-- 16. DISPLAY ALL TABLES
-- ============================================

SHOW TABLES;

- Display data

SHOW TABLES;

SELECT * FROM department;
SELECT * FROM professor;
SELECT * FROM student;
SELECT * FROM course;
SELECT * FROM enrollment;
SELECT * FROM teaching;
SELECT * FROM prerequisite;


## Assignment-1

1. Show the roll no and name of the students who read B.E.
2. Show the roll no and name of the students who read M.E. 
3. Show the roll no and name of the male students. 
4. Show the roll no and name of the female students.
5. Show the department id and phone no of Computer Sc & Engg. Dept. 
6. Show the Emp id, name, sex and phone no of the professors who joind before 2000. 
7. Show the name and phone nof of the fhe male professors. 
8. Show the roll no, course id and grade of top graded students. 
9. Show the roll no and course id of the first year students. 
10. Show the roll no and course id of the other than 1st year students. 
11. Show the credit point of under gradute C.S.E course. 
12. Show the course name whose credit points are 4.
13. Show the start year and phone no of the female professors. 
14. Show the roll no and course id of the students who have below B grade. 
15. Show the Roll no, year and degree of the student whose name is Aparajita. 

## Assignment-2

## Assignment-3
## Assignment-4