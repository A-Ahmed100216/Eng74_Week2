# *Contents*
* *Introduction to SQL*
* *SQL Syntax*

# Introduction to SQL:
An IP address is like a phone number, it allows you to interact with a graphical interface like Azure Data Studio. 

## What is a Database?
* A structured set of data held in a computer, that is accessible in various ways.
* Can be used to gather information via queries. 
* A simple example of a database is a Microsoft Excel Sheet. 
* Databases are used on a daily basis from looking at houses, browsing TikTok, or purchasing plane tickets.
* We must be able to structure table so we can query data. 
* Efficiency is key when it comes to databases. Space is money so avoid repeating data i.e. if you have a column for first name and last name, don’t add a column for the full name. 

## Terminology 
* Column – Individual columns corresponding to attributes of the object. 
* Row – A row consists of one set of attributes corresponding to one instance that a table describes. Can also be known as **Records** or **Tuples**.
* Table – A predefined format of rows and columns that define an entity. Also known as a **File**. 
* DBMS – Database Management Systems allows a computer to perform database functions of storing, retrieving, adding, deleting and modifying data. 


## Types of databases
* Flat-file database- Stores everything in one table. Good for small number of records related to a single topic.
* Relational Database – Gives you the ability to separate masses of data into numerous tables. Linked to each other through the use of keys. 
* Big Data Database – Used for Data Analytics and Business Intelligence. Related to Internet of Things. Popular Big Data databases include MongoDB and Vertica. 

## Relational Databases
Relational Databases contain connected data therefore the tables should be related.  

### Relationship Types
* One to One
  * Each row in table a is linked to no more than one row in Table B. This is an attribute of the relationship, not the tables. 
  * For example, a student may have one row in the Contact_Info table.
* One to Many 
  * Each row in the table can be related to many rows in the relating table. 
  * This allows frequently used information to be saved only once in a table and referenced many times in all other tables.
* Many to Many
  * One or more rows in a table can be related to 0, 1 or many rows in another table. 
  * A third table called a mapping or link table is required in order to implement such a relationship. 
  * For example, customers can purchase many products.
  * Another example, book checking out system. One user can check out many books and one book can be checked out by many users.
![ERD](https://github.com/A-Ahmed100216/Eng74_Week2/blob/main/Images/ERD.png) 

### Primary key
* Unique identifier - identifies each record in the table.
* Most tables should have a primary key
*Each table can have more than one column which is part of its primary key (composite key) e.g. Order No. + Order Line No. 
* It can either be an attribute that is guaranteed to be unique e.g. NI number, or it can be generated by the DBMS.
* The DBMS will enforce the uniqueness of the primary key, not allowing repeat records to exist in the table. 

#### Primary Key Constraints 
* **Must be unique.**
* Must always have an entry - cannot be blank or null.
* The value must never change.
* Each table may have a maximum of one Primary Key. 

#### Types of primary keys:
* Simple
* Composite/compound – combines two values.

#### Foreign keys 
* A Foreign Key is a Primary Key in a secondary table. 
* Builds the relationship to primary table.  
* Natural relationships exist between tables in most database structures, foreign keys create solid relationships.
* Foreign keys ensure that the row of information in Table A corresponds to the correct row of information in Table B.
* The constraint is used to prevents actions that would destroy linked between tables.
* Prevent invalid data form being inserted into the foreign key column – has to match one of the values contained in the table it points to.
* No uniqueness constraint for Foreign Keys.
* A table can have any number of Foreign Keys
* A row cannot be deleted from a reference table if it is in use by a Foreign Key. 

Database tools
* Access- Microsoft product for databases 
* SQL Servers – also Microsoft
* PostgreSQL – open source 
* SQLite – small database
* MySQL 
* redis – open source 
* mongoDB – Big Data 
* Oracle


# SQL Syntax 
SQL is an acronym for **Structured Query Language** 

## DML DDL DCL and TCL
* DML - Data manipulation language 
  * SELECT
  * INSERT
  * UPDATE
  * DELETE
* DDL - Data definition language 
  * CREATE
  * ALTER 
  * DROP
  * TRUNCATE
* DCL - Data Control Language 
  * GRANT 
  * REVOKE
* TCL - Transaction Control Language
  * COMMIT
  * ROLLBACK 
  * SAVEPOINT

## Data Types 
* VARCHAR – Adaptable to different lengths of characters. Records MAX size. Equivalent to strings in python. 
* CHARACTER or CHAR- data at fixed length, fixed amount of space used.
* INT – Hold a whole number/integer value (variations include BIGINT, SMALLINT, TINYINT). Can be positive or negatives.
 * DATE or TIME or DATETIME – stores date, time or both date and time. 
* DECIMAL or NUMERIC- fixed precision and scale (digits to right of decimal point) numbers.
* BINARY – stores binary data such as images or files.
* FLOAT – scientific use (very large numbers).
* BIT – equivalent to binary (0,1 or NULL).

# Task - Create a film database
```sql
CREATE DATABASE db_group2;
USE  db_group2;
CREATE TABLE film_table (
film_name VARCHAR(10),
        film_type VARCHAR(6),
  	date_of_release DATE,
	director VARCHAR(20),
	writer VARCHAR(20),
	star VARCHAR(20),
	film_language VARCHAR(20),
	official_website VARCHAR(MAX))

ALTER TABLE db_group2
ADD plot_summary VARCHAR(MAX)

INSERT INTO film_table (
film_name, film_type, date_of_release, director, writer, star, film_language, official_website, plot_summary)
VALUES (
'Avengers', 'Action', '2012','Joss Whedon', 'Zakk Penn', 'Chris Evans', 'English', 'https://www.marvel.com/movies/the-avengers', 'When an unexpected enemy emerges that threatens global safety and security, Nick Fury, Director of the international peacekeeping agency known as S.H.I.E.L.D., finds himself in need of a team to pull the world back from the brink of disaster. Spanning the globe, a daring recruitment effort begins.')

INSERT INTO film_table (
film_name, film_type, date_of_release, director, writer, star, film_language, official_website, plot_summary)
VALUES (
'Hulk','Action','2003-06-20','Ang Lee','Stan Lee','Eric Bana','English','https://www.marvel.com/characters/hulk-bruce-banner','Bruce Banner, a genetics researcher with a tragic past, suffers an accident that causes him to transform into a raging green monster when he gets angry.')

UPDATE film_table
SET date_of_release = '2012-05-04'
        WHERE date_of_release='2012'

--DELETE FROM film_table
--    WHERE film_name= 'Hulk'


SELECT * FROM film_table
```
