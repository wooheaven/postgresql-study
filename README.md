# Install and Run PostgreSQL
&ensp;[Install PostgreSQL9.3.6 : on docker](01_Install_and_Run_PostgreSQL/01_Install_PostgreSQL9.3.6_on_docker.md)  
&ensp;[Run PostgreSQL9.3.6 : on docker](01_Install_and_Run_PostgreSQL/02_Run_PostgreSQL9.3.6_on_docker.md)

# Documents
[PostgreSQL current Documentation](https://www.postgresql.org/docs/current/static/index.html)  
Table of Contents  
╠═II. [The SQL Language](https://www.postgresql.org/docs/current/static/sql.html)  
║&ensp; ╠═8. [Data Types](https://www.postgresql.org/docs/current/static/datatype.html)  
║&ensp; ║&ensp; ╚═8.1. [Numeric Types](https://www.postgresql.org/docs/current/static/datatype-numeric.html)  
║&ensp; ║&ensp; &ensp; &ensp; ╚═8.1.4. [Serial Types](https://www.postgresql.org/docs/current/static/datatype-numeric.html#DATATYPE-SERIAL)    
║&ensp; ║&ensp; &ensp; &ensp; &ensp; &ensp; ╚═8.1.4.1. [add column id as SERIAL NOT NULL PRIMARY KEY](02_Use_PostgreSQL/current/02_II/08/01/4/01_add_column_as_serial_to_prevent_duplication.md)  
║&ensp; ╚═9. [Functions and Operators](https://www.postgresql.org/docs/current/static/functions.html)  
║&ensp; &ensp; &ensp; ╠═9.4. [String Functions and Operators](https://www.postgresql.org/docs/current/static/functions-string.html)  
║&ensp; &ensp; &ensp; ║&ensp; ╚═9.4.1. [String columns concatenation](02_Use_PostgreSQL/current/02_II/09/4/09_Concatenate_Columns.md)  
║&ensp; &ensp; &ensp; ╚═9.21. [Window Functions](https://www.postgresql.org/docs/current/static/functions-window.html)  
║&ensp; &ensp; &ensp; &ensp; &ensp; ╚═9.21.1. [row_number() by column with partition](02_Use_PostgreSQL/current/02_II/09/21/06_row_number.md)  
╠═VI. [Reference](https://www.postgresql.org/docs/current/static/reference.html)  
║&ensp; ╠═I. [SQL Commands](https://www.postgresql.org/docs/current/static/sql-commands.html)  
║&ensp; ║&ensp; ╠═[CREATE TABLE](https://www.postgresql.org/docs/current/static/sql-createtable.html)  
║&ensp; ║&ensp; ║&ensp; ╚═[Example_CREATE_TABLE.sql](02_Use_PostgreSQL/current/06_VI/01_I/CREATE_TABLE/02_Create_Table.md)  
║&ensp; ║&ensp; ╠═[DELETE TABLE](https://www.postgresql.org/docs/current/static/sql-delete.html)  
║&ensp; ║&ensp; ║&ensp; ╚═[Delete_duplicated_rows.sql](02_Use_PostgreSQL/current/06_VI/01_I/DELETE/01_delete_duplicated_rows.md)   
║&ensp; ║&ensp; ╚═[UPDATE](https://www.postgresql.org/docs/current/static/sql-update.html)  
║&ensp; ║&ensp; &ensp; &ensp; ╚═[Update_rows.sql](02_Use_PostgreSQL/current/06_VI/01_I/UPDATE/01_update_table.md)  
║&ensp; ╚═II.[PostgreSQL Client Applications](https://www.postgresql.org/docs/current/static/reference-client.html)  
║&ensp; &ensp; &ensp; ╚═[pg_restore](https://www.postgresql.org/docs/current/static/app-pgrestore.html)  
║&ensp; &ensp; &ensp; &ensp; &ensp; ╚═[Import_MySQL_sakila_sample_dataset_file_to_Postgresql_Database.sql](02_Use_PostgreSQL/current/06_VI/02_II/pg_restore/01_Import_MySQL_sakila_sample_dataset_to_PostgreSQL.md)  
╚═VIII. [Appendixes](https://www.postgresql.org/docs/current/static/appendixes.html)  
&ensp; &ensp; ╚═F. [Additional Supplied Modules](https://www.postgresql.org/docs/current/static/contrib.html)  
&ensp; &ensp; &ensp; &ensp; ╚═F.39 [tablefunc](https://www.postgresql.org/docs/current/static/tablefunc.html)  
&ensp; &ensp; &ensp; &ensp; &ensp; &ensp; ╚═F.39.1.4 [crosstab : Pivot_Table.sql](02_Use_PostgreSQL/current/08_VIII/F/39/01_Pivot_Table.md)  
( ║ ╠ ═ ╚ )

# Not registed Use Case
[Configure Role, Database, Previlege](02_Use_PostgreSQL/01_Configure_Role_Database_Preivilege.md)

[Insert Into Table](02_Use_PostgreSQL/03_Insert_Into_Table.md)

[regexp_split_to_table](02_Use_PostgreSQL/04_regexp_split_to_table.md)

[regexp_matches](02_Use_PostgreSQL/05_regexp_matches.md)

[COPY table between file](02_Use_PostgreSQL/07_copy_table_and_file.md)

[STRING AGG with ORDER BY](02_Use_PostgreSQL/08_STRING_AGG_ORDER_BY.md)

# Use ToadPole

[Install and Use ToadPole for Postgresql](03_Use_Toad_Pole/01_use_toadpole.md)
