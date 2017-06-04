# run PostgreSQL on docker
```{bash}
	# on host

	$ docker start postgresql9.3.6-Container 
	postgresql9.3.6-Container

	$ docker exec -it postgresql9.3.6-Container bash
	
		# on container

		root@b85570693bcb:/# 
		
		root@b85570693bcb:/# psql -h localhost -p 5432 -U postgres
		psql (9.3.6)
		Type "help" for help.

		postgres=# \q

		root@b85570693bcb:/# exit
		exit

	$
```
