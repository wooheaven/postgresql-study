[ Concatenate Columns on PostgresQL ]

PostgreSQL9.3 Document : [Table 9.8. SQL String Functions and Operators] in https://www.postgresql.org/docs/9.3/static/functions-string.html

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

mydatabase=> select id ||','|| name as rows from t ;
  rows  
--------
 1,cam
 2,zoo
 3,adam
(3 rows)
```
