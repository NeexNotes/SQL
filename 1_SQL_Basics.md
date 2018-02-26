# SQL Basics

[teamtreehouse.com/library/sql-basics/data-databases-and-sql/](https://teamtreehouse.com/library/sql-basics/data-databases-and-sql)

[TOC]

## Data, Databases and SQL

Data is everything. Save, go back in the future. 

SQL stands for **Structured Query Language**. SQL has been around since the 1970s!

Reading data from a database is known as querying. Database (SQL) stores data in tables. With vertical columns, and horizontal rows. Each entry is a row.

**Further Reading**:  

- [SQL Entry in Wikipedia](https://en.wikipedia.org/wiki/SQL)

#### SQL Database Websites

- [MySQL](http://www.mysql.com/)
- [PostgreSQL](http://www.postgresql.org/)
- [SQLite](http://www.sqlite.org/)
- [Microsoft SQL Server](https://www.microsoft.com/en-us/server-cloud/products/sql-server/)
- [Oracle](https://www.oracle.com/database/index.html)

#### NoSQL Database Websites

- [MongoDB](https://www.mongodb.org/)
- [CouchBase](http://www.couchbase.com/)
- [Redis](http://redis.io/)



### Data + Schema

Databases allow users to store data in well defined sections. This keeps the data uniform. However, the SQL you write can show the data in different ways which is handy for reporting subsets of data.

Database is data (what is in it) and schema (how it is stored and related between and in tables). 

Filtering data by anything, and show only what you need. Nothing is destroyed when querying, even though the data is shown in different ways.

**Further Reading**:  

- [Schema](https://en.wikipedia.org/wiki/Database_schema)

### Types of data

There are good reasons why your data should be categorized in to different types. In this video we'll explore some of them.

Sorting, math, dates - sorting and querying. 

**Types of Data**  

Here's a slightly larger list of data types than in the video.

- Text Type Examples
  - TEXT
  - VARCHAR
- Numeric Type Examples
  - INT
  - INTEGER
- Date Type Examples
  - DATETIME
  - DATE
  - TIMESTAMP

Here's documentation sites for some other databases where you can see the similarities and differences in data types.

- [MySQL Data Types](http://dev.mysql.com/doc/refman/5.7/en/data-types.html)
- [SQLite Data Types](http://www.sqlite.org/datatype3.html)
- [PostgreSQL Data Types](http://www.postgresql.org/docs/8.4/static/datatype.html)
- [Microsoft SQL Data Types](https://msdn.microsoft.com/en-us/library/ms187752.aspx?f=255&MSPPError=-2147217396)


### Tools

In this video we'll look at some different tools that you may use in a professional setting and what you'll use while learning here, SQL Playgrounds.

**Different Database Tools**  

- [Mode Analytics](http://modeanalytics.com/) used for businesses to get insights from their database.
- [pgAdmin](http://pgadmin.org/) for PostgreSQL
- [phpMyAdmin](https://www.phpmyadmin.net/) and [MySQL Workbench](http://mysqlworkbench.org/) for MySQL

## Getting Data from a Database

### Definitions

**Syntax** The vocabulary and grammatical rules surrounding the structure of your code.

**Keywords** The vocabulary words of a programming language used to issue commands to a computer.

**SQL examples:**    

```sql
SELECT * FROM <table name>;
```

The asterisk or star symbol (`*`) means all columns.

The semi-colon (`;`) terminates the statement like a period in sentence or question mark in a question.

Examples:

```sql
SELECT * FROM books;
SELECT * FROM products;
SELECT * FROM users;
SELECT * FROM countries;
```

See all of the SQL used in SQL Basics in the [SQL Basics Cheat Sheet](SQL_cheatsheet.md). 

### Retrieving Specific Columns of Information

You don't have to retrieve all the information from a table. You can retrieve only the information you want from the columns you want and filter out the rest.

**SQL examples:**    

Retrieving a single column:

```sql
SELECT <column name> FROM <table name>;
```

Examples:

```sql
SELECT email FROM users;
SELECT first_name FROM users;
SELECT name FROM products;
SELECT zip_code FROM addresses;
```

Retrieving multiple columns:

```sql
SELECT <column name 1>, <column name 2>, ... FROM <table name>;
```

Examples:

```sql
SELECT first_name, last_name FROM customers;
SELECT name, description, price FROM products;
SELECT title, author, isbn, year_released FROM books;
SELECT name, species, legs FROM pets;
```

### Categorizing Your Output with 'AS'

You're not restricted to displaying the column names from the table at the top of your results. You can specify your own names for result sets.

**SQL examples:**    

```sql
SELECT <column name> AS <alias> FROM <table name>;
SELECT <column name> <alias> FROM <table name>;
```

Examples:

```sql
SELECT username AS Username, first_name AS "First Name" FROM users;
SELECT title AS Title, year AS "Year Released" FROM movies;
select name AS "Product Name", description as "Product Description" from products;
SELECT name AS Name, description AS Description, price AS "Current Price" FROM products;
SELECT name Name, description Description, price "Current Price" FROM products;
```

* multi-words must be strings - avoid space (diff SQL has diff syntax here)

### Searching Tables with 'WHERE'

The real power of SQL comes from filtering rows of information. You've filtered columns, now you're going to filter rows.

**SQL examples:**    

##### A `WHERE` Clause

```sql
SELECT <columns> FROM <table> WHERE <condition>;
```

##### Equality Operator

Find all rows that a given value matches a column's value.

```sql
SELECT <columns> FROM <table> WHERE <column name> = <value>;
```

Examples:

```sql
SELECT * FROM contacts WHERE first_name = "Andrew";
SELECT first_name, email FROM users WHERE last_name = "Chalkley";
SELECT name AS "Product Name" FROM products WHERE stock_count = 0;
SELECT title "Book Title" FROM books WHERE year_published = 1999;
```

##### Inequality Operator

Find all rows that a given value doesn't match a column's value.

```sql
SELECT <columns> FROM <table> WHERE <column name> != <value>;
SELECT <columns> FROM <table> WHERE <column name> <> <value>;
```

The not equal to or inequality operator can be written in two ways `!=` and `<>`. The latter is *less* common.

Examples:

```sql
SELECT * FROM contacts WHERE first_name != "Kenneth";
SELECT first_name, email FROM users WHERE last_name != "L:one";
SELECT name AS "Product Name" FROM products WHERE stock_count != 0;
SELECT title "Book Title" FROM books WHERE year_published != 2015;
```
### Filtering by Comparing Values

You don't need to just search for equal or unequal values. You can compare them to a value you decide.

#### Relational Operators

There are several relational operators you can use:

- `=` equal to
- `!=` `<>` not equal to
- `<` less than
- `<=` less than or equal to
- `>` greater than
- `>=` greater than or equal to

These are primarily used to compare *numeric* and *date/time* types.

**SQL examples:**    

```sql
SELECT <columns> FROM <table> WHERE <column name> < <value>;
SELECT <columns> FROM <table> WHERE <column name> <= <value>;
SELECT <columns> FROM <table> WHERE <column name> > <value>;
SELECT <columns> FROM <table> WHERE <column name> >= <value>;
```

Examples:

```sql
SELECT first_name, last_name FROM users WHERE date_of_birth < '1998-12-01';
SELECT title AS "Book Title", author AS Author FROM books WHERE year_released <= 2015;
SELECT name, description FROM products WHERE price > 9.99;
SELECT title FROM movies WHERE release_year >= 2000;
```

### Filtering on More than One Condition

You're not restricted to just using one condition, you can test rows of information against multiple conditions. You can choose whether you retrieve rows that match both of your conditions or either of them.

**SQL examples:**    

You can compare multiple values in a `WHERE` condition. If you want to test that *both* conditions are true use the `AND` keyword, or *either* conditions are true use the `OR` keyword.

```sql
SELECT <columns> FROM <table> WHERE <condition 1> AND <condition 2> ...;
SELECT <columns> FROM <table> WHERE <condition 1> OR <condition 2> ...;
```

Examples:

```sql
SELECT username FROM users WHERE last_name = "Chalkley" AND first_name = "Andrew";
SELECT * FROM products WHERE category = "Games Consoles" AND price < 400;
SELECT * FROM movies WHERE title = "The Matrix" OR title = "The Matrix Reloaded" OR title = "The Matrix Revolutions";
SELECT country FROM countries WHERE population < 1000000 OR population > 100000000;
```
### Filtering by Dates

Filtering results by date can be handy for finding entries before or after a specific date. In this video we'll explore filtering by dates.

These are primarily used to compare *numeric* and *date/time* types.

**SQL examples:**    

```sql
SELECT first_name, last_name FROM users WHERE date_of_birth < '1998-12-01';
SELECT title AS "Book Title", author AS Author FROM books WHERE year_released <= 2015;
SELECT name, description FROM products WHERE price > 9.99;
SELECT title FROM movies WHERE release_year >= 2000;
```

### Searching Within a Set of Values

Writing multiple conditions could could lead to typos and possible errors in our reporting. In this video we'll take a look at a short hand syntax.

**SQL examples:**    

```sql
SELECT <columns> FROM <table> WHERE <column> IN (<value 1>, <value 2>, ...);
```

Examples:

```sql
SELECT name FROM islands WHERE id IN (4, 8, 15, 16, 23, 42);
SELECT * FROM products WHERE category IN ("eBooks", "Books", "Comics");
SELECT title FROM courses WHERE topic IN ("JavaScript", "Databases", "CSS");
SELECT * FROM campaigns WHERE medium IN ("email", "blog", "ppc");
```

To find all rows that are not in the set of values you can use `NOT IN`.

```sql
SELECT <columns> FROM <table> WHERE <column>  NOT IN (<value 1>, <value 2>, ...);
```

Examples:

```sql
SELECT answer FROM answers WHERE id IN (7, 42);
SELECT * FROM products WHERE category NOT IN ("Electronics");
SELECT title FROM courses WHERE topic NOT IN ("SQL", "NoSQL");
```
### Searching Within a Range of Values

Again, writing shorter queries can help with readability and tracking down mistakes in our SQL code. In this video we'll go over the syntax of handling ranges of values in SQL.

**SQL examples:**    

  ```sql
SELECT <columns> FROM <table> WHERE <column> BETWEEN <lesser value> AND <greater value>;
  ```

 Examples:

  ```sql
SELECT * FROM movies WHERE release_year BETWEEN 2000 AND 2010;
SELECT name, description FROM products WHERE price BETWEEN 9.99 AND 19.99;
SELECT name, appointment_date FROM appointments WHERE appointment_date BETWEEN "2015-01-01" AND "2015-01-07";
  ```
### Finding Data that Matches a Pattern

You don't have to be that specific when searching a database table. You can use patterns of characters to help find those trickier bits of data you're trying to track down.

**SQL examples:**    

Placing the percent symbol (`%`) any where in a string in conjunction with the `LIKE` keyword will operate as a wildcard. Meaning it can be substituted by any number of characters, including zero!

```sql
SELECT <columns> FROM <table> WHERE <column> LIKE <pattern>;
```

Examples:

```sql
SELECT title FROM books WHERE title LIKE "Harry Potter%Fire";
SELECT title FROM movies WHERE title LIKE "Alien%";
SELECT * FROM contacts WHERE first_name LIKE "%drew";
SELECT * FROM books WHERE title LIKE "%Brief History%";
```

#### PostgreSQL Specific Keywords

`LIKE` in PostgreSQL is case-sensitive. To case-insensitive searches do `ILIKE`.

```sql
SELECT * FROM contacts WHERE first_name ILIKE "%drew";
```
### Filtering Out or Finding Missing Information

Sometimes you don't have all the information filled out in a row. Whether that's by the design of your database or because someone failed to enter anything, it can be handy to retrieve rows with or without information missing.

```sql
SELECT * FROM loans WHERE return_by > "2015-11-18" AND returned_on IS NULL;
SELECT * FROM loans WHERE return_by > "2015-11-18" AND returned_on IS NOT NULL;
```
