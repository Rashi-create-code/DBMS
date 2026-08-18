# Lab Practice : Library Management System Architecture

This repository contains the complete ER Model design, Object-Oriented Class Diagram, and relational schema mappings for the **Library Management System**.

---

## Question 1: Entity-Relationship (ER) Model

![Library ER Diagram](./ER_Model.png)

### 1. Entities & Attributes
* **LIBRARY**: `Lib_ID` (**PK**), `Name`, `City`
* **STAFF**: `Staff_ID` (**PK**), `Name`, `Salary`
* **MEMBER**: `Member_ID` (**PK**), `Name`, `Phone`
* **BOOK**: `Book_ID` (**PK**), `Title`, `Author`
* **LOAN**: `Loan_ID` (**PK**), `Issue_Date`, `Due_Date`

### 2. Relationships & Cardinalities
* **1:1 (`LIBRARY` $\leftrightarrow$ `STAFF`)**: One Library branch is managed by one key Staff member (`manages`).
* **1:N (`LIBRARY` $\rightarrow$ `BOOK`)**: One Library branch owns multiple Books (`owns`).
* **1:N (`STAFF` $\rightarrow$ `MEMBER`)**: One Staff member registers multiple Members (`registers`).
* **M:N (`MEMBER` $\leftrightarrow$ `BOOK`)**: Members borrow multiple Books over time (`borrows`).
  * *Relational Decomposition*: The **M:N** relationship is decomposed into two **1:N** relationships using **`LOAN`** as a junction entity:
    * `MEMBER` $\rightarrow$ `LOAN` (**1:N**)
    * `BOOK` $\rightarrow$ `LOAN` (**1:N**)

### 3. Mapping Consistency to Q3 Relational Schema
* **Library** (**Lib_ID**, Name, City)
* **Staff** (**Staff_ID**, Name, Salary, Lib_ID*)
* **Member** (**Member_ID**, Name, Phone, Staff_ID*)
* **Book** (**Book_ID**, Title, Author, Lib_ID*)
* **Loan** (**Loan_ID**, Issue_Date, Due_Date, Member_ID*, Book_ID*)

*(Note: **Bold** attributes represent Primary Keys [PK]; asterisked `*` attributes represent Foreign Keys [FK]).*

---

## Question 2: Object-Oriented (OO) Model

![Object-Oriented Class Diagram](./OO_Model.png)

### 1. Class Definitions
* **`Person`** *(Superclass)*
  * Attributes: `- person_id: String`, `- name: String`, `- phone: String`
  * Methods: `+ getDetails(): String`
* **`Staff`** *(Subclass — Inherits from Person)*
  * Attributes: `- staff_id: String`, `- salary: float`
  * Methods: `+ registerMember(): void`, `+ issueLoan(): void`
* **`Member`** *(Subclass — Inherits from Person)*
  * Attributes: `- member_id: String`, `- join_date: Date`
  * Methods: `+ requestBook(): void`, `+ payFine(): void`
* **`Book`**
  * Attributes: `- book_id: String`, `- title: String`, `- author: String`
  * Methods: `+ checkAvailability(): boolean`
* **`Loan`**
  * Attributes: `- loan_id: String`, `- issue_date: Date`, `- due_date: Date`
  * Methods: `+ calculateFine(): float`

### 2. Class Relationships
* **Inheritance ($\Delta$)**: `Staff` $\rightarrow$ `Person`, `Member` $\rightarrow$ `Person`
* **Associations**:
  * `Staff` $\rightarrow$ `Book` (**1:N**)
  * `Member` $\rightarrow$ `Loan` (**1:N**)
  * `Book` $\rightarrow$ `Loan` (**1:N**)

---

## Submissions
* **`ER_Model.png`**: High-resolution ER Diagram (200% zoom, solid white background)
* **`OO_MODEL.png`**: High-resolution Class Diagram
* **`README.md`**: Complete structural mapping and documentation
