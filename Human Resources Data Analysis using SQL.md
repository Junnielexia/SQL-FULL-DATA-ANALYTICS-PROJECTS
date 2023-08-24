# Create Database

```
CREATE DATABASE projects;
```
# Import Data to SQL
Right click the table in the data base to import the human Resources Data
![Screenshot (241)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/cac05a90-1047-4118-b558-5fb0efdfc714)

# Visualize the Imported Data

```
USE projects;
SELECT * FROM hr;
```
![Screenshot (243)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/53f71aed-2547-444c-8706-13e19b1ff075)

# Data Cleaning

## ID COLUMN
**Renaming the ID column to Employee ID**
```
ALTER TABLE hr
CHANGE COLUMN ﻿id em﻿p_id varchar (20) NULL;
```
![Screenshot (244)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/ec29ff19-b5f7-46ba-941f-df3e3a315fdb)

## Check the Datatypes
```
DESCRIBE hr;
```
![Screenshot (245)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/1ce0a48d-b2ef-4838-89f7-77986890a931)

## Birthdate Column
**change Date type from text to standard date format**

```
SELECT birthdate From hr;
```
![Screenshot (246)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/79b8a0cd-9772-40bc-808a-80760e87b272)

**To update the table we must first of all bypass the security  using the code below**

```
SET Sql_safe_updates = 0;
```
**After that we can now update the birthdate table**

```
UPDATE hr
SET birthdate = CASE
WHEN  birthdate LIKE'%/%' THEN date_format(str_to_date(birthdate,'%m/%d/%Y'), '%Y-%m-%d')
WHEN  birthdate LIKE'%-%' THEN date_format(str_to_date(birthdate,'%m-%d-%Y'), '%Y-%m-%d')
 ELSE null
END;
```
![Screenshot (247)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/dfb23e4f-1a87-438c-87e7-52f47f838bc9)

**To change date type**

```
ALTER TABLE hr
MODIFY COLUMN birthdate DATE;
```

## HIRE Date

```
UPDATE hr
SET hire_date = CASE
WHEN  hire_date LIKE'%/%' THEN date_format(str_to_date(hire_date,'%m/%d/%Y'), '%Y-%m-%d')
WHEN  hire_date LIKE'%-%' THEN date_format(str_to_date(hire_date,'%m-%d-%Y'), '%Y-%m-%d')
 ELSE null
END;
SELECT hire_date From hr;
```
![Screenshot (248)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/2edc4302-191c-4b3d-9474-6f54ea78eb20)

**TO Alter the data type  i used the code below 
```
ALTER TABLE hr
MODIFY COLUMN hire_date DATE;
```

## Term Date Column
The term date column has a lot of empty column and thae available date also has timestamps which we wont be needing for the analysis.

![Screenshot (249)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/59356a89-8b51-44db-9c46-0de1d4d7b564)

```
UPDATE hr
SET termdate = date(str_to_date(termdate,'%Y-%m-%d %H:%i:%sUTC'))
WHERE true;
SET sql_mode='ALLOW_INVALID_DATES';
```
**TO Alter the data type  i used the code below 
```
ALTER TABLE hr
MODIFY COLUMN termdate DATE;
SELECT termdate From hr;
```
![Screenshot (250)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/8cd5f96a-d0d0-4a48-b53d-8e88418b9e7e)

VIEW ALL THE DATATYPE TO ENSURE THEY ALL NOW IN THERE CORRECT FORM

```
DESCRIBE hr;
```
![Screenshot (251)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/bc2cd8f3-cfc7-4485-a385-1579443dcb04)

# Create an AGE Column

```
ALTER TABLE hr ADD COLUMN age INT;
```
**Update the column with The Calculated Age and visualize**
```
UPDATE hr
SET age = timestampdiff(YEAR,birthdate,CURDATE());
SELECT birthdate,age FROM hr;
```
![Screenshot (252)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/f9b68cc5-c7c4-4008-806d-f812bb05c7ca)

**due to the presence of future date in the age column we have to re examine the column to fish out the invalid data.***

SELECT MIN AND MAX AGE
```
SELECT
MIN(age) AS youngest,
MAX(age) AS oldest
FROM hr;
```
![Screenshot (253)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/5fc33cde-6b68-4dff-a80c-2745cdbbde80)

LETs take alook at every age under 18
```
SELECT count(*) FROM hr WHERE age < 18;
```
![Screenshot (254)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/259cac12-77a3-4be5-9ca4-bb5e4af51042)

# Business Question

1.  What is the gender breakdown of employees in the country?
```
  SELECT gender, count(*) AS count
FROM hr
WHERE age >= 18 AND termdate = '0000-00-00'
```
![Screenshot (255)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/a43659b0-f753-4db1-ad58-b45f27af03ee)


2. What is the race/Ethnicity breakdown of employees in the company?

   ```
   SELECT race, COUNT(*) AS count
FROM hr
WHERE age >= 18 AND termdate = '0000-00-00'
GROUP BY race
ORDER BY count(*) DESC;
 ```
![Screenshot (257)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/e238fff9-b063-4c92-861a-d0416b382584)


3. What is the age distribution of remployees in the company

A. **OLD & YOUNG**
```
SELECT
MIN(age) AS youngest,
MAX(age) AS oldest
FROM hr
WHERE age >=18 AND termdate = '0000-00-00';
```
B. **AGE GROUP**
```
SELECT
 CASE
  WHEN age >= 18 AND age <= 24 THEN '18-24'
  WHEN age >= 25 AND age <= 34 THEN '25-34'
  WHEN age >= 35 AND age <= 44 THEN '35-44'
  WHEN age >= 45 AND age <= 54 THEN '35-54'
  WHEN age >= 55 AND age <= 64 THEN '55-64'
 ELSE '65+'
END AS age_group,
count(*) AS count
FROM hr
WHERE age >=18 AND termdate = '0000-00-00'
GROUP BY age_group
ORDER BY age_group;
```
![Screenshot (258)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/bd29e748-a17d-4a1f-b170-14845d9eb354)

C. - Gender Distribution within the different age group
```
SELECT
 CASE
  WHEN age >= 18 AND age <= 24 THEN '18-24'
  WHEN age >= 25 AND age <= 34 THEN '25-34'
  WHEN age >= 35 AND age <= 44 THEN '35-44'
  WHEN age >= 45 AND age <= 54 THEN '35-54'
  WHEN age >= 55 AND age <= 64 THEN '55-64'
 ELSE '65+'
END AS age_group, gender,
count(*) AS count
FROM hr
WHERE age >=18 AND termdate = '0000-00-00'
GROUP BY age_group, gender
ORDER BY age_group, gender;
```
![Screenshot (259)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/d92ecc1e-c8a5-491b-af43-3bcb47acef8b)


4. How Many EMPLOYEE work from the Headquarters or Remote location;
'''
SELECT location, count(*) AS count
FROM hr
WHERE age >=18 AND termdate = '0000-00-00'
GROUP BY location;
'''
![Screenshot (260)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/e9a1303e-d090-4d13-8e31-ff1f4669ff46)

-- 5. What is the average duration of employment for employees who have been terminated (ROUND UP)
'''
SELECT
round(avg(datediff(termdate, hire_date))/365,0) AS avg_duration_employment
FROM hr
WHERE termdate <= CURDATE() AND termdate <> '0000-00-00'AND age >= 18;
'''
![image](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/66609e3f-8f93-40a8-b4a3-e28b2a4f9111)

-- 6. How does the gender distribution vary across departments and ajob titles



