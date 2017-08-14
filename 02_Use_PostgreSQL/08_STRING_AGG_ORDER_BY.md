[ Concatenate Columns on PostgresQL ]

PostgreSQL9.3 Document https://www.postgresql.org/docs/9.3/static/functions-aggregate.html

```{sql}
mydatabase=> CREATE TABLE t (
mydatabase(>     id int,
mydatabase(>     name text
mydatabase(> ) ;
CREATE TABLE

mydatabase=> INSERT INTO t ( id, name ) VALUES ( 1, 'cam' ) ;
INSERT 0 1
mydatabase=> INSERT INTO t ( id, name ) VALUES ( 2, 'zoo' ) ;
INSERT 0 1
mydatabase=> INSERT INTO t ( id, name ) VALUES ( 3, 'adam' ) ;
INSERT 0 1

mydatabase=> SELECT * FROM t ;
 id | name 
----+------
  1 | cam
  2 | zoo
  3 | adam
(3 rows)

mydatabase=> SELECT STRING_AGG( name, ' | ' ) FROM t ;
    string_agg    
------------------
 cam | zoo | adam
(1 row)

mydatabase=> SELECT STRING_AGG( name, ' | ' ORDER BY name ) FROM t ;
    string_agg    
------------------
 adam | cam | zoo
(1 row)

mydatabase=> SELECT STRING_AGG( new_name, ' | ' )
mydatabase-> FROM (
mydatabase(>     SELECT name as new_name
mydatabase(>     FROM t
mydatabase(>     ORDER BY name
mydatabase(> ) AS a ;
    string_agg    
------------------
 adam | cam | zoo
(1 row)
```
