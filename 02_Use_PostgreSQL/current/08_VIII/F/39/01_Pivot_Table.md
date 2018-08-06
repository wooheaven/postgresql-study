[ Pivot Table on PostgresQL ]

PostgreSQL9.6 Document https://www.postgresql.org/docs/current/static/tablefunc.html

Login as superuser like postgres
```{bash}
root@e2f2397d8ee3:/# psql -h localhost -p 5432 -U postgres -d mydatabase
psql (9.6.4)
Type "help" for help.

mydatabase=#
```
Create Extension
```{sql}
mydatabase=# CREATE EXTENSION tablefunc ;
CREATE EXTENSION
mydatabase=# \q
```

Login as user
```{bash}
root@e2f2397d8ee3:/# psql -h localhost -p 5432 -U myuser -d mydatabase
mydatabase=>
```

Create Table and Insert into Table
```{sql}
mydatabase=> create table sales(year int, month int, qty int);

mydatabase=> insert into sales values(2007, 1, 1000);
mydatabase=> insert into sales values(2007, 2, 1500);
mydatabase=> insert into sales values(2007, 7, 500);
mydatabase=> insert into sales values(2007, 11, 1500);
mydatabase=> insert into sales values(2007, 12, 2000);
mydatabase=> insert into sales values(2008, 1, 1000);
```

Pivot Table
```{sql}
mydatabase=> SELECT * FROM sales ;
 year | month | qty
------+-------+------
 2007 |     1 | 1000
 2007 |     2 | 1500
 2007 |     7 |  500
 2007 |    11 | 1500
 2007 |    12 | 2000
 2008 |     1 | 1000
(6 rows)

mydatabase=> 
select * from crosstab(
    'select year, month, qty from sales order by 1',
    'select m from generate_series(1,12) m'
 ) as (
    year int,
    "Jan" int,
    "Feb" int,
    "Mar" int,
    "Apr" int,
    "May" int,
    "Jun" int,
    "Jul" int,
    "Aug" int,
    "Sep" int,
    "Oct" int,
    "Nov" int,
    "Dec" int
 );

 year | Jan  | Feb  | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov  | Dec
------+------+------+-----+-----+-----+-----+-----+-----+-----+-----+------+------
 2007 | 1000 | 1500 |     |     |     |     | 500 |     |     |     | 1500 | 2000
 2008 | 1000 |      |     |     |     |     |     |     |     |     |      |
(2 rows)
```

Create Table and Insert into Table
```{sql}
mydatabase=> CREATE TABLE cth(rowid text, rowdt timestamp, attribute text, val text);

mydatabase=> INSERT INTO cth VALUES('test1','01 March 2003','temperature','42');
mydatabase=> INSERT INTO cth VALUES('test1','01 March 2003','test_result','PASS');
mydatabase=> INSERT INTO cth VALUES('test1','01 March 2003','volts','2.6987');
mydatabase=> INSERT INTO cth VALUES('test2','02 March 2003','temperature','53');
mydatabase=> INSERT INTO cth VALUES('test2','02 March 2003','test_result','FAIL');
mydatabase=> INSERT INTO cth VALUES('test2','02 March 2003','test_startdate','01 March 2003');
mydatabase=> INSERT INTO cth VALUES('test2','02 March 2003','volts','3.1234');
```

Pivot Table
```{sql}
mydatabase=> SELECT * FROM cth ;
 rowid |        rowdt        |   attribute    |      val
-------+---------------------+----------------+---------------
 test1 | 2003-03-01 00:00:00 | temperature    | 42
 test1 | 2003-03-01 00:00:00 | test_result    | PASS
 test1 | 2003-03-01 00:00:00 | volts          | 2.6987
 test2 | 2003-03-02 00:00:00 | temperature    | 53
 test2 | 2003-03-02 00:00:00 | test_result    | FAIL
 test2 | 2003-03-02 00:00:00 | test_startdate | 01 March 2003
 test2 | 2003-03-02 00:00:00 | volts          | 3.1234
(7 rows)

mydatabase=> 
SELECT * FROM crosstab (
    'SELECT rowid, rowdt, attribute, val FROM cth ORDER BY 1',
    'SELECT DISTINCT attribute FROM cth ORDER BY 1'
) AS (
    rowid text,
    rowdt timestamp,
    temperature int4,
    test_result text,
    test_startdate timestamp,
    volts float8
);
 rowid |          rowdt           | temperature | test_result |      test_startdate      | volts
-------+--------------------------+-------------+-------------+--------------------------+--------
 test1 | Sat Mar 01 00:00:00 2003 |          42 | PASS        |                          | 2.6987
 test2 | Sun Mar 02 00:00:00 2003 |          53 | FAIL        | Sat Mar 01 00:00:00 2003 | 3.1234
(2 rows)
```
