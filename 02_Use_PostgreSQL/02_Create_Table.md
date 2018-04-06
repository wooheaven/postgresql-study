# CREATE TABLE
```{sql}
mydatabase=> DROP TABLE IF EXISTS myTable ;
NOTICE:  table "mytable" does not exist, skipping
DROP TABLE

mydatabase=> CREATE TABLE myTable ( num integer NOT NULL, name VARCHAR(40) ) ;
CREATE TABLE

mydatabase=> \d mytable
           Table "public.mytable"
 Column |         Type          | Modifiers 
--------+-----------------------+-----------
 num    | integer               | not null
 name   | character varying(40) | 
``` 

# ref
```
https://www.postgresql.org/docs/current/static/sql-createtable.html
```
