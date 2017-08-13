# Install PostgreSQL9.3.6 by docker

## docker pull
```{bash}
	$ docker pull busybox:latest
	$ docker pull postgres:9.3.6
```

## postgresql data folder
```{bash}
	$ cd /home/rwoo/02_WorkSpace/04_PostgreSQL/PostgreSQL/
	$ mkdir -p ./var
	$ mkdir -p ./var/lib
	$ mkdir -p ./var/lib/postgresql
	$ mkdir -p ./var/lib/postgresql/data
```

## docker DataContainer and Container
```{bash}
	$ pwd
	/home/rwoo/02_workspace/08_PostgreSQL_Workspace/PostgreSQL
	
	$ docker create -v `pwd`/var/lib/postgresql/data:/var/lib/postgresql/data --name postgresql9.3.6-DataContainer busybox:latest
	efd04289796bd519aa6a2e1160ed95150f5b757f916fca05b9383c83b540bc76

	$ docker run --name postgresql9.3.6-Container -p 65432:5432 -e POSTGRES_PASSWORD=123qwe -d --volumes-from postgresql9.3.6-DataContainer postgres:9.3.6
	b85570693bcb7277f1823b15dc19cd7edf40a10bff4b943c3bb69051bbf0ad34

	$ docker ps
	CONTAINER ID    IMAGE               COMMAND                  CREATED              STATUS                 PORTS                            NAMES
	b85570693bcb    postgres:9.3.6      "/docker-entrypoin..."   About a minute ago   Up About a minute      0.0.0.0:65432->5432/tcp          postgresql9.3.6-Container
```

## PostgreSQL9.3.6 start on docker container.
```{bash}
	$ docker start postgresql9.3.6-Container 
	postgresql9.3.6-Container

	$ docker exec -it postgresql9.3.6-Container bash
	root@b85570693bcb:/# 
```

## Configure roel, database, privileges.
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
	
## PostgreSQL9.3.6 stop
```{bash}
	postgres=# \q
	
	# exit
	
	$ docker stop postgresql9.3.6-Container 
	postgresql9.3.6-Container

	$ docker ps
	CONTAINER ID	IMAGE	COMMAND 	CREATED 	STATUS 	PORTS 	NAMES

```
