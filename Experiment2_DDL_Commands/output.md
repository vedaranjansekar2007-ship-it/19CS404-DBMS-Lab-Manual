# Experiment 2: DDL Commands

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
Create a new table named item with the following specifications and constraints:  
item_id as TEXT and as primary key.  
item_desc as TEXT.  
rate as INTEGER.  
icom_id as TEXT with a length of 4.  
icom_id is a foreign key referencing com_id in the company table.  
The foreign key should cascade updates and deletes.  
item_desc and rate should not accept NULL.  

```sql
CREATE TABLE item(
item_id TEXT PRIMARY KEY,
item_desc TEXT NOT NULL,
rate INTEGER NOT NULL,
icom_id TEXT(4),
FOREIGN KEY (icom_id) REFERENCES company(com_id) ON UPDATE CASCADE ON DELETE CASCADE
);
```

**Output:**
<img width="1032" height="250" alt="image" src="https://github.com/user-attachments/assets/901ec2ba-33b1-4ffb-a05e-857fdf61a28c" />
<img width="447" height="250" alt="image" src="https://github.com/user-attachments/assets/dbaa4536-c8c7-408c-8919-a7914608b524" />

**Question 2**
---
Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'

```sql
ALTER TABLE books ADD COLUMN ISBN varchar(30);
ALTER TABLE books ADD COLUMN domain_dept varchar(30);
```

**Output:**
<img width="953" height="282" alt="image" src="https://github.com/user-attachments/assets/e8071940-cb7c-4a14-af18-0ce9f36800c6" />
<img width="645" height="280" alt="image" src="https://github.com/user-attachments/assets/9fac07f5-00a5-4521-8ed1-bf2100041e06" />

**Question 3**
---
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

```sql
INSERT into Customers(CustomerID, Name, Address, City, ZipCode)
values(301, 'Michael Jordan', '123 Maple St', 'Chicago', 60616);
```

**Output:**
<img width="1077" height="135" alt="image" src="https://github.com/user-attachments/assets/c366c458-29d2-4dd5-beea-0f100a45ec4d" />
<img width="537" height="117" alt="image" src="https://github.com/user-attachments/assets/273ec4cf-8f99-4001-a696-04a0678d2299" />

**Question 4**
---
Create a table named ProjectAssignments with the following constraints:  
AssignmentID as INTEGER should be the primary key.  
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).  
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).  
AssignmentDate as DATE should be NOT NULL.  

```sql
CREATE TABLE ProjectAssignments(
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER REFERENCES Employees(EmployeeID),
ProjectID INTEGER REFERENCES Projects(ProjectID),
AssignmentDate DATE NOT NULL
);
```

**Output:**
<img width="1117" height="178" alt="image" src="https://github.com/user-attachments/assets/961ee3c0-e249-482c-917d-40c4fd09ad21" />
<img width="970" height="177" alt="image" src="https://github.com/user-attachments/assets/c3ab9a29-ce3b-44ed-a2bb-d355bac35fbd" />

**Question 5**
---
Create a table named Reviews with the following columns:  
ReviewID as INTEGER  
ProductID as INTEGER  
Rating as REAL  
ReviewText as TEXT  

```sql
CREATE TABLE Reviews(
ReviewID INTEGER,
ProductID INTEGER,
Rating REAL,
ReviewText TEXT
);
```

**Output:**

<img width="565" height="297" alt="image" src="https://github.com/user-attachments/assets/5bd4bd16-cae1-4ea2-9f55-8f23e64d3076" />
<img width="648" height="297" alt="image" src="https://github.com/user-attachments/assets/c630e624-ad88-414a-aa22-91d666165cb2" />
<img width="646" height="293" alt="image" src="https://github.com/user-attachments/assets/e208498c-deaf-4a70-bc25-07751925c410" />

**Question 6**
---
Insert the following students into the Student_details table:  
RollNo      Name        Gender      Subject     MARKS  
202            Ella King         F           Chemistry   87  
203            James Bond   M          Literature    78  

```sql
INSERT into Student_details
values(202, 'Ella King', 'F', 'Chemistry', 87),
      (203, 'James Bond', 'M', 'Literature', 78);
```

**Output:**

<img width="285" height="152" alt="image" src="https://github.com/user-attachments/assets/dd49d72d-b145-4010-8921-126606a87bd8" />
<img width="1078" height="157" alt="image" src="https://github.com/user-attachments/assets/b2f8defe-0948-452d-a2bc-87f5b4aadf27" />

**Question 7**
---
Create a table named Bonuses with the following constraints:  
BonusID as INTEGER should be the primary key.  
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).  
BonusAmount as REAL should be greater than 0.  
BonusDate as DATE.  
Reason as TEXT should not be NULL.  

```sql
CREATE TABLE Bonuses(
BonusID INTEGER PRIMARY KEY,
EmployeeID INTEGER REFERENCES Employees(EmployeeID),
BonusAmount REAL CHECK(BonusAmount > 0),
BonusDate DATE,
Reason TEXT NOT NULL
);
```

**Output:**
<img width="1132" height="157" alt="image" src="https://github.com/user-attachments/assets/5d69f170-75ac-46c8-b003-0725fea8a419" />
<img width="1198" height="160" alt="image" src="https://github.com/user-attachments/assets/c0e625bf-6494-41ef-a526-7a18ecde3d95" />

**Question 8**
---
Create a new table named orders with the following specifications:  
ord_id as TEXT with a length of 4.  
item_id as TEXT.  
ord_date as DATE.  
ord_qty as INTEGER.  
cost as INTEGER.  
The primary key is a composite key consisting of item_id and ord_date.  
ord_id and item_id should not accept NULL  

```sql
CREATE TABLE orders(
ord_id TEXT NOT NULL CHECK(LENGTH(ord_id) = 4),
item_id TEXT NOT NULL,
ord_date DATE NOT NULL,
ord_qty INTEGER,
cost INTEGER,
PRIMARY KEY(item_id, ord_date)
);
```

**Output:**

<img width="997" height="221" alt="image" src="https://github.com/user-attachments/assets/01f8c1c0-bb0c-48a2-94e0-ac1b1de8057c" />
<img width="1076" height="220" alt="image" src="https://github.com/user-attachments/assets/b90b6c92-a997-4df1-b143-76117e0b0536" />

**Question 9**
---
Write an SQL command can to add a column named email of type TEXT to the customers table

```sql
ALTER TABLE customers ADD COLUMN email TEXT;
```

**Output:**

<img width="292" height="182" alt="image" src="https://github.com/user-attachments/assets/93ab4b30-cceb-4bb0-8cdd-0408cc2977b4" />
<img width="1165" height="165" alt="image" src="https://github.com/user-attachments/assets/d6ac9092-540e-4d65-af41-9b36641ff811" />

**Question 10**
---
Insert all customers from Old_customers into Customers
Table attributes are CustomerID, Name, Address, Email

```sql
INSERT into Customers(CustomerID, Name, Address, Email)
SELECT CustomerID, Name, Address, Email 
FROM Old_customers;
```

**Output:**

<img width="233" height="182" alt="image" src="https://github.com/user-attachments/assets/22394e6b-513c-4acb-90af-09d7b096e778" />
<img width="1102" height="165" alt="image" src="https://github.com/user-attachments/assets/45ee7c5b-b2b3-4e1e-af17-b27b8be019d1" />

## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
