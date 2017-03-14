[Install PostgreSQL9.3.6 by docker]
```{text}
# docker pull

	$ docker pull busybox:latest
	$ docker pull postgres:9.3.6

# postgresql data folder


	$ cd /home/rwoo/02_WorkSpace/04_PostgreSQL/PostgreSQL/
	$ mkdir -p ./var
	$ mkdir -p ./var/lib
	$ mkdir -p ./var/lib/postgresql
	$ mkdir -p ./var/lib/postgresql/data

# docker DataContainer and Container

	$ docker create -v /home/rwoo/02_WorkSpace/04_PostgreSQL/PostgreSQL/var/lib/postgresql/data:/var/lib/postgresql/data --name postgres9.3.6-DataContainer busybox:latest
	fdf5eb0b7614461ee6c9b923ed4607717a6f0833ee905d4ba4608046cd08c948

	$ docker run --name postgres9.3.6-Container -p 5432:5432 -e POSTGRES_PASSWORD=123qwe -d --volumes-from postgres9.3.6-DataContainer postgres:9.3.6
	75f9476e383d277fa62f7ccc176d790660a7a1cd83d03079e392d68f17ccc30b

# PostgreSQL9.3.6 start on docker container And Configure database, role, privileges.

	$ docker start 75f9476e383d 
	75f9476e383d

	$ docker exec -it postgres9.3.6-Container sh 
	# psql -h localhost -p 5432 -U postgres
	Password for user postgres: 
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
	
	postgres=# GRANT ALL privileges ON DATABASE mydatabase TO myuser ;
	GRANT
											
	postgres=# \l
	List of databases
	Name    |  Owner   | Encoding |  Collate   |   Ctype    |   Access privileges   
	------------+----------+----------+------------+------------+-----------------------
	mydatabase | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =Tc/postgres         +
	|          |          |            |            | postgres=CTc/postgres+
	|          |          |            |            | myuser=CTc/postgres
	postgres   | postgres | UTF8     | en_US.utf8 | en_US.utf8 | 
	template0  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
	|          |          |            |            | postgres=CTc/postgres
	template1  | postgres | UTF8     | en_US.utf8 | en_US.utf8 | =c/postgres          +
	|          |          |            |            | postgres=CTc/postgres
	(4 rows)
	
# PostgreSQL9.3.6 stop

	postgres=# \q
	
	# exit
	
	$ docker stop 75f9476e383d
	$ docker ps
	CONTAINER ID	IMAGE	COMMAND 	CREATED 	STATUS 	PORTS 	NAMES

```
