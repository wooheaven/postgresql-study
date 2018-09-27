# GRANT
```{sql}
root@b85570693bcb:/# psql -h localhost -p 5432 -U postgres

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

postgres=# GRANT ALL privileges ON DATABASE testdatabase TO myuser ;
GRANT

postgres=# \l
                                  List of databases
     Name     |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges
--------------+----------+----------+------------+------------+-----------------------
 postgres     | postgres | UTF8     | en_US.utf8 | en_US.utf8 |
 template0    | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
              |          |          |            |            | postgres=CTc/postgres
 template1    | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
              |          |          |            |            | postgres=CTc/postgres
 testdatabase | myuser   | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/myuser           +
              |          |          |            |            | myuser=CTc/myuser
(4 rows)
```
