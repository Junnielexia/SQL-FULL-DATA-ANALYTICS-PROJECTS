# in  this file i documented the sql problems and solution  from this website below. The problem ranges from easy to medium to hard using two Databases ( Northwind and Hospital). 
https://www.sql-practice.com/

# Northwind Database
## Easy
- **Question 1: Show the category_name and description from the categories table sorted by category_name.**

### solution:
```
SELECT category_name, description
FROM categories
ORDER BY category_name;
```
- **question 2:Show all the contact_name, address, city of all customers which are not from 'Germany', 'Mexico', 'Spain'. **

### solution
```
SELECT contact_name, address, city
FROM customers
WHERE country NOT IN ('Germany', 'Mexico', 'Spain');
```
-**question 3:Show order_date, shipped_date, customer_id, Freight of all orders placed on 2018 Feb 26.**

### Solution
```
SELECT order_date, shipped_date, customer_id, Freight
FROM orders
WHERE DATE(order_date) = '2018-02-26';
```
-**question 4:Show the employee_id, order_id, customer_id, required_date, shipped_date from all orders shipped later than the required date.**

### Solution
```
SELECT employee_id, order_id, customer_id, required_date, shipped_date
FROM orders
WHERE shipped_date > required_date;
```
- **question 5: Show all the even numbered Order_id from the orders table.**

### Solution
```
SELECT order_id
FROM orders
WHERE order_id % 2 = 0;
```
- **Question 6: Show all the even numbered Order_id from the orders table.**

### Solution
```
SELECT order_id
FROM orders
WHERE order_id % 2 = 0;
```
- **Question 7:Show the city, company_name, contact_name of all customers from cities which contains the letter 'L' in the city name, sorted by contact_name.**

### Solution
```
SELECT city, company_name, contact_name
FROM customers
WHERE city LIKE '%L%'
ORDER BY contact_name;
```
- **question 8:Show the company_name, contact_name, fax number of all customers that has a fax number. (not null).**

### Solution
```
SELECT company_name, contact_name, fax
FROM customers
WHERE fax IS NOT NULL;
```
- **Question 9: Show the first_name, last_name. hire_date of the most recently hired employee.**

 ### Solution
 ```
SELECT first_name, last_name, hire_date
FROM employees
ORDER BY hire_date DESC
LIMIT 1;
```
- **Question 10:Show the average unit price rounded to 2 decimal places, the total units in stock, total discontinued products from the products table.**

### Solution
```
SELECT
    ROUND(AVG(unit_price), 2) AS average_unit_price,
    SUM(units_in_stock) AS total_units_in_stock,
    SUM(CASE WHEN discontinued = 1 THEN 1 ELSE 0 END) AS total_discontinued_products
FROM products;
```
# Mediuum

- **Question 11:Show the ProductName, CompanyName, CategoryName from the products, suppliers, and categories table.**

### Solution
```
SELECT
    p.product_name AS ProductName,
    s.company_name AS CompanyName,
    c.category_name AS CategoryName
FROM products p
JOIN suppliers s ON p.supplier_id = s.supplier_id
JOIN categories c ON p.category_id = c.category_id;
```

-**Question 12:Show the category_name and the average product unit price for each category rounded to 2 decimal places.**

### Solution
```
SELECT
    c.category_name,
    ROUND(AVG(p.unit_price), 2) AS average_unit_price
FROM categories c
JOIN products p ON c.category_id = p.category_id
GROUP BY c.category_name;
```
# Hard
- **Question 13: Show the employee's first_name and last_name, a "num_orders" column with a count of the orders taken, and a column called "Shipped" that displays "On Time" if the order shipped on time and "Late" if the order shipped late.
Order by employee last_name, then by first_name, and then descending by number of orders.**

### Solution
```
SELECT
    e.first_name,
    e.last_name,
    COUNT(o.order_id) AS num_orders,
    CASE
        WHEN o.shipped_date <o.required_date THEN 'On Time'
        ELSE 'Late'
    END AS Shipped
FROM employees e
JOIN orders o ON e.employee_id = o.employee_id
GROUP BY e.employee_id, e.first_name, e.last_name
ORDER BY e.last_name, e.first_name, num_orders DESC;
```

# Hospital Database
## Easy

- **question 1:Show first name, last name, and gender of patients whose gender is 'M'.**

### Solution
```
SELECT first_name, last_name, gender
FROM patients
WHERE gender = 'M';
```
-**Question 2:Show first name and last name of patients who does not have allergies. (null)**

### Solution
```
SELECT first_name, last_name
FROM patients
WHERE allergies IS NULL;
```

- **Question 3:Show first name of patients that start with the letter 'C'.**

### Solution
```
SELECT first_name
FROM patients
WHERE first_name LIKE 'C%';
```

- **Question 4:Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)**

### Solution
```
SELECT first_name, last_name
FROM patients
WHERE weight BETWEEN 100 AND 120;
```
- **Question 5: Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'.**

### Solution
```
UPDATE patients
SET allergies = 'NKA'
WHERE allergies IS NULL;
```

- **Question 6:Show first name and last name concatinated into one column to show their full name.**

### Solution
```
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM patients;
```
- **Question 7:Show first name, last name, and the full province name of each patient.
Example: 'Ontario' instead of 'ON'.**

### Solution
```
SELECT p.first_name, p.last_name, pn.province_name
FROM patients p
JOIN province_names pn ON p.province_id = pn.province_id;
```

- **Question 8:Show how many patients have a birth_date with 2010 as the birth year.**

### Solution
```
SELECT COUNT(*)
FROM patients
WHERE YEAR(birth_date) = 2010;
```

- **Question 9:Show the first_name, last_name, and height of the patient with the greatest height.**

### Solution
```
SELECT first_name, last_name, height
FROM patients
ORDER BY height DESC
LIMIT 1;
```
- **Question 10: Show all columns for patients who have one of the following patient_ids:
1,45,534,879,1000.**

### Solution
```
SELECT *
FROM patients
WHERE patient_id IN (1, 45, 534, 879, 1000);
```

- **Question 11:Show the total number of admissions**

### Solution
```
SELECT COUNT(*) AS total_admissions
FROM admissions;
```
- **Question 12: Show all the columns from admissions where the patient was admitted and discharged on the same day.**

### Solution
```
SELECT *
FROM admissions
WHERE DATE(admission_date) = DATE(discharge_date);
```

- **Question 13:Show the patient id and the total number of admissions for patient_id 579.**

### Solution
```
SELECT patient_id, COUNT(*) AS total_admissions
FROM admissions
WHERE patient_id = 579;
```

- **Question 14:Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?**

### Solution
```
SELECT DISTINCT city
FROM patients
WHERE province_id = 'NS';
```
- **Question 15:Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70.**

### Solution
```
SELECT first_name, last_name, birth_date
FROM patients
WHERE height > 160 AND weight > 70;
```

- **Question 16:Write a query to find list of patients first_name, last_name, and allergies from Hamilton where allergies are not null.**

### Solution
```
SELECT first_name, last_name, allergies
FROM patients
WHERE city = 'Hamilton' AND allergies IS NOT NULL;
```

- **Question 17: Based on cities where our patient lives in, write a query to display the list of unique city starting with a vowel (a, e, i, o, u). Show the result order in ascending by city.**

### Solution
```
SELECT DISTINCT city
FROM patients
WHERE city LIKE 'A%' OR city LIKE 'E%' OR city LIKE 'I%' OR city LIKE 'O%' OR city LIKE 'U%'
ORDER BY city ASC;
```

- **Question 18:Show unique birth years from patients and order them by ascending.**

### Solution
```
SELECT DISTINCT YEAR(birth_date) AS birth_year
FROM patients
ORDER BY birth_year ASC;
```

- **Question 19:Show unique first names from the patients table which only occurs once in the list.**

### Solution
```
SELECT first_name
FROM patients
GROUP BY first_name
HAVING COUNT(first_name) = 1;
```

- **Question 20:Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.**

### Solution
```
SELECT patient_id, first_name
FROM patients
WHERE LENGTH(first_name) >= 6 AND
      first_name LIKE 's%s';
```

- **Question 21:Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.
Primary diagnosis is stored in the admissions table.
Note there are two tables n the common column is patients id.**

### Solution
```
SELECT p.patient_id, p.first_name, p.last_name
FROM patients p
JOIN admissions a ON p.patient_id = a.patient_id
WHERE a.primary_diagnosis = 'Dementia';
```

- **Question 22:Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.**

### Solution
```
SELECT p.patient_id, p.first_name, p.last_name
FROM patients p
JOIN admissions a ON p.patient_id = a.patient_id
WHERE a.diagnosis = 'Dementia';
```

- **Question 23:Display every patient's first_name.
Order the list by the length of each name and then by alphbetically**

### Solution
```
SELECT first_name
FROM patients
ORDER BY LENGTH(first_name), first_name;
```

- **Question 24;Show the total amount of male patients and the total amount of female patients in the patients table.
Display the two results in the same row.**

### Solution
```
SELECT
    SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) AS total_male_patients,
    SUM(CASE WHEN gender = 'F' THEN 1 ELSE 0 END) AS total_female_patients
FROM patients;
```

- **Question 25:Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.**

### Solution
```
SELECT first_name, last_name, allergies
FROM patients
WHERE allergies IN ('Penicillin', 'Morphine')
ORDER BY allergies ASC, first_name ASC, last_name ASC;
```

-**Question 26:Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.**

### solution
```
SELECT patient_id, diagnosis
FROM admissions
GROUP BY patient_id, diagnosis
HAVING COUNT(*) > 1;
```

- **Question 27:Show the city and the total number of patients in the city.
Order from most to least patients and then by city name ascending.**

### Solution
```
SELECT city, COUNT(*) AS total_patients
FROM patients
GROUP BY city
ORDER BY total_patients DESC, city ASC;
```

- **Question 28:Show first name, last name and role of every person that is either patient or doctor.
The roles are either "Patient" or "Doctor.**

### Solution
```
SELECT first_name, last_name, 'Patient' AS role
FROM patients
UNION ALL
SELECT first_name, last_name, 'Doctor' AS role
FROM doctors;
```

- **Question 29:Show all of the patients grouped into weight groups.
Show the total amount of patients in each weight group.
Order the list by the weight group decending.**

### Solution
```
SELECT
    FLOOR(weight / 10) * 10 AS weight_group,
    COUNT(*) AS total_patients
FROM patients
GROUP BY weight_group
ORDER BY weight_group DESC;
```

- **Question 30:Show patient_id, weight, height, isObese from the patients table.
Display isObese as a boolean 0 or 1.
Obese is defined as weight(kg)/(height(m)2) >= 30.
weight is in units kg.
height is in units cm.**

### Solution
```
SELECT
    patient_id,
    weight,
    height,
    CASE WHEN (weight / POWER(height / 100.0, 2)) >= 30 THEN 1 ELSE 0 END AS isObese
FROM patients;
```

- **Question 31:Show patient_id, first_name, last_name, and attending doctor's specialty.
Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first name is 'Lisa'.
Check patients, admissions, and doctors tables for required information.**

### Solution
```
SELECT
    p.patient_id,
    p.first_name,
    p.last_name,
    d.specialty AS attending_doctor_specialty
FROM patients p
JOIN admissions a ON p.patient_id = a.patient_id
JOIN doctors d ON a.attending_doctor_id = d.doctor_id
WHERE a.diagnosis = 'Epilepsy'
  AND d.first_name = 'Lisa';
```

- **Question 32:All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password.
The password must be the following, in order:**
1. patient_id
2. the numerical length of patient's last_name
3. year of patient's birth_date.

### Solution
```
SELECT
    patient_id,
    CONCAT(patient_id, LENGTH(last_name), YEAR(birth_date)) AS temp_password
FROM patients
WHERE patient_id IN (SELECT DISTINCT patient_id FROM admissions);
```
- **Question 33:Each admission costs $50 for patients without insurance, and $10 for patients with insurance. All patients with an even patient_id have insurance.**

Give each patient a 'Yes' if they have insurance, and a 'No' if they don't have insurance. Add up the admission_total cost for each has_insurance group

### Solution
```
SELECT
    CASE WHEN patient_id % 2 = 0 THEN 'Yes' ELSE 'No' END AS has_insurance,
    SUM(CASE WHEN patient_id % 2 = 0 THEN 10 ELSE 50 END) AS admission_total_cost
FROM admissions
GROUP BY has_insurance;
```

- **Question 34:Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name.**

### Solution
```
SELECT pn.province_name
FROM province_names pn
JOIN patients p ON pn.province_id = p.province_id
GROUP BY pn.province_name
HAVING SUM(CASE WHEN p.gender = 'M' THEN 1 ELSE 0 END) > SUM(CASE WHEN p.gender = 'F' THEN 1 ELSE 0 END);
```

- **question 35:We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:**
- First_name contains an 'r' after the first two letters.
- Identifies their gender as 'F'
- Born in February, May, or December
- Their weight would be between 60kg and 80kg
- Their patient_id is an odd number
- They are from the city 'Kingston

### Solution
```
SELECT *
FROM patients
WHERE first_name LIKE '__r%'
  AND gender = 'F'
  AND MONTH(birth_date) IN (2, 5, 12)
  AND weight BETWEEN 60 AND 80
  AND patient_id % 2 = 1
  AND city = 'Kingston';

```
- **Question 36:Show the percent of patients that have 'M' as their gender. Round the answer to the nearest hundreth number and in percent form.**

### Solution
```
SELECT ROUND((COUNT(CASE WHEN gender = 'M' THEN 1 ELSE NULL END) * 100.0 / COUNT(*)), 2) || '%' AS percentage_male
FROM patients;
```

- **Question 37:For each day display the total amount of admissions on that day. Display the amount changed from the previous date.**

### Solution
```
SELECT
    admission_date,
    COUNT(*) AS total_admissions,
    COUNT(*) - LAG(COUNT(*)) OVER (ORDER BY admission_date) AS change_from_previous
FROM admissions
GROUP BY admission_date
ORDER BY admission_date;
```

- **Question 38:Sort the province names in ascending order in such a way that the province 'Ontario' is always on top.**

### Solution
```
SELECT province_name
FROM province_names
ORDER BY
    CASE WHEN province_name = 'Ontario' THEN 0 ELSE 1 END,
    province_name ASC;
```

- **Question 39:We need a breakdown for the total amount of admissions each doctor has started each year. Show the doctor_id, doctor_full_name, specialty, year, total_admissions for that year.**

### Solution
```
SELECT
    d.doctor_id,
    CONCAT(d.first_name, ' ', d.last_name) AS doctor_full_name,
    d.specialty,
    YEAR(a.admission_date) AS year,
    COUNT(*) AS total_admissions
FROM doctors d
JOIN admissions a ON d.doctor_id = a.attending_doctor_id
GROUP BY d.doctor_id, doctor_full_name, d.specialty, year
ORDER BY d.doctor_id, year;
```

- **Question 40:Show all allergies ordered by popularity. Remove NULL values from query.**

### Solution

```
SELECT allergies, COUNT(*) AS total_allergies
FROM patients
WHERE allergies IS NOT NULL
GROUP BY allergies
ORDER BY total_allergies DESC;
```

- **Question 41:Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.**

### Solution
```
SELECT first_name, last_name, birth_date
FROM patients
WHERE birth_date BETWEEN '1970-01-01' AND '1979-12-31'
ORDER BY birth_date;
```
- **Question 42:We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order.**
EX: SMITH,jane

### Solution
```
SELECT CONCAT(UPPER(last_name), ',', LOWER(first_name)) AS full_name
FROM patients
ORDER BY first_name DESC;
```

- **Question 43:Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.**

### Solution
```
SELECT province_id, SUM(height) AS total_height
FROM patients
GROUP BY province_id
HAVING SUM(height) >= 7000;
```
- **Question 44:Show the difference between the largest weight and smallest weight for patients with the last name'Maroni'.**

### Solution
```
SELECT MAX(weight) - MIN(weight) AS weight_difference
FROM patients
WHERE last_name = 'Maroni';
```
- **Question 45:Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.**

### Solution
```
SELECT
    DAY(admission_date) AS day_of_month,
    COUNT(*) AS total_admissions
FROM admissions
GROUP BY DAY(admission_date)
ORDER BY total_admissions DESC;
```

- **Question 46:Show all columns for patient_id 542's most recent admission_date**

### Solution
```SELECT *
FROM admissions
WHERE patient_id = 542
ORDER BY admission_date DESC
LIMIT 1;
```

- **Question 47:Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:**
1. patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.
2. attending_doctor_id contains a 2 and the length of patient_id is 3 characters.

### Solution
```
SELECT patient_id, attending_doctor_id, diagnosis
FROM admissions
WHERE 
    (MOD(patient_id, 2) = 1 AND attending_doctor_id IN (1, 5, 19))
    OR (attending_doctor_id LIKE '%2%' AND LENGTH(patient_id) = 3);
```
- **Question 48:Show first_name, last_name, and the total number of admissions attended for each doctor.
Every admission has been attended by a doctor.**

### Solution
```
SELECT
    d.first_name,
    d.last_name,
    COUNT(a.admission_id) AS total_admissions_attended
FROM doctors d
JOIN admissions a ON d.doctor_id = a.attending_doctor_id
GROUP BY d.first_name, d.last_name
ORDER BY total_admissions_attended DESC;
```
- **Question 49:For each doctor, display their id, full name, and the first and last admission date they attended.**

### Solution
```
SELECT
    d.doctor_id,
    CONCAT(d.first_name, ' ', d.last_name) AS doctor_full_name,
    MIN(a.admission_date) AS first_admission_date,
    MAX(a.admission_date) AS last_admission_date
FROM doctors d
JOIN admissions a ON d.doctor_id = a.attending_doctor_id
GROUP BY d.doctor_id, doctor_full_name
ORDER BY d.doctor_id;
```

- **Question 50: Display the total amount of patients for each province. Order by descending.**

### Solution
```
SELECT
    pn.province_name,
    COUNT(p.patient_id) AS total_patients
FROM patients p
JOIN province_names pn ON p.province_id = pn.province_id
GROUP BY pn.province_name
ORDER BY total_patients DESC;
```

- **Question 51:For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.**

### Solution
```
SELECT
    CONCAT(p.first_name, ' ', p.last_name) AS patient_full_name,
    a.diagnosis AS admission_diagnosis,
    CONCAT(d.first_name, ' ', d.last_name) AS doctor_full_name
FROM admissions a
JOIN patients p ON a.patient_id = p.patient_id
JOIN doctors d ON a.attending_doctor_id = d.doctor_id;
```

- **Question 52:display the number of duplicate patients based on their first_name and last_name**

### Solution
```
SELECT
    first_name,
    last_name,
    COUNT(*) AS duplicate_count
FROM patients
GROUP BY first_name, last_name
HAVING COUNT(*) > 1;
```

- **Question 53:Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.)**

### Solution
```
SELECT patient_id, first_name, last_name
FROM patients
WHERE patient_id NOT IN (SELECT DISTINCT patient_id FROM admissions);
```

- **Question 54:Display patient's full name,
height in the units feet rounded to 1 decimal,
weight in the unit pounds rounded to 0 decimals,
birth_date,
gender non abbreviated.**

Convert CM to feet by dividing by 30.48.
Convert KG to pounds by multiplying by 2.205.

### Solution
```
SELECT
    CONCAT(first_name, ' ', last_name) AS full_name,
    ROUND(height / 30.48, 1) AS height_feet,
    ROUND(weight * 2.205, 0) AS weight_pounds,
    birth_date,
    CASE gender
        WHEN 'M' THEN 'Male'
        WHEN 'F' THEN 'Female' 
        ELSE 'Other'
    END AS non_abbreviated_gender
FROM patients;
```
# Medium
# Hard
