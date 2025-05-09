# Experiment 7: PL/SQL – Variables, Control Structures and Loops

## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

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

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

## Program:

```
DECLARE
   num1 NUMBER := 45;
   num2 NUMBER := 80;
BEGIN
   IF num1 > num2 THEN
      DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num1);
   ELSE
      DBMS_OUTPUT.PUT_LINE('Greater number is: ' || num2);
   END IF;
END;

```

## Output:

![Screenshot 2025-05-08 143651](https://github.com/user-attachments/assets/a0607095-4695-4e32-af03-261cf8b43fc9)


## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

## Program:

```
DECLARE
   n   NUMBER := 10;
   i   NUMBER := 1;
   sum NUMBER := 0;
BEGIN
   WHILE i <= n LOOP
      sum := sum + i;
      i := i + 1;
   END LOOP;

   DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || sum);
END;

```

## Output:

![Screenshot 2025-05-08 144017](https://github.com/user-attachments/assets/fc13bfd1-3dcb-44f1-af5f-928d778df65a)


## 3. Write a PL/SQL program to generate Fibonacci series

## Program:

```
DECLARE
   n   NUMBER := 7;      -- Number of terms to generate
   a   NUMBER := 0;
   b   NUMBER := 1;
   c   NUMBER;
   i   NUMBER := 3;      -- Start from 3rd term since first two are fixed
BEGIN
   DBMS_OUTPUT.PUT_LINE('Fibonacci sequence:');
   DBMS_OUTPUT.PUT_LINE(a);
   DBMS_OUTPUT.PUT_LINE(b);

   WHILE i <= n LOOP
      c := a + b;
      DBMS_OUTPUT.PUT_LINE(c);
      a := b;
      b := c;
      i := i + 1;
   END LOOP;
END;
```

## Output:

![Screenshot 2025-05-08 144351](https://github.com/user-attachments/assets/18dc6753-ba74-4a05-9ce2-bcc1f963ae73)


## 4. Write a PL/SQL Program to display the number in Reverse Order

## Program:

```
DECLARE
    n NUMBER := 1535;
    temp NUMBER;
    rev NUMBER := 0;
    digit NUMBER;
BEGIN
    temp := n;
    WHILE temp > 0 LOOP
        digit := MOD(temp, 10);           -- Get last digit
        rev := rev * 10 + digit;          -- Build reversed number
        temp := TRUNC(temp / 10);         -- Remove last digit
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('n = ' || n);
    DBMS_OUTPUT.PUT_LINE('Reversed number is ' || rev);
END;

```

## Output:

![Screenshot 2025-05-08 154342](https://github.com/user-attachments/assets/511abc1c-6295-4771-abd1-b981a542dcb4)


## 5. Write a PL/SQL program to find the largest of three numbers

## Program:

```

DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
    largest NUMBER;
BEGIN
    IF (a >= b) AND (a >= c) THEN
        largest := a;
    ELSIF (b >= a) AND (b >= c) THEN
        largest := b;
    ELSE
        largest := c;
    END IF;

    DBMS_OUTPUT.PUT_LINE('a = ' || a || ', b = ' || b || ', c = ' || c);
    DBMS_OUTPUT.PUT_LINE('Largest of three number is ' || largest);
END;

```
## Output:

![Screenshot 2025-05-08 154635](https://github.com/user-attachments/assets/aab96cf1-b4f3-44d0-85be-c692cb267c97)


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
