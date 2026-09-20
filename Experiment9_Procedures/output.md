# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

### Code:
```
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE find_square (num IN NUMBER)
IS
    result NUMBER;
BEGIN
    result := num * num;
    DBMS_OUTPUT.PUT_LINE('Square of ' || num || ' is ' || result);
END;
/

BEGIN
    find_square(6);
END;
/
```

### Expected Output:  
Square of 6 is 36

### Output:
<img width="947" height="746" alt="image" src="https://github.com/user-attachments/assets/9173abbb-8bbf-4a21-8581-df3135907a95" />

---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

### Code:
```
SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION get_factorial (num IN NUMBER)
RETURN NUMBER
IS
    fact NUMBER := 1;
BEGIN
    FOR i IN 1..num LOOP
        fact := fact * i;
    END LOOP;
    RETURN fact;
END;
/

BEGIN
    DBMS_OUTPUT.PUT_LINE('Factorial of 5 is ' || get_factorial(5));
END;
/
```

### Expected Output:  
Factorial of 5 is 120

### Output:
<img width="950" height="752" alt="image" src="https://github.com/user-attachments/assets/cb96a6bf-6209-4b1d-b92c-549ffdc37fc0" />

---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

### Code:
```
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE check_even_odd (num IN NUMBER)
IS
BEGIN
    IF MOD(num, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(num || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(num || ' is Odd');
    END IF;
END;
/

BEGIN
    check_even_odd(12);
END;
/
```

### Expected Output: 
12 is Even

### Output:
<img width="950" height="747" alt="image" src="https://github.com/user-attachments/assets/977f126e-3ae3-46a9-ad7b-16cf1d823d2f" />

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

### Code:
```
SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION reverse_number (num IN NUMBER)
RETURN NUMBER
IS
    temp NUMBER := num;
    rev NUMBER := 0;
    rem NUMBER;
BEGIN
    WHILE temp > 0 LOOP
        rem := MOD(temp, 10);
        rev := (rev * 10) + rem;
        temp := TRUNC(temp / 10);
    END LOOP;
    RETURN rev;
END;
/

BEGIN
    DBMS_OUTPUT.PUT_LINE('Reversed number of 1234 is ' || reverse_number(1234));
END;
/
```

### Expected Output: 
Reversed number of 1234 is 4321

### Output:
<img width="952" height="751" alt="image" src="https://github.com/user-attachments/assets/3eb5f716-3ba9-42f0-aac1-c3ed21c132db" />

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

### Code:
```
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE print_table (num IN NUMBER)
IS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || num || ':');
    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(num || ' x ' || i || ' = ' || (num * i));
    END LOOP;
END;
/

BEGIN
    print_table(5);
END;
/
```

### Expected Output:
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

### Output:
<img width="950" height="752" alt="image" src="https://github.com/user-attachments/assets/96135935-69c3-4ec7-b98d-dab3ebf42d2d" />

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
