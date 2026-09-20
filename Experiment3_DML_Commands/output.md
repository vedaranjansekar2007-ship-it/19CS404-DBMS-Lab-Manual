# Experiment 3: DML Commands

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
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.  

PRODUCTS TABLE  
name               type  
product_id         INT  
product_name       VARCHAR(100)  
category           VARCHAR(50)  
cost_price         DECIMAL(10,2)  
sell_price         DECIMAL(10,2)  
reorder_lvl        INT  
quantity           INT  
supplier_id        INT  

```sql
UPDATE PRODUCTS SET reorder_lvl = 40 WHERE category = 'Grocery';
```

**Output:**  
<img width="447" height="297" alt="Screenshot 2026-09-01 212204" src="https://github.com/user-attachments/assets/7d825761-2b74-4ff2-adbe-83e87818133b" />
<img width="992" height="297" alt="Screenshot 2026-09-01 212215" src="https://github.com/user-attachments/assets/4a7a9a86-8ab5-4416-96d0-76afbc0ac4fe" />
<img width="986" height="297" alt="Screenshot 2026-09-01 212228" src="https://github.com/user-attachments/assets/a3d4d95b-ddf7-4066-8459-52bc7391cb1a" />

**Question 2**
---
Write a SQL statement to Update the grade of all customers in Chennai city as  5.   
Customer table (customer_id,cust_name,city,grade,salesman_id)

```sql
UPDATE Customer SET grade = 5 WHERE city = 'Chennai';
```

**Output:**  
<img width="412" height="367" alt="image" src="https://github.com/user-attachments/assets/11a8ef38-1cf9-4503-839f-0f4387bf516d" />
<img width="1037" height="332" alt="image" src="https://github.com/user-attachments/assets/3a8a1000-ee2a-4287-b8c7-545347017048" />

**Question 3**
---
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

```sql
DELETE FROM Customer WHERE (GRADE = 3 OR AGENT_CODE = 'A008') AND OUTSTANDING_AMT < 5000;
```

**Output:**  
<img width="152" height="267" alt="image" src="https://github.com/user-attachments/assets/58329cb9-d594-4dde-b9e4-ee8fee4f4b4f" />
<img width="1122" height="238" alt="image" src="https://github.com/user-attachments/assets/f64cfc85-6072-4f31-bcda-abf82313e23f" />
<img width="1127" height="238" alt="image" src="https://github.com/user-attachments/assets/7f02e957-bc3a-4688-a864-5ce5f9e612ad" />

**Question 4**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_CITY' is not 'New York' and 'OUTSTANDING_AMT' is greater than 5000.

```sql
DELETE FROM Customer WHERE CUST_CITY != 'New York' AND OUTSTANDING_AMT > 5000;
```

**Output:**  
<img width="170" height="493" alt="image" src="https://github.com/user-attachments/assets/451a04c1-3df5-4089-9925-2f38fddb1c38" />
<img width="1122" height="397" alt="image" src="https://github.com/user-attachments/assets/7f196434-9bdb-479b-8888-b3b483b4cf36" />
<img width="1122" height="392" alt="image" src="https://github.com/user-attachments/assets/5be69530-6eb0-4595-8397-eca124920893" />


**Question 5**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is less than 2.

```sql
DELETE FROM Customer WHERE GRADE < 2;
```

**Output:**  
<img width="551" height="467" alt="image" src="https://github.com/user-attachments/assets/66616223-6f20-460f-9d2e-fa6c7077f1ce" />

**Question 6**
---
Write a query to fetch the number of employees working in the department ‘HR’.  

EmployeeInfo
EmpID EmpFname EmpLname Department Project Address DOB Gender  
1 Sanjay Mehra HR P1 Hyderabad(HYD) 01/12/1976 M  
2 Ananya Mishra Admin P2 Delhi(DEL) 02/05/1968 F  

```sql
SELECT COUNT(*) FROM Employeeinfo WHERE Department = 'HR';
```

**Output:**  
<img width="212" height="132" alt="image" src="https://github.com/user-attachments/assets/547831a1-bf2d-49ef-94a3-53ff14b17d4a" />

**Question 7**
---
Write a SQL query to calculate the absolute value of the value1 column from the Calculations table.

cid         name        type        notnull     dflt_value  pk   
0           id          INTEGER     0                       1  
1           value1      REAL        0                       0  
2           value2      REAL        0                       0  
3           base        INTEGER     0                       0  
4           exponent    INTEGER     0                       0  
5           number      REAL        0                       0  
6           decimal     REAL        0                       0  

```sql
SELECT id, value1, ABS(value1) AS absolute_value FROM Calculations;
```

**Output:**  
<img width="717" height="208" alt="image" src="https://github.com/user-attachments/assets/092922fc-23f6-43d7-b510-890fd248da92" />

**Question 8**
---
Write a SQL query to calculate the discounted price for products where the discount percentage is greater than 0, and order the results by discounted_price in ascending order. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products  
product_id | original_price | discount_percentage     
101 | 50.00 | 0.10   
102 | 75.00 | 0.00   
103 | 100.00 | 0.20  

```sql
SELECT product_id, original_price, discount_percentage, 
(original_price - (original_price * discount_percentage)) AS discounted_price
FROM Products;
```

**Output:**
<img width="1081" height="165" alt="image" src="https://github.com/user-attachments/assets/a40db792-bccf-41c2-bb9d-f8ce4da04c96" />

**Question 9**
---
Write a SQL query to retrieve the year, month, and day from the hiredate column in the emp table.

```sql
SELECT 
    strftime('%Y', hiredate) AS Year,
    strftime('%m', hiredate) AS Month,
    strftime('%d', hiredate) AS Day
FROM emp;
```

**Output:**  
<img width="643" height="276" alt="image" src="https://github.com/user-attachments/assets/58cea3d2-f666-4445-b87f-ff208da40a18" />

**Question 10**
---
Write a SQL query to retrieve all employee names in lower case.   

Table name: emp  
name        type  
empno       INT  
ename       VARCHAR(100)  
job         VARCHAR(50)  
mgr         INT  
hiredate    DATE  
sal         DECIMAL(10,2)  
comm        DECIMAL(10,2)  
deptno      INT  

```sql
SELECT LOWER(ename) AS EmpName FROM emp;
```

**Output:**  
<img width="212" height="471" alt="image" src="https://github.com/user-attachments/assets/7ae34c6d-d6bc-455b-bb83-9919def1fe29" />

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
