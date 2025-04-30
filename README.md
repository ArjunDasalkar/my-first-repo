# NPTEL SQL Practice Exercises

This document contains a set of SQL exercises including DDL, DML, functions, joins, loops, cursors, and more.

---

## 1 & 2. Execute Basic DDL and DML Commands

```sql
CREATE TABLE student (
    std_id INTEGER PRIMARY KEY,
    std_name VARCHAR(20),
    std_branch VARCHAR(20)
);

ALTER TABLE student ADD phone_no INTEGER;

INSERT INTO student (std_id, std_name, std_branch, phone_no) VALUES
(1, 'Adi', 'CSE', 111),
(2, 'Siddhesh', 'CSE', 222),
(3, 'Aryan', 'CSE', 333),
(4, 'Ronit', 'CSE', 444),
(5, 'Arjun', 'CSE', 555),
(6, 'Ved', 'CSE', 666);

UPDATE student SET std_branch = 'IT' WHERE std_id = 3;

DELETE FROM student WHERE std_id = 6;

SELECT * FROM student;
```

---

## 3. Execute Database Functions (COUNT, DATE, etc.)

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(20),
    salary DECIMAL(10,2),
    joining_date DATE,
    department VARCHAR(20)
);

INSERT INTO employees(id, name, salary, joining_date, department) VALUES
(1, 'Alice', 50000, '2023-05-10', 'HR'),
(2, 'Bob', 60000, '2022-07-15', 'Finance'),
(3, 'Charlie', 70000, '2021-09-20', 'IT'),
(4, 'David', 80000, '2020-11-25', 'HR'),
(5, 'Eve', 55000, '2023-01-25', 'Finance');

SELECT name, salary,
ROUND(salary, 0) AS Rounded_Salary,
CEILING(salary) AS Ceiling_value,
FLOOR(salary) AS Floor_value
FROM employees;

SELECT name, joining_date,
YEAR(joining_date) AS Year_Joined,
MONTH(joining_date) AS Month_Joined,
DAY(joining_date) AS Day_Joined
FROM employees;

SELECT department,
COUNT(*) AS Total_Employees,
AVG(salary) AS Average_Salary,
SUM(salary) AS Total_salary,
MAX(salary) AS Highest_salary,
MIN(salary) AS Lowest_salary
FROM employees
GROUP BY department;

SELECT name,
UPPER(name) AS Upper_case,
LOWER(name) AS Lower_case,
LEN(name) AS Name_Length
FROM employees;

SELECT COUNT(*) AS Total_Employees FROM employees;

SELECT * FROM employees;
```

---

## 4. Perform Join Operation

```sql
CREATE TABLE department(
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(20)
);

CREATE TABLE employee(
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(20),
    dept_id INT,
    salary DECIMAL(10,2),
    FOREIGN KEY(dept_id) REFERENCES department(dept_id)
);

INSERT INTO department(dept_id, dept_name) VALUES
(1, 'HR'),
(2, 'Finance'),
(3, 'IT'),
(4, 'Marketing');

INSERT INTO employee(emp_id, emp_name, dept_id, salary) VALUES
(101, 'Alice', 1, 50000),
(102, 'Bob', 2, 60000),
(103, 'Charlie', 3, 70000),
(104, 'David', 4, 80000),
(105, 'Eve', NULL, 55000);

SELECT employee.emp_name, employee.salary, department.dept_name
FROM employee
INNER JOIN department ON employee.dept_id = department.dept_id;

SELECT employee.emp_name, employee.salary, department.dept_name
FROM employee
LEFT JOIN department ON employee.dept_id = department.dept_id;

SELECT employee.emp_name, employee.salary, department.dept_name
FROM employee
RIGHT JOIN department ON employee.dept_id = department.dept_id;

SELECT employee.emp_name, employee.salary, department.dept_name
FROM employee
FULL JOIN department ON employee.dept_id = department.dept_id;

SELECT * FROM department;
SELECT * FROM employee;
```

---

## 5. Run SQL Query Using GROUP BY Clause

```sql
CREATE TABLE employee(
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(20),
    department VARCHAR(20),
    salary DECIMAL(10,2)
);

INSERT INTO employee(emp_id, emp_name, department, salary) VALUES
(101, 'Alice', 'HR', 50000),
(102, 'Bob', 'Finance', 60000),
(103, 'Charlie', 'IT', 70000),
(104, 'David', 'HR', 80000),
(105, 'Eve', 'Finance', 55000),
(106, 'Frank', 'IT', 75000),
(107, 'Grace', 'HR', 52000);

SELECT department, COUNT(*) AS Total_Employee FROM employee GROUP BY department;
SELECT department, SUM(salary) AS Total_Salary FROM employee GROUP BY department;
SELECT department, AVG(salary) AS Average_Salary FROM employee GROUP BY department;
SELECT department, MAX(salary) AS Maximum_Salary FROM employee GROUP BY department;
SELECT department, MIN(salary) AS Minimum_Salary FROM employee GROUP BY department;
SELECT * FROM employee;
```

---

## 6. Program to Create View in SQL

*Content marked "IN PDF" – not included.*

---

## 7. Arithmetic Commands

```plsql
DECLARE
    num1 NUMBER := 20;
    num2 NUMBER := 5;
    sum_result NUMBER;
    sub_result NUMBER;
    mul_result NUMBER;
    div_result NUMBER;
BEGIN
    sum_result := num1 + num2;
    sub_result := num1 - num2;
    mul_result := num1 * num2;
    div_result := num1 / num2;

    DBMS_OUTPUT.PUT_LINE('Addition: ' || sum_result);
    DBMS_OUTPUT.PUT_LINE('Subtraction: ' || sub_result);
    DBMS_OUTPUT.PUT_LINE('Multiplication: ' || mul_result);
    DBMS_OUTPUT.PUT_LINE('Division: ' || div_result);
END;
/
```

---

## 8. Loops in SQL Server

```sql
DECLARE @i INT = 10;
WHILE @i <= 40
BEGIN
    PRINT(@i);
    SET @i = @i + 10;
END;

DECLARE @j INT = 10;
WHILE @j <= 40
BEGIN
    PRINT(@j);
    SET @j = @j + 10;
    IF (@j = 30)
        BREAK;
END;
```

---

## 9. Cursor in SQL

```plsql
DECLARE
    v_name students.name%TYPE;
    v_marks students.marks%TYPE;

    CURSOR student_cursor IS
        SELECT name, marks FROM students;
BEGIN
    OPEN student_cursor;

    LOOP
        FETCH student_cursor INTO v_name, v_marks;
        EXIT WHEN student_cursor%NOTFOUND;

        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Marks: ' || v_marks);
    END LOOP;

    CLOSE student_cursor;
END;
```
