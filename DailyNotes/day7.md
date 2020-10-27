# Contents
* *Querying in SQL*

# Querying an SQL Database
* Use the SELECT command.
* The Syntax sequence is as follows:   
```SQL
SELECT <column_name> FROM <databse>
```   
* The * can be used to select every column i.e. show the entire database.
* WHERE can be used to better define our queries. 

![SElect]()

## Examples
```sql
USE Northwind

Select CustomerID, city FROM Customers WHERE Country='France'
SELECT ProductName,UnitPrice, CategoryID FROM Products WHERE CategoryID=1
SELECT ProductName,UnitPrice, CategoryID FROM Products WHERE CategoryID=1 and Discontinued = 0

-- Counts the number of times the query is satisfied
SELECT COUNT(*) FROM Customers WHERE Country='France'


-- IN- look for collections
SELECT ContactName, Region From Customers WHERE Region In('WA','SP')
-- Between - ranges
SELECT * From EmployeeTerritories where TerritoryID between 06800 and 09999

-- AS - changes column names
-- Constructing output from two columns 
Select CompanyName AS 'CompanyName',
    City +', ' + Country AS 'City' 
from Customers

Select CompanyName AS 'CompanyName',
    City +', ' + Country AS 'City' 
from Customers Where Region is null


-- Wildcards - Allow more matching, it's less restrictive or includes everything
-- % sign, multiple unknown characters 
Select ProductName from Products Where ProductName Like 'Ch%'
-- _ sign, a single unknown character, each underscore represents a character
Select ProductName from Products Where ProductName Like 'Cha__'
Select ProductName from Products Where ProductName Like '__ai'
-- [charlist], Sets and ranges of characters to match
--[^charlist], Sets a range that does not match range of characters
```

# Exercise 1
```sql
USE Northwind
--Exercises 
-- 1. How many employees have a home in London?
SELECT * FROM Employees WHERE City='London'
-- Answer: 4

-- 2. Which employee is a Doctor? 
SELECT FirstName, LastName FROM Employees WHERE TitleOfCourtesy='Dr.'
-- Answer: Andrew Fuller

-- 3. How many products are discontinued?
SELECT COUNT(*) FROM Products WHERE Discontinued = 0
-- Answer: 69
-- 4. What are the names and product IDs of the prodcts with a unit price below 5.00?
SELECT ProductName, CategoryID FROM Products WHERE UnitPrice < 5.00
--5. Which categories have a category name with initials beginning with B or S?
SELECT CategoryName FROM Categories WHERE CategoryName LIKE 'B%' or CategoryName LIKE 'S%' 
-- Answer: Beverages, Seafood
-- 6. How many orders are there for EmployeeIDs 5 and 7 (The total for both)?
SELECT COUNT(*) FROM Orders WHERE EmployeeID =5 OR EmployeeID=7
--Answer: 114
-- 7. Write a SELECT using the Employees table and concatenate First Name and Last Name together. Use a column alias to rename the column to Employee Name.
Select FirstName +' ' + LastName AS 'Employee Name' FROM Employees

-- 8. Write a SELECT statement to list the six countries that have Region Codes in the Customers Table. 
SELECT Distinct Country FROM Customers WHERE Region IS NOT NULL
```

