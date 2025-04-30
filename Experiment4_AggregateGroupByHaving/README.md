# Experiment 4: Aggregate Functions, Group By and Having Clause
### Name: Kavya V
## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
![image](https://github.com/user-attachments/assets/e5fe5d1f-9c38-4ab6-a286-73eab9a0acc0)


```sql
select 
PatientID,
count(*) as TotalAppointments
from
Appointments
group by
PatientID
order by
PatientID;
```

**Output:**

![image](https://github.com/user-attachments/assets/2060e74e-97aa-431e-8b91-f9b0f83a7bc7)


**Question 2**
---
![image](https://github.com/user-attachments/assets/8885caa3-281f-4aeb-88f0-7afa0185e081)


```sql
select
strftime('%H',AppointmentDateTime) as "HourOfDay",
count(*) as "TotalAppointments"
from
Appointments
group by
strftime('%H',AppointmentDateTime)
order by
HourOfDay;
```

**Output:**

![image](https://github.com/user-attachments/assets/55f969fb-60a0-4e89-a0fc-8662549691ed)


**Question 3**
---
![image](https://github.com/user-attachments/assets/224fc4d0-39b7-48c7-874e-94d9011d23d8)


```sql
select
strftime('%Y',ValidityPeriod) as "ValidityYear",
count(*) as "TotalPatients"
from
Insurance 
group by
strftime('%Y',ValidityPeriod)
order by
ValidityYear;
```

**Output:**

![image](https://github.com/user-attachments/assets/0936b749-8391-4182-bc16-b2edc0bc3e81)


**Question 4**
---
![image](https://github.com/user-attachments/assets/fcf08c59-b0af-45e0-a879-f20e6dd9c1de)

```sql
select
count(*) as "COUNT"
from
customer
where
city!= 'Noida';
```

**Output:**

![image](https://github.com/user-attachments/assets/90b81076-e286-4d68-9278-bba182753305)


**Question 5**
---
![image](https://github.com/user-attachments/assets/47611793-243b-4f6a-9390-784da6dace89)


```sql
select
name as "fruit_name",
min(inventory) as "lowest_quantity"
from
fruits
group by
name
order by
min(inventory)asc
limit 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/0617bc96-029c-49cf-9653-47faa14779dd)


**Question 6**
---
![image](https://github.com/user-attachments/assets/09348511-7c11-4730-9779-e06f37ba0197)


```sql
select
name,
max(length(name)) as "length"
from
customer
order by
max(length(name))asc
 limit 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/6c4b4326-1afa-47c8-8999-1bf2361f0c47)


**Question 7**
---
![image](https://github.com/user-attachments/assets/8309e2d0-1947-4721-92fa-93325427cd38)


```sql
select
name,
email,
min(length(email)) as"min_email_length"
from
customer
order by
min(length(email))
limit 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/0a49384a-cf42-4214-88ab-05937c114359)


**Question 8**
---
![image](https://github.com/user-attachments/assets/bb331ac0-48c1-4f84-9c35-c78213d5dc55)


```sql
select 
(age/5)*5 as "age_group",
min(salary) as"MIN(salary)"
from
customer1
group by
(age/5)*5
having
min(salary)<2000
order by
age_group;
```

**Output:**

![image](https://github.com/user-attachments/assets/8804fd70-316c-47fd-8be3-1f1514366b5b)


**Question 9**
---
![image](https://github.com/user-attachments/assets/9f0fc2ed-6c22-4f60-a4f1-1dccda133298)


```sql
select
jdate,
sum(workhour) as "SUM(workhour)"
from
employee1
group by
jdate
having
sum(workhour)>40
order by
jdate;
```

**Output:**

![image](https://github.com/user-attachments/assets/8597cef1-7e9a-4675-a642-18bce88e3708)


**Question 10**
---
![image](https://github.com/user-attachments/assets/cd6cb97a-ecc0-44bc-ae5b-7746ce2b148d)


```sql
select
address,
sum(salary) as "SUM(salary)"
from
customer1
group by
address
having
sum(salary)>2000
order by
address;
```

**Output:**

![image](https://github.com/user-attachments/assets/a12b4b65-6ef5-4c55-880b-debf34f54a49)



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
