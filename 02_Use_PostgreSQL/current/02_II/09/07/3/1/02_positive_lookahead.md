```{sql}
mydatabase=> SELECT  regexp_split_to_table( 'a1=1,2;B2b=2,3,4;C3c={3,4,5;4,5,6};D4d={4,5,6;7,8,9}', '(;(?=[A-Z]))');
 regexp_split_to_table 
-----------------------
 a1=1,2
 B2b=2,3,4
 C3c={3,4,5;4,5,6}
 D4d={4,5,6;7,8,9}
(4 rows)
```
