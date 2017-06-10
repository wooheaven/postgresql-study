[ row_number() on PostgreSQL]

PostgreSQL9.3 Document https://www.postgresql.org/docs/9.3/static/functions-window.html

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

mydatabase=> INSERT INTO team_a_b VALUES ('A','a',90) ;
mydatabase=> INSERT INTO team_a_b VALUES ('A','a',80) ;
mydatabase=> INSERT INTO team_a_b VALUES ('A','a',85) ;
mydatabase=> INSERT INTO team_a_b VALUES ('B','b',90) ;
mydatabase=> INSERT INTO team_a_b VALUES ('B','b',100) ;

mydatabase=> SELECT * FROM team_a_b ;
 team | id | score 
------+----+-------
 A    | a  |    90
 A    | a  |    80
 A    | a  |    85
 B    | b  |    90
 B    | b  |   100
(5 rows)

mydatabase=> SELECT team,row_number() OVER (PARTITION BY team ORDER BY score DESC) as new_id,score FROM team_a_b ;
 team | new_id | score 
------+--------+-------
 A    |      1 |    90
 A    |      2 |    85
 A    |      3 |    80
 B    |      1 |   100
 B    |      2 |    90
(5 rows)
``` 
