# SQL codecademy      
(notes by Christos C.Y.)

-------


## 1. Relational databases and organization 

**Relational database**: database that organizes information into one or more __table__.

**Table**: collection of data organized into rows and columns. 
They are referred to as **relations**.

**Column**: set of data values of particular type. 

**Row**: Single record in a table.

### Most common data types###
**integer**: positive or negative whole number   
**text**: text string   
**date**: the date formatted as YYYY-MM-DD   
**real**: a decimal vaule



###SQL statements###
	CREATE TABLE table_name (
    	column_1 data_type, 
    	column_2 data_type, 
    	column_3 data_type
 	 );

A __*statement*__ is text that the databases recognizes as valid command.

`CREATE TABLE` is a clause. Clauses perform specific tasks in SQL. By convention, clauses are written in capital letters. Clauses can also be referred to as commands.

`table_name` refers to the name of the table that the command is applied to.

`(column_1 data_type, column_2 data_type, column_3 data_type)` is a parameter. A parameter is a list of columns, data types, or values that are passed to a clause as an argument. Here, the parameter is a list of column names and the associated data type.

The structure of SQL statements vary. The number of lines used do not matter. A statement can be written all on one line, or split up across multiple lines if it makes it easier to read. In this course, you will become familiar with the structure of common statements.

### Specific example ###
####Creating table ####
`CREATE TABLE celebs (id INTEGER, name TEXT, age INTEGER);`

This `CREATE` statement creates a new table in the database named celebs. You can use the `CREATE` statement anytime you want to create a new table from scratch.

1. `CREATE TABLE` is a clause that tells SQL you want to create a new table. 
2. `celebs` is the name of the table. 
3. `(id INTEGER, name TEXT, age INTEGER)` is a list of parameters defining each column in the table and its data type. 

`id` is the first column in the table. It stores values of data type `INTEGER`   
`name` is the second column in the table. It stores values of data type `TEXT`   
`age` is the third column in the table. It stores values of data type `INTEGER`

####Inserting into table ####

` INSERT INTO celebs (id, name, age) VALUES (1, 'Justin Bieber', 21);`   

This `INSERT` statement inserts new rows into a table. You can use the `INSERT` statement when you want to add new records.

1. `INSERT INTO` is a clause that adds the specified row or rows. 
2. `celebs` is the name of the table the row is added to. 
3. `(id, name, age)` is a parameter identifying the columns that data will be inserted into. 
4. `VALUES` is a clause that indicates the data being inserted. 
`(1, 'Justin Bieber', 21)` is a parameter identifying the values being inserted.

`1` is an integer that will be inserted into the `id` column   
`'Justin Bieber'` is text that will be inserted into the `name` column   
`21` is an integer that will be inserted into the `age` column


####Selecting from table####
`SELECT * FROM celebs;`  
`*` is a special wildcard character. It allows you to select every column in a table without having to name each one individually. Here, the result set contains every column in the `celebs` table.

`SELECT` statements always return a new table called the __*result set*__.

`SELECT name FROM celebs;`

`SELECT` returns all data in the `name` column of the `celebs` table.  
 
1. `SELECT` is a clause that indicates that the statement is a query.
2. `name` specifies the column to query data from. 
3. `FROM` celebs specifies the name of the table to query data from. In this statement, data is queried from the celebs table. 

####Updating values####

    UPDATE celebs
    SET age = 22
    WHERE id = 1;
	
The `UPDATE` statement edits a row in the table. You can use the `UPDATE` statement when you want to change existing records.

1. `UPDATE` is a clause that edits a row in the table. 
2. `celebs` is the name of the table. 
3. `SET` is a clause that indicates the column to edit
.     
`age` is the name of the column that is going to be updated   
`22` is the new value that is going to be inserted into the age column.
4. `WHERE` is a clause that indicates which row(s) to update with the new column value. Here the row with a 1 in the `id` column is the row that will have the age updated to 22.

 
####Adding new columns
    ALTER TABLE celebs ADD COLUMN twitter_handle TEXT; 
    SELECT * FROM celebs;

The `ALTER TABLE´` statement added a new column to the table. You can use this command when you want to add columns to a table.

1. `ALTER TABLE` is a clause that lets you make the specified changes. 
2. `celebs` is the name of the table that is being changed. 
3. `ADD COLUMN` is a clause that lets you add a new column to a table
.  
`twitter_handle` is the name of the new column being added   
`TEXT` is the data type for the new column
4. `NULL` is a special value in SQL that represents missing or unknown data. Here, the rows that existed before the column was added have `NULL` values for `twitter_handle`. 

####Updating

    UPDATE celebs 
 	SET twitter_handle = '@taylorswift13' 
	WHERE id = 4; 

	DELETE FROM celebs WHERE twitter_handle IS NULL;

	SELECT * FROM celebs;

The `DELETE FROM` statement deletes one or more rows from a table. You can use the statement when you want to delete existing records.

`DELETE FROM` is a clause that lets you delete rows from a table.
`celebs` is the name of the table we want to delete rows from.
`WHERE` is a clause that lets you select which rows you want to delete. Here we want to delete all of the rows where the twitter_handle column IS NULL.
`IS NULL` is a condition in SQL that returns true when the value is `NULL` and false otherwise.

####Summary
`CREATE TABLE` creates a new table.    
`INSERT INTO` adds a new row to a table.    
`SELECT` queries data from a table.   
`UPDATE` edits a row in a table.   
`ALTER TABLE` changes an existing table.    	
`DELETE FROM` deletes rows from a table.

## 2. Performing calculations using SQL

###Counting     
`COUNT()`: function that takes the name of a column as an argument and counts the number of rows where the column is not `NULL`. Here, we want to count every row so we pass `*` as an argument.

	SELECT COUNT(*) FROM fake_apps WHERE price = 0;

	SELECT price, COUNT(*) FROM fake_apps GROUP BY price;

Aggregate functions are more useful when they organize data into groups.

`GROUP BY` is a clause in SQL that is only used with aggregate functions. It is used in collaboration with the `SELECT` statement to arrange identical data into groups.

Here, our aggregate function is `COUNT()` and we are passing price as an argument to `GROUP BY`. SQL will count the total number of apps for each `price` in the table.

It is usually helpful to `SELECT` the column you pass as an argument to `GROUP BY`. Here we select price and `COUNT(*). You can see that the result set is organized into two columns making it easy to see the number of apps at each price.


     SELECT SUM(downloads) FROM fake_apps;
     
`SUM()` is a function that takes the name of a column as an argument and returns the sum of all the values in that column. Here, it adds all the values in the `downloads` column.


     SELECT MAX(downloads) FROM fake_apps;
     
`MAX()` is a function that takes the name of a column as an argument and returns the largest value in that column. Here, we pass `downloads as an argument so it will return the largest value in the `downloads` column.

Similar functions:    
`MIN()`, `AVG()`

	 SELECT price, ROUND(AVG(downloads), 2) FROM fake_apps GROUP BY price;


`ROUND()` is a function that takes a column name and an integer as an argument. It rounds the values in the column to the number of decimal places specified by the integer (if no value is passed, it rounds to the closest integer). Here, we pass the column `AVG(downloads)` and `2 as arguments. SQL first calculates the average for each price and then rounds the result to two decimal places in the result set.

###Summary

Aggregate functions combine multiple rows together to form a single value of more meaningful information.   

`COUNT` takes the name of a column(s) as an argument and counts the number of rows where the value(s) is not `NULL`.   
`GROUP BY` is a clause used with aggregate functions to combine data from one or more columns.   
`SUM()` takes the column name as an argument and returns the sum of all the values in that column.   
`MAX()` takes the column name as an argument and returns the largest value in that column.   
`MIN()` takes the column name as an argument and returns the smallest value in that column.   
`AVG()` takes a column name as an argument and returns the average value for that column.    
`ROUND()` takes two arguments, a column name and the number of decimal places to round the values in that column.




##3. Multiple tables
    CREATE TABLE artists(id INTEGER PRIMARY KEY, name TEXT);

A **primary** key serves as a unique identifier for each row or record in a given table. The primary key is literally an id value for a record. We're going to use this value to _connect artists to the albums_ they have produced.    
By specifying that the `id` column is the `PRIMARY KEY`, SQL makes sure that:   
- None of the values in this column are `NULL`.    
- Each value in this column is unique.    
A table can not have more than one `PRIMARY KEY` column.

----------

	SELECT * FROM albums WHERE artist_id = 3;
	SELECT * FROM artists WHERE id = 3;

A foreign key is a column that contains the primary key of another table in the database. _We use foreign keys and primary keys to connect rows in two different tables_. One _table's foreign key holds the value of another table's primary key_. Unlike primary keys, _foreign keys do not need to be unique_ and can be `NULL`.

Here, `artist_id` is a foreign key in the albums table. We can see that Michael Jackson has an id of 3 in the artists table. All of the albums by Michael Jackson also have a 3 in the `artist_id` column in the albums table.

This is how SQL is **linking data** between the two tables. The relationship between the artists table and the albums table is the id value of the artists

----------
#### Cross join
	SELECT albums.name, albums.year, artists.name FROM albums, artists;

One way to query multiple tables is to write a `SELECT` statement with multiple table names separated by a comma. This is also known as a **cross join**. Here, albums and artists are the different tables we are querying.

When querying more than one table, column names need to be specified by `table_name.column_name`. Here, the result set includes the `name` and `year` columns from the `albums` table and the `name` column from the `artists` table.

Unfortunately the result of this cross join is not very useful. It combines every row of the `artists` table with every row of the `albums` table. It would be more useful to only combine the rows where the album was created by the artist.

---------
####Inner join

	SELECT * FROM albums JOIN artists ON albums.artist_id = artists.id;


In SQL, joins are used to combine rows from two or more tables. The most common type of join in SQL is an **inner join**.

An **inner join** will _combine rows from different tables if the join condition is true_. Let's look at the syntax to see how it works.

1. `SELECT *` specifies the columns our result set will have. Here, we want to include every column in both tables.
2. `FROM albums` specifies the first table we are querying.
3. `JOIN artists ON` specifies the type of join we are going to use as well as the name of the second table. Here, we want to do an inner join and the second table we want to query is `artists`.
4. `albums.artist_id = artists.id` is the _join condition_ that describes how the two tables are related to each other. Here, SQL uses the **foreign key** column _artist_id_ in the `albums` table to match it with exactly one row in the `artists` table with the same value in the `id` column. We know it will only match one row in the artists table because `id` is the `PRIMARY KEY` of artists.      

----------
####Outer join
	SELECT * FROM albums JOIN artists ON albums.artist_id = artists.id;

**Outer joins** also combine rows from two or more tables, but unlike inner joins, they _do not require the join condition to be met_. Instead, _every row in the left table is returned in the **result set**_, and if the join condition is not met, then `NULL` values are used to fill in the columns from the right table.

The left table is simply the first table that appears in the statement. Here, the left table is `albums`. Likewise, the right table is the second table that appears. Here, `artists` is the right table.

---------
#### Renaming columns
	SELECT albums.name AS 'Album', albums.year, artists.name AS 'Artist' FROM albums JOIN artists ON      
	albums.artist_id = artists.id WHERE albums.year > 1980;

`AS` is a keyword in SQL that allows you to rename a column or table using an **alias**. The new name can be anything you want as long as you put it inside of **single quotes**. Here we want to rename the `albums.name` column as `'Album'`, and the `artists.name` column as `'Artist'`.

It is important to note that _the columns have not been renamed in either table_. The _aliases only appear in the result set_.

####Summary
1. **Primary Key** is a column that serves a _unique identifier for row_ in the table. Values in this column must be **unique** and cannot be `NULL`.   
2. **Foreign Key** is a column that contains the primary key to another table in the database. It is used to _identify a particular row in the referenced table_.
3. **Joins** are used in SQL to combine data from multiple tables.
4. `INNER JOIN` will combine rows from different tables _if the join condition is **true**_.
5. `LEFT OUTER JOIN` will return every row in the left table, and if the join condition is not met, `NULL` values are used to fill in the columns from the right table.
6. `AS` is a keyword in SQL that allows you to rename a column or table in the result set using an **alias**.