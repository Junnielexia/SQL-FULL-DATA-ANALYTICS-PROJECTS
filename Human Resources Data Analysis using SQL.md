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
