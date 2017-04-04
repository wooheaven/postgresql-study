[ Create Table on PostgreSQL]

PostgreSQL9.3 Document https://www.postgresql.org/docs/9.3/static/sql-createtable.html

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
