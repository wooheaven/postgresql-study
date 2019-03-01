[DELETE](https://www.postgresql.org/docs/current/static/sql-delete.html)  

```{sql}
mydatabase=> 
SELECT 
    id--,date
FROM (
    SELECT 
        id,date,num,
        ROW_NUMBER() OVER( PARTITION BY date,num ORDER BY date,num ) AS row_num
    FROM match
) AS t
WHERE t.row_num > 1 
;
  id  
------
 1488
 1481
 1480
 1487
 1486
 1483
 1492
 1499
 1496
 1493
 1484
 1476
 1489
 1491
(14 rows)

mydatabase=> 
DELETE FROM match
WHERE id IN (
    SELECT 
        id--,date
    FROM (
        SELECT 
            id,date,num,
            ROW_NUMBER() OVER( PARTITION BY date,num ORDER BY date,num ) AS row_num
        FROM match
    ) AS t
    WHERE t.row_num > 1 
);
DELETE 14

mydatabase=> 
SELECT 
    id--,date
FROM (
    SELECT 
        id,date,num,
        ROW_NUMBER() OVER( PARTITION BY date,num ORDER BY date,num ) AS row_num
    FROM match
) AS t                                                                         
WHERE t.row_num > 1 
;
 id 
----
(0 rows)
```
