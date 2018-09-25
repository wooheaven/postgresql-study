# create role
```{sql}
root@ae6b9915c8d5:/# psql -h localhost -p 5432 -U postgres
psql (10.2 (Debian 10.2-1.pgdg90+1))
Type "help" for help.

postgres=# CREATE ROLE myuser WITH LOGIN PASSWORD '123qwe' ;
CREATE ROLE

postgres=# \dg 
List of roles
Role name |                   Attributes                   | Member of  
-----------+------------------------------------------------+-----------
myuser    |                                                | {}
postgres  | Superuser, Create role, Create DB, Replication | {}

postgres=# SELECT * FROM PG_SHADOW;
 usename  | usesysid | usecreatedb | usesuper | userepl | usebypassrls |               passwd                | valuntil | useconfig 
----------+----------+-------------+----------+---------+--------------+-------------------------------------+----------+-----------
 postgres |       10 | t           | t        | t       | t            | md533a9a79ffee1cc8bf4fbc63f24518e44 |          | 
 myuser   |    16384 | f           | f        | f       | f            | md57ce713c078f8aaabd7254eeb4c57aa5e |          | 
(2 rows)
```
