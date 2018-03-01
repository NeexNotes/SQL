# Reporting with SQL

## Retrieving Results in a Particular Order

In this video we're going to take a look at ordering results, that is, retrieving data in a specific order.

#### Ordering by a single column criteria:

```sql
SELECT * FROM <table name> ORDER BY <column> [ASC|DESC];
```

`ASC` is used to order results in ascending order.

`DESC` is used to order results in descending order.

Examples:

```sql
SELECT * FROM books ORDER BY title ASC;
SELECT * FROM products WHERE name = "Sonic T-Shirt" ORDER BY stock_count DESC;
SELECT * FROM users ORDER BY signed_up_on DESC;
SELECT * FROM countries ORDER BY population DESC;
```

#### Ordering by multiple column criteria:

```sql
SELECT * FROM <table name> ORDER BY <column> [ASC|DESC],
                                    <column 2> [ASC|DESC],
                                    ...,
                                    <column n> [ASC|DESC];
```

Ordering is prioritized left to right.

Examples:

```sql
SELECT * FROM books ORDER BY    genre ASC, 
                                title ASC;

SELECT * FROM books ORDER BY    genre ASC,
                                year_published DESC;

SELECT * FROM users ORDER BY    last_name ASC,
                                first_name ASC;
```
## Limiting the Number of Results

Databases can store massive amounts of data, and often you don't want to bring back all of the results. It's slow and it affects the performance for other users. In most cases you only want a certain subset of the rows.

**SQLite, PostgreSQL and MySQL**

To limit the number of results returned, use the `LIMIT` keyword.

```sql lite
SELECT <columns> FROM <table> LIMIT <# of rows>;
SELECT * FROM <table> LIMIT <# of rows>;
SELECT * FROM <table> WHERE <condition> LIMIT <# of rows>;
SELECT * FROM <table> ORDER BY <column> DESC LIMIT <# of rows>;
SELECT * FROM books WHERE genre = "Fantasy" ORDER BY first_published LIMIT 5;
SELECT * FROM books WHERE genre = "Science Fiction" ORDER BY first_published DESC LIMIT 1;
```

**MS SQL**

To limit the number of results returned, use the `TOP` keyword.

```mssql
SELECT TOP <# of rows> <columns> FROM <table>;
```

**Oracle**

To limit the number of results returned, use the `ROWNUM` keyword in a `WHERE` clause.

```sql
SELECT <columns> FROM <table> WHERE ROWNUM <= <# of rows>;
```

## Paging Through Results

Limiting just by the top set of results is a fine thing, but let's say you wanted to generate a multi page report. Having a blog archive or listing search results in batches of 50 is where you want paging.

**SQLite, PostgreSQL and MySQL**  

To page through results you can either use the `OFFSET` keyword in conjunction with the `LIMIT` keyword or just with LIMIT alone.

```sql
SELECT <columns> FROM <table> LIMIT <# of rows> OFFSET <skipped rows>;
SELECT <columns> FROM <table> LIMIT <skipped rows>, <# of rows>;
```

**MS SQL and Oracle**  

To page through results you can either use the `OFFSET` keyword in conjunction with the `FETCH` keyword. Cannot be used with `TOP`.

```mssql
SELECT <columns> FROM <table> OFFSET <skipped rows> ROWS FETCH NEXT <# of rows> ROWS ONLY;
```
## Functions

You've seen keywords and operators, now it's time to see a new concept in the SQL programming language: functions.

**Syntax definitions**  

- **Keywords**: Commands issued to a database. The data presented in queries is unaltered.
- **Operators**: Performs comparisons and simple manipulation
- **Functions**: Presents data differently through more complex manipulation

A function looks like:

```sql
<function name>(<value or column>)
```

Example:

```sql
UPPER("Andrew Chalkley") 
```

### Adding Text Columns Together

You are not restricted by the column definitions in the database schema. You can join columns together so they're more human readable as one.

**SQLite, PostgreSQL and Oracle**  

Use the concatenation operator `||`.

```sql
SELECT <value or column> || <value or column> || <value or column>  FROM <table>;  
```

**MS SQL** 

Use the concatenation operator `+`.

```sql
SELECT <value or column> + <value or column> + <value or column>  FROM <table>;  
```

**MySQL, Postgres and MS SQL**  

Use the `CONCAT()` function.

```sql
SELECT CONCAT(<value or column>, <value or column>, <value or column>) FROM <table>;
```

**example**

```sql
SELECT first_name || " " || last_name || " <" || email ||">" AS "to_field" FROM patrons;
```


| to_field                                   |
| ------------------------------------------ |
| Andrew Chalkley <andrew@teamtreehouse.com> |
| Dave McFarland <dave@teamtreehouse.com>    |
| Alena Holligan <alena@teamtreehouse.com>   |
| Michael Poley <michael@teamtreehouse.com>  |

### Finding the Length of Text

ou can obtain lengths of pieces of text using the LENGTH() function. To obtain the length of a value or column use the LENGTH() function.

```sql
SELECT LENGTH(<value or column>) FROM <tables>;
```

### Changing the Case of Text Columns

There are two functions for changing cases, UPPER() and LOWER(). Let's look how to use them.

Use the `UPPER()` function to uppercase text.

```sql
SELECT UPPER(<value or column>) FROM <table>;
```

Use the `LOWER()` function to lowercase text.

```sql
SELECT LOWER(<value or column>) FROM <table>;
```

### Creating Excerpts From Text

Wouldn't it be cool to create excerpts like this...

To create smaller strings from larger piece of text you can use the SUBSTR() funciton or the substring function.'

```sql
SELECT SUBSTR(<value or column>, <start>, <length>) FROM <table>;
SELECT name, SUBSTR(description, 1, 30) || "..." FROM products;
```
### Replacing Portions of Text

Replacing parts of text is handy for privacy concerns, standardization or improving output.

To replace piece of strings of text in a larger body of text you can use the `REPLACE()` function.

```sql
SELECT REPLACE(<original value or column>, <target string>, <replacement string>) FROM <table>;

SELECT * FROM addresses WHERE REPLACE(state, "California", "CA") = "CA"; ???
SELECT REPLACE(email, "@", "<at>") as obfuscated_email FROM customers;
```

## Counting Results

### Counting Rows

Counting the number of rows is great for answering questions such as "How many users do we have?" and "How many sales happened this week?".

To count rows you can use the `COUNT()` function.

```sql
SELECT COUNT(*) FROM <table>;
```

To count unique entries use the `DISTINCT` keyword too:

```sql
SELECT COUNT(DISTINCT <column>) FROM <table>;
```

example:

```sql
SELECT COUNT(*) AS "scifi_book_count" FROM books WHERE genre = "Science Fiction";
```

### Counting Groups of Rows

It’s often handy to group rows together to count them. For example you could answer the question "How many books are in each genre?"

To count aggregated rows with common values use the `GROUP BY` keywords:

```sql
SELECT COUNT(<column>) FROM <table> GROUP BY <column with common value>;
SELECT category, COUNT(*) AS product_count FROM products GROUP BY category;
```

```
Books 20
CDes 34
Shoes 12
```

### Getting the Grand Total

Calculating grand totals are handy for answering questions like "How much was spent today on the site?" and "What are the total number of goals scored by a particular team?"

o total up numeric columns use the `SUM()` function.

```sql
SELECT SUM(<numeric column) FROM <table>;
SELECT SUM(<numeric column) AS <alias> FROM <table>
                                       GROUP BY <another column>
                                       HAVING <alias> <operator> <value>;
```

```sql
SELECT SUM(cost) AS total_spent, user_id FROM orders
											GROUP BY user_id
											HAVING total_spent > 250
											ORDER BY total_spent DESC;
```

The `HAVING` keyword works just like like `WHERE`, but WHERE cannot be used before GROUP BY because 