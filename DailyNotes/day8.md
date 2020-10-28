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

--Example – In the example below, both methods yield the same result (45) but
--using the IN is much more efficient, particularly as the conditions grow. 
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
* SELECT CASE - Can be useful when you need varying result outputs based on differing data. When building these case statements, put the most specific at the top. 
```sql
SELECT <column_name>, CASE
WHEN <condition1> THEN <output1>
ELSE <output2> END AS <column_name>
FROM <table_name>;

--Example 1
SELECT CASE
WHEN DATEDIFF(d,OrderDate,ShippedDate)<10 THEN 'On Time'
ELSE 'Overdue'
END AS 'Status'
FROM Orders

-- Example 2
SELECT 
    FirstName + ' ' + LastName AS 'Full Name',
    BirthDate,
    DATEDIFF(yyyy,BirthDate,GETDATE()) AS 'Age',
CASE 
    WHEN DATEDIFF(yyyy,BirthDate,GETDATE())>65
        THEN 'Retired'
    WHEN DATEDIFF(yyyy,BirthDate,GETDATE())>60
        THEN 'Retirement due'
    ELSE 'More than 5 years to go'
END AS 'Employment Status'
FROM Employees
```   
## String Functions
* **IMPORTANT---> SQL INDEXING BEGINS AT 1.**
* SUBSTRING (text, start, length) i.e. Substring(hello,1,1)
* CHARINDEX(arg1,arg2) - arg 1 is what you are looking for, and arg2 is where you are looking. 
* LEFT(arg1,arg2) or RIGHT(arg1,arg2) – arg 1 is the string  and arg2 is the amount you want to move. 
* CHARINDEX('a', 'text')- This will search for the letter a in 'text' and return the index.
* LTRIM or RTRIM - used to remove spaces at the beginning or end of a string.
* LEN(name) - returns the length of the string 
* REPLACE(text,' ','_')- This will replace spaces with underscores.
* UPPER(text) or LOWER(text) - convert characters to desired form

### Exercises
```sql
SELECT UnitPrice, Quantity, Discount, UnitPrice*Quantity AS 'Gross Total' FROM [Order Details]
SELECT UnitPrice, Quantity, Discount, UnitPrice*Quantity AS 'Gross Total', UnitPrice*Quantity*(1-Discount) AS 'Net total' FROM [Order Details]


SELECT TOP 5 OrderID,UnitPrice, Quantity, Discount, 
    UnitPrice*Quantity AS 'Gross Total', 
    (UnitPrice*Quantity)*(1-Discount) AS 'Net Total' 
FROM [Order Details] ORDER BY 'Net Total' DESC


SELECT PostalCode AS 'Post Code',
    LEFT(PostalCode,CHARINDEX(' ',PostalCode)-1) AS 'Post Code region',
    CHARINDEX(' ',PostalCode) AS 'Where index begins',
    Country
FROM Customers
WHERE Country='UK'

--Apostrophe’s escaped by following with another apostrophe. 
SELECT ProductName AS 'Product''s with apostrophes' FROM Products
WHERE CHARINDEX('''',ProductName)!=0
```

## Date functions
* GETDATE() - returns the date.   
```sql 
SELECT GETDATE()``` 
* SYSDATETIME() - returns the date and time of the computer being used.     
```sql 
SELECT SYSDATETIME()```   
* DATEADD – Adds the specified amount of time to a column in the DATE format.
  * d=Days, mm=Months, yyyy= Years   

```sql
DATEADD (<type>, <amount>, <column_name>); 

--Example – Adds 5 days onto the OrderDate and stores this in a new column titled Due Date. 
DATEADD(d,5,OrderDate) AS 'Due Date’
```
* DATEDIFF – Calculates the difference between dates.
```sql
DATEDIFF(<type>, <column1>, <column2>);

--Example – Calculates the difference between two dates and stores in a new column titled Ship Time. 
DATEDIFF(d,OrderDate,ShippedDate) AS 'Ship Time'
```
* YEAR – Extracts the year from a date
```sql
SELECT YEAR(<column_name>);

--Example – Extracts year from OrderDate.
SELECT YEAR(OrderDate) AS 'Order Year'
```
* MONTH – Extracts the month from a date
```sql
SELECT MONTH(<column_name>);

--Example – Extracts month from OrderDate.
SELECT MONTH(OrderDate) AS 'Order Month'
```
* DAY – Extracts the day from a date
```sql
SELECT DAY(<column_name>);

--Example – Extracts day from OrderDate.
SELECT DAY(OrderDate) AS 'Order Day'
```  
### Further Examples and Exercises
```sql
--Extracts the month from the OrderDate column in the Orders table. 
SELECT Month(OrderDate) AS 'Order Month' from Orders

--Adds 5 days onto the shipping data and classifies this as the Due Date.
--The difference between the order date and shipping date is stored in Ship Days.
--Sorts by ‘Ship Days’ column. 
SELECT OrderDate, ShippedDate,DATEADD(d,5,OrderDate) AS 'Due Date',
    DATEDIFF(d,OrderDate,ShippedDate) AS 'Ship Days'
FROM Orders ORDER BY 'Ship Days' DESC

--Gives the full name and age of employees.
SELECT 
    FirstName + ' ' + LastName AS 'Full Name',
    BirthDate,
    DATEDIFF(yyyy,BirthDate,GETDATE()) AS 'Age'
FROM Employees
```

# Aggregate Functions
* These include SUM, AVG, MIN and MAX.
``` sql
SELECT 
    SUM(<column_name>) AS '<new_name>',
    AVG(<column_name>) AS '<new_name>',
    MIN(<column_name>) AS '<new_name>',
    MAX(<column_name>) AS '<new_name>'
FROM <table_name>;

--Example
SELECT 
    SUM(UnitsOnOrder) AS 'Total on Order',
    AVG(UnitsOnOrder) AS 'Avg on order',
    MIN(UnitsOnOrder) AS 'Min on order',
    MAX(UnitsOnOrder) AS 'MAX on order'
FROM Products;
```

* GROUP BY – Groups according to a specified category
```sql
SELECT <grouping_column>, 
    SUM(<column>) AS <new_name>,
    AVG(<column>) AS <new_name>
FROM table_name
GROUP BY <grouping_column>

--Example – Groups according to the SupplierID category and 
--outputs results of the aggregate functions SUM, AVG and MAX. 
SELECT SupplierID, 
    SUM(UnitsOnOrder) AS 'Total on Order',
    AVG(UnitsOnOrder) AS 'Avg on order',
    MAX(UnitsOnOrder) AS 'Max on order'
FROM Products
GROUP BY SupplierID
```

* HAVING- Used instead of WHERE when filtering on subgroups. Essentially when we try to call an alias using WHERE, it will throw an error as it has not yet been created. HAVING allows us to call this alias.
```sql
SELECT <grouping_column>, 
    SUM(<column>) AS <new_name>,
    AVG(<column>) AS <new_name>
FROM table_name
GROUP BY <grouping_column>
HAVING AVG(<column>) > value

--Example – Groups by Supplier ID and only shows order which have more than 5 units on order. 
SELECT SupplierID, 
    SUM(UnitsOnOrder) AS 'Total on Order',
    AVG(UnitsOnOrder) AS 'Avg on order'
FROM Products
GROUP BY SupplierID
HAVING AVG(UnitsOnOrder)>5
```

### Further Examples and Exercises
```sql
--Aggregates, Grouping and Sorting
SELECT SupplierID, 
    SUM(UnitsOnOrder) AS 'Total on Order',
    AVG(UnitsOnOrder) AS 'Avg on order',
    MAX(UnitsOnOrder) AS 'Max on order'
FROM Products
GROUP BY SupplierID
ORDER BY 'Total on Order' DESC

-- Aggregates, Grouping and Having
SELECT SupplierID, 
    SUM(UnitsOnOrder) AS 'Total on Order',
    AVG(UnitsOnOrder) AS 'Avg on order'
FROM Products
GROUP BY SupplierID
HAVING AVG(UnitsOnOrder)>5
```   
# Joins 
* Join is a keyword used to combine matched rows from two or more tables.
* It allows you to create a list of combined rows of matching data from different tables. 
* Various types of joins.   
![joins](https://github.com/A-Ahmed100216/Eng74_Week2/blob/main/Images/joins.png)    
* When aliasing tables you don’t need AS
```sql
SELECT *
FROM <table_a>
JOIN <table_b>
ON <table_a.matchingid> = <table_b.matchingid>

-- Syntax when using aliases a and b 
SELECT * 
FROM <table_a> a
JOIN <table_b> b
ON <a.matchingid> = <b.matchingid>

--Example 1
SELECT Orders.OrderID, Customers.CompanyName, Customers.ContactName, Customers.Country, Orders.OrderDate 
FROM Orders
INNER JOIN Customers ON Orders.CustomerID=Customers.CustomerID 
WHERE Customers.Country='Brazil' or Orders.ShipCountry='Brazil'

--Example 2- Using Aliases
SELECT o.OrderID, c.CustomerID, c.CompanyName, c.ContactName
FROM Orders o
INNER JOIN Customers c
ON o.CustomerID=c.CustomerID 
WHERE c.Country='Brazil' or o.ShipCountry='Brazil'
ORDER BY c.CompanyName
```   
