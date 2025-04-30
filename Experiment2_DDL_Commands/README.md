# Experiment 2: DDL Commands
### Name: Kavya V


## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
![image](https://github.com/user-attachments/assets/4683f382-2e9a-4a0c-be3d-2eaf747fe6f2)


```sql
alter table  Student_details add  State TEXT;
```

**Output:**

![image](https://github.com/user-attachments/assets/7e22ae5e-fe44-469d-bc72-fdb73d2d1733)


**Question 2**
---
![image](https://github.com/user-attachments/assets/2dab3e22-d78b-4405-b87e-4b5452a2647d)


```sql
create table jobs(
job_id int primary key,
job_title text,
min_salary integer default(8000),
max_salary int);
```

**Output:**

![image](https://github.com/user-attachments/assets/24d465c4-3abb-43d5-ad98-35721345ccb3)


**Question 3**
---
![image](https://github.com/user-attachments/assets/bf07be15-eb02-406a-bdee-b6811730ea51)


```sql
create table contacts(
contact_id INTEGER primary key,
first_name TEXT not NULL,
last_name  TEXT  not NULL,
email TEXT,
phone  TEXT  not NULL check(length(phone)=10));
```

**Output:**

![image](https://github.com/user-attachments/assets/c224e867-cee6-467a-8ab9-f1888906e560)


**Question 4**
---
![image](https://github.com/user-attachments/assets/60f7acb0-62ae-4405-92c4-97f7d0df15fc)


```sql
insert into Employee(EmployeeID,Name,Position)values(5,'George Clark','Consultant');
insert into Employee(EmployeeID,Name,Position,Department,Salary)values(7,'Noah Davis','Manager','HR',60000);
insert into Employee(EmployeeID,Name,Position,Department)values(8,'Ava Miller','Consultant','IT');
```

**Output:**

![image](https://github.com/user-attachments/assets/c84e6469-5dfb-4bd2-ab51-f8d1cea9eb00)


**Question 5**
---
![image](https://github.com/user-attachments/assets/a61f9784-ce8f-4ac0-adc7-f3f17b6dad4b)


```sql
create table Orders(
OrderID INTEGER primary key,
OrderDate  DATE not NULL,
CustomerID INTEGER, 
foreign key(CustomerID) references Customers(CustomerID));
```

**Output:**

![image](https://github.com/user-attachments/assets/db65ce6a-dc2b-4aca-acfd-f88e2b36f533)


**Question 6**
---
![image](https://github.com/user-attachments/assets/4cb4eded-91e0-4275-bd3f-6c4f557c92e4)


```sql
create table Tasks(
TaskID  INTEGER,
TaskName TEXT,
DueDate DATE);
```

**Output:**

![image](https://github.com/user-attachments/assets/a81961c8-f420-4b39-aedc-29d70d737cef)


**Question 7**
---
![image](https://github.com/user-attachments/assets/15f37d8a-afaa-4d9f-86ca-656864657b6d)


```sql
insert into Employee(EmployeeID,Name,Position)values(4,'Emily White','Analyst');
```

**Output:**

![image](https://github.com/user-attachments/assets/c9e99710-1752-4238-9f7b-c4abc2e11b6b)


**Question 8**
---
![image](https://github.com/user-attachments/assets/27147b0c-e666-4143-81bd-f61cbf4ddaa3)


```sql
insert into  Customers(CustomerID, Name, Address, Email)
select CustomerID, Name, Address, Email
from Old_customers;
```

**Output:**

![image](https://github.com/user-attachments/assets/e32a0275-4c48-424f-a1b4-8cddda9cd44e)


**Question 9**
---
![image](https://github.com/user-attachments/assets/ebf725dd-ada9-4063-807a-cc65635f781e)


```sql
alter table Employees add salary INTEGER check(salary>0);
```

**Output:**

![image](https://github.com/user-attachments/assets/3e61b4fe-acfb-4742-ac1a-b21d0528a2ab)


**Question 10**
---
![image](https://github.com/user-attachments/assets/7ab67193-6fe5-4a6c-af2b-b8c0fe39d108)


```sql
create table Invoices(
InvoiceID INTEGER  primary key,
InvoiceDate DATE,
Amount  REAL check(Amount>0),
DueDate  DATE check(DueDate>InvoiceDate),
OrderID  INTEGER,
foreign key(OrderID) references Orders(OrderID));
```

**Output:**

![image](https://github.com/user-attachments/assets/43ab6c25-6206-42bc-a192-ec52eb6a17d6)

## GRADE
![image](https://github.com/user-attachments/assets/f517a877-e237-457f-822d-a8adcd66f48f)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
