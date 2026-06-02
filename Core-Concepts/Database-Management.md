# Database Management Systems
## 1. Fundamentals

- **Data** is defined as raw, unorganized facts, often stored as bits and bytes (integers, text, etc.). It has no inherent meaning or significance until it is processed.
- **Information** is the result of processing or interpreting data. It provides **context** and is the foundation for **decision-making** in business and administration
- **Database** is a digital repository for interacting with the data that is stored in a **structured** manner. DBMS is the tool that manages this Database

### **Why we use a database instead of sheets/etc?**

- **Data Redundancy and Inconsistency:** Files often duplicate the same information in different places, leading to conflicting data (e.g., a student's address being updated in one file but not another).
- **Difficulty in Accessing Data:** Retrieving specific data in a file system requires writing a new program for every unique request.
- **Integrity Problems:** Hard-coding "constraints" (rules like a bank balance never being negative) into multiple files is difficult and prone to error.
- **Concurrency Anomalies:** When multiple users access the same data simultaneously, file systems struggle to maintain consistency.
- **Security Problems:** It is difficult to restrict users to only specific parts of the data in a flat file.

**Database Management System (DBMS)** is a software system that enables creating, maintaining, and controlling access, and deleting (**CRUD**) to a database, while handling concurrency, recovery, security, and querying through a unified interface between the user and the database.

**Structured Query Language (SQL)** is a language that we use to interact with the database, it stands for Structured Query Language.

## 2. Database System Architecture

A DBMS serves **three completely different types of people** at the same time.
![[dbms-three-level-arch.png]]
Example of Google Maps.

- **External level:** You see a clean map with routes and restaurant pins
- **Conceptual level:** There's a full data model — roads, nodes, coordinates, ratings, reviews, all linked
- **Internal level:** Petabytes of binary data on Google's servers, indexed for fast geospatial lookup

**Data Independence** means you can change one level of database design without affecting other levels. It has two types:

1. **Logical Data Independence -** If you change the conceptual schema (add a column, restructure a table) it won’t affect external views or applications.
2. **Physical Data Independence -** If you change how data is stored on disk (switch index type, change file format) it won’t affect the conceptual or external levels.

## 3. What is MySQL

MySQL is a server program that stores structured data in tables and lets you query and manipulate it using SQL. It is a Relational Database Management System (RDBMS):

1. relational - data is organized in such a way that tables relate to each other.
2. database - organized storage
3. Management System - software that controls, protects and enforces rules over the data.

#### Types of SQL commands

### Schema and Instances

**Schema** is the structure or blueprint of the database, it defines tables, columns, data types, and constraints.

**Instance** is the actual data stored in those tables at a specific moment in time.

### Data Models:

1. **ER Model** (Entity-Relationship Model) - is used during the design phase
2. **Relational Model** - this is what databases like MySQL implement
3. Network Model
4. Hierarchical Model

DDL (Data Definition Language) and DML () are languages used to define