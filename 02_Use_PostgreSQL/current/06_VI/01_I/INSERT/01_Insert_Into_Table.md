[ Insert Into Table on PostgreSQL]

PostgreSQL9.3 Document https://www.postgresql.org/docs/9.3/static/sql-insert.html

```{sql}
mydatabase=> INSERT INTO mytable (num, name) VALUES (1, 'bobby') ;
INSERT 0 1

mydatabase=> SELECT num, name FROM mytable ;
 num | name  
-----+-------
   1 | bobby
(1 row)
``` 
