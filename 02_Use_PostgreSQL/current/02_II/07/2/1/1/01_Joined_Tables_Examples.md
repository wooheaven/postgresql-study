# prepare input table
```{sql}
mydatabase=> CREATE TABLE t1 (num integer primary key, name varchar(1)) ;
CREATE TABLE

mydatabase=> INSERT INTO t1 (num,name) VALUES (1,'a') ;
INSERT 0 1
mydatabase=> INSERT INTO t1 (num,name) VALUES (2,'b') ;
INSERT 0 1
mydatabase=> INSERT INTO t1 (num,name) VALUES (3,'c') ;
INSERT 0 1

mydatabase=> SELECT * FROM t1 ;
 num | name
-----+------
   1 | a
   2 | b
   3 | c
(3 rows)

mydatabase=> CREATE TABLE t2 (num integer primary key, value varchar(1)) ;
CREATE TABLE

mydatabase=> INSERT INTO t2 (num,value) VALUES (2,'y') ;
INSERT 0 1
mydatabase=> INSERT INTO t2 (num,value) VALUES (3,'z') ;
INSERT 0 1
mydatabase=> INSERT INTO t2 (num,value) VALUES (4,'z') ;
INSERT 0 1

mydatabase=> SELECT * FROM t2 ;
 num | value
-----+-------
   2 | x
   3 | y
   4 | z
(3 rows)
```

# cross join
```{sql}
mydatabase=> SELECT * FROM t1 CROSS JOIN t2 ;
 num | name | num | value
-----+------+-----+-------
   1 | a    |   2 | x
   1 | a    |   3 | y
   1 | a    |   4 | z
   2 | b    |   2 | x
   2 | b    |   3 | y
   2 | b    |   4 | z
   3 | c    |   2 | x
   3 | c    |   3 | y
   3 | c    |   4 | z
(9 rows)

-- For every possible combination of rows from T1 and T2 (i.e., a Cartesian product), 
-- the joined table will contain a row consisting of all columns in T1 followed by all columns in T2.
```

# inner (outer) join 
```{sql}
mydatabase=> SELECT * FROM t1 INNER JOIN t2 ON t1.num = t2.num;
 num | name | num | value
-----+------+-----+-------
   2 | b    |   2 | x   
   3 | c    |   3 | y   
(2 rows)

mydatabase=> SELECT * FROM t1 INNER JOIN t2 USING (num);
 num | name | value
-----+------+-------
   2 | b    | x
   3 | c    | y
(2 rows)

-- For each row R1 of T1, 
-- the joined table has a row for each row in T2 that satisfies the join condition with R1.
```

# left (outer) join
```{sql}
mydatabase=> SELECT * FROM t1 LEFT JOIN t2 ON t1.num = t2.num;
 num | name | num | value
-----+------+-----+-------
   1 | a    |     |
   2 | b    |   2 | x
   3 | c    |   3 | y
(3 rows)

mydatabase=> SELECT * FROM t1 LEFT JOIN t2 USING(num);
 num | name | value
-----+------+-------
   1 | a    |
   2 | b    | x
   3 | c    | y
(3 rows)

-- First, an inner join is performed. 
-- Then, for each row in T1 that does not satisfy the join condition with any row in T2, 
-- a joined row is added with null values in columns of T2. 
-- Thus, the joined table always has at least one row for each row in T1.
```

# right (outer) join
```{sql}
mydatabase=> SELECT * FROM t1 RIGHT JOIN t2 ON t1.num = t2.num;
 num | name | num | value
-----+------+-----+-------
   2 | b    |   2 | x
   3 | c    |   3 | y
     |      |   4 | z
(3 rows)

mydatabase=> SELECT * FROM t1 RIGHT JOIN t2 USING(num);
 num | name | value
-----+------+-------
   2 | b    | x
   3 | c    | y
   4 |      | z
(3 rows)

-- First, an inner join is performed. 
-- Then, for each row in T2 that does not satisfy the join condition with any row in T1, 
-- a joined row is added with null values in columns of T1. 
-- This is the converse of a left join: 
-- the result table will always have a row for each row in T2.
```

# full (outer) join
```{sql}
mydatabase=> SELECT * FROM t1 FULL JOIN t2 ON t1.num = t2.num;
 num | name | num | value
-----+------+-----+-------
   1 | a    |     |
   2 | b    |   2 | x
   3 | c    |   3 | y
     |      |   4 | z
(4 rows)

mydatabase=> SELECT * FROM t1 FULL JOIN t2 USING(num) ;
 num | name | value
-----+------+-------
   1 | a    |
   2 | b    | x
   3 | c    | y
   4 |      | z
(4 rows)

-- First, an inner join is performed. 
-- Then, for each row in T1 that does not satisfy the join condition with any row in T2, 
-- a joined row is added with null values in columns of T2. 
-- Also, for each row of T2 that does not satisfy the join condition with any row in T1, 
-- a joined row with null values in the columns of T1 is added.
```

# matters on outer joins.
```{sql}
mydatabase=> SELECT * FROM t1 LEFT JOIN t2 ON t1.num = t2.num AND t2.value = 'x';
 num | name | num | value
-----+------+-----+-------
   1 | a    |     |
   2 | b    |   2 | x
   3 | c    |     |
(3 rows)

mydatabase=> SELECT * FROM t1 LEFT JOIN t2 ON t1.num = t2.num WHERE t2.value = 'x';
 num | name | num | value
-----+------+-----+-------
   2 | b    |   2 | x
(1 row)

-- This is because a restriction placed in the ON clause is processed before the join, 
-- while a restriction placed in the WHERE clause is processed after the join.
-- That does not matter with inner joins, but it matters a lot with outer joins.
```