# Install and Run PostgreSQL
&ensp;[Install PostgreSQL9.3.6 : on docker](01_Install_and_Run_PostgreSQL/01_Install_PostgreSQL9.3.6_on_docker.md)  
&ensp;[Run PostgreSQL9.3.6 : on docker](01_Install_and_Run_PostgreSQL/02_Run_PostgreSQL9.3.6_on_docker.md)

# Use PostgreSQL
| Part             | Chapter                        | Head1           | Head2                          | Link of Details                                     |
|------------------|--------------------------------|-----------------|--------------------------------|-----------------------------------------------------|
| VIII. Appendixes | F. Additional Supplied Modules | F.38. tablefunc | F.38.1.4. crosstab(text, text) | [Pivot Table](02_Use_PostgreSQL/10_Pivot_Table.md)  |

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
╚═VI. [Reference](https://www.postgresql.org/docs/current/static/reference.html)  
&ensp; &ensp; ╠═I. [SQL Commands](https://www.postgresql.org/docs/current/static/sql-commands.html)  
&ensp; &ensp; ║&ensp; ╠═[CREATE TABLE](https://www.postgresql.org/docs/current/static/sql-createtable.html)  
&ensp; &ensp; ║&ensp; ║&ensp; ╚═[Example CREATE TABLE.sql](02_Use_PostgreSQL/current/06_VI/01_I/CREATE_TABLE/02_Create_Table.md)  
&ensp; &ensp; ║&ensp; ╠═[DELETE TABLE](https://www.postgresql.org/docs/current/static/sql-delete.html)  
&ensp; &ensp; ║&ensp; ║&ensp; ╚═[Delete duplicated rows.sql](02_Use_PostgreSQL/current/06_VI/01_I/DELETE/01_delete_duplicated_rows.md)   
&ensp; &ensp; ║&ensp; ╚═[UPDATE](https://www.postgresql.org/docs/current/static/sql-update.html)  
&ensp; &ensp; ║&ensp; &ensp; &ensp; ╚═[Update rows.sql](02_Use_PostgreSQL/current/06_VI/01_I/UPDATE/01_update_table.md)  
&ensp; &ensp; ╚═II.[PostgreSQL Client Applications](https://www.postgresql.org/docs/current/static/reference-client.html)  
&ensp; &ensp; &ensp; &ensp; ╚═[pg_restore](https://www.postgresql.org/docs/current/static/app-pgrestore.html)  
&ensp; &ensp; &ensp; &ensp; &ensp; &ensp; ╚═[Import MySQL sakila sample dataset file to Postgresql Database.sql](02_Use_PostgreSQL/current/06_VI/02_II/pg_restore/01_Import_MySQL_sakila_sample_dataset_to_PostgreSQL.md)  
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
