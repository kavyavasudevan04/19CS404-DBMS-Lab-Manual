# Experiment 8: PL/SQL Cursor Programs

## AIM
To write and execute PL/SQL programs using cursors and exception handling to manage runtime errors effectively and display appropriate messages.

## THEORY

In PL/SQL, cursors are used to handle query result sets row-by-row. 

There are two types of cursors:

- Implicit Cursors: Automatically created by PL/SQL for single-row queries.
- Explicit Cursors: Declared and controlled by the programmer for multi-row queries.

Types of Explicit Cursors:

1. Simple Cursor: Basic cursor to iterate over multiple rows.

2. Parameterized Cursor: Accepts parameters to filter the result dynamically.

3. Cursor FOR Loop: Simplifies cursor operations (open, fetch, close).

4. %ROWTYPE Cursor: Fetches entire row into a record using %ROWTYPE.

5. Cursor with FOR UPDATE: Used for row-level locking and updating the rows while looping.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:

- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

**Exception Handling**

PL/SQL provides a robust mechanism to handle runtime errors using exception handling blocks. When an error occurs during execution, control is passed to the EXCEPTION section, where specific or general errors can be handled gracefully.

### Components of Exception Handling:
- Predefined Exceptions: Automatically raised by PL/SQL for common errors (e.g., NO_DATA_FOUND, TOO_MANY_ROWS, ZERO_DIVIDE).
- User-defined Exceptions: Declared explicitly in the declaration section using the EXCEPTION keyword.
- WHEN OTHERS: A generic handler for all exceptions not handled explicitly.

```sql
BEGIN
   -- Statements
EXCEPTION
   WHEN exception_name THEN
      -- Handling code
   WHEN OTHERS THEN
      -- Handling for unknown errors
END;
```

### **Question 1: Simple Cursor with Exception Handling**

**Write a PL/SQL program using a simple cursor to fetch employee names and designations from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: When no rows are fetched.
2. **OTHERS**: Any other unexpected errors during execution.

**Query:**
```
DECLARE
    CURSOR emp_cursor IS
        SELECT emp_name, designation FROM employees;

    v_emp_name     employees.emp_name%TYPE;
    v_designation  employees.designation%TYPE;

    v_found BOOLEAN := FALSE;  -- Flag to check if any data was fetched
BEGIN
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO v_emp_name, v_designation;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_found := TRUE;  -- At least one row fetched
        DBMS_OUTPUT.PUT_LINE('Name: ' || v_emp_name || ', Designation: ' || v_designation);
    END LOOP;

    CLOSE emp_cursor;

    -- If no rows were fetched
    IF NOT v_found THEN
        RAISE NO_DATA_FOUND;
    END IF;

-- Exception handling
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
```
**Output:**  

![Screenshot 2025-05-19 110342](https://github.com/user-attachments/assets/125c9dc1-f5d2-4a62-bb21-ee0631480991)

---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Query:**
```
DECLARE
    -- Declare the parameterized cursor
    CURSOR emp_cursor(min_sal NUMBER, max_sal NUMBER) IS
        SELECT emp_name, designation, salary
        FROM employees
        WHERE salary BETWEEN min_sal AND max_sal;

    -- Variables to hold fetched values
    v_emp_name     employees.emp_name%TYPE;
    v_designation  employees.designation%TYPE;
    v_salary       employees.salary%TYPE;

    -- Input salary range
    v_min_sal NUMBER := 60000;
    v_max_sal NUMBER := 80000;

    -- Flag to check if any data was fetched
    v_found BOOLEAN := FALSE;

BEGIN
    -- Open and fetch from the parameterized cursor
    FOR emp_rec IN emp_cursor(v_min_sal, v_max_sal) LOOP
        v_found := TRUE;
        DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.emp_name ||
                             ', Designation: ' || emp_rec.designation ||
                             ', Salary: ' || emp_rec.salary);
    END LOOP;

    -- Raise exception if no records found
    IF NOT v_found THEN
        RAISE NO_DATA_FOUND;
    END IF;

-- Exception handling
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the salary range ' ||
                             v_min_sal || ' to ' || v_max_sal || '.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
```
**Output:**  

![Screenshot 2025-05-19 111251](https://github.com/user-attachments/assets/004aa50b-a4b6-4173-b5f7-4c494a90d4b0)


---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Query:**
```
DECLARE
    v_found BOOLEAN := FALSE;  -- Flag to track if any rows are fetched

BEGIN
    -- Cursor FOR loop to fetch and display employee names with department numbers
    FOR emp_rec IN (
        SELECT emp_name, dept_no FROM employees
        WHERE dept_no IS NOT NULL
    ) LOOP
        v_found := TRUE;
        DBMS_OUTPUT.PUT_LINE('Name: ' || emp_rec.emp_name ||
                             ', Department No: ' || emp_rec.dept_no);
    END LOOP;

    -- If no rows were found, raise NO_DATA_FOUND
    IF NOT v_found THEN
        RAISE NO_DATA_FOUND;
    END IF;

-- Exception handling
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found with department numbers.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
```

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.


---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Query:**
```
DECLARE
    -- Cursor to select all employee data
    CURSOR emp_cursor IS
        SELECT * FROM employees;

    -- Record of the same type as a row in employees table
    emp_record employees%ROWTYPE;

    -- Flag to track if any rows are found
    v_found BOOLEAN := FALSE;

BEGIN
    -- Open and loop through the cursor
    OPEN emp_cursor;

    LOOP
        FETCH emp_cursor INTO emp_record;
        EXIT WHEN emp_cursor%NOTFOUND;

        v_found := TRUE;

        DBMS_OUTPUT.PUT_LINE('Emp ID: ' || emp_record.emp_id ||
                             ', Name: ' || emp_record.emp_name ||
                             ', Designation: ' || emp_record.designation ||
                             ', Salary: ₹' || emp_record.salary);
    END LOOP;

    CLOSE emp_cursor;

    -- If no rows found, raise NO_DATA_FOUND
    IF NOT v_found THEN
        RAISE NO_DATA_FOUND;
    END IF;

-- Exception handling
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employee records found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
```
**Output:**  
The program should display employee records or the appropriate error message if no data is found.

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Query:**
```
DECLARE
    -- Cursor to select employees in a specific department and lock the rows
    CURSOR emp_cursor IS
        SELECT emp_id, salary
        FROM employees
        WHERE dept_no = 10
        FOR UPDATE;

    v_found BOOLEAN := FALSE;

BEGIN
    -- Loop through each employee in the cursor
    FOR emp_rec IN emp_cursor LOOP
        v_found := TRUE;

        -- Increase salary by 10%
        UPDATE employees
        SET salary = emp_rec.salary * 1.10
        WHERE emp_id = emp_rec.emp_id;

        DBMS_OUTPUT.PUT_LINE('Updated salary for Emp ID ' || emp_rec.emp_id);
    END LOOP;

    -- If no employees were found in the department, raise exception
    IF NOT v_found THEN
        RAISE NO_DATA_FOUND;
    END IF;

    COMMIT;

-- Exception handling
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('No employees found in the specified department.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('An unexpected error occurred: ' || SQLERRM);
END;
```
**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 

