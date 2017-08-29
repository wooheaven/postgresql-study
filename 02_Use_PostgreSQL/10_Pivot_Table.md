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
mydatabase=> select * from crosstab(
mydatabase=>     'select year, month, qty from sales order by 1',
mydatabase=>     'select m from generate_series(1,12) m'
mydatabase=> ) as (
mydatabase=>     year int,
mydatabase=>     "Jan" int,
mydatabase=>     "Feb" int,
mydatabase=>     "Mar" int,
mydatabase=>     "Apr" int,
mydatabase=>     "May" int,
mydatabase=>     "Jun" int,
mydatabase=>     "Jul" int,
mydatabase=>     "Aug" int,
mydatabase=>     "Sep" int,
mydatabase=>     "Oct" int,
mydatabase=>     "Nov" int,
mydatabase=>     "Dec" int
mydatabase=> );

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
mydatabase=> SELECT * FROM crosstab (
mydatabase=>     'SELECT rowid, rowdt, attribute, val FROM cth ORDER BY 1',
mydatabase=>     'SELECT DISTINCT attribute FROM cth ORDER BY 1'
mydatabase=> ) AS (
mydatabase=>     rowid text,
mydatabase=>     rowdt timestamp,
mydatabase=>     temperature int4,
mydatabase=>     test_result text,
mydatabase=>     test_startdate timestamp,
mydatabase=>     volts float8
mydatabase=> );

 rowid |          rowdt           | temperature | test_result |      test_startdate      | volts
-------+--------------------------+-------------+-------------+--------------------------+--------
 test1 | Sat Mar 01 00:00:00 2003 |          42 | PASS        |                          | 2.6987
 test2 | Sun Mar 02 00:00:00 2003 |          53 | FAIL        | Sat Mar 01 00:00:00 2003 | 3.1234
(2 rows)
```
