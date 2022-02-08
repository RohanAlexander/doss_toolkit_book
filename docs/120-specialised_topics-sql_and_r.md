


# SQL and R

*Written by Yena Joo and last updated on January 2022.*

## Introduction
You can always import CSV files and local dataset using a simple functions such as `read_csv`. However, what if you have to import a dataset that is too large for your computer? Here, we connect to database to store data and allows you to use whenever you need them. 

Structured Query Language (SQL) can be used to manage data and communicate with a database. SQL is used in most database systems, but the commands may vary depending on what Relational Database Management Systems you use (i.e. MySQL, Oracle, PostgreSQL, etc.).  

Using this, you can query, update, delete, reorganize, everything 

In this lesson, you will learn:  

- How to connect and disconnect R with SQL
- How to import data from queries
- how to view table, edit data, and delete data using DML (Data Manipulation Language) by connecting to SQL from R. 

Prerequisite skills include:  
- How to write SQL Queries  
- Have SQL server ready

## hmm 

### DBI
DBI is a basic database infrastructure for R. There are many different R packages that help to connect the database such as `RMySQL` for MySQL, `RPostgres` for PostgreSQL, etc. The DBI package is used to connect R to DBMS (Database Management Systems). 

The first step is to install the package `DBI`. 

```
install.packages("DBI")
```

If you would like to learn more about the DBI package, [here](https://dbi.r-dbi.org) is an additional resource you may find helpful.  


### dbConnect()  

In order to use data of MySQL database in R, you need to connect MySQL to R. The `RMySQL` package is a package that allows R to connect to MySQL. 


```r
library(RMySQL)
#> Loading required package: DBI
```

Note that installing `RMySQL` package automatically installs DBI package mentioned above as well, so you have a several options to choose the packages depending on your choice of SQL.
You can enter the host address and login information in the `dbConnect()` function parameters.

```
connection <- dbConnect(
  MySQL(),
  user = 'root',
  password = '{your password}',
  host = '127.0.0.1',
  dbname = "dbName"
)
```

By using the `dbConnect()` function, you can directly connect to the DB in the MySQL host. Here are the important arguments when using the function:
- MySQL(): Declare that MySQL will be used among SQL types
- user: username
- password: password
- host: the host where the DB is in
- dbname: the name of the database you are connecting to
All arguments must be passed in a string format, enclosed with quotation marks. 

If you would like to learn more about `dbConnect()`, [here](https://www.rdocumentation.org/packages/DBI/versions/0.5-1/topics/dbConnect) is an additional resource you may find helpful.  

Note that you have to declare the character sets of the DB as UTF-8 by using the dbSendQuery() function to prevent encoding from breaking. Without declaring the character sets using the function, you might not successfully extract the data with the correct format. 

When it is successfully connected to the MySQL, the variables are created and you can check the DB connection information by using the dbGetInfo() function.


### Create a Table: dbWriteTable()
Once you successfully connected to the DB, you can now generate tables. You can view the lists of tables currently in the DB using the following function
```
dbListTables(Name of the DB)
```

The function will print the list of the tables.

```
con <- dbConnect(SQLite())
dbWriteTable(con, "mtcars", mtcars)
dbReadTable(con, "mtcars")
```

### Create a Table: dbGetQuery()
dbGetQuery(db,"create table dummy ( Id INT PRIMARY KEY,Name VARCHAR(5))")

### View the created table: dbSendQuery() 

Function `dbSendQuery()` allows you to view, insert, edit, and delete the data.  
  
**View data** 

```
data <- dbGetQuery(
  DBvariableName, 
  "SELECT * FROM `TableName`;" 
)
print(data)
```

When writing a query, make sure to enclose the table name and field name with ``` , and enclose with `'` if it is a string.  

You can select a specific set of data from a table using various clauses such as `WHERE`, `GROUP BY`, `JOIN` and etc.  

**Insert Data**  
Similarly, you can insert data using `INSERT INTO` clause.  

```
dbSendQuery(
  DBvariableName, 
  "INSERT INTO `TableName` (field1, field2)
  VALUES (value1, value2);"
)
``` 

**Update Data**  
You can update specific data like the following example:  

```
dbSendQuery(
DBvariableName,
"UPDATE `TableName`
SET `field1`= value1, `field2` = value2,  
WHERE `field` = value;"
)
```

**Delete Data**  
```
"DELETE FROM `TableName`
WHERE `field`= `value`;" 
```
  

### Delete a table: dbRemoveTable()
You can easily delete a table of your choice by using the function `dbRemoveTable()`. The function removes the entire table, not just a single data in the table.   

```
dbRemoveTable(DBvariableName, "Table Name")
```


### dbDisconnect()

To disconnect from the database, simply use the `dbDisconnect()` function using a previously created connection as the following example.  

```
dbDisconnect(connection)
```

Once you learn how to connect SQL with R, you can query however you want and manipulate the data from R!   


## Exercises
### Question 1
True or False: read.csv() is the only way to import a dataset.  
  a. True  
  b. False  

### Question 2
What package do you need to connect to the Oracle database?  
  a. RODBC   
  b. JDBC   
  c. RMySQL   
  d. RPostgreSQL   

### Question 3
If I want to delete an entire table, which function would I use (pick one)? 
  a. `dbSendQuery()`  
  b. `dbDeleteTable()`  
  c. `dbRemoveTable()`  
  d. `dbRemoveDB()` 
  
### Question 4
What query should I write if I want to view the data?   
  a. VIEW * FROM `TableName`  
  b. SELECT * FROM `TableName`  
  c. SELECT * FROM 'TableName'  
  d. INSERT * INTO 'TableName'  

### Question 5
Read the code chunk below: 

```
connect_to_sql <- dbConnect(
  MySQL(),
  user = kellyj,
  password = '{password}',
  host = 127.0.0.1,
  dbname = UofT
)
```
Which argument inside the function will cause an error?  
  a. `user`  
  c. `host`  
  d. `dbname`  
  e. all of the above  
  
### Question 6
(True or False) You can both insert and delete data using a same function, dbSendQuery().  
  a. True  
  b. False

### Question 7

### Question 8

### Question 9

### Question 10

## Common Mistakes & Errors 

## Next Steps  


## Reference
