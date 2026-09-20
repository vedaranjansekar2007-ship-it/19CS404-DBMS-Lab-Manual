# Experiment 6: Joins

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
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id    
        3002 | Nick Rimando   | New York   |   100 |        5001  
        3007 | Brad Davis     | New York   |   200 |        5001  
        3005 | Graham Zusi    | California |   200 |        5002  
        3008 | Julian Green   | London     |   300 |        5002  
        3004 | Fabian Johnson | Paris      |   300 |        5006  
        3009 | Geoff Cameron  | Berlin     |   100 |        5003  
        3003 | Jozy Altidor   | Moscow     |   200 |        5007  
        3001 | Brad Guzan     | London     |       |        5005  
        
Sample table: salesman

 salesman_id |    name    |   city   | commission    
        5001 | James Hoog | New York |       0.15  
        5002 | Nail Knite | Paris    |       0.13  
        5005 | Pit Alex   | London   |       0.11  
        5006 | Mc Lyon    | Paris    |       0.14  
        5007 | Paul Adam  | Rome     |       0.13  
        5003 | Lauson Hen | San Jose |       0.12  

```sql
SELECT 
C.cust_name AS 'Customer Name',
C.city,
S.name AS 'Salesman',
S.city AS 'city',
S.commission 
FROM customer AS C
JOIN salesman AS S
ON C.salesman_id = S.salesman_id
WHERE C.city <> S.city AND S.commission > 0.12;
```

**Output:**  
<img width="1150" height="431" alt="image" src="https://github.com/user-attachments/assets/e58cd057-fe05-4cfd-a851-f45fd8a9a991" />

**Question 2**
---
Write an SQL query to select all columns from the 'customer' table (aliased as 'c') by performing a LEFT JOIN with the 'orders' table on the 'customer_id' column, including only those orders where the order date falls between '2012-08-01' and '2012-08-30'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT 
c.customer_id, c.cust_name, c.city, c.grade, c.salesman_id
FROM customer AS c 
LEFT JOIN orders AS o 
ON c.customer_id = o.customer_id
WHERE o.ord_date BETWEEN '2012-08-01' AND '2012-08-30';
```

**Output:**  
<img width="1167" height="310" alt="image" src="https://github.com/user-attachments/assets/6584cdc2-4a69-465b-9360-cbd0b3b653a2" />

**Question 3**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id  
        3002 | Nick Rimando   | New York   |   100 |        5001  
        3007 | Brad Davis     | New York   |   200 |        5001  
        3005 | Graham Zusi    | California |   200 |        5002  
        3008 | Julian Green   | London     |   300 |        5002  
        3004 | Fabian Johnson | Paris      |   300 |        5006  
        3009 | Geoff Cameron  | Berlin     |   100 |        5003  
        3003 | Jozy Altidor   | Moscow     |   200 |        5007  
        3001 | Brad Guzan     | London     |       |        5005  
        
Sample table: salesman

 salesman_id |    name    |   city   | commission  
        5001 | James Hoog | New York |       0.15  
        5002 | Nail Knite | Paris    |       0.13  
        5005 | Pit Alex   | London   |       0.11  
        5006 | Mc Lyon    | Paris    |       0.14  
        5007 | Paul Adam  | Rome     |       0.13  
        5003 | Lauson Hen | San Jose |       0.12  

```sql
SELECT 
c.cust_name, c.city, c.grade, s.name AS Salesman, s.city
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE c.grade < 300
ORDER BY c.customer_id;
```

**Output:**  
<img width="1153" height="547" alt="image" src="https://github.com/user-attachments/assets/73fac803-2ac3-4fcd-bdb8-56206937b351" />

**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

NURSES TABLE:

ATTRIBUTES - nurse_id, first_name, last_name, department_id

DEPARTMENTS TABLE:

ATTRIBUTES - department_id, department_name

```sql
SELECT 
n.nurse_id, n.first_name, n.last_name, n.department_id, d.department_name
FROM NURSES n
INNER JOIN DEPARTMENTS d
ON n.department_id = d.department_id;
```

**Output:**
<img width="1222" height="365" alt="image" src="https://github.com/user-attachments/assets/4693f3c3-241e-45af-a317-9d59fb0424b3" />

**Question 5**
---
From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id  
        3002 | Nick Rimando   | New York   |   100 |        5001  
        3007 | Brad Davis     | New York   |   200 |        5001  
        3005 | Graham Zusi    | California |   200 |        5002  
        3008 | Julian Green   | London     |   300 |        5002  
        3004 | Fabian Johnson | Paris      |   300 |        5006  
        3009 | Geoff Cameron  | Berlin     |   100 |        5003  
        3003 | Jozy Altidor   | Moscow     |   200 |        5007  
        3001 | Brad Guzan     | London     |       |        5005  
        
Sample table: salesman

 salesman_id |    name    |   city   | commission  
        5001 | James Hoog | New York |       0.15  
        5002 | Nail Knite | Paris    |       0.13  
        5005 | Pit Alex   | London   |       0.11  
        5006 | Mc Lyon    | Paris    |       0.14  
        5007 | Paul Adam  | Rome     |       0.13  
        5003 | Lauson Hen | San Jose |       0.12  

```sql
SELECT 
c.cust_name AS 'Customer Name', c.city, s.name AS 'Salesman', s.commission 
FROM customer c
JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE s.commission > 0.12;
```

**Output:** 
<img width="1097" height="613" alt="image" src="https://github.com/user-attachments/assets/749357c9-7350-4b4f-9d1a-0cd980a72cc2" />

**Question 6**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id  
        3002 | Nick Rimando   | New York   |   100 |        5001  
        3007 | Brad Davis     | New York   |   200 |        5001  
        3005 | Graham Zusi    | California |   200 |        5002  
        3008 | Julian Green   | London     |   300 |        5002  
        3004 | Fabian Johnson | Paris      |   300 |        5006  
        3009 | Geoff Cameron  | Berlin     |   100 |        5003  
        3003 | Jozy Altidor   | Moscow     |   200 |        5007  
        3001 | Brad Guzan     | London     |       |        5005  
        
Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id  
70001       150.5       2012-10-05  3005         5002  
70009       270.65      2012-09-10  3001         5005  
70002       65.26       2012-10-05  3002         5001  
70004       110.5       2012-08-17  3009         5003  
70007       948.5       2012-09-10  3005         5002  
70005       2400.6      2012-07-27  3007         5001  
70008       5760        2012-09-10  3002         5001  
70010       1983.43     2012-10-10  3004         5006  
70003       2480.4      2012-10-10  3009         5003  
70012       250.45      2012-06-27  3008         5002  
70011       75.29       2012-08-17  3003         5007  
70013       3045.6      2012-04-25  3002         5001  

```sql
SELECT o.ord_no, o.purch_amt, c.cust_name, c.city
FROM orders o
JOIN customer c
ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**  
<img width="1101" height="346" alt="image" src="https://github.com/user-attachments/assets/1da4688c-3bd1-430f-8636-193ee216396a" />

**Question 7**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

 salesman_id |    name    |   city   | commission   
        5001 | James Hoog | New York |       0.15  
        5002 | Nail Knite | Paris    |       0.13  
        5005 | Pit Alex   | London   |       0.11  
        5006 | Mc Lyon    | Paris    |       0.14  
        5007 | Paul Adam  | Rome     |       0.13  
        5003 | Lauson Hen | San Jose |       0.12  
        
Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id  
        3002 | Nick Rimando   | New York   |   100 |        5001  
        3007 | Brad Davis     | New York   |   200 |        5001  
        3005 | Graham Zusi    | California |   200 |        5002  
        3008 | Julian Green   | London     |   300 |        5002  
        3004 | Fabian Johnson | Paris      |   300 |        5006  
        3009 | Geoff Cameron  | Berlin     |   100 |        5003  
        3003 | Jozy Altidor   | Moscow     |   200 |        5007  
        3001 | Brad Guzan     | London     |       |        5005  

```sql
SELECT s.name AS 'Salesman', c.cust_name, c.city
FROM salesman s
JOIN customer c
ON s.city = c.city;
```

**Output:**  
<img width="915" height="606" alt="image" src="https://github.com/user-attachments/assets/a33beb9b-6368-44af-965a-312b9add26b4" />

**Question 8**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the first name from the "doctors" table (aliased as "doctor_name"), with an inner join on the "doctor_id" column and a condition filtering for patients with a null discharge date.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

DOCTORS TABLE:

ATTRIBUTES - doctor_id, first_name, last_name, specialization

```sql
SELECT p.first_name AS 'patient_name', d.first_name AS 'doctor_name'
FROM PATIENTS p
INNER JOIN DOCTORS d
ON p.doctor_id = d.doctor_id
WHERE p.discharge_date IS NULL;
```

**Output:**  
<img width="610" height="387" alt="image" src="https://github.com/user-attachments/assets/7f3f3e4a-1ae6-4132-b028-02fa177711fc" />

**Question 9**
---
Write an SQL query to retrieve all columns from the 'customer' table (aliased as 'c') using a LEFT JOIN with the 'orders' table on the 'customer_id' column, and filter the results to include only those orders placed between '2012-07-01' and '2012-07-30'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```sql
SELECT 
c.customer_id, c.cust_name, c.city, c.grade, c.salesman_id
FROM customer c 
LEFT JOIN orders o 
ON c.customer_id = o.customer_id
WHERE o.ord_date BETWEEN '2012-07-01' AND '2012-07-30';
```

**Output:**  
<img width="1167" height="252" alt="image" src="https://github.com/user-attachments/assets/1d06b3c0-212c-484b-a7d3-8929c6ecb230" />

**Question 10**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:

name             type  
patient_id       INT  
first_name       VARCHAR(50)  
last_name        VARCHAR(50)  
date_of_birth    DATE  
admission_date   DATE  
discharge_date   DATE  
doctor_id        INT  

SURGERIES TABLE:

name             type  
surgery_id       INT  
patient_id       INT  
surgeon_id       INT  
surgery_date     DATE  

```sql
SELECT p.first_name, s.*
FROM PATIENTS p
INNER JOIN SURGERIES s
ON p.patient_id = s.patient_id
WHERE p.first_name LIKE 'Alice';
```

**Output:**  
<img width="1180" height="253" alt="image" src="https://github.com/user-attachments/assets/3522530d-d19b-46b4-9a84-bdaf43188310" />

## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
