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

**TO Alter the data type  i used the code below**

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

![Screenshot (264)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/511e49dc-9b6a-455c-a97d-90d870757020)

# Business Question

1.  What is the gender breakdown of employees in the company?

```
  SELECT gender, COUNT(*) AS count
FROM hr
WHERE age >= 18 AND termdate = '0000-00-00'
GROUP BY gender;

```

![Screenshot (266)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/4c2ed170-2a48-481a-adb3-51c6697f740c)

2. What is the race/Ethnicity breakdown of employees in the company?

```
SELECT race, COUNT(*) AS count
FROM hr
WHERE age >= 18 AND termdate = '0000-00-00'
GROUP BY race
ORDER BY count(*) DESC;
```

![Screenshot (267)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/be13f9eb-a22a-48cc-99b0-2baf89687e6b)


3. What is the age distribution of employees in the company

A. **OLD & YOUNG**

```
SELECT
MIN(age) AS youngest,
MAX(age) AS oldest
FROM hr
WHERE age >=18 AND termdate = '0000-00-00';
```

![Screenshot (268)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/9cd4143f-7fb9-4bf8-a4d6-0351eb15cda6)

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

![Screenshot (269)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/dc3e3d18-1e44-4d2b-bd1e-c98506d3954d)

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

![Screenshot (270)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/de82cb09-ba31-4e53-8fd1-f2823d5a1539)


4. How Many EMPLOYEE work from the Headquarters or Remote location;

'''
SELECT location, count(*) AS count
FROM hr
WHERE age >=18 AND termdate = '0000-00-00'
GROUP BY location;
'''

![Screenshot (271)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/42729a07-4d85-4eac-8dc9-87e2ae3e47b4)


5. What is the average duration of employment for employees who have been terminated (ROUND UP)


'''
SELECT
round(avg(datediff(termdate, hire_date))/365,0) AS avg_duration_employment
FROM hr
WHERE termdate <= CURDATE() AND termdate <> '0000-00-00'AND age >= 18;
'''

![Screenshot (272)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/5273dda9-9b52-4f3a-b779-f6d87891c230)


6. How does the gender distribution vary across departments and ajob titles

'''
SELECT department, gender, count(*) AS count
FROM hr
WHERE age >=18 AND termdate = '0000-00-00'
GROUP BY department, gender
ORDER BY department, gender;
'''

![Screenshot (273)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/f03f8d52-7092-4a04-931f-08ff8c347f81)


7. What is the distribution of job title across the company?

'''
SELECT jobtitle , count(*) AS count
FROM hr
WHERE age >=18 AND termdate = '0000-00-00'
GROUP BY jobtitle
ORDER BY jobtitle DESC;
'''

![Screenshot (274)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/9b807477-4dd2-4bfb-a6d1-a8249608cc68)

8. Which Department has the highest turnover rate

'''
SELECT 
    department,
    COUNT(*) AS total_count,
    SUM(CASE WHEN termdate != '0000-00-00' AND termdate <= CURDATE() THEN 1 ELSE 0 END) AS terminated_count,
    IFNULL((SUM(CASE WHEN termdate IS NOT NULL AND termdate <= CURDATE() THEN 1 ELSE 0 END) / COUNT(*)), 0) AS termination_rate
FROM hr
WHERE age >= 18
GROUP BY department
ORDER BY termination_rate DESC;
'''

![Screenshot (275)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/bf48179c-4a8c-4bdb-83cc-15329993f876)


9. WHAT Is the distribution of employees across  locations, cities and state

'''
SELECT location_state, count(*) AS count
FROM hr
WHERE age >=18 AND termdate = '0000-00-00'
GROUP BY location_state
ORDER BY count DESC;
'''

![Screenshot (276)](https://github.com/Junnielexia/SQL-FULL-DATA-ANALYTICS-PROJECTS/assets/95970546/5fc082ad-4132-4889-be8b-5789cbff5161)

## Summary of Insights from HR Dataset Analysis

- **Gender Distribution:** The dataset indicates a higher number of male employees compared to females.

- **Ethnicity Distribution:** Among the racial groups, individuals identifying as White constitute the largest segment, while Native Hawaiian and American Indian categories have the lowest representation.

- **Age Distribution:** The age range of employees spans from 20 to 57 years. To better analyze age demographics, five distinct age groups were created: 18-24, 25-34, 35-44, 45-54, and 55-64. The majority of employees fall within the 25-34 age bracket, followed by the 35-44 group. Conversely, the 55-64 age group represents the smallest portion.

- **Work Location:** A substantial portion of employees work on-site at the headquarters, with remote workers forming a smaller segment.

- **Length of Employment:** For terminated employees, the average employment tenure is approximately 7 years.

- **Gender Distribution by Department:** While gender distribution across departments shows a relative balance, there is a general prevalence of male employees over female employees.

- **Turnover Rates by Department:** The Marketing department exhibits the highest turnover rate, closely followed by the Training department. Conversely, the Research and Development, Support, and Legal departments have the lowest turnover rates.

- **Geographical Origin:** A significant number of employees originate from the state of Ohio.

- **Employee Changes:** The dataset reveals a consistent increase in the net employee count over the years.

- **Tenure by Department:** On average, employees have a tenure of approximately 8 years within their respective departments. Notably, the Legal and Auditing departments have the longest average tenure, while the Services, Sales, and Marketing departments display the shortest average tenures.
