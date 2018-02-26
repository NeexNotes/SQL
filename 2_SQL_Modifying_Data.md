# Modifying Data with SQL

## Introduction to CRUD

Data isn't static, it changes over time. Databases allow you to modify that data over time.

Four Main Data Operations

- Create
- Read
- Update
- Delete


### Adding a Row to a Table

In this video we'll take a look at adding rows of information into a table.

**SQL examples:**

Inserting a single row:

```sql
INSERT INTO <table> VALUES (<value 1>, <value 2>, ...);
```

This will insert values in the order of the columns prescribed in the schema.

Examples:

```sql
INSERT INTO users VALUES  (1, "chalkers", "Andrew", "Chalkley");
INSERT INTO users VALUES  (2, "ScRiPtKiDdIe", "Kenneth", "Love");

INSERT INTO movies VALUES (3, "Starman", "Science Fiction", 1984);
INSERT INTO movies VALUES (4, "Moulin Rouge!", "Musical", 2001);
```

Inserting a single row with values in any order (have to specify them in wanted order):

```sql
INSERT INTO <table> (<column 1>, <column 2>) VALUES (<value 1>, <value 2>);
INSERT INTO <table> (<column 2>, <column 1>) VALUES (<value 2>, <value 1>);
```

Examples:

```sql
INSERT INTO users (username, first_name, last_name) VALUES ("chalkers", "Andrew", "Chalkley");
INSERT INTO users (first_name, last_name, username) VALUES  ("Kenneth", "Love", "ScRiPtKiDdIe");

INSERT INTO movies (title, genre, year_released) VALUES ("Starman", "Science Fiction", 1984);
INSERT INTO movies (title, year_released, genre) VALUES ("Moulin Rouge!", 2001,  "Musical");
```

See all of the SQL used in Modifying Data With SQL in the  - SQL_modifying_data_cheatsheet.md

### Adding Multiple Rows to a Table

Inserting data into a table doesn't have to be restricted to one row at a time. You can insert multiple rows in a single statement. You can use as much space and return as you need to make it look nice. It is all based on commas and semis ,;

**SQL examples:**  

Inserting multiple rows in a single statement:

```sql
INSERT INTO <table> (<column 1>, <column 2>, ...) 
             VALUES 
                    (<value 1>, <value 2>, ...),
                    (<value 1>, <value 2>, ...),
                    (<value 1>, <value 2>, ...);
```

Examples:

```sql
INSERT INTO users (username, first_name, last_name) 
    VALUES 
                  ("chalkers", "Andrew", "Chalkley"),
                  ("ScRiPtKiDdIe", "Kenneth", "Love");

INSERT INTO movies (title, genre, year_released) 
     VALUES 
                   ("Starman", "Science Fiction", 1984),
                   ("Moulin Rouge!", "Musical", 2001);
```

### Updating All Rows in a Table

**SQL examples:**  

An update statement for all rows:

```sql
UPDATE <table> SET <column> = <value>;
```

The `=` sign is different from an equality operator from a `WHERE` condition. It's an assignment operator because you're assigning a new value to something that is already there.

Examples:

```sql
UPDATE users SET password = "thisisabadidea"; -- all passwords / in all rows
UPDATE products SET price = 2.99; -- all prices / in all rows
```

Update multiple columns in all rows:

```sql
UDPATE <table> SET <column 1> = <value 1>, <column 2> = <value 2>;
```

Examples:

```sql
UPDATE users SET first_name = "Anony", last_name = "Moose";
UPDATE products SET stock_count = 0, price = 0;
```
### Updating Specific Rows

It's more useful to update specific rows. Like with SELECT statements, you can use conditions to target specific rows.

**SQL examples:**  

An update statement for specific rows:

```sql
UPDATE <table> SET <column> = <value>;
UPDATE <table> SET <column> = <value> WHERE <condition>;
```

Examples:

```sql
UPDATE users SET password = "thisisabadidea" WHERE id = 3;
UPDATE blog_posts SET view_count = 1923 WHERE title = "SQL is Awesome";
```

Update multiple columns for specific rows:

```sql
UPDATE <table> SET <column 1> = <value 1>, <column 2> = <value 2> WHERE <condition>;
```

Examples:

```sql
UPDATE users SET entry_url = "/home", last_login = "2016-01-05" WHERE id = 329;
UPDATE products SET status = "SOLD OUT", availability = "In 1 Week" WHERE stock_count = 0;
```

### Removing Data from All Rows in a Table

In this video we'll see how to delete all data from a table.

**SQL examples:**  

To delete **ALL** rows from a table:

```sql
DELETE FROM <table>;
```

Examples:

```sql
DELETE FROM logs;
DELETE FROM users;
DELETE FROM products;
```

### Removing Specific Rows

Like with SELECT and UPDATE statements, you can use a WHERE clause to narrow in on specific rows to remove for a table.

**SQL examples:**  

To delete specific rows from a table:

```sql
DELETE FROM <table> WHERE <condition>;
```

Examples:

```sql
DELETE FROM users WHERE email = "andrew@teamtreehouse.com";
DELETE FROM movies WHERE genre = "Musical";
DELETE FROM products WHERE stock_count = 0;
DELETE FROM products WHERE color = "green" AND price = 0.99;
```

## Database AUTO-COMMIT

### Introduction to Transactions

When seeding or populating a database for the first time, you will have lots of data to add. But what happens when there's an error in the middle of that process?

**Definitions**  

* **Autocommit** - every statement you write gets saved to disk.
* **Seeding** - populating a database for the first time.
* **Script file** - a file containing SQL statements.

**SQL Used:**

Switch autocommit off and begin a transaction:

```sql
BEGIN TRANSACTION;
```

Or simply:

```sql
BEGIN;
```

To save all results of the statements after the start of the transaction to disk:

```sql
COMMIT;
```
### Rollback

Sometimes errors happen in the middle of a transaction. How do you recover from that? This video shows you how!

To reset the state of the database to before the beginning of the transaction:

```sql
BEGIN;
* do some stuf here *
ROLLBACK; -- BEFORE COMMIT!
```
### Databases with Frameworks

Many developers, while using databases, aren't required to write a single line of SQL code. They use special software libraries called ORMs.

**Definitions**  

**ORM** - Object-Relational Mapping – used to perform CRUD operations with a language other than SQL.
**DML** - Data Manipulation Language - the subset of the SQL programming language that deals with CRUD operations.

**Examples of ORMs**  

- [Hibernate](http://hibernate.org/) for Java
- [CoreData](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CoreData/index.html) for Objective-C or Swift
- [Django ORM](https://docs.djangoproject.com/en/1.9/#the-model-layer) for Python
- [ActiveRecord](http://api.rubyonrails.org/classes/ActiveRecord/Base.html) for Ruby

