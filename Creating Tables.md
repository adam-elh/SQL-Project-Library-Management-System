# SQL-Project-Library-Management-System

![ERD](https://github.com/user-attachments/assets/3a40977e-ba6d-44b0-a191-d4d77f230261)


```sql

-- SQL Project Library Management System ERD

-- Create Table Queries with relationships

DROP TABLE IF EXISTS branch;
CREATE TABLE branch (
            branch_id VARCHAR(10) PRIMARY KEY,
            manager_id VARCHAR(10),
            branch_address VARCHAR(30),
            contact_no VARCHAR(15)
);

DROP TABLE IF EXISTS employees;
CREATE TABLE employees (
            emp_id VARCHAR(10) PRIMARY KEY,
            emp_name VARCHAR(30),
            position VARCHAR(30),
            salary DECIMAL(10,2),
            branch_id VARCHAR(10),
            FOREIGN KEY (branch_id) REFERENCES  branch(branch_id)
);

DROP TABLE IF EXISTS members;
CREATE TABLE members (
            member_id VARCHAR(10) PRIMARY KEY,
            member_name VARCHAR(30),
            member_address VARCHAR(30),
            reg_date DATE
);

DROP TABLE IF EXISTS books;
CREATE TABLE books (
            isbn VARCHAR(50) PRIMARY KEY,
            book_title VARCHAR(80),
            category VARCHAR(30),
            rental_price DECIMAL(10,2),
            status VARCHAR(10),
            author VARCHAR(30),
            publisher VARCHAR(30)
);

DROP TABLE IF EXISTS issued_status;
CREATE TABLE issued_status (
            issued_id VARCHAR(10) PRIMARY KEY,
            issued_member_id VARCHAR(30),
            issued_book_name VARCHAR(80),
            issued_date DATE,
            issued_book_isbn VARCHAR(50),
            issued_emp_id VARCHAR(10),
            FOREIGN KEY (issued_member_id) REFERENCES members(member_id),
            FOREIGN KEY (issued_emp_id) REFERENCES employees(emp_id),
            FOREIGN KEY (issued_book_isbn) REFERENCES books(isbn) 
);

DROP TABLE IF EXISTS return_status;
CREATE TABLE return_status (
            return_id VARCHAR(10) PRIMARY KEY,
            issued_id VARCHAR(30),
            return_book_name VARCHAR(80),
            return_date DATE,
            return_book_isbn VARCHAR(50),
            FOREIGN KEY (return_book_isbn) REFERENCES books(isbn)
);

-- Create Table Queries without relationships


DROP TABLE IF EXISTS branch;
CREATE TABLE branch (
            branch_id VARCHAR(10) PRIMARY KEY,
            manager_id VARCHAR(10),
            branch_address VARCHAR(30),
            contact_no VARCHAR(15)
);

DROP TABLE IF EXISTS employees;
CREATE TABLE employees (
            emp_id VARCHAR(10) PRIMARY KEY,
            emp_name VARCHAR(30),
            position VARCHAR(30),
            salary DECIMAL(10,2),
            branch_id VARCHAR(10) --FK
);

DROP TABLE IF EXISTS members;
CREATE TABLE members (
            member_id VARCHAR(10) PRIMARY KEY,
            member_name VARCHAR(30),
            member_address VARCHAR(30),
            reg_date DATE
);

DROP TABLE IF EXISTS books;
CREATE TABLE books (
            isbn VARCHAR(50) PRIMARY KEY,
            book_title VARCHAR(80),
            category VARCHAR(30),
            rental_price DECIMAL(10,2),
            status VARCHAR(10),
            author VARCHAR(30),
            publisher VARCHAR(30)
);

DROP TABLE IF EXISTS issued_status;
CREATE TABLE issued_status (
            issued_id VARCHAR(10) PRIMARY KEY,
            issued_member_id VARCHAR(30), -- Foreign Key
            issued_book_name VARCHAR(80),
            issued_date DATE,
            issued_book_isbn VARCHAR(50), -- Foreign Key
            issued_emp_id VARCHAR(10) -- Foreign Key
);

DROP TABLE IF EXISTS return_status;
CREATE TABLE return_status (
            return_id VARCHAR(10) PRIMARY KEY,
            issued_id VARCHAR(30),
            return_book_name VARCHAR(80),
            return_date DATE,
            return_book_isbn VARCHAR(50)
);

-- Creating Table Relationships with Foreign keys

ALTER TABLE issued_status 
ADD CONSTRAINT fk_members
FOREIGN KEY (issued_member_id)
REFERENCES members(member_id);

ALTER TABLE issued_status 
ADD CONSTRAINT fk_books
FOREIGN KEY (issued_book_isbn)
REFERENCES books(isbn);

ALTER TABLE issued_status 
ADD CONSTRAINT fk_employees
FOREIGN KEY (issued_emp_id)
REFERENCES employees(emp_id);

ALTER TABLE employees 
ADD CONSTRAINT fk_branch
FOREIGN KEY (branch_id)
REFERENCES branch(branch_id);

ALTER TABLE return_status
ADD CONSTRAINT fk_issued_status
FOREIGN KEY (issued_id)
REFERENCES issued_status(issued_id);

```sql

```
