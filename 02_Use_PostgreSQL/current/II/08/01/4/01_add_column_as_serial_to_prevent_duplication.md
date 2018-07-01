# Add column as serial to prevent duplication using autoincrementing
PostgreSQL Current Document  
&emsp;https://www.postgresql.org/docs/current/static/datatype-numeric.html  
&emsp;https://www.postgresql.org/docs/current/static/datatype-numeric.html#DATATYPE-SERIAL

# before
```{sql}
mydatabase=> \d match
                                   Table "public.match"
 Column |         Type         | Collation | Nullable |              Default              
--------+----------------------+-----------+----------+-----------------------------------
 date   | date                 |           |          | 
 po     | character varying(5) |           |          | 
 num    | integer              |           |          | 
 rt     | numeric(2,1)         |           |          | 
 smin   | integer              |           |          | 
 emin   | integer              |           |          | 
```

# after
```{sql}
mydatabase=> \d match
                                   Table "public.match"
 Column |         Type         | Collation | Nullable |              Default              
--------+----------------------+-----------+----------+-----------------------------------
 id     | integer              |           | not null | nextval('match_id_seq'::regclass)
 date   | date                 |           |          | 
 po     | character varying(5) |           |          | 
 num    | integer              |           |          | 
 rt     | numeric(2,1)         |           |          | 
 smin   | integer              |           |          | 
 emin   | integer              |           |          | 
Indexes:
    "match_pkey" PRIMARY KEY, btree (id)
```

# real log
```{sql}
-- create backup table
DROP TABLE IF EXISTS match_tmp ;
CREATE TABLE match_tmp (
    id   SERIAL NOT NULL PRIMARY KEY, -- 01 Prevent Duplication
    date DATE,                        -- 02 Date
    po   VARCHAR(5),                  -- 03 Position
    num  INT,                         -- 04 Number
    rt   NUMERIC(2, 1),               -- 05 Rating
    smin INT,                         -- 06 Start Min
    emin INT                          -- 07 End Min
) ; 
INSERT INTO match_tmp (
    date, -- 02
    po,   -- 03
    num,  -- 04
    rt,   -- 05
    smin, -- 06
    emin  -- 07
) (
    SELECT 
        date,
        po,
        num,
        rt,
        smin,
        emin
    FROM 
        match
    ORDER BY 
        date,
        CASE                                  
            WHEN po = 'KP' THEN 1             
            WHEN po = 'WB' THEN 2             
            WHEN po = 'CD' THEN 3             
            WHEN po = 'W'  THEN 4             
            WHEN po = 'IM' THEN 5             
            WHEN po = 'FW' THEN 6             
            ELSE 7                            
        END,
        num
) ;
SELECT * FROM match_tmp ;

-- drop and create original table
DROP TABLE IF EXISTS match ;
CREATE TABLE match (
    id   SERIAL NOT NULL PRIMARY KEY, -- 01 Prevent Duplication
    date DATE,                        -- 02 Date
    po   VARCHAR(5),                  -- 03 Position
    num  INT,                         -- 04 Number
    rt   NUMERIC(2, 1),               -- 05 Rating
    smin INT,                         -- 06 Start Min
    emin INT                          -- 07 End Min
) ; 
INSERT INTO match (
    date, -- 02
    po,   -- 03
    num,  -- 04
    rt,   -- 05
    smin, -- 06
    emin  -- 07
) (
    SELECT 
        date,
        po,
        num,
        rt,
        smin,
        emin
    FROM 
        match_tmp
    ORDER BY 
        id
) ;
SELECT * FROM match ;

-- delete backup table
DELETE FROM match_tmp ;
```
