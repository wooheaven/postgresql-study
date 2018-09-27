# CREATE DATABASE
```{sql}
root@b85570693bcb:/# psql -h localhost -p 5432 -U postgres

postgres=# CREATE DATABASE testdatabase WITH OWNER = myuser ENCODING = 'UTF8' ;
CREATE DATABASE

postgres=# \l
                                  List of databases
     Name     |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
--------------+----------+----------+------------+------------+-----------------------
 postgres     | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0    | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
              |          |          |            |            | postgres=CTc/postgres
 template1    | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
              |          |          |            |            | postgres=CTc/postgres
 testdatabase | myuser   | UTF8     | en_US.utf8 | en_US.utf8 |
(4 rows)
```
