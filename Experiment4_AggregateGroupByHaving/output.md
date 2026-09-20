# Experiment 4: Aggregate Functions, Group By and Having Clause

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
What is the average duration of insurance coverage for patients covered by each insurance company?

Sample table: Insurance Table 

name               type  
InsuranceID        INTEGER  
PatientID          INTEGER  
InsuranceCompany   TEXT  
PolicyNumber       TEXT  
PolicyHolder       TEXT  
StartDate          DATE  
EndDate            DATE  

```sql
SELECT InsuranceCompany, 
AVG(EndDate-StartDate) AS AvgCoverageDurationDays
FROM Insurance 
GROUP BY InsuranceCompany;
```

**Output:**  
<img width="772" height="587" alt="image" src="https://github.com/user-attachments/assets/fa98c258-61e9-4412-8343-4ae783931048" />

**Question 2**
---
What is the most common diagnosis among patients?  

Sample table: MedicalRecords Table  

```sql
SELECT Diagnosis,
Count(*) AS DiagnosisCount 
FROM MedicalRecords
GROUP BY Diagnosis
ORDER BY DiagnosisCount DESC LIMIT 1;
```

**Output:**  
<img width="700" height="222" alt="image" src="https://github.com/user-attachments/assets/3555adcb-00d6-44d4-8214-d154d2a25746" />

**Question 3**
---
How many male and female doctors are there in each medical specialty?  

Sample table: Doctors Table  

```sql
SELECT Specialty, Gender,
Count(*) AS TotalDoctors
FROM Doctors
GROUP BY Specialty, Gender;
```

**Output:**  
<img width="806" height="566" alt="image" src="https://github.com/user-attachments/assets/9acf2ca8-fe3a-49dc-92a7-b5de2a6b669e" />

**Question 4**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.  

Sample table: customer  

```sql
SELECT COUNT(*) AS COUNT FROM customer WHERE city LIKE 'Noida';
```

**Output:**  
<img width="210" height="221" alt="image" src="https://github.com/user-attachments/assets/50153da6-750f-434e-bc02-ef7b17c72052" />

**Question 5**
---
Write a SQL query to find the difference between the maximum and minimum price of fruits?  

Table: fruits  

name        type  
id          INTEGER  
name        TEXT  
unit        TEXT  
inventory   INTEGER  
price       REAL  

```sql
SELECT MAX(price)-MIN(price) AS price_diff FROM fruits;
```

**Output:**  
<img width="210" height="221" alt="image" src="https://github.com/user-attachments/assets/42a0816f-c54c-4653-8cea-8241dc315fa5" />

**Question 6**
---
Write a SQL query to find the total number of unique cities in the customer table?  

Table: customer  

name        type  
id          INTEGER  
name        TEXT  
city        TEXT  
email       TEXT  
phone       INTEGER  

```sql
SELECT COUNT(DISTINCT city) AS unique_cities FROM customer;
```

**Output:**  
<img width="265" height="225" alt="image" src="https://github.com/user-attachments/assets/c52aae65-d9d0-4921-bc29-e9daee5dfcf7" />

**Question 7**
---
Write a SQL query to find Who has the highest income among employee living in California?  

Table: employee  

name        type  
id          INTEGER  
name        TEXT  
age         INTEGER  
city        TEXT  
income      INTEGER  

```sql
SELECT name, max(income) FROM employee WHERE city = 'California';
```

**Output:**  
<img width="465" height="225" alt="image" src="https://github.com/user-attachments/assets/75169370-264b-422f-a001-28ede2edec42" />

**Question 8**
---
Write the SQL query that achieves the selection of category and calculates the sum of the product of price and category ID as Revenue for each category from the "products" table, and includes only those products where the total revenue is greater than 25.

Sample table: products  

```sql
SELECT category_id,
SUM(price * category_id) AS Revenue
FROM products
GROUP BY category_id;
```

**Output:**  
<img width="445" height="345" alt="image" src="https://github.com/user-attachments/assets/2ea60cc6-fb61-4598-a034-c2cef8dfc274" />

**Question 9**
---
Write the SQL query that performs grouping by age groups and displays the maximum salary for each group, excluding groups where the maximum salary is not greater than 8000. 
Note: Calculate the age group as multiples of 5.  
Eg., 20,22,23 comes in age group 20. 
25,27,29 comes in age group 25.

Sample table: customer1  

```sql
SELECT 
    (age - (age % 5)) AS age_group,
    MAX(salary) 
FROM customer1
GROUP BY (age - (age % 5))
HAVING MAX(salary) > 8000;
```

**Output:**  
<img width="446" height="272" alt="image" src="https://github.com/user-attachments/assets/356e7fdd-bb05-4dbb-965a-334b2afda57e" />

**Question 10**
---
Write the SQL query that accomplishes the grouping of data by age, calculates the average income for each age group, and includes only those age groups where the average income falls between 300,000 and 500,000.  

Sample table: employee  

```sql
SELECT age, AVG(income) 
FROM employee 
GROUP BY age
HAVING AVG(income) BETWEEN 300000 AND 500000;
```

**Output:**  
<img width="446" height="252" alt="image" src="https://github.com/user-attachments/assets/c0c434aa-c6ec-448f-8d4d-9df71e1adc52" />

## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
