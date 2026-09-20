# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1032" height="682" alt="fitness" src="https://github.com/user-attachments/assets/da561460-e66f-4bdf-97b8-56988258a6a2" />

### Entities and Attributes

| Entity           | Attributes (PK, FK)                                                                | Notes                           |
| ---------------- | ---------------------------------------------------------------------------------- | ------------------------------- |
| Member           | **Member_ID (PK),** Name, Membership_Type, Start_Date                              | Stores member information       |
| Program          | **Program_ID (PK),** Program_Name, Duration                                        | Fitness programs offered        |
| Trainer          | **Trainer_ID (PK),** Trainer_Name, Specialization                                  | Trainers assigned to programs   |
| Training_Session | **Session_ID (PK),** Session_Date, Attendance, **Member_ID (FK), Trainer_ID (FK)** | Personal training sessions      |
| Payment          | **Payment_ID (PK),** Amount, Payment_Date, Payment_Type, **Member_ID (FK)**        | Membership and session payments |

### Relationships and Constraints

| Relationship                               | Cardinality                                                                | Participation                      | Notes                                                                     |
| ------------------------------------------ | -------------------------------------------------------------------------- | ---------------------------------- | ------------------------------------------------------------------------- |
| Member joins Program                       | Many-to-Many (M:N)                                                         | Partial                            | A member can join multiple programs, and a program can have many members. |
| Trainer assigned to Program                | Many-to-Many (M:N)                                                         | Total (Program), Partial (Trainer) | Every program has at least one trainer.                                   |
| Member books Training Session with Trainer | Member (1:M), Trainer (1:M), Session belongs to one member and one trainer | Total (Session)                    | A member may book multiple sessions with trainers.                        |
| Member makes Payment                       | One-to-Many (1:M)                                                          | Partial                            | A member can make multiple payments.                                      |



### Assumptions
- Attendance is recorded for every personal training session.
- Each training session involves one member and one trainer.
- Payments include both membership fees and personal training session fees.
---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="1102" height="798" alt="library" src="https://github.com/user-attachments/assets/7ec9892a-ea7c-438b-816e-5703b2f95d3b" />

### Entities and Attributes

| Entity  | Attributes (PK, FK)                                                                               | Notes                                  |
| ------- | ------------------------------------------------------------------------------------------------- | -------------------------------------- |
| Member  | **Member_ID (PK),** Name, Phone, Email                                                            | Library members                        |
| Book    | **Book_ID (PK),** Title, Author, Category                                                         | Books available in the library         |
| Loan    | **Loan_ID (PK),** Loan_Date, Return_Date, Due_Date, Fine_Amount, **Member_ID (FK), Book_ID (FK)** | Records borrowed books                 |
| Event   | **Event_ID (PK),** Event_Name, Event_Date                                                         | Library events                         |
| Speaker | **Speaker_ID (PK),** Speaker_Name, Expertise                                                      | Authors or speakers invited for events |
| Room    | **Room_ID (PK),** Room_Name, Capacity                                                             | Rooms used for events and study        |

### Relationships and Constraints

| Relationship               | Cardinality                     | Participation | Notes                                                                      |
| -------------------------- | ------------------------------- | ------------- | -------------------------------------------------------------------------- |
| Member borrows Book        | Many-to-Many (M:N) through Loan | Partial       | A member can borrow many books, and a book can be borrowed multiple times. |
| Member registers for Event | Many-to-Many (M:N)              | Partial       | Members may register for multiple events.                                  |
| Event has Speaker          | Many-to-Many (M:N)              | Total (Event) | Every event has at least one speaker.                                      |
| Event uses Room            | Many-to-One (M:1)               | Total (Event) | Each event is conducted in one room.                                       |

### Assumptions
- A book can be borrowed by only one member at a time.
- Fine amount is calculated only for overdue books.
- Every event is conducted in a single room but a room can host many events over time.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="1142" height="802" alt="restaurant" src="https://github.com/user-attachments/assets/3fea8ee5-6602-48bd-9af2-5f0cdb985031" />

### Entities and Attributes

| Entity      | Attributes (PK, FK)                                                                                       | Notes                              |
| ----------- | --------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| Customer    | **Customer_ID (PK),** Customer_Name, Phone                                                                | Restaurant customers               |
| Reservation | **Reservation_ID (PK),** Reservation_Date, Reservation_Time, Guests, **Customer_ID (FK), Waiter_ID (FK)** | Table reservations                 |
| Order       | **Order_ID (PK),** Order_Date, Total_Amount, **Reservation_ID (FK)**                                      | Food orders placed by customers    |
| Dish        | **Dish_ID (PK),** Dish_Name, Price, Category                                                              | Menu items                         |
| Bill        | **Bill_ID (PK),** Food_Charges, Service_Charges, Total_Bill, **Reservation_ID (FK)**                      | Billing details                    |
| Waiter      | **Waiter_ID (PK),** Waiter_Name, Shift                                                                    | Restaurant staff serving customers |

### Relationships and Constraints

| Relationship                   | Cardinality        | Participation       | Notes                                                                       |
| ------------------------------ | ------------------ | ------------------- | --------------------------------------------------------------------------- |
| Customer makes Reservation     | One-to-Many (1:M)  | Partial             | A customer may have multiple reservations.                                  |
| Reservation places Order       | One-to-Many (1:M)  | Total (Order)       | Each order belongs to one reservation.                                      |
| Order contains Dish            | Many-to-Many (M:N) | Total (Order)       | An order may contain multiple dishes, and a dish can appear in many orders. |
| Reservation assigned to Waiter | Many-to-One (M:1)  | Total (Reservation) | Each reservation is served by one waiter.                                   |
| Reservation generates Bill     | One-to-One (1:1)   | Total               | One bill is generated for each completed reservation.                       |

### Assumptions
- Walk-in customers are also recorded as reservations.
- Each reservation is served by one waiter.
- One bill is generated for each reservation after all orders are completed.

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
