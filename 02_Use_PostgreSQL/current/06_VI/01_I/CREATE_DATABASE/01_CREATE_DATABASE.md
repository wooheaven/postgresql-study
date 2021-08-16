# CREATE DATABASE
```{sql}
root@b85570693bcb:/# psql -h localhost -p 5432 -U postgres

postgres=# CREATE DATABASE blog WITH OWNER = myuser ENCODING = 'UTF8' TEMPLATE template0 LC_COLLATE 'C' LC_CTYPE 'ko_KR.utf8' ;
CREATE DATABASE

postgres=# \l
                                 List of databases
    Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
------------+----------+----------+------------+------------+-----------------------
 blog       | myuser   | UTF8     | C          | ko_KR.utf8 | 
 postgres   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
            |          |          |            |            | postgres=CTc/postgres
 template1  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
            |          |          |            |            | postgres=CTc/postgres
(4 rows)

postgres=# GRANT ALL privileges ON DATABASE blog TO myuser ;
GRANT

postgres=# \l
                                 List of databases
    Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
------------+----------+----------+------------+------------+-----------------------
 blog       | myuser   | UTF8     | C          | ko_KR.utf8 | =Tc/myuser           +
            |          |          |            |            | myuser=CTc/myuser
 postgres   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
 template0  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
            |          |          |            |            | postgres=CTc/postgres
 template1  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
            |          |          |            |            | postgres=CTc/postgres
(4 rows)
```

# Korean 
```
Encoding(지원하는 문자 집합)
LC_COLLATE(string 정렬 순서) : 'C' 로 지정해야 한글정렬 정상임, 'ko_KR.utf8' 로 지정하면 한글정렬 안됨
LC_CTYPE(문자 분류) : 'ko_KR.utf8' 로 지정하여 한글입력 가능함
```
