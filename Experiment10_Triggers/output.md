# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
### Steps:
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.

### Code:
```
CREATE TABLE employees (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE TABLE employee_log (
    log_id NUMBER GENERATED ALWAYS AS IDENTITY,
    emp_id NUMBER,
    action_date DATE,
    action_type VARCHAR2(20)
);

CREATE OR REPLACE TRIGGER trg_log_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log (emp_id, action_date, action_type)
    VALUES (:NEW.emp_id, SYSDATE, 'INSERT');
END;
/

INSERT INTO employees VALUES (101, 'Alice', 5000);
SELECT * FROM employee_log;
```

### Expected Output:
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

### Output:
<img width="948" height="757" alt="image" src="https://github.com/user-attachments/assets/f6f23c00-4bcf-4db9-b261-21653ad98f67" />

---

## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

### Code:
```
CREATE TABLE sensitive_data (
    id NUMBER PRIMARY KEY,
    secret_info VARCHAR2(100)
);

INSERT INTO sensitive_data VALUES (1, 'Confidential Project Key');

CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
END;
/

DELETE FROM sensitive_data WHERE id = 1;
```

### Expected Output:
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

### Output:
<img width="942" height="752" alt="image" src="https://github.com/user-attachments/assets/c9b84332-51ac-4f68-af69-bbe487c51fd0" />

---

## 3. Write a trigger to automatically update a `last_modified` timestamp.
### Steps:
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

### Code:
```
CREATE TABLE products (
    product_id NUMBER PRIMARY KEY,
    product_name VARCHAR2(50),
    price NUMBER,
    last_modified DATE
);

INSERT INTO products VALUES (1, 'Laptop', 1200, SYSDATE);

CREATE OR REPLACE TRIGGER trg_update_timestamp
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSDATE;
END;
/

UPDATE products SET price = 1100 WHERE product_id = 1;
SELECT * FROM products;
```

### Expected Output:
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

### Output:
<img width="960" height="753" alt="image" src="https://github.com/user-attachments/assets/83e60322-66fd-4364-bb42-b61b5a8f0935" />

---

## 4. Write a trigger to keep track of the number of updates made to a table.
### Steps:
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

### Code:
```
CREATE TABLE customer_orders (
    order_id NUMBER PRIMARY KEY,
    customer_name VARCHAR2(50),
    status VARCHAR2(20)
);

CREATE TABLE audit_log (
    table_name VARCHAR2(50),
    update_count NUMBER
);

INSERT INTO audit_log VALUES ('CUSTOMER_ORDERS', 0);
INSERT INTO customer_orders VALUES (101, 'Bob', 'Pending');

CREATE OR REPLACE TRIGGER trg_count_updates
AFTER UPDATE ON customer_orders
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1
    WHERE table_name = 'CUSTOMER_ORDERS';
END;
/

UPDATE customer_orders SET status = 'Shipped' WHERE order_id = 101;
SELECT * FROM audit_log;
```

### Expected Output:
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

### Output:
<img width="947" height="750" alt="Screenshot 2026-08-24 213904" src="https://github.com/user-attachments/assets/a4523f83-e753-44a2-a2b7-76fca0c1efb3" />

---

## 5. Write a trigger that checks a condition before allowing insertion into a table.
### Steps:
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

### Code:
```
CREATE TABLE emp_records (
    emp_id NUMBER PRIMARY KEY,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT ON emp_records
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(-20002, 'ERROR: Salary below minimum threshold.');
    END IF;
END;
/

INSERT INTO emp_records VALUES (201, 'Charlie', 2500);
```

### Expected Output:
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

### Output:
<img width="1796" height="876" alt="image" src="https://github.com/user-attachments/assets/08b529f1-5fb6-4f43-89a9-b70f7f08d992" />



## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
