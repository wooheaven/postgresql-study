[ COPY on PostgreSQL]

PostgreSQL9.3 Document https://www.postgresql.org/docs/9.3/static/sql-copy.html
```{bash}
$ cat Team_A_B.csv
A,a,90
A,a,80
A,a,85
B,b,90
B,b,100
```
```{sql}
mydatabase=> DROP TABLE IF EXISTS team_a_b ;
NOTICE:  table "team_a_b" does not exist, skipping
DROP TABLE

mydatabase=> CREATE TABLE Team_A_B (
mydatabase(> team VARCHAR(2),
mydatabase(> id VARCHAR(1),
mydatabase(> score INT
mydatabase(> )
mydatabase-> ;
CREATE TABLE

mydatabase=> COPY Team_A_B FROM '/Team_A_B.csv' WITH DELIMITER ',' ;
ERROR:  must be superuser to COPY to or from a file
HINT:  Anyone can COPY to stdout or from stdin. psql's \copy command also works for anyone.

mydatabase=> \COPY Team_A_B FROM '/Team_A_B.csv' WITH DELIMITER ',' ;

mydatabase=> SELECT * FROM Team_A_B ;
 team | id | score 
------+----+-------
 A    | a  |    90
 A    | a  |    80
 A    | a  |    85
 B    | b  |    90
 B    | b  |   100
(5 rows)

mydatabase=> COPY Team_A_B TO '/Team_A_B_tmp.csv' WITH DELIMITER ',' ;
ERROR:  must be superuser to COPY to or from a file
HINT:  Anyone can COPY to stdout or from stdin. psql's \copy command also works for anyone.

mydatabase=> \COPY Team_A_B TO '/Team_A_B_tmp.csv' WITH DELIMITER ',' ;
```
```{bash}
root@b85570693bcb:/# cat Team_A_B_tmp.csv 
A,a,90
A,a,80
A,a,85
B,b,90
B,b,100
```
