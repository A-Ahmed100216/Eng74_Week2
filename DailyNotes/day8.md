# *Contents*
* *SQL Queries Continued*
* *Aggregates*
* *Joins*

# SQL Queries Continued
* Range – Uses the BETWEEN keyword
```sql
SELECT <column_name> FROM <table_name> WHERE <column_name> BETWEEN <value1> AND <value2>;
---Example 
SELECT * from EmployeeTerritories where TerritoryID BETWEEN 06800 and 09999
```  
* CHARLIST – Returns instances of specified values. In the example, products beginning with the letter B or S are returned. 
```sql
SELECT * From <table_name> where <column_name> LIKE '[ABC]%'
--Example
SELECT * From Products where ProductName LIKE '[BS]%'
```   
* Alias – Renames a column or makes a new column for example, can be used to create a full name column from a last name and full name column. 
```sql
SELECT <column_name > AS <'new_name'> FROM <table_name>
-- Example 1
SELECT CompanyName AS 'Company Name',
    City + ', '+ Country AS 'City and Country'
FROM Customers WHERE City='London'
-- Example 2
SELECT EmployeeID, FirstName, FirstName + ' ' + LastName AS 'Employee Name' FROM Employees
```   
* IN – Can be used if you have multiple queries and do not want to keep using or.
```sql
SELECT COUNT(*) FROM <table_name> WHERE <column_name> IN ('value1','value2','value3')

--Example – In the example below, both methods yield the same result (45) but using the IN is much more efficient, particularly as the conditions grow. 

SELECT COUNT(*) FROM Orders WHERE ShipCity='Lyon' or ShipCity='Reims' or ShipCity='Graz'
SELECT COUNT(*) FROM Orders WHERE ShipCity IN ('Lyon','Reims','Graz')
```   
* TOP - Identifies specified number or percent of values from the top of the table
```sql
SELECT TOP num column_name FROM table_name
--Examples
SELECT TOP 5 * FROM Employees
SELECT TOP 75 PERCENT * FROM Employees
```   
* ORDER BY - Sort a table based on a column. **ASC**ending or **DESC**ending
```sql
SELECT column_name, column_name, FROM table_name ORDER BY column_you_want_to_order DESC/ASC
--Example
SELECT UnitPrice, Quantity, Discount, UnitPrice*Quantity AS 'Gross Total'
FROM [Order Details] ORDER BY 'Gross Total' DESC
```   







