## Configure role, database, privileges.
```{sql}
        root@b85570693bcb:/# psql -h localhost -p 5432 -U postgres
    
        psql (9.3.6)
        Type "help" for help.

        postgres=# CREATE ROLE myuser WITH LOGIN PASSWORD '123qwe' ;
        CREATE ROLE

        postgres=# \dg 
        List of roles
        Role name |                   Attributes                   | Member of  
        -----------+------------------------------------------------+-----------
        myuser    |                                                | {}
        postgres  | Superuser, Create role, Create DB, Replication | {}

        postgres=# CREATE DATABASE mydatabase WITH OWNER = myuser ENCODING = 'UTF8' ;
        CREATE DATABASE 
    
        postgres=# GRANT ALL privileges ON DATABASE mydatabase TO myuser ;
        GRANT
    
        postgres=# \l
                                         List of databases
            Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
        ------------+----------+----------+------------+------------+-----------------------
         mydatabase | myuser   | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/myuser           +
                    |          |          |            |            | myuser=CTc/myuser
         postgres   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
         template0  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
                    |          |          |            |            | postgres=CTc/postgres
         template1  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
                    |          |          |            |            | postgres=CTc/postgres
        (4 rows)
```

