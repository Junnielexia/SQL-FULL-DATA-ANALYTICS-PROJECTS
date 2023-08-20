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


# Medium
# Hard
