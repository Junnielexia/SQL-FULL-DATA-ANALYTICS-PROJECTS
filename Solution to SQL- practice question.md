# in  this file i documented the solution to all the question from this website
https://www.sql-practice.com/

# Northwind Database
# Easy
- question 1:Show the category_name and description from the categories table sorted by category_name.
solution:

SELECT category_name, description
FROM categories
ORDER BY category_name;

- question 2:Show all the contact_name, address, city of all customers which are not from 'Germany', 'Mexico', 'Spain'
solution
SELECT contact_name, address, city
FROM customers
WHERE country NOT IN ('Germany', 'Mexico', 'Spain');

- question 3:Show order_date, shipped_date, customer_id, Freight of all orders placed on 2018 Feb 26
Solution
SELECT order_date, shipped_date, customer_id, Freight
FROM orders
WHERE DATE(order_date) = '2018-02-26';

- question 4:Show the employee_id, order_id, customer_id, required_date, shipped_date from all orders shipped later than the required date.
Solution
SELECT employee_id, order_id, customer_id, required_date, shipped_date
FROM orders
WHERE shipped_date > required_date;

- question 5: Show all the even numbered Order_id from the orders table
Solution
SELECT order_id
FROM orders
WHERE order_id % 2 = 0;

- Question 6: Show all the even numbered Order_id from the orders table
Solution
SELECT order_id
FROM orders
WHERE order_id % 2 = 0;

- Question 7:Show the city, company_name, contact_name of all customers from cities which contains the letter 'L' in the city name, sorted by contact_name.
Solution
SELECT city, company_name, contact_name
FROM customers
WHERE city LIKE '%L%'
ORDER BY contact_name;

- question 8:Show the company_name, contact_name, fax number of all customers that has a fax number. (not null)
Solution
SELECT company_name, contact_name, fax
FROM customers
WHERE fax IS NOT NULL;

- Question 9: Show the first_name, last_name. hire_date of the most recently hired employee.
 Solution
SELECT first_name, last_name, hire_date
FROM employees
ORDER BY hire_date DESC
LIMIT 1;

- Question 10:Show the average unit price rounded to 2 decimal places, the total units in stock, total discontinued products from the products table.
Solution
SELECT
    ROUND(AVG(unit_price), 2) AS average_unit_price,
    SUM(units_in_stock) AS total_units_in_stock,
    SUM(CASE WHEN discontinued = 1 THEN 1 ELSE 0 END) AS total_discontinued_products
FROM products;

#Mediuum

- Question 11:Show the ProductName, CompanyName, CategoryName from the products, suppliers, and categories table
Solution
SELECT
    p.product_name AS ProductName,
    s.company_name AS CompanyName,
    c.category_name AS CategoryName
FROM products p
JOIN suppliers s ON p.supplier_id = s.supplier_id
JOIN categories c ON p.category_id = c.category_id;

-Question 12:Show the category_name and the average product unit price for each category rounded to 2 decimal places.
Solution
SELECT
    c.category_name,
    ROUND(AVG(p.unit_price), 2) AS average_unit_price
FROM categories c
JOIN products p ON c.category_id = p.category_id
GROUP BY c.category_name;
# Hard
- Question 13: Show the employee's first_name and last_name, a "num_orders" column with a count of the orders taken, and a column called "Shipped" that displays "On Time" if the order shipped on time and "Late" if the order shipped late.
Order by employee last_name, then by first_name, and then descending by number of orders.

Solution
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

# Hospital Database
## Easy
question 1:Show first name, last name, and gender of patients whose gender is 'M'
Solution
SELECT first_name, last_name, gender
FROM patients
WHERE gender = 'M';

-Question 2:Show first name and last name of patients who does not have allergies. (null)
Solution
SELECT first_name, last_name
FROM patients
WHERE allergies IS NULL;

- Question 3:Show first name of patients that start with the letter 'C'
Solution

SELECT first_name
FROM patients
WHERE first_name LIKE 'C%';

- Question 4:Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)
Solution
SELECT first_name, last_name
FROM patients
WHERE weight BETWEEN 100 AND 120;

- Question 5: Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'
Solution

UPDATE patients
SET allergies = 'NKA'
WHERE allergies IS NULL;

- Question 6:Show first name and last name concatinated into one column to show their full name.
Solution
SELECT CONCAT(first_name, ' ', last_name) AS full_name
FROM patients;

- Question 7:Show first name, last name, and the full province name of each patient.
Example: 'Ontario' instead of 'ON'
Solution
SELECT p.first_name, p.last_name, pn.province_name
FROM patients p
JOIN province_names pn ON p.province_id = pn.province_id;

- Question 8:Show how many patients have a birth_date with 2010 as the birth year.
Solution

SELECT COUNT(*)
FROM patients
WHERE YEAR(birth_date) = 2010;

- Question 9:Show the first_name, last_name, and height of the patient with the greatest height.
Solution
SELECT first_name, last_name, height
FROM patients
ORDER BY height DESC
LIMIT 1;

- Question 10: Show all columns for patients who have one of the following patient_ids:
1,45,534,879,1000
Solution
SELECT *
FROM patients
WHERE patient_id IN (1, 45, 534, 879, 1000);

- Question 11:Show the total number of admissions
-Solution
SELECT COUNT(*) AS total_admissions
FROM admissions;

-Question 12: Show all the columns from admissions where the patient was admitted and discharged on the same day.
Solution
SELECT *
FROM admissions
WHERE DATE(admission_date) = DATE(discharge_date);

- Question 13:Show the patient id and the total number of admissions for patient_id 579.
Solution

SELECT patient_id, COUNT(*) AS total_admissions
FROM admissions
WHERE patient_id = 579;

- Question 14:Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?
Solution
SELECT DISTINCT city
FROM patients
WHERE province_id = 'NS';

- Question 15:Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70
Solution
SELECT first_name, last_name, birth_date
FROM patients
WHERE height > 160 AND weight > 70;

- Question 16:Write a query to find list of patients first_name, last_name, and allergies from Hamilton where allergies are not null
Solution
SELECT first_name, last_name, allergies
FROM patients
WHERE city = 'Hamilton' AND allergies IS NOT NULL;

- Question 17: Based on cities where our patient lives in, write a query to display the list of unique city starting with a vowel (a, e, i, o, u). Show the result order in ascending by city.
Solution
SELECT DISTINCT city
FROM patients
WHERE city LIKE 'A%' OR city LIKE 'E%' OR city LIKE 'I%' OR city LIKE 'O%' OR city LIKE 'U%'
ORDER BY city ASC;

- Question 18:Show unique birth years from patients and order them by ascending.
Solution
SELECT DISTINCT YEAR(birth_date) AS birth_year
FROM patients
ORDER BY birth_year ASC;

# Medium
# Hard
