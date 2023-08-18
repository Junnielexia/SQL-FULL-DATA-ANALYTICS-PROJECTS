# SQL-FULL-DATA-ANALYTICS-PROJECTS
# MySQL

## MySQL Workbench for Data Analysts

### Database Connection
1. Launch MySQL Workbench and establish a connection to your MySQL database by clicking on "Database" and selecting "Connect to Database."

### SQL Syntax and Execution
1. Querying Data: Use the SQL `SELECT` statement to retrieve data from tables.
```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

2. Filtering Results: Utilize the `WHERE` clause to filter query results based on specific conditions.
```sql
SELECT column1, column2
FROM table_name
WHERE condition1 AND condition2;
```

3. Sorting Data: Apply the `ORDER BY` clause to sort query results in ascending or descending order.
```sql
SELECT column1, column2
FROM table_name
ORDER BY column1 ASC;
```

4. Aggregating Data: Aggregate data using functions such as `COUNT`, `SUM`, `AVG`, etc.
```sql
SELECT COUNT(column1), AVG(column2)
FROM table_name
GROUP BY column3;
```

5. Joining Tables: Combine data from multiple tables using different types of joins (`INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN`).
```sql
SELECT *
FROM table1
JOIN table2 ON table1.column1 = table2.column2;
```

### Data Manipulation
1. Inserting Data: Use the `INSERT INTO` statement to add new records to a table.
```sql
INSERT INTO table_name (column1, column2)
VALUES (value1, value2);
```

2. Updating Data: Update existing records using the `UPDATE` statement.
```sql
UPDATE table_name
SET column1 = new_value
WHERE condition;
```

3. Deleting Data: Remove specific records from a table with the `DELETE` statement.
```sql
DELETE FROM table_name
WHERE condition;
```

### Database Design
1. Creating Tables: Use the `CREATE TABLE` statement to define the structure of a new table.
```sql
CREATE TABLE table_name (
    column1 datatype,
    column2 datatype,
    ...
);
```

2. Modifying Tables: Alter existing tables using `ALTER TABLE` statement to add, modify, or drop columns.
```sql
ALTER TABLE table_name
ADD column_name datatype;

ALTER TABLE table_name
MODIFY COLUMN column_name datatype;

ALTER TABLE table_name
DROP COLUMN column_name;
```

### Exporting and Importing Data
1. Exporting Data: Right-click on a table, select "Table Data Export Wizard," and choose the desired export format (e.g., CSV, SQL).

2. Importing Data: Right-click on a table, select "Table Data Import Wizard," and follow the steps to import data from a file.

### Visual Database Design
1. Entity-Relationship Diagrams: Use the "Modeling" perspective to create Entity-Relationship (ER) diagrams and visually design the database schema.

### Note: 
This guide provides an overview of essential MySQL Workbench features and syntax commonly used by data analysts. However, MySQL Workbench offers additional functionalities for database administration, stored procedures, and more. For further information, consult the MySQL Workbench documentation.
***
Here's the formatted text in Markdown:

## Task One
1. Create a database named `students_information`.
2. In the database you have created, create a table that has the following columns with the right data type:
   - `students_Id`
   - `first_name`
   - `last_name`
   - `Age`
   - `Exam_score`
   - `passing_grade` (A, B, C, D).
3. Populate the table for 10 students.

### Answer
```sql
-- Create the database
CREATE DATABASE students_information;
USE students_information;

-- Create the students table
CREATE TABLE students (
    students_Id INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    Age INT,
    Exam_score INT,
    passing_grade CHAR(1)
);

-- Insert data into the students table
INSERT INTO students (students_Id, first_name, last_name, Age, Exam_score, passing_grade) VALUES
    (1, 'Aang', 'Airbender', 112, 90, 'A'),
    (2, 'Katara', 'Waterbender', 15, 85, 'B'),
    (3, 'Sokka', 'Warrior', 16, 78, 'C'),
    (4, 'Toph', 'Beifong', 12, 92, 'A'),
    (5, 'Zuko', 'Firebender', 17, 88, 'B'),
    (6, 'Azula', 'Firebender', 14, 95, 'A'),
    (7, 'Iroh', 'Dragon', 60, 89, 'B'),
    (8, 'Suki', 'Kyoshi Warrior', 16, 87, 'B'),
    (9, 'Mai', 'Assassin', 17, 84, 'B'),
    (10, 'Ty Lee', 'Circus Performer', 16, 82, 'C');
```
![image](images/Screenshot%20(86).png)

***
### Task two
1. insert 5 more rows of infformation into the table you already created
2. update the Scores and Grades of the first 5 students in your Table to the following respectively ( scores: 60,65,50.5,45 and 71.5) (Grades: B,B,C,D and A)
3. delete the records of student id 6,7,8,9,10
4. Show the first Names and Grades of every student
5. show the records for students with the following GRades only (Grades : A and B)
#### ANSWER

### Task Two

1. Insert 5 more rows of information into the table you already created.

```
#### Answer - Inserting 5 More Rows

To insert 5 more rows into the existing table, you can use the following syntax:

```sql
INSERT INTO students (students_Id, first_name, last_name, Age, Exam_score, passing_grade) VALUES
    (11, 'SokkI', 'Swordmaster', 18, 85, 'B'),
    (12, 'ZukI', 'Firelord', 19, 92, 'A'),
    (13, 'AzulI', 'Princess', 17, 78, 'C'),
    (14, 'KatarI', 'Healer', 20, 90, 'A'),
    (15, 'TopI', 'Metalbender', 16, 88, 'B');

```
![image](images/Screenshot%20(88).png)


2. Update the Scores and Grades of the first 5 students in your table to the following respectively (scores: 60, 65, 50.5, 45, and 71.5) (Grades: B, B, C, D, and A).

```
#### Answer - Updating Scores and Grades

To update the scores and grades of the first 5 students in your table, you can use the following syntax:

```sql
UPDATE students
SET Exam_score = CASE students_Id
    WHEN 1 THEN 60
    WHEN 2 THEN 65
    WHEN 3 THEN 50.5
    WHEN 4 THEN 45
    WHEN 5 THEN 71.5
    ELSE Exam_score
    END,
    passing_grade = CASE students_Id
    WHEN 1 THEN 'B'
    WHEN 2 THEN 'B'
    WHEN 3 THEN 'C'
    WHEN 4 THEN 'D'
    WHEN 5 THEN 'A'
    ELSE passing_grade
    END
WHERE students_Id IN (1, 2, 3, 4, 5);
```
![image](images/Screenshot%20(90).png)

3.#### Answer - Deleting Records

To delete the records of student IDs 6, 7, 8, 9, and 10 from the `students` table, you can use the `DELETE` statement as follows:

```sql
DELETE FROM students
WHERE students_Id IN (6, 7, 8, 9, 10);

![image](images/Screenshot%20(91).png)

4. Show the first Names and Grades of every student.

```
#### Answer - Showing First Names and Grades

To display the first names and grades of every student, you can use the following syntax:

```sql
SELECT first_name, passing_grade
FROM students;
```

![image](images/Screenshot%20(92).png)

5. Show the records for students with the following Grades only (Grades: A and B).

```
#### Answer - Showing Records for Grades A and B

To retrieve the records for students with grades A and B only, you can use the following syntax:

```sql
SELECT *
FROM students
WHERE passing_grade IN ('A', 'B');
```
![image](images/Screenshot%20(93).png)

 # SQL PROJECT DETAILS
``` For this project, you are going to demonstrate the knowledge of the following concepts in SQL;
## 1.	DATABASE DESIGN
Create an EMPLOYEES_INFORMATION database 
Create 3 tables in this database: Employees, Department and Salary
Insert the following information into the tables specified:
```
### a.	EMPLOYEES;
```
INSERT INTO Employees (employee_id, name, email, phone_number, hire_date, department_id)
VALUES
  (1, 'John Smith', 'john.smith@example.com', '555-1234', '2021-07-15', 1),
  (2, 'Jane Doe', 'jane.doe@example.com', '555-5678', '2022-02-28', 1),
  (3, 'Michael Johnson', 'michael.johnson@example.com', '555-9012', '2021-11-10', 2),
  (4, 'Emily Davis', 'emily.davis@example.com', '555-3456', '2023-01-07', 3),
  (5, 'Daniel Brown', 'daniel.brown@example.com', '555-7890', '2022-09-22', 1),
  (6, 'Sophia Wilson', 'sophia.wilson@example.com', '555-2345', '2021-06-18', 2),
  (7, 'Oliver Taylor', 'oliver.taylor@example.com', '555-6789', '2022-05-11', 2),
  (8, 'Isabella Anderson', 'isabella.anderson@example.com', '555-0123', '2021-09-03', 3),
  (9, 'James Martinez', 'james.martinez@example.com', '555-4567', '2021-08-29', 4),
  (10, 'Mia Johnson', 'mia.johnson@example.com', '555-8901', '2023-03-14', 1),
  (11, 'Alexander Davis', 'alexander.davis@example.com', '555-2345', '2022-11-19', 2),
  (12, 'Sofia Thompson', 'sofia.thompson@example.com', '555-6789', '2023-02-08', 3),
  (13, 'Emma Moore', 'emma.moore@example.com', '555-0123', '2021-10-25', 4),
  (14, 'Benjamin Lee', 'benjamin.lee@example.com', '555-4567', '2022-12-30', 1),
  (15, 'Ava Hill', 'ava.hill@example.com', '555-8901', '2022-08-02', 2),
  (16, 'William Walker', 'william.walker@example.com', '555-2345', '2021-12-17', 3),
  (17, 'Charlotte Hernandez', 'charlotte.hernandez@example.com', '555-6789', '2023-01-20', 4),
  (18, 'Henry Gonzalez', 'henry.gonzalez@example.com', '555-0123', '2021-07-27', 1),
  (19, 'Luna Wilson', 'luna.wilson@example.com', '555-4567', '2022-05-06', 2),
  (20, 'Elijah Clark', 'elijah.clark@example.com', '555-8901', '2021-11-30', 3),
  (21, 'Scarlett Moore', 'scarlett.moore@example.com', '555-2345', '2022-04-21', 4),
  (
  22, 'Lucas Baker', 'lucas.baker@example.com', '555-6789', '2023-03-09', 1),
  (23, 'Mila Scott', 'mila.scott@example.com', '555-0123', '2022-01-13', 2),
  (24, 'Jackson Green', 'jackson.green@example.com', '555-4567', '2021-10-09', 3),
  (25, 'Penelope Adams', 'penelope.adams@example.com', '555-8901', '2023-02-05', 4),
  (26, 'Gabriel Hall', 'gabriel.hall@example.com', '555-2345', '2022-09-18', 1),
  (27, 'Aria Mitchell', 'aria.mitchell@example.com', '555-6789', '2021-06-24', 2),
  (28, 'Carter Perez', 'carter.perez@example.com', '555-0123', '2023-03-17', 3),
  (29, 'Madison Wright', 'madison.wright@example.com', '555-4567', '2022-05-22', 4),
  (30, 'Leo King', 'leo.king@example.com', '555-8901', '2021-11-25', 1),
  (31, 'Layla Lopez', 'layla.lopez@example.com', '555-2345', '2022-08-08', 2),
  (32, 'Jack Young', 'jack.young@example.com', '555-6789', '2021-09-12', 3),
  (33, 'Victoria Turner', 'victoria.turner@example.com', '555-0123', '2022-04-28', 4),
  (34, 'Josiah Morgan', 'josiah.morgan@example.com', '555-4567', '2022-10-16', 1),
  (35, 'Nora Lewis', 'nora.lewis@example.com', '555-8901', '2021-07-02', 2),
  (36, 'Ethan Carter', 'ethan.carter@example.com', '555-2345', '2022-11-14', 3),
  (37, 'Hannah Hall', 'hannah.hall@example.com', '555-6789', '2022-01-07', 4),
  (38, 'Samuel Perez', 'samuel.perez@example.com', '555-0123', '2021-08-18', 1),
  (39, 'Grace Wright', 'grace.wright@example.com', '555-4567', '2022-03-05', 2),
  (40, 'Wyatt King', 'wyatt.king@example.com', '555-8901', '2022-09-26', 3),
  (41, 'Evelyn Lopez', 'evelyn.lopez@example.com', '555-2345', '2022-06-12', 4),
  (42, 'Sebastian Young', 'sebastian.young@example.com', '555-6789', '2023-04-29', 1),
  (43, 'Addison Turner', 'addison.turner@example.com', '555-0123', '2021-12-24', 2),
  (44, 'Joseph Morgan', 'joseph.morgan@example.com', '555-4567', '2023-02-19', 3),
  (45, 'Avery Lewis', 'avery.lewis@example.com', '555-8901', '2021-10-14', 4),
  (46, 'Levi Carter', 'levi.carter@example.com', '555-2345', '2022-07-27', 1),
  (47, 'Aubrey Hall', 'aubrey.hall@example.com', '555-6789', '2021-12-08', 2),
  (48, 'Elizabeth Perez', 'elizabeth.perez@example.com', '555-0123', '2022-08-23', 3),
  (49, 'Owen Wright', 'owen.wright@example.com', '555-4567', '2021-07-17', 4),
  (50, 'Ryan King', 'ryan.king@example.com', '555-8901', '2023-03-20', 1),
  (51, 'Scarlett Lopez', 'scarlett.lopez@example.com', '555-2345', '2021-10-24', 2),
  (52, 'Liam Young', 'liam.young@example.com', '555-6789', '2021-09-05', 3),
  (53, 'Ella Turner', 'ella.turner@example.com', '555-0123', '2023-01-27', 4),
  (54, 'Noah Morgan', 'noah.morgan@example.com', '555-4567', '2022-03-13', 1),
  (55, 'Chloe Lewis', 'chloe.lewis@example.com', '555-8901', '2022-12-07', 2),
  (56, 'Mason Carter', 'mason.carter@example.com', '555-2345', '2023-03-03', 3),
  (57, 'Lucy Hall', 'lucy.hall@example.com', '555-6789', '2021-12-30', 4),
  (58, 'Logan Perez', 'logan.perez@example.com', '555-0123', '2022-06-23', 1),
  (59, 'Harper Wright', 'harper.wright@example.com', '555-4567', '2021-07-20', 2),
  (60, 'Evelyn King', 'evelyn.king@example.com', '555-8901', '2022-10-30', 3),
  (61, 'Oliver Lopez', 'oliver.lopez@example.com', '555-2345', '2023-01-15', 4),
  (62, 'Amelia Young', 'amelia.young@example.com', '555-6789', '2021-11-28', 1),
  (63, 'Mia Turner', 'mia.turner@example.com', '555-0123', '2022-09-08', 2),
  (64, 'Sebastian Morgan', 'sebastian.morgan@example.com', '555-4567', '2021-09-02', 3),
  (65, 'Charlotte Lewis', 'charlotte.lewis@example.com', '555-8901', '2023-02-05', 4),
  (66, 'Henry Carter', 'henry.carter@example.com', '555-2345', '2021-08-10', 1),
  (67, 'Luna Hall', 'luna.hall@example.com', '555-6789', '2022-07-23', 2),
  (68, 'Elijah Perez', 'elijah.perez@example.com', '555-0123', '2022-04-18', 3),
  (69, 'Stella Wright', 'stella.wright@example.com', '555-4567', '2021-10-05', 4),
  (70, 'Samuel King', 'samuel.king@example.com', '555-8901', '2022-11-27', 1),
  (71, 'Hazel Lopez', 'hazel.lopez@example.com', '555-2345', '2022-08-13', 2),
  (72, 'Aiden Young', 'aiden.young@example.com', '555-6789', '2021-07-28', 3),
  (73, 'Lucy Turner', 'lucy.turner@example.com', '555-0123', '2023-01-19', 4),
  (74, 'Benjamin Morgan', 'benjamin.morgan@example.com', '555-4567', '2022-03-08', 1),
  (75, 'Nora Lewis', 'nora.lewis@example.com', '555-8901', '2021-07-02', 2),
  (76, 'Ethan Carter', 'ethan.carter@example.com', '555-2345', '2022-11-14', 3),
  (77, 'Hannah Hall', 'hannah.hall@example.com', '555-6789', '2022-01-07', 4),
  (78, 'Samuel Perez', 'samuel.perez@example.com', '555-0123', '2021-08-18', 1),
  (79, 'Grace Wright', 'grace.wright@example.com', '555-4567', '2022-03-05', 2),
  (80, 'Wyatt King', 'wyatt.king@example.com', '555-8901', '2022-09-26', 3),
  (81, 'Evelyn Lopez', 'evelyn.lopez@example.com', '555-2345', '2022-06-12', 4),
  (82, 'Sebastian Young', 'sebastian.young@example.com', '555-6789', '2023-04-29', 1),
  (83, 'Addison Turner', 'addison.turner@example.com', '555-0123', '2021-12-24', 2),
  (84, 'Joseph Morgan', 'joseph.morgan@example.com', '555-4567', '2023-02-19', 3),
  (85, 'Avery Lewis', 'avery.lewis@example.com', '555-8901', '2021-10-14', 4),
  (86, 'Levi Carter', 'levi.carter@example.com', '555-2345', '2022-07-27', 1),
  (87, 'Aubrey Hall', 'aubrey.hall@example.com', '555-6789', '2021-12-08', 2),
  (88, 'Elizabeth Perez', 'elizabeth.perez@example.com', '555-0123', '2022-08-23', 3),
  (89, 'Owen Wright', 'owen.wright@example.com', '555-4567', '2021-07-17', 4),
  (90, 'Ryan King', 'ryan.king@example.com', '555-8901', '2023-03-20', 1),
  (91, 'Scarlett Lopez', 'scarlett.lopez@example.com', '555-2345', '2021-10-24', 2),
  (92, 'Liam Young', 'liam.young@example.com', '555-6789', '2021-09-05', 3),
  (93, 'Ella Turner', 'ella.turner@example.com', '555-0123', '2023-01-27', 4),
  (94, 'Noah Morgan', 'noah.morgan@example.com', '555-4567', '2022-03-13', 1),
  (95, 'Chloe Lewis', 'chloe.lewis@example.com', '555-8901', '2022-12-07', 2),
  (96, 'Mason Carter', 'mason.carter@example.com', '555-2345', '2023-03-03', 3),
  (97, 'Lucy Hall', 'lucy.hall@example.com', '555-6789', '2021-12-30', 4),
  (98, 'Logan Perez', 'logan.perez@example.com', '555-0123', '2022-06-23', 1),
  (99, 'Harper Wright', 'harper.wright@example.com', '555-4567', '2021-07-20', 2),
  (100, 'Evelyn King', 'evelyn.king@example.com', '555-8901', '2022-10-30', 3);
```

### b.	DEPARTMENT
```
INSERT INTO departments (dept_id, dept_name, dept_head)
VALUES
  (1, 'Sales', 'John Smith'),
  (2, 'Marketing', 'Jane Johnson'),
  (3, 'Human Resources', 'Michael Davis'),
  (4, 'Finance', 'Sarah Thompson');
```
### c.	SALARY
```
INSERT INTO salaries (salary_id, emp_id, salary_amount, start_date, end_date)
VALUES
  (1, 14, 55000.00, '2021-05-10', '2021-12-31'),
  (2, 32, 65000.00, '2022-01-01', '2022-12-31'),
  (3, 44, 60000.00, '2021-08-20', '2022-07-31'),
  (4, 49, 75000.00, '2022-11-05', '2022-12-31'),
  (5, 57, 58000.00, '2021-06-15', '2021-12-31'),
  (6, 59, 68000.00, '2022-01-01', '2022-12-31'),
  (7, 62, 62000.00, '2021-09-15', '2022-12-31'),
  (8, 68, 70000.00, '2022-11-05', '2022-12-31'),
  (9, 70, 56000.00, '2021-07-15', '2021-12-31'),
  (10, 72, 67000.00, '2022-01-01', '2022-12-31'),
  (11, 74, 59000.00, '2021-08-20', '2022-07-31'),
  (12, 76, 72000.00, '2022-11-05', '2022-12-31'),
  (13, 78, 61000.00, '2021-09-15', '2022-12-31'),
  (14, 83, 69000.00, '2022-01-01', '2022-12-31'),
  (15, 86, 54000.00, '2021-07-15', '2021-12-31'),
  (16, 88, 64000.00, '2022-01-01', '2022-12-31'),
  (17, 90, 60000.00, '2021-09-15', '2022-12-31'),
  (18, 94, 73000.00, '2022-11-05', '2022-12-31'),
  (19, 96, 57000.00, '2021-08-20', '2022-07-31'),
  (20, 98, 68000.00, '2022-01-01', '2022-12-31'),
  (21, 3, 56000.00, '2021-07-15', '2021-12-31'),
  (22, 4, 67000.00, '2022-01-01', '2022-12-31'),
  (23, 7, 59000.00, '2021-08-20', '2022-07-31'),
  (24, 8, 72000.00, '2022-11-05', '2022-12-31'),
  (25, 12, 61000.00, '2021-09-15', '2022-12-31'),
  (26, 17, 69000.00, '2022-01-01', '2022-12-31'),
  (27, 22, 54000.00, '2021-07-15', '2021-12-31'),
  (28, 23, 64000.00, '2022-01-01', '2022-12-31'),
  (29, 28, 60000.00, '2021-09-15', '2022-12-31'),
  (30, 29, 73000.00, '2022-11-05', '2022-12-31'),
  (31, 31, 57000.00, '2021-08-20', '2022-07-31'),
  (32, 33, 68000.00, '2022-01-01', '2022-12-31'),
  (33, 34, 55000.00, '2021-05-10', '2021-12-31'),
  (34, 35, 65000.00, '2022-01-01', '2022-12-31'),
  (35, 37, 60000.00, '2021-08-20', '2022-07-31'),
  (36, 38, 75000.00, '2022-11-05', '2022-12-31'),
  (37, 39, 58000.00, '2021-06-15', '2021-12-31'),
  (38, 40, 68000.00, '2022-01-01', '2022-12-31'),
  (39, 41, 62000.00, '2021-09-15', '2022-12-31'),
  (40, 42, 70000.00, '2022-11-05', '2022-12-31'),
  (41, 43, 56000.00, '2021-07-15', '2021-12-31'),
  (42, 46, 67000.00, '2022-01-01', '2022-12-31'),
  (43, 48, 59000.00, '2021-08-20', '2022-07-31'),
  (44, 52, 72000.00, '2022-11-05', '2022-12-31'),
  (45, 55, 61000.00, '2021-09-15', '2022-12-31'),
  (46, 58, 69000.00, '2022-01-01', '2022-12-31'),
  (47, 60, 54000.00, '2021-07-15', '2021-12-31'),
  (48, 63, 64000.00, '2022-01-01', '2022-12-31'),
  (49, 64, 60000.00, '2021-09-15', '2022-12-31'),
  (50, 65, 73000.00, '2022-11-05', '2022-12-31'),
  (51, 67, 57000.00, '2021-08-20', '2022-07-31'),
  (52, 69, 68000.00, '2022-01-01', '2022-12-31'),
  (53, 71, 55000.00, '2021-05-10', '2021-12-31'),
  (54, 73, 65000.00, '2022-01-01', '2022-12-31'),
  (55, 75, 60000.00, '2021-08-20', '2022-07-31'),
  (56, 77, 75000.00, '2022-11-05', '2022-12-31'),
  (57, 79, 58000.00, '2021-06-15', '2021-12-31'),
  (58, 80, 68000.00, '2022-01-01', '2022-12-31'),
  (59, 81, 62000.00, '2021-09-15', '2022-12-31'),
  (60, 82, 70000.00, '2022-11-05', '2022-12-31'),
  (61, 84, 56000.00, '2021-07-15', '2021-12-31'),
  (62, 85, 67000.00, '2022-01-01', '2022-12-31'),
  (63, 87, 59000.00, '2021-08-20', '2022-07-31'),
  (64, 89, 72000.00, '2022-11-05', '2022-12-31'),
  (65, 91, 61000.00, '2021-09-15', '2022-12-31');

```

### 2.	DATA UPDATE
a.	Delete the start_date and end_date columns in the SALARY table
b.	Where the employee_id is 9, 10 and 11, update the department_ids to ‘4’ 

### 3.	JOINS
Determine which JOIN type is suitable for manipulating the data you have added to the EMPLOYEES_INFORMATION database

### 4.	AGGREGATION
a.	Calculate the total number of employees in this company
b.	How many employees were hired in the year 2023?
c.	What is the average salary for employees in each department?
d.	How many employees are there in each department?
e.	Who are the department heads and their corresponding departments?
f.	What is the highest salary earned by an employee?
g.	What is the total salary expense for each department?
h.	How many employees were hired each year?

### 5.	DATA QUERYING
Think of additional questions and provide answers to them. Use your knowledge of CTEs, Subqueries, Aggregate functions e.t.c to flex your overall knowledge of SQL.

5.	Which employees have salaries higher than the average salary in their respective departments?
6.	What is the highest salary in each department, and which employees earn that salary?
***
# ANSWER

 ### Question 1
 ```
CREATE DATABASE EMPLOYEES_INFORMATION ;
USE EMPLOYEES_INFORMATION ;
```
***
### Question 1a
```
CREATE TABLE EMPLOYEE(
  employee_id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL,
  phone_number VARCHAR(20),
  hire_date DATE NOT NULL,
  department_id INT
);
INSERT INTO EMPLOYEE (employee_id, name, email, phone_number, hire_date, department_id)
VALUES
  (1, 'John Smith', 'john.smith@example.com', '555-1234', '2021-07-15', 1),
  (2, 'Jane Doe', 'jane.doe@example.com', '555-5678', '2022-02-28', 1),
  (3, 'Michael Johnson', 'michael.johnson@example.com', '555-9012', '2021-11-10', 2),
  (4, 'Emily Davis', 'emily.davis@example.com', '555-3456', '2023-01-07', 3),
  (5, 'Daniel Brown', 'daniel.brown@example.com', '555-7890', '2022-09-22', 1),
  (6, 'Sophia Wilson', 'sophia.wilson@example.com', '555-2345', '2021-06-18', 2),
  (7, 'Oliver Taylor', 'oliver.taylor@example.com', '555-6789', '2022-05-11', 2),
  (8, 'Isabella Anderson', 'isabella.anderson@example.com', '555-0123', '2021-09-03', 3),
  (9, 'James Martinez', 'james.martinez@example.com', '555-4567', '2021-08-29', 4),
  (10, 'Mia Johnson', 'mia.johnson@example.com', '555-8901', '2023-03-14', 1),
  (11, 'Alexander Davis', 'alexander.davis@example.com', '555-2345', '2022-11-19', 2),
  (12, 'Sofia Thompson', 'sofia.thompson@example.com', '555-6789', '2023-02-08', 3),
  (13, 'Emma Moore', 'emma.moore@example.com', '555-0123', '2021-10-25', 4),
  (14, 'Benjamin Lee', 'benjamin.lee@example.com', '555-4567', '2022-12-30', 1),
  (15, 'Ava Hill', 'ava.hill@example.com', '555-8901', '2022-08-02', 2),
  (16, 'William Walker', 'william.walker@example.com', '555-2345', '2021-12-17', 3),
  (17, 'Charlotte Hernandez', 'charlotte.hernandez@example.com', '555-6789', '2023-01-20', 4),
  (18, 'Henry Gonzalez', 'henry.gonzalez@example.com', '555-0123', '2021-07-27', 1),
  (19, 'Luna Wilson', 'luna.wilson@example.com', '555-4567', '2022-05-06', 2),
  (20, 'Elijah Clark', 'elijah.clark@example.com', '555-8901', '2021-11-30', 3),
  (21, 'Scarlett Moore', 'scarlett.moore@example.com', '555-2345', '2022-04-21', 4),
  (22, 'Lucas Baker', 'lucas.baker@example.com', '555-6789', '2023-03-09', 1),
  (23, 'Mila Scott', 'mila.scott@example.com', '555-0123', '2022-01-13', 2),
  (24, 'Jackson Green', 'jackson.green@example.com', '555-4567', '2021-10-09', 3),
  (25, 'Penelope Adams', 'penelope.adams@example.com', '555-8901', '2023-02-05', 4),
  (26, 'Gabriel Hall', 'gabriel.hall@example.com', '555-2345', '2022-09-18', 1),
  (27, 'Aria Mitchell', 'aria.mitchell@example.com', '555-6789', '2021-06-24', 2),
  (28, 'Carter Perez', 'carter.perez@example.com', '555-0123', '2023-03-17', 3),
  (29, 'Madison Wright', 'madison.wright@example.com', '555-4567', '2022-05-22', 4),
  (30, 'Leo King', 'leo.king@example.com', '555-8901', '2021-11-25', 1),
  (31, 'Layla Lopez', 'layla.lopez@example.com', '555-2345', '2022-08-08', 2),
  (32, 'Jack Young', 'jack.young@example.com', '555-6789', '2021-09-12', 3),
  (33, 'Victoria Turner', 'victoria.turner@example.com', '555-0123', '2022-04-28', 4),
  (34, 'Josiah Morgan', 'josiah.morgan@example.com', '555-4567', '2022-10-16', 1),
  (35, 'Nora Lewis', 'nora.lewis@example.com', '555-8901', '2021-07-02', 2),
  (36, 'Ethan Carter', 'ethan.carter@example.com', '555-2345', '2022-11-14', 3),
  (37, 'Hannah Hall', 'hannah.hall@example.com', '555-6789', '2022-01-07', 4),
  (38, 'Samuel Perez', 'samuel.perez@example.com', '555-0123', '2021-08-18', 1),
  (39, 'Grace Wright', 'grace.wright@example.com', '555-4567', '2022-03-05', 2),
  (40, 'Wyatt King', 'wyatt.king@example.com', '555-8901', '2022-09-26', 3),
  (41, 'Evelyn Lopez', 'evelyn.lopez@example.com', '555-2345', '2022-06-12', 4),
  (42, 'Sebastian Young', 'sebastian.young@example.com', '555-6789', '2023-04-29', 1),
  (43, 'Addison Turner', 'addison.turner@example.com', '555-0123', '2021-12-24', 2),
  (44, 'Joseph Morgan', 'joseph.morgan@example.com', '555-4567', '2023-02-19', 3),
  (45, 'Avery Lewis', 'avery.lewis@example.com', '555-8901', '2021-10-14', 4),
  (46, 'Levi Carter', 'levi.carter@example.com', '555-2345', '2022-07-27', 1),
  (47, 'Aubrey Hall', 'aubrey.hall@example.com', '555-6789', '2021-12-08', 2),
  (48, 'Elizabeth Perez', 'elizabeth.perez@example.com', '555-0123', '2022-08-23', 3),
  (49, 'Owen Wright', 'owen.wright@example.com', '555-4567', '2021-07-17', 4),
  (50, 'Ryan King', 'ryan.king@example.com', '555-8901', '2023-03-20', 1),
  (51, 'Scarlett Lopez', 'scarlett.lopez@example.com', '555-2345', '2021-10-24', 2),
  (52, 'Liam Young', 'liam.young@example.com', '555-6789', '2021-09-05', 3),
  (53, 'Ella Turner', 'ella.turner@example.com', '555-0123', '2023-01-27', 4),
  (54, 'Noah Morgan', 'noah.morgan@example.com', '555-4567', '2022-03-13', 1),
  (55, 'Chloe Lewis', 'chloe.lewis@example.com', '555-8901', '2022-12-07', 2),
  (56, 'Mason Carter', 'mason.carter@example.com', '555-2345', '2023-03-03', 3),
  (57, 'Lucy Hall', 'lucy.hall@example.com', '555-6789', '2021-12-30', 4),
  (58, 'Logan Perez', 'logan.perez@example.com', '555-0123', '2022-06-23', 1),
  (59, 'Harper Wright', 'harper.wright@example.com', '555-4567', '2021-07-20', 2),
  (60, 'Evelyn King', 'evelyn.king@example.com', '555-8901', '2022-10-30', 3),
  (61, 'Oliver Lopez', 'oliver.lopez@example.com', '555-2345', '2023-01-15', 4),
  (62, 'Amelia Young', 'amelia.young@example.com', '555-6789', '2021-11-28', 1),
  (63, 'Mia Turner', 'mia.turner@example.com', '555-0123', '2022-09-08', 2),
  (64, 'Sebastian Morgan', 'sebastian.morgan@example.com', '555-4567', '2021-09-02', 3),
  (65, 'Charlotte Lewis', 'charlotte.lewis@example.com', '555-8901', '2023-02-05', 4),
  (66, 'Henry Carter', 'henry.carter@example.com', '555-2345', '2021-08-10', 1),
  (67, 'Luna Hall', 'luna.hall@example.com', '555-6789', '2022-07-23', 2),
  (68, 'Elijah Perez', 'elijah.perez@example.com', '555-0123', '2022-04-18', 3),
  (69, 'Stella Wright', 'stella.wright@example.com', '555-4567', '2021-10-05', 4),
  (70, 'Samuel King', 'samuel.king@example.com', '555-8901', '2022-11-27', 1),
  (71, 'Hazel Lopez', 'hazel.lopez@example.com', '555-2345', '2022-08-13', 2),
  (72, 'Aiden Young', 'aiden.young@example.com', '555-6789', '2021-07-28', 3),
  (73, 'Lucy Turner', 'lucy.turner@example.com', '555-0123', '2023-01-19', 4),
  (74, 'Benjamin Morgan', 'benjamin.morgan@example.com', '555-4567', '2022-03-08', 1),
  (75, 'Nora Lewis', 'nora.lewis@example.com', '555-8901', '2021-07-02', 2),
  (76, 'Ethan Carter', 'ethan.carter@example.com', '555-2345', '2022-11-14', 3),
  (77, 'Hannah Hall', 'hannah.hall@example.com', '555-6789', '2022-01-07', 4),
  (78, 'Samuel Perez', 'samuel.perez@example.com', '555-0123', '2021-08-18', 1),
  (79, 'Grace Wright', 'grace.wright@example.com', '555-4567', '2022-03-05', 2),
  (80, 'Wyatt King', 'wyatt.king@example.com', '555-8901', '2022-09-26', 3),
  (81, 'Evelyn Lopez', 'evelyn.lopez@example.com', '555-2345', '2022-06-12', 4),
  (82, 'Sebastian Young', 'sebastian.young@example.com', '555-6789', '2023-04-29', 1),
  (83, 'Addison Turner', 'addison.turner@example.com', '555-0123', '2021-12-24', 2),
  (84, 'Joseph Morgan', 'joseph.morgan@example.com', '555-4567', '2023-02-19', 3),
  (85, 'Avery Lewis', 'avery.lewis@example.com', '555-8901', '2021-10-14', 4),
  (86, 'Levi Carter', 'levi.carter@example.com', '555-2345', '2022-07-27', 1),
  (87, 'Aubrey Hall', 'aubrey.hall@example.com', '555-6789', '2021-12-08', 2),
  (88, 'Elizabeth Perez', 'elizabeth.perez@example.com', '555-0123', '2022-08-23', 3),
  (89, 'Owen Wright', 'owen.wright@example.com', '555-4567', '2021-07-17', 4),
  (90, 'Ryan King', 'ryan.king@example.com', '555-8901', '2023-03-20', 1),
  (91, 'Scarlett Lopez', 'scarlett.lopez@example.com', '555-2345', '2021-10-24', 2),
  (92, 'Liam Young', 'liam.young@example.com', '555-6789', '2021-09-05', 3),
  (93, 'Ella Turner', 'ella.turner@example.com', '555-0123', '2023-01-27', 4),
  (94, 'Noah Morgan', 'noah.morgan@example.com', '555-4567', '2022-03-13', 1),
  (95, 'Chloe Lewis', 'chloe.lewis@example.com', '555-8901', '2022-12-07', 2),
  (96, 'Mason Carter', 'mason.carter@example.com', '555-2345', '2023-03-03', 3),
  (97, 'Lucy Hall', 'lucy.hall@example.com', '555-6789', '2021-12-30', 4),
  (98, 'Logan Perez', 'logan.perez@example.com', '555-0123', '2022-06-23', 1),
  (99, 'Harper Wright', 'harper.wright@example.com', '555-4567', '2021-07-20', 2),
  (100, 'Evelyn King', 'evelyn.king@example.com', '555-8901', '2022-10-30', 3);
  ```

![image](images/Screenshot%20(115).png)

***
### Question 1b
```
CREATE TABLE DEPARTMENT(
  dept_id INT AUTO_INCREMENT PRIMARY KEY,
  dept_name VARCHAR(255) NOT NULL,
  dept_head VARCHAR(255) NOT NULL
);
INSERT INTO DEPARTMENT (dept_id, dept_name, dept_head)
VALUES 
  (1, 'Sales', 'John Smith'),
  (2, 'Marketing', 'Jane Johnson'),
  (3, 'Human Resources', 'Michael Davis'),
  (4, 'Finance', 'Sarah Thompson');
  ```
![image](images/Screenshot%20(109).png)

***
### Question 1c
```
CREATE TABLE SALARY(
  salary_id INT AUTO_INCREMENT PRIMARY KEY,
  emp_id INT,
  salary_amount DECIMAL (10,2) NOT NULL,
  start_date DATE NOT NULL,
  end_date DATE NOT NULL
);
INSERT INTO SALARY (salary_id, emp_id, salary_amount, start_date, end_date)
VALUES
  (1, 14, 55000.00, '2021-05-10', '2021-12-31'),
  (2, 32, 65000.00, '2022-01-01', '2022-12-31'),
  (3, 44, 60000.00, '2021-08-20', '2022-07-31'),
  (4, 49, 75000.00, '2022-11-05', '2022-12-31'),
  (5, 57, 58000.00, '2021-06-15', '2021-12-31'),
  (6, 59, 68000.00, '2022-01-01', '2022-12-31'),
  (7, 62, 62000.00, '2021-09-15', '2022-12-31'),
(8, 68, 70000.00, '2022-11-05', '2022-12-31'),
  (9, 70, 56000.00, '2021-07-15', '2021-12-31'),
  (10, 72, 67000.00, '2022-01-01', '2022-12-31'),
  (11, 74, 59000.00, '2021-08-20', '2022-07-31'),
  (12, 76, 72000.00, '2022-11-05', '2022-12-31'),
  (13, 78, 61000.00, '2021-09-15', '2022-12-31'),
  (14, 83, 69000.00, '2022-01-01', '2022-12-31'),
  (15, 86, 54000.00, '2021-07-15', '2021-12-31'),
  (16, 88, 64000.00, '2022-01-01', '2022-12-31'),
  (17, 90, 60000.00, '2021-09-15', '2022-12-31'),
  (18, 94, 73000.00, '2022-11-05', '2022-12-31'),
  (19, 96, 57000.00, '2021-08-20', '2022-07-31'),
  (20, 98, 68000.00, '2022-01-01', '2022-12-31'),
  (21, 3, 56000.00, '2021-07-15', '2021-12-31'),
  (22, 4, 67000.00, '2022-01-01', '2022-12-31'),
  (23, 7, 59000.00, '2021-08-20', '2022-07-31'),
  (24, 8, 72000.00, '2022-11-05', '2022-12-31'),
  (25, 12, 61000.00, '2021-09-15', '2022-12-31'),
  (26, 17, 69000.00, '2022-01-01', '2022-12-31'),
  (27, 22, 54000.00, '2021-07-15', '2021-12-31'),
  (28, 23, 64000.00, '2022-01-01', '2022-12-31'),
  (29, 28, 60000.00, '2021-09-15', '2022-12-31'),
  (30, 29, 73000.00, '2022-11-05', '2022-12-31'),
  (31, 31, 57000.00, '2021-08-20', '2022-07-31'),
  (32, 33, 68000.00, '2022-01-01', '2022-12-31'),
  (33, 34, 55000.00, '2021-05-10', '2021-12-31'),
  (34, 35, 65000.00, '2022-01-01', '2022-12-31'),
  (35, 37, 60000.00, '2021-08-20', '2022-07-31'),
  (36, 38, 75000.00, '2022-11-05', '2022-12-31'),
  (37, 39, 58000.00, '2021-06-15', '2021-12-31'),
  (38, 40, 68000.00, '2022-01-01', '2022-12-31'),
  (39, 41, 62000.00, '2021-09-15', '2022-12-31'),
  (40, 42, 70000.00, '2022-11-05', '2022-12-31'),
  (41, 43, 56000.00, '2021-07-15', '2021-12-31'),
  (42, 46, 67000.00, '2022-01-01', '2022-12-31'),
  (43, 48, 59000.00, '2021-08-20', '2022-07-31'),
  (44, 52, 72000.00, '2022-11-05', '2022-12-31'),
  (45, 55, 61000.00, '2021-09-15', '2022-12-31'),
  (46, 58, 69000.00, '2022-01-01', '2022-12-31'),
  (47, 60, 54000.00, '2021-07-15', '2021-12-31'),
  (48, 63, 64000.00, '2022-01-01', '2022-12-31'),
  (49, 64, 60000.00, '2021-09-15', '2022-12-31'),
  (50, 65, 73000.00, '2022-11-05', '2022-12-31'),
  (51, 67, 57000.00, '2021-08-20', '2022-07-31'),
  (52, 69, 68000.00, '2022-01-01', '2022-12-31'),
  (53, 71, 55000.00, '2021-05-10', '2021-12-31'),
  (54, 73, 65000.00, '2022-01-01', '2022-12-31'),
  (55, 75, 60000.00, '2021-08-20', '2022-07-31'),
  (56, 77, 75000.00, '2022-11-05', '2022-12-31'),
  (57, 79, 58000.00, '2021-06-15', '2021-12-31'),
  (58, 80, 68000.00, '2022-01-01', '2022-12-31'),
  (59, 81, 62000.00, '2021-09-15', '2022-12-31'),
  (60, 82, 70000.00, '2022-11-05', '2022-12-31'),
  (61, 84, 56000.00, '2021-07-15', '2021-12-31'),
  (62, 85, 67000.00, '2022-01-01', '2022-12-31'),
  (63, 87, 59000.00, '2021-08-20', '2022-07-31'),
  (64, 89, 72000.00, '2022-11-05', '2022-12-31'),
  (65, 91, 61000.00, '2021-09-15', '2022-12-31');
  ```
  ***
### Question 2
**S2.	DATA UPDATE
a.	Delete the start_date and end_date columns in the SALARY table
b.	Where the employee_id is 9, 10 and 11, update the department_ids to ‘4’ */ **
```
ALTER TABLE SALARY
DROP COLUMN start_date ,
DROP COLUMN  end_date ;
SELECT * FROM SALARY ;
UPDATE EMPLOYEE
SET department_id = '4'
WHERE employee_id IN (9, 10, 11);
```
![image](images/Screenshot%20(110).png)

***
### Question 3.	JOINS
Determine which JOIN type is suitable for manipulating the data you have added to the EMPLOYEES_INFORMATION database
```
SELECT *
FROM EMPLOYEE
INNER JOIN SALARY ON EMPLOYEE.employee_id = SALARY.emp_id;
```
![image](images/Screenshot%20(94).png)

***
### Question 4
### 4a.	Calculate the total number of employees in this company
```
SELECT COUNT(*) AS total_employees
FROM EMPLOYEE;
```
![image](images/Screenshot%20(111).png)

***
 ### 4b.	How many employees were hired in the year 2023? 
 ```
SELECT COUNT(*) AS employees_hired_2023
FROM EMPLOYEE
WHERE YEAR(hire_date) = 2023;
```
![image](images/Screenshot%20(96).png)

***
 ### 4c.What is the average salary for employees in each department? 
 ```
SELECT EMPLOYEE.department_id, DEPARTMENT.dept_name, AVG(SALARY.salary_amount) AS average_salary
FROM EMPLOYEE
JOIN Department ON EMPLOYEE.department_id = Department.dept_id
JOIN SALARY ON EMPLOYEE.EMPLOYEE_id = SALARY.emp_id
GROUP BY EMPLOYEE.department_id, DEPARTMENT.dept_name;
```
![image](images/Screenshot%20(114).png)

***
### 4d.	How many employees are there in each department
```
SELECT DEPARTMENT.dept_id, DEPARTMENT.dept_name, COUNT(EMPLOYEE.employee_id) AS employee_count
FROM DEPARTMENT
LEFT JOIN EMPLOYEE ON DEPARTMENT.dept_id = EMPLOYEE.department_id
GROUP BY DEPARTMENT.dept_id, DEPARTMENT.dept_name;
```
![image](images/Screenshot%20(112).png)

***
### 4e.	Who are the department heads and their corresponding departments 
```
SELECT dept_head, dept_name
FROM DEPARTMENT;
```
![image](images/Screenshot%20(109).png)

***
### 4f.	What is the highest salary earned by an employee?
```
SELECT MAX(salary_amount) AS highest_salary
FROM SALARY;
```
![image](images/Screenshot%20(113).png)

***
### 4g.	What is the total salary expense for each department?
```
SELECT EMPLOYEE.department_id, DEPARTMENT.dept_name, SUM(SALARY.salary_amount) AS total_salary_expense
FROM EMPLOYEE
JOIN DEPARTMENT ON EMPLOYEE.department_id = DEPARTMENT.dept_id
JOIN SALARY ON EMPLOYEE.employee_id = SALARY.emp_id
GROUP BY EMPLOYEE.department_id, DEPARTMENT.dept_name;
```
![image](images/Screenshot%20(102).png)

***
### 4h.	How many employees were hired each year?
```
SELECT YEAR(hire_date) AS hire_year, COUNT(*) AS employees_hired
FROM Employees
GROUP BY YEAR(hire_date);
```
images/Screenshot (103).png

***
### Question 5-DATA QUERRYING--
### 5a.	What is the highest salary in each department, and which employees earn that salary?
use employees_information;
```
WITH avg_salaries AS (
    SELECT e.department_id, AVG(s.salary_amount) AS avg_salary
    FROM Employee e
    JOIN Salary s ON e.employee_id = s.emp_id
    GROUP BY e.department_id 
)
SELECT e.employee_id, e.name, s.salary_amount, e.department_id
FROM Employee e
JOIN Salary s ON e.employee_id = s.emp_id
JOIN avg_salaries a ON e.department_id = a.department_id
WHERE s.salary_amount > a.avg_salary
ORDER BY e.department_id ASC;
```
![image](images/Screenshot%20(107).png)

***
### 5b. What is the highest salary in each department, and which employees earn that salary?
```
WITH max_salaries AS (
    SELECT e.department_id, MAX(s.salary_amount) AS max_salary
    FROM Employee e
    JOIN Salary s ON e.employee_id = s.emp_id
    GROUP BY e.department_id
)
SELECT e.employee_id, e.name, s.salary_amount, e.department_id
FROM Employee e
JOIN Salary s ON e.employee_id = s.emp_id
JOIN max_salaries m ON e.department_id = m.department_id AND s.salary_amount = m.max_salary
ORDER BY e.name ASC
```
![image](images/Screenshot%20(109).png)

***

