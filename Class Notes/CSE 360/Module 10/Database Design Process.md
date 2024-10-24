202406231807
Meta Tags: #class
Tags: [[software engineering]]

# Database Design Process


| Phase                                   | Parallel Activities                               |                         |
| --------------------------------------- | ------------------------------------------------- | ----------------------- |
| 1. Requirements Collection & Analysis   | Data Requirements                                 | Processing Requirements |
| 2. Conceptual Design (DBMS independent) | Conceptual & External Schema Design (ER Diagrams) | Transaction Design      |
| 3. Choice of DBMS                       |                                                   |                         |
| 4. Logical Design                       | Mapping conceptual design to a specific DBMS      |                         |
| 5. Physical Design                      | Internal Schema Design                            |                         |
| 6. Implementation                       | Build and populate database                       | Transaction programming |

### Phase 1 - Requirements Collection and Analysis

Major activities:
- identify groups that will use the application and key individuals that will participate in the requirements collection and analysis process
- examine existing documents concerning the application, including manuals, forms, reports, charts
- study the current operating environment. Determine the flow of information in the system. Identify specific transactions. Define when tractions are used and identify all input and output data
- Interview key individuals of the user group. Determine user needs and establish priorities for the development process

### Phase 2 - Conceptual Schema Design

Purpose:
- Emphasizes development of the semantic meaning of an application rather than implementation details
- The conceptual description remains constant even through the DBMS implementation platorm may change
- Data models used for conceptual design are generally more expressive than data models of specific DBMSs

The ER model is the high-level conceptual data modeling tool that is widely used in the industry

## Introduction to Databases

- a database is an ordered collection of information from which a computer program can quickly access information
- **relation is a table** - so, data is stored in a tabular format
- each **row** in a database table is called a record
- a record is a single complete set of related information
- each **column** in a database table is called a field
- fields are the individual categories of information stored in a record

![[Pasted image 20240623182151.png]]

## Relational Databases

- Databases can have more than one table
- Tables are usually related to each other. First, we will focus on only one table

![[Pasted image 20240623182356.png]]

## Introduction to SQL

![[Pasted image 20240623182517.png]]

- SQL stands for Structured Query Language
- a programming language for relational databases
- consists of many types of statements, which are sometimes called (sub)languages
	- data definition: design and modify database schema
	- data manipulation: store and retrieve data from database

### Data Definition Language

Examples:
- CREATE - creates new databases, table, and view
	- Create database test;
	- Create table customers;
	- Create view for_customers;
- DROP - drops views, tables, and databases
	- Drop view for_customers;
	- Drop table customers;
	- Drop database test;
- ALTER - modifies database schema
	- Alter table customers add customer_email varchar;

### Data Manipulation Language

DML modifies the database instance by inserting, updating and deleting its data:
- SELECT
	- Select from 'table' where 'condition'
- INSERT
	- INSERT INTO table 'columns' VALUES 'values'
- UPDATE
	- UPDATE table_name SET column_name=value where 'condition'
- DELETE
	- DELETE FROM table_name where 'condition'


### CREATE TABLE

- create a table w/ specified columns, each column having a specified type of data and satisfying certain constraints:

```
CREATE TABLE table_name(
	column_name_1 data_type constraints,
	...
	column_name_n data_type constraints);
```

Example:

```
CREATE TABLE PersonInfo ( 
	SSn INT,
	first_Name VARCHAR(32),
	last_Name VARCHAR(32),
	Age INT,
	annual_Income float);
```

### INSERT

Inserts a new row into a table

```
INSERT INTO table_name (col_1, ..., col_n)
VALUES (val_1, ..., val_n)
```

- The values provided will be placed into the corresponding columns
- Columns not named will receive no value (this will cause an error if the column was created with a NOT NULL constraint)

Example:

```
INSERT INTO PersonInfo (SSn, first_Name, last_Name, Age, annual_Income) VALUES (5780, 'Jake', 'Illingworth', 34, 363456.45);
```

### SELECT

Used to query databases; the command returns a result, a virtual table.

```
SELECT column-names FROM table-names [WHERE condition];
```

- the result table has columns as named
- rows are derived from the tables named
- the WHERE clause is optional, and specifies constraints on the rows selected

Examples:

```
SELECT * from PersonInfo;

SELECT first_Name from PersonInfo;

SELECT first_Name from PersonInfo where Ssn=7808;

SELECT first_Name from PersonInfo ORDER BY Age;

SELECT first_Name from PersonInfo where annual_Income > 50000 AND age > 50 ORDER BY Age;

SELECT AVG(Age) from PersonInfo;

SELECT MAX(annual_Income) from PersonInfo;
```

+ COUNT, SUM, MIN

### UPDATE

changes values in existing row:

```
UPDATE table_name
SET column_name_1 = value_1,
	...
	column_name_n = value_n
WHERE column_name = value
```

WHERE identifies the row to be updated.

```
UPDATE PersonInfo set first_Name = "Judy" where Age > 60;
```

### DELETE

Changes values in an existing row

```
DELETE FROM table_name
WHERE column_name = value;
```

### DROP

Remove a table/database from the system

```
DROP (TABLE|DATABASE) [IF EXISTS] name;
```

## Database Schema and SQL - Removing Duplicates and Primary Key

Primary key is not mandatory if duplicates are ok.

However, in order to block duplicate entries, a column in the table should be designated as a PRIMARY KEY.
- uniquely identifies each record in a database table
- must contain unique values
- cannot contain NULL values
- each table can have one or more primary key

```
CREATE TABLE PersonInfo
(...);
Primary Key(Ssn);
```

## Multiple Tables

- consider a situation where you need to create a database to represent Employee Info, Payroll Info, and Programming Language Proficiency of employees for management
- In this case, it makes sense to create three tables Employee, Payroll, and Languages

![[Pasted image 20240623185926.png]]

Employee table: consists of Employee related data; employee_id is the primary key

Payroll table: also has employee_id as the primary key. Since the two tables are related to each other, employee_id in the payroll table can be the foreign key, which models a one-to-one relationship.

### One-to-One Relationships

- exists between two tables when a related table contains exactly one record for each record in the primary table
- create one-to-one relationships to break information into multiple, logical sets
- information in the table in a one-to-one relationships can be placed within a single table
- make the information in one of the table confidential and only accessible by certain individuals

### One-to-Many Relationships

![[Pasted image 20240623195158.png]]

- this table has entry per language proficiency per employee.
- in order to get rid of redundancy, we can relate this table to the Employee table so that first_name and last_name can be obtained from the Employee table
- employee_id can be used as a Foreign Key here as well.

- this relationship exists in a relational database when one record in a primary table has many related records in a related table
- breaking tables into multiple related tables to reduce redundant and duplicate information is called **normalization**
- provides more efficiency and less redundancy

```
CREATE TABLE languages(
employee_id INT NOT NULL,
language VARCHAR(32),
FOREIGN KEY (employee_id)
REFERENCES
Employees(employee_id)
)
```

```
SELECT e.first_name, p.pay_rate
FROM Employee e, Payroll p
WHERE e.employee_id = p.employee_id
AND p.pay_rate>30.00
```

## Entity Relationship Diagrams

- Entity Relationship Model is a graphical approach to database design. It is a high-level data model that defines data elements and their relationship for a specified software system.
- An entity is something definable within a system, such as a person/role (e.g. Student), object (e.g. Invoice), concept (e.g. Profile), or event (e.g. Transaction)
- ER diagrams provide a visual starting point for database design

### Data Entity and Attributes

- Entity is an object, represented as rectangle in an ER diagram
- An attribute describes the property of an entity, represented as Oval in ER diagram. There are four types of attributes:
	- primary key attribute: uniquely identify an entity from an entity set, represented by oval with text underlined
	- composite attribute: a combination of other attributes
	- multivalued attribute: attribute that can hold multiple values, represented with double ovals
	- derived attribute: one whose value is dynamic and derived from another attribute, represented by dashed oval

![[Pasted image 20240623200432.png]]

![[Pasted image 20240623200546.png]]





---
# *References*