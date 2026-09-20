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

**Steps:**

- Create an `employees` table with fields `emp_id`, `emp_name`, and `designation`.
- Insert some sample data into the table.
- Use a simple cursor to fetch and display employee names and designations.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

### Table Setup:
```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    designation VARCHAR2(50),
    salary NUMBER,
    dept_no NUMBER
);

INSERT INTO employees VALUES (101, 'John Doe', 'Manager', 75000, 10);
INSERT INTO employees VALUES (102, 'Jane Smith', 'Developer', 55000, 20);
INSERT INTO employees VALUES (103, 'Sam Brown', 'Analyst', 45000, 10);
INSERT INTO employees VALUES (104, 'Alice White', 'Clerk', 30000, 30);
COMMIT;
```

### Code:
```
SET SERVEROUTPUT ON;

DECLARE
    v_name employees.emp_name%TYPE;
    v_desig employees.designation%TYPE;
    v_count NUMBER := 0;
    no_records_found EXCEPTION;

    CURSOR emp_cursor IS
        SELECT emp_name, designation FROM employees;
BEGIN
    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO v_name, v_desig;
        EXIT WHEN emp_cursor%NOTFOUND;
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Name: ' || v_name || ', Designation: ' || v_desig);
    END LOOP;
    CLOSE emp_cursor;

    IF v_count = 0 THEN
        RAISE no_records_found;
    END IF;

EXCEPTION
    WHEN no_records_found THEN
        DBMS_OUTPUT.PUT_LINE('Error: No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected Error: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display the employee details or an error message.
<img width="952" height="735" alt="image" src="https://github.com/user-attachments/assets/a862e162-8ce9-4e2d-8d82-3a7600b15776" />

---

### **Question 2: Parameterized Cursor with Exception Handling**

**Write a PL/SQL program using a parameterized cursor to retrieve and display employees with a salary in a given range. Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees meet the salary criteria.
2. **OTHERS**: For any unexpected errors during the execution.

**Steps:**

- Modify the `employees` table by adding a `salary` column.
- Insert sample salary values for the employees.
- Use a parameterized cursor to accept a salary range as input and fetch employees within that range.
- Implement exception handling to catch and display relevant error messages.

### Code:
```
SET SERVEROUTPUT ON;

DECLARE
    v_min_sal NUMBER := 40000;
    v_max_sal NUMBER := 70000;
    v_id employees.emp_id%TYPE;
    v_name employees.emp_name%TYPE;
    v_sal employees.salary%TYPE;
    v_count NUMBER := 0;
    no_records_found EXCEPTION;

    CURSOR emp_range_cursor (min_s NUMBER, max_s NUMBER) IS
        SELECT emp_id, emp_name, salary 
        FROM employees 
        WHERE salary BETWEEN min_s AND max_s;
BEGIN
    OPEN emp_range_cursor(v_min_sal, v_max_sal);
    LOOP
        FETCH emp_range_cursor INTO v_id, v_name, v_sal;
        EXIT WHEN emp_range_cursor%NOTFOUND;
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('ID: ' || v_id || ', Name: ' || v_name || ', Salary: ' || v_sal);
    END LOOP;
    CLOSE emp_range_cursor;

    IF v_count = 0 THEN
        RAISE no_records_found;
    END IF;

EXCEPTION
    WHEN no_records_found THEN
        DBMS_OUTPUT.PUT_LINE('Error: No employees found in the given salary range.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected Error: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display the employee details within the specified salary range or an error message if no data is found.
<img width="937" height="741" alt="image" src="https://github.com/user-attachments/assets/435f3b2e-5d6d-4102-a2a5-ef99c8865762" />

---

### **Question 3: Cursor FOR Loop with Exception Handling**

**Write a PL/SQL program using a cursor FOR loop to retrieve and display all employee names and their department numbers from the `employees` table. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no employees are found in the database.
2. **OTHERS**: For any other unexpected errors.

**Steps:**

- Modify the `employees` table by adding a `dept_no` column.
- Insert sample department numbers for employees.
- Use a cursor FOR loop to fetch and display employee names along with their department numbers.
- Implement exception handling to catch the relevant exceptions.

### Code:
```
SET SERVEROUTPUT ON;

DECLARE
    v_count NUMBER := 0;
    no_records_found EXCEPTION;

    CURSOR emp_dept_cursor IS
        SELECT emp_name, dept_no FROM employees;
BEGIN
    FOR rec IN emp_dept_cursor LOOP
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('Name: ' || rec.emp_name || ', Dept No: ' || rec.dept_no);
    END LOOP;

    IF v_count = 0 THEN
        RAISE no_records_found;
    END IF;

EXCEPTION
    WHEN no_records_found THEN
        DBMS_OUTPUT.PUT_LINE('Error: No employees found in the database.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected Error: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display employee names with their department numbers or the appropriate error message if no data is found.
<img width="943" height="748" alt="image" src="https://github.com/user-attachments/assets/4e10738a-0ea4-4033-849a-c1d70d51c154" />

---

### **Question 4: Cursor with `%ROWTYPE` and Exception Handling**

**Write a PL/SQL program that uses a cursor with `%ROWTYPE` to fetch and display complete employee records (emp_id, emp_name, designation, salary). Implement exception handling for the following errors:**

1. **NO_DATA_FOUND**: When no employees are found in the database.
2. **OTHERS**: For any other errors that occur.

**Steps:**

- Modify the `employees` table by adding `emp_id`, `emp_name`, `designation`, and `salary` fields.
- Insert sample data into the `employees` table.
- Declare a cursor using `%ROWTYPE` to fetch complete rows from the `employees` table.
- Implement exception handling to catch the relevant exceptions and display appropriate messages.

### Code:
```
SET SERVEROUTPUT ON;

DECLARE
    CURSOR emp_row_cursor IS
        SELECT * FROM employees;

    emp_rec emp_row_cursor%ROWTYPE;
    v_count NUMBER := 0;
    no_records_found EXCEPTION;
BEGIN
    OPEN emp_row_cursor;
    LOOP
        FETCH emp_row_cursor INTO emp_rec;
        EXIT WHEN emp_row_cursor%NOTFOUND;
        v_count := v_count + 1;
        DBMS_OUTPUT.PUT_LINE('ID: ' || emp_rec.emp_id || 
                             ', Name: ' || emp_rec.emp_name || 
                             ', Desig: ' || emp_rec.designation || 
                             ', Salary: ' || emp_rec.salary || 
                             ', Dept: ' || emp_rec.dept_no);
    END LOOP;
    CLOSE emp_row_cursor;

    IF v_count = 0 THEN
        RAISE no_records_found;
    END IF;

EXCEPTION
    WHEN no_records_found THEN
        DBMS_OUTPUT.PUT_LINE('Error: No employee records found.');
    WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('Unexpected Error: ' || SQLERRM);
END;
/
```

**Output:**  
The program should display employee records or the appropriate error message if no data is found.
<img width="943" height="745" alt="image" src="https://github.com/user-attachments/assets/cbd2653a-3e72-4bfa-954e-5d09440c9aba" />

---

### **Question 5: Cursor with FOR UPDATE Clause and Exception Handling**

**Write a PL/SQL program using a cursor with the `FOR UPDATE` clause to update the salary of employees in a specific department. Implement exception handling for the following cases:**

1. **NO_DATA_FOUND**: If no rows are affected by the update.
2. **OTHERS**: For any unexpected errors during execution.

**Steps:**

- Modify the `employees` table to include a `dept_no` and `salary` field.
- Insert sample data into the `employees` table with different department numbers.
- Use a cursor with the `FOR UPDATE` clause to lock the rows of employees in a specific department and update their salary.
- Implement exception handling to handle `NO_DATA_FOUND` or other errors that may occur.

### Code:
```
SET SERVEROUTPUT ON;

DECLARE
    v_target_dept NUMBER := 10;
    v_count NUMBER := 0;
    no_records_found EXCEPTION;

    CURSOR update_sal_cursor IS
        SELECT emp_id, salary 
        FROM employees 
        WHERE dept_no = v_target_dept 
        FOR UPDATE OF salary;
BEGIN
    FOR rec IN update_sal_cursor LOOP
        v_count := v_count + 1;
        UPDATE employees
        SET salary = salary + 5000
        WHERE CURRENT OF update_sal_cursor;
    END LOOP;

    IF v_count = 0 THEN
        RAISE no_records_found;
    ELSE
        COMMIT;
        DBMS_OUTPUT.PUT_LINE('Successfully updated salaries for ' || v_count || ' employee(s) in Dept ' || v_target_dept);
    END IF;

EXCEPTION
    WHEN no_records_found THEN
        ROLLBACK;
        DBMS_OUTPUT.PUT_LINE('Error: No employees found in department ' || v_target_dept || ' to update.');
    WHEN OTHERS THEN
        ROLLBACK;
        DBMS_OUTPUT.PUT_LINE('Unexpected Error: ' || SQLERRM);
END;
/
```

**Output:**  
The program should update employee salaries and display a message, or it should display an error message if no data is found.
<img width="945" height="750" alt="image" src="https://github.com/user-attachments/assets/62fcfb28-4379-4e60-97cf-d25180d473c8" />

---

## RESULT
Thus, the program successfully executed and displayed employee details using a cursor. 
