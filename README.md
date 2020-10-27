# Azure Commands 

1. Create - Used to create an element such as a table or database.

``` CREATE DATABASE <name>```

```sql
CREATE TABLE <table_name>(
Column_1 DATATYPE,
Column_2 DATATYPE,
Column_3 DATATYPE)
```
2. Drop - Delete an entity. 

```DROP TABLE <table_name>```

3. Alter - Ammend an entry. Alter is used in conjunction with Add, Rename, Modify or Drop. 
```sql
ALTER TABLE <table_name>
ADD/RENAME/MODIFY/DROP column_name DATATYPE;
```

4. Insert - Place an entry into the table.
```sql
INSERT INTO table_name (
	Column 1, Column 2, …)
VALUES (
	‘Value 1’, ‘Value 2’, … )
```

5. Update - Update table 
```sql
UPDATE <table_name>
	SET column_name = ‘new value’
WHERE entry you want to change = 'value'
```

6. Delete- Delete an entry 
```
DELETE FROM <table_name?
	WHERE entry you want to change = 'value'
```
