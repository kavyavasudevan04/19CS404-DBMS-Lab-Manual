# Experiment 6: Joins
## Name: Kavya.V

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;

```

**Question 1**
--
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

![Screenshot 2025-05-09 104401](https://github.com/user-attachments/assets/fc88a51e-176d-4134-9923-d8eae5bad99f)

**Query:**

```sql

SELECT nurses.*, departments.department_name
FROM nurses
INNER JOIN departments
ON nurses.department_id = departments.department_id;

```

**Output:**

![Screenshot 2025-05-09 104459](https://github.com/user-attachments/assets/9f253537-93af-4e5c-a2e7-93e2ba93e15e)


**Question 2**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), the "cust_name," "city," "grade," and "salesman_id" columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for customers with a grade less than or equal to 100.

![Screenshot 2025-05-09 104733](https://github.com/user-attachments/assets/86b0357a-966d-4f4b-9e31-bf1d4b55843b)

**Query:**

```sql
SELECT 
    s.name, 
    c.cust_name, 
    c.city, 
    c.grade, 
    c.salesman_id
FROM 
    salesman s
LEFT JOIN 
    customer c 
ON 
    s.salesman_id = c.salesman_id
WHERE 
    c.grade <= 100;

```

**Output:**

![Screenshot 2025-05-09 105020](https://github.com/user-attachments/assets/20bd12da-c917-4cc5-b890-6b60d761bee6)


**Question 3**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

![Screenshot 2025-05-09 105053](https://github.com/user-attachments/assets/581a6f0b-9614-4ec3-b3a5-e9a1e7f95ecb)

**Query:**

```sql
SELECT 
    c.cust_name, 
    c.city, 
    c.grade, 
    s.name AS Salesman, 
    s.city AS city
FROM 
    customer c
JOIN 
    salesman s 
ON 
    c.salesman_id = s.salesman_id
WHERE 
    c.grade < 300
ORDER BY 
    c.customer_id ASC;

```

**Output:**

![Screenshot 2025-05-09 105110](https://github.com/user-attachments/assets/edcf532a-5532-409a-b5bd-0a6e1a6e1613)


**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date between '2012-07-01' and '2012-07-30'.

![Screenshot 2025-05-09 105129](https://github.com/user-attachments/assets/fa9b6396-89bf-4111-b5f1-564e16c88733)

**Query:**

```sql
SELECT 
    c.*
FROM 
    customer c
LEFT JOIN 
    orders o 
ON 
    c.customer_id = o.customer_id
WHERE 
    o.ord_date BETWEEN '2012-07-01' AND '2012-07-30';

```

**Output:**

![Screenshot 2025-05-09 105149](https://github.com/user-attachments/assets/dcec4f94-0360-4890-931f-a0da335b8e35)


**Question 5**
---
Write the SQL query that achieves the selection of all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

![Screenshot 2025-05-09 105208](https://github.com/user-attachments/assets/fa5f0790-f0b1-4646-a688-7505fcc41762)

**Query:**

```sql

SELECT 
    t.*
FROM 
    test_results t
INNER JOIN 
    patients p 
ON 
    t.patient_id = p.patient_id
WHERE 
    p.first_name = 'Alice';

```

**Output:**

![Screenshot 2025-05-09 105224](https://github.com/user-attachments/assets/37feb3f3-e32f-4038-ac47-8a739b1b67e5)


**Question 6**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  

![Screenshot 2025-05-09 105246](https://github.com/user-attachments/assets/3c4b91c2-5d36-4516-806a-d39ac96c14de)

**Query:**

```sql

SELECT 
    c.cust_name AS "Customer Name", 
    c.city AS "city", 
    s.name AS "Salesman", 
    s.city AS "city", 
    s.commission
FROM 
    customer c
JOIN 
    salesman s 
ON 
    c.salesman_id = s.salesman_id
WHERE 
    c.city <> s.city
    AND s.commission > 0.12;


```

**Output:**

![Screenshot 2025-05-09 105308](https://github.com/user-attachments/assets/e0a54108-de53-43f3-8987-52ea31d23f46)


**Question 7**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

![Screenshot 2025-05-09 105430](https://github.com/user-attachments/assets/b865d66a-2b37-4d41-a7bb-4fa6b3f32ada)

**Query:**

```sql
SELECT 
    o.ord_no, 
    o.purch_amt, 
    o.ord_date, 
    c.cust_name, 
    c.city AS customer_city, 
    c.grade, 
    s.name AS salesman_name, 
    s.city AS salesman_city, 
    s.commission
FROM 
    orders o
JOIN 
    customer c ON o.customer_id = c.customer_id
JOIN 
    salesman s ON o.salesman_id = s.salesman_id;

```

**Output:**

![Screenshot 2025-05-09 105502](https://github.com/user-attachments/assets/a934c792-d31d-4f2b-a4ee-9b0259fdbb52)


**Question 8**
---
Write the SQL query that achieves the selection of all columns from the "patients" table and the specialization from the "doctors" table (aliased as "doctor_specialization"), with an inner join on the "doctor_id" column.

![Screenshot 2025-05-09 105524](https://github.com/user-attachments/assets/7981f2d2-ec3f-4bcb-a5f7-115043af3136)

**Query:**

```sql

SELECT 
    p.patient_id, 
    p.first_name, 
    p.last_name, 
    p.date_of_birth, 
    p.admission_date, 
    p.discharge_date, 
    p.doctor_id, 
    d.specialization AS doctor_specialization
FROM 
    patients p
INNER JOIN 
    doctors d 
ON 
    p.doctor_id = d.doctor_id;

```

**Output:**

![Screenshot 2025-05-09 105550](https://github.com/user-attachments/assets/ac6823a4-db34-4e71-a95b-125f0edeede1)


**Question 9**
---
 From the following tables write a SQL query to find the salesperson(s) and the customer(s) he represents. Return Customer Name, city, Salesman, commission.

![Screenshot 2025-05-09 105615](https://github.com/user-attachments/assets/06eec569-3189-4113-a20c-acafa571c17d)

**Query:**

```sql

SELECT 
    c.cust_name AS "Customer Name", 
    c.city AS "city", 
    s.name AS "Salesman", 
    s.commission
FROM 
    customer c
JOIN 
    salesman s 
ON 
    c.salesman_id = s.salesman_id;

```

**Output:**

![Screenshot 2025-05-09 105634](https://github.com/user-attachments/assets/8d25935d-e611-431a-ab0f-cebcecd409b3)


**Question 10**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

![Screenshot 2025-05-09 105654](https://github.com/user-attachments/assets/0a330f8a-4390-473d-ba6e-aa031605b2a1)

**Query:**

```sql

SELECT 
    o.ord_no, 
    o.purch_amt, 
    c.cust_name, 
    c.city
FROM 
    orders o
JOIN 
    customer c 
ON 
    o.customer_id = c.customer_id
WHERE 
    o.purch_amt BETWEEN 500 AND 2000;

```

**Output:**

![Screenshot 2025-05-09 105711](https://github.com/user-attachments/assets/57cad913-ecee-428b-8ee0-79890f9d12d5)

## Module 5 - Home Challenge

![Screenshot 2025-05-09 113331](https://github.com/user-attachments/assets/a3d8431d-d118-4550-b94c-906cae358914)


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
