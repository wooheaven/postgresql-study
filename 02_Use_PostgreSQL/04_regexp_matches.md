[ regexp_matches on PostgreSQL]

PostgreSQL9.3 Document https://www.postgresql.org/docs/9.3/static/functions-string.html

```{sql}
mydatabase=> -- regexp_matches capturing group and etc
mydatabase=> SELECT regexp_matches( 'a1=1,2;B2b=2,3,4;C3c={3,4,5;4,5,6};D4d={4,5,6;7,8,9}', '([a-z|A-Z][0-9][a-z]{0,1}=.{0,13};)', 'g');
     regexp_matches     
------------------------
 {"a1=1,2;B2b=2,3,4;"}
 {"C3c={3,4,5;4,5,6};"}
 {"D4d={4,5,6;"}
(3 rows)
``` 
