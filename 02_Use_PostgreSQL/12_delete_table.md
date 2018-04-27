[ Concatenate Columns on PostgresQL ]

PostgreSQL current Document https://www.postgresql.org/docs/current/static/sql-delete.html 

```{sql}
DELETE FROM player
WHERE date IN (
    SELECT 
        date
    FROM (
        SELECT 
            date, num,
            ROW_NUMBER() OVER( PARTITION BY date,num ORDER BY date,num ) AS row_num
        FROM player 
    ) AS t
    WHERE t.row_num > 1 
);
```
