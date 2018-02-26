# SQLite on CLI

SQLite is installed in Linux and Mac (but just in case https://www.tutorialspoint.com/sqlite/sqlite_installation.htm):

```bash
neex@panda ~ $ sqlite3
```

```sql lite
SQLite version 3.20.1 2017-08-24 16:21:36
Enter ".help" for usage hints.
Connected to a transient in-memory database.
Use ".open FILENAME" to reopen on a persistent database.
sqlite> 
```

### Commands

```sql lite
.help // in SQLite
.quit // in SQLite

sqlite3 mydatabase.db //created db on CLI
```

Just use it !!!! :blue_heart:

```sql lite
CREATE TABLE cars (ID PRIMARY KEY, MAKE, MODEL, YEAR);
```

Add stuff on CLI:

```sql lite
INSERT INTO CARS VALUES(2, 'Honda', 'Civic', 2014);
INSERT INTO CARS VALUES(3, 'DeLorean', 'DMC-12', 1982);
INSERT INTO CARS VALUES(4, 'Jeep', 'Cherokee', 2011);
INSERT INTO CARS VALUES(5, 'Tesla', 'Model X', 2017);
INSERT INTO CARS VALUES(6, 'Toyota', 'Prius', 2015);
```

Execute command from a file:

putt all of the above in new_cars.txt:

```sql lite
.read new_cars.txt
```

will insert all of that like before.

Turn headers one and make it look like columns::

```sql lite
sqlite>.headers on
sqlite> SELECT * from cars;

ID|MAKE|MODEL|YEAR
2|Honda|Civic|2014
3|DeLorean|DMC-12|1982
4|Jeep|Cherokee|2011
5|Tesla|Model X|2017
6|Toyota|Prius|2015

sqlite> .mode column
sqlite> SELECT * from cars;

ID          MAKE        MODEL       YEAR      
----------  ----------  ----------  ----------
2           Honda       Civic       2014      
3           DeLorean    DMC-12      1982      
4           Jeep        Cherokee    2011      
5           Tesla       Model X     2017      
6           Toyota      Prius       2015      
```

