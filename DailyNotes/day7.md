# Contents
* *Querying in SQL*

# Querying an SQL Database
* Use the SELECT command.
* The Syntax sequence is as follows:   
```SQL
SELECT <column_name> FROM <databse>
```   
* The * can be used to select every column i.e. show the entire database.
* **WHERE** - used to better define our queries. 

![Select](https://github.com/A-Ahmed100216/Eng74_Week2/blob/main/Images/Select.png)

```sql
USE Northwind -- Directs to the correct database

Select CustomerID, city FROM Customers WHERE Country='France';
SELECT ProductName,UnitPrice, CategoryID FROM Products WHERE CategoryID=1;
SELECT ProductName,UnitPrice, CategoryID FROM Products WHERE CategoryID=1 and Discontinued=1;
```

* **COUNT** -  Counts the number of times the query is satisfied
```sql
SELECT COUNT(*) FROM Customers WHERE Country='France'  
```

* **Range** – Uses the BETWEEN keyword
```sql
SELECT <column_name> FROM <table_name> WHERE <column_name> BETWEEN <value1> AND <value2>;

---Example
SELECT * from EmployeeTerritories where TerritoryID BETWEEN 06800 and 09999;
```

* **Alias** – Renames a column or makes a new column. Uses the AS keyword.
```sql
SELECT <column_name > AS <'new_name'> FROM <table_name>

--Examples
SELECT CompanyName AS 'CompanyName',
    City +', ' + Country AS 'City'
FROM Customers;

SELECT CompanyName AS 'CompanyName',
    City +', ' + Country AS 'City'
FROM Customers WHERE Region IS NULL;
```

* **Arithmetic Operators** - Can be used in conjunction with WHERE. 
  * = Equal To
  * != Not Equal To
  * \> Greater Than 
  * \>= Greater Than or Equal To
  * < Less Than 
  * <= Less Than or Equal To


*  **Wildcards** - Allow more matching, it's less restrictive or includes everything.    
  (1)  % sign, multiple unknown characters
```sql
Select ProductName from Products Where ProductName Like 'Ch%'
```
  (2)  _ sign, a single unknown character, each underscore represents a character
```sql
Select ProductName from Products Where ProductName Like 'Cha__'
Select ProductName from Products Where ProductName Like '__ai'
```
  (3) CHARLIST – Sets and ranges to match characters. Returns all results that sart with the specified characters. In the example, products beginning with B or S shall be returned. 
```sql
SELECT * From <table_name> where <column_name> LIKE '[ABC]%'

--Example
SELECT * From Products where ProductName LIKE '[BS]%'
```
  (4) ^CHARLIST - Opposite of CHARLIST,sets a range that does not match range of characters. This will return results that do not start with the specified characters.



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

