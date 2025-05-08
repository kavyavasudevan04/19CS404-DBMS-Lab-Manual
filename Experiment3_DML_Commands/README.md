# Experiment 3: DML Commands
### Name:Kavya V
## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
![image](https://github.com/user-attachments/assets/9da6c96f-36f1-4a16-8a7c-5e000d72108d)


```sql
update sales
set sell_price= sell_price*1.05
where product_id =15;
```

**Output:**

![image](https://github.com/user-attachments/assets/838735b2-7bf2-4fab-bb94-4838724fef55)


**Question 2**
---
![image](https://github.com/user-attachments/assets/76c26221-47fd-45e8-9617-b857f615b360)


```sql
update sales
set sell_price = sell_price +3
where product_id in(
select product_id
from PRODUCTS
where supplier_id=4);
```

**Output:**

![image](https://github.com/user-attachments/assets/fd6d6d2d-8a7b-4b90-a051-4b991399e8e1)


**Question 3**
---
![image](https://github.com/user-attachments/assets/14d2ab3f-4b29-41b0-b12d-d31bdd8fd1e1)


```sql
update Employees
set EMAIL= 'not available' ,
COMMISSION_PCT =0.55
where department_id =110;
```

**Output:**

![image](https://github.com/user-attachments/assets/cb74d6b3-7573-44b1-a5e7-8cbe489e64f1)


**Question 4**
---
![image](https://github.com/user-attachments/assets/75754ae7-fe7d-4980-8b26-0f87f2bf42a2)


```sql
update products
set reorder_lvl=reorder_lvl*1.30
where category = 'Food' and quantity<50;
```

**Output:**

![image](https://github.com/user-attachments/assets/e88b612b-3152-4c37-8358-2a54aa260f33)


**Question 5**
---
![image](https://github.com/user-attachments/assets/c7918f1c-91c8-4c25-849a-6bcf9c7e40c0)


```sql
update PRODUCTS
set reorder_lvl= reorder_lvl*0.7
where product_name like '%cream%' and quantity >reorder_lvl;
```

**Output:**

![image](https://github.com/user-attachments/assets/97ad3fec-6f1b-4860-be8a-5f7c026c6c76)


**Question 6**
---
![image](https://github.com/user-attachments/assets/f2540b66-2661-4114-a9f2-4af237d6e0b6)


```sql
delete from Doctors
where specialization ='Cardiology';
```

**Output:**

![image](https://github.com/user-attachments/assets/21f6f95e-b8b3-44aa-976b-0fafa0ac3f00)


**Question 7**
---
![image](https://github.com/user-attachments/assets/554ef8e6-fe51-46af-93ab-5f4d1d54f3f8)


```sql
delete from Doctors
where doctor_id  = 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/ccd509a0-3ffd-4be0-9647-8759b5dbf167)


**Question 8**
---
![image](https://github.com/user-attachments/assets/68a669aa-692d-4705-8ad0-074ce0976b63)


```sql
delete from Surgeries
where surgery_id = 3;
```

**Output:**

![image](https://github.com/user-attachments/assets/cb6f9a8e-de8c-45f7-9677-f17c0be1d91e)


**Question 9**
---
![image](https://github.com/user-attachments/assets/362956f4-6744-4323-9467-e4082dcf40eb)


```sql
delete from Customer
where (GRADE=2 and CUST_NAME like 'M%')
and PAYMENT_AMT<3000;
```

**Output:**

![image](https://github.com/user-attachments/assets/6ab65e7f-55f3-485e-b2dd-e66b6848563f)


**Question 10**
---
![image](https://github.com/user-attachments/assets/eb452a4b-37fb-4abf-8dce-b57b3b35619c)


```sql
delete from Customer
where GRADE >2 
and PAYMENT_AMT <(select avg(PAYMENT_AMT)from Customer)
or OUTSTANDING_AMT>8000;
```

**Output:**

![image](https://github.com/user-attachments/assets/d601592d-82c9-4691-864e-8a62c9efb449)


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
