# Configure postgresql.conf
```{sql}
root@78779b6363ea:/# psql -U postgres

psql (10.4 (Debian 10.4-2.pgdg90+1))
Type "help" for help.

postgres=# SHOW config_file ;
               config_file
------------------------------------------
 /var/lib/postgresql/data/postgresql.conf
(1 row)

postgres=# SHOW data_directory ;
      data_directory
--------------------------
 /var/lib/postgresql/data
(1 row)

postgres=# \q
```

```{bash}
root@78779b6363ea:/# grep log_destination /var/lib/postgresql/data/postgresql.conf
#log_destination = 'stderr'        # Valid values are combinations of

root@78779b6363ea:/# sed -i "s/#log_destination \= 'stderr'/log_destination \= 'csvlog'/g" /var/lib/postgresql/data/postgresql.conf

root@78779b6363ea:/# grep log_destination /var/lib/postgresql/data/postgresql.conf
log_destination = 'csvlog'        # Valid values are combinations of

root@78779b6363ea:/# grep logging_collector /var/lib/postgresql/data/postgresql.conf
                    # requires logging_collector to be on.
#logging_collector = off        # Enable capturing of stderr and csvlog
# These are only used if logging_collector is on:

root@78779b6363ea:/# sed -i "s/#logging_collector \= off/logging_collector \= on/g" /var/lib/postgresql/data/postgresql.conf

root@78779b6363ea:/# grep logging_collector /var/lib/postgresql/data/postgresql.conf
                    # requires logging_collector to be on.
logging_collector = on        # Enable capturing of stderr and csvlog
# These are only used if logging_collector is on:

root@78779b6363ea:/# grep log_directory /var/lib/postgresql/data/postgresql.conf
#log_directory = 'log'            # directory where log files are written,

root@78779b6363ea:/# sed -i "s/#log_directory \= 'log'/log_directory \= 'pg_log'/g" /var/lib/postgresql/data/postgresql.conf

root@78779b6363ea:/# grep log_directory /var/lib/postgresql/data/postgresql.conf
log_directory = 'pg_log'            # directory where log files are written,

root@78779b6363ea:/# grep log_filename /var/lib/postgresql/data/postgresql.conf
#log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'    # log file name pattern,

root@78779b6363ea:/# sed -i "s/#log_filename/log_filename/" /var/lib/postgresql/data/postgresql.conf

root@78779b6363ea:/# grep log_filename /var/lib/postgresql/data/postgresql.conf
log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'    # log file name pattern,

root@78779b6363ea:/# grep log_statement /var/lib/postgresql/data/postgresql.conf
#log_statement = 'none'            # none, ddl, mod, all
#log_statement_stats = off

root@78779b6363ea:/# sed -i "s/#log_statement \= 'none'/log_statement \= 'all'/" /var/lib/postgresql/data/postgresql.conf

root@78779b6363ea:/# grep log_statement postgresql.conf
log_statement = 'all'            # none, ddl, mod, all
#log_statement_stats = off

root@78779b6363ea:/# exit
exit

user@ubuntu:~$ docker stop pg
pg

user@ubuntu:~$ docker start pg
pg

user@ubuntu:~$ docker exec -it pg bash
```

```{bash}
root@78779b6363ea:/# tail -f /var/lib/postgresql/data/pg_log/postgresql-2018-10-02_0
postgresql-2018-10-02_064821.csv  postgresql-2018-10-02_064821.log  postgresql-2018-10-02_071818.csv  postgresql-2018-10-02_071818.log
root@78779b6363ea:/# tail -f /var/lib/postgresql/data/pg_log/postgresql-2018-10-02_071818.csv
2018-10-02 07:18:18.021 UTC,,,1,,5bb31bb9.1,1,,2018-10-02 07:18:17 UTC,,0,LOG,00000,"ending log output to stderr",,"Future log output will go to log destination ""csvlog"".",,,,,,,""
2018-10-02 07:18:18.053 UTC,,,25,,5bb31bba.19,1,,2018-10-02 07:18:18 UTC,,0,LOG,00000,"database system was shut down at 2018-10-02 07:18:11 UTC",,,,,,,,,""
2018-10-02 07:18:18.089 UTC,,,1,,5bb31bb9.1,2,,2018-10-02 07:18:17 UTC,,0,LOG,00000,"database system is ready to accept connections",,,,,,,,,""
2018-10-02 07:19:06.660 UTC,"myuser","mydatabase",55,"127.0.0.1:34982",5bb31be7.37,1,"idle",2018-10-02 07:19:03 UTC,3/4,0,LOG,00000,"statement: SELECT n.nspname as ""Schema"",
  c.relname as ""Name"",
  CASE c.relkind WHEN 'r' THEN 'table' WHEN 'v' THEN 'view' WHEN 'm' THEN 'materialized view' WHEN 'i' THEN 'index' WHEN 'S' THEN 'sequence' WHEN 's' THEN 'special' WHEN 'f' THEN 'foreign table' WHEN 'p' THEN 'table' END as ""Type"",
  pg_catalog.pg_get_userbyid(c.relowner) as ""Owner""
FROM pg_catalog.pg_class c
     LEFT JOIN pg_catalog.pg_namespace n ON n.oid = c.relnamespace
WHERE c.relkind IN ('r','p','v','m','S','f','')
      AND n.nspname <> 'pg_catalog'
      AND n.nspname <> 'information_schema'
      AND n.nspname !~ '^pg_toast'
  AND pg_catalog.pg_table_is_visible(c.oid)
ORDER BY 1,2;",,,,,,,,,"psql"
2018-10-02 07:19:23.636 UTC,"myuser","mydatabase",55,"127.0.0.1:34982",5bb31be7.37,2,"idle",2018-10-02 07:19:03 UTC,3/5,0,LOG,00000,"statement: SELECT pg_catalog.quote_ident(c.relname) FROM pg_catalog.pg_class c WHERE c.relkind IN ('r', 'p') AND substring(pg_catalog.quote_ident(c.relname),1,2)='te' AND pg_catalog.pg_table_is_visible(c.oid) AND c.relnamespace <> (SELECT oid FROM pg_catalog.pg_namespace WHERE nspname = 'pg_catalog')
UNION
SELECT pg_catalog.quote_ident(n.nspname) || '.' FROM pg_catalog.pg_namespace n WHERE substring(pg_catalog.quote_ident(n.nspname) || '.',1,2)='te' AND (SELECT pg_catalog.count(*) FROM pg_catalog.pg_namespace WHERE substring(pg_catalog.quote_ident(nspname) || '.',1,2) = substring('te',1,pg_catalog.length(pg_catalog.quote_ident(nspname))+1)) > 1
UNION
SELECT pg_catalog.quote_ident(n.nspname) || '.' || pg_catalog.quote_ident(c.relname) FROM pg_catalog.pg_class c, pg_catalog.pg_namespace n WHERE c.relnamespace = n.oid AND c.relkind IN ('r', 'p') AND substring(pg_catalog.quote_ident(n.nspname) || '.' || pg_catalog.quote_ident(c.relname),1,2)='te' AND substring(pg_catalog.quote_ident(n.nspname) || '.',1,2) = substring('te',1,pg_catalog.length(pg_catalog.quote_ident(n.nspname))+1) AND (SELECT pg_catalog.count(*) FROM pg_catalog.pg_namespace WHERE substring(pg_catalog.quote_ident(nspname) || '.',1,2) = substring('te',1,pg_catalog.length(pg_catalog.quote_ident(nspname))+1)) = 1
LIMIT 1000",,,,,,,,,"psql"
2018-10-02 07:19:24.790 UTC,"myuser","mydatabase",55,"127.0.0.1:34982",5bb31be7.37,3,"idle",2018-10-02 07:19:03 UTC,3/6,0,LOG,00000,"statement: drop table test ;",,,,,,,,,"psql"
```

```{bash}
user@ubuntu:~$ docker exec -it pg bash

root@78779b6363ea:/# ./mydatabase.sh
psql (10.4 (Debian 10.4-2.pgdg90+1))
Type "help" for help.
```

```{sql}
mydatabase=> \d
                    List of relations
 Schema |            Name             |   Type   | Owner
--------+-----------------------------+----------+--------
 public | asis_graph                  | table    | myuser
 public | asis_graph_policy_id_seq    | sequence | myuser
 public | cth                         | table    | myuser
 public | greedy_graph                | table    | myuser
 public | greedy_graph_policy_id_seq  | sequence | myuser
 public | new_graph                   | table    | myuser
 public | new_graph_policy_id_seq     | sequence | myuser
 public | softmax_graph               | table    | myuser
 public | softmax_graph_policy_id_seq | sequence | myuser
 public | states                      | table    | myuser
 public | states_id_seq               | sequence | myuser
 public | states_tmp                  | table    | myuser
 public | states_tmp_id_seq           | sequence | myuser
 public | t1                          | table    | myuser
 public | t2                          | table    | myuser
 public | test                        | table    | myuser
(16 rows)

mydatabase=> drop table test ;
DROP TABLE
```

```{sql}
root@78779b6363ea:/# cat >> rm_pg_log_files.sh << EOF
> rm /var/lib/postgresql/data/pg_log/*
> ls -lh /var/lib/postgresql/data/pg_log/
> EOF

root@78779b6363ea:/# chmod +x rm_pg_log_files.sh
total 0

root@78779b6363ea:/# cat >> tail_pg_log_file.sh << EOF
> tail -f /var/lib/postgresql/data/pg_log/postgresql-*.csv
> EOF
root@78779b6363ea:/# chmod +x tail_pg_log_file.sh
```
