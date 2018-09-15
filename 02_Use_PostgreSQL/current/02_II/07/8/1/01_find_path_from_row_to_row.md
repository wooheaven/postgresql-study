# input table
```{sql}
mydatabase=> 
CREATE TABLE graph AS (
    SELECT
        id,
        next_id,
        reward
    FROM (
        SELECT
            (id-1) AS id,
            (next_id-1) AS next_id,
            reward
        FROM (
            SELECT
                id,
                unnest(string_to_array(next_ids, ',')) :: INT AS next_id,
                value_function -> 'reward' AS reward
            FROM states
            WHERE id <= 31
            ORDER BY id
        ) AS a
    ) AS b
    WHERE
        id < next_id -- pick up as spanning tree 
    ORDER BY id desc, next_id desc
);

mydatabase=> SELECT * FROM graph ORDER BY id;

 id | next_id | reward 
----+---------+--------
  0 |       2 | 100
  0 |       1 | 100
  1 |       3 | 94
  1 |       4 | 94
  2 |       6 | 94
  2 |       5 | 94
  3 |       7 | 89
  4 |       9 | 89
  4 |       8 | 89
  4 |      10 | 89
  5 |      12 | 89
  5 |      11 | 89
  5 |      13 | 89
  6 |      14 | 89
  7 |      15 | 83
  7 |      16 | 83
  8 |      17 | 83
  8 |      18 | 83
  9 |      20 | 83
  9 |      19 | 83
 10 |      21 | 89
 10 |      22 | 89
 11 |      24 | 83
 11 |      23 | 83
 12 |      25 | 83
 12 |      26 | 83
 13 |      27 | 89
 13 |      28 | 89
 14 |      29 | 83
 14 |      30 | 83
 15 |      31 | 78
 16 |      34 | 83
 16 |      32 | 83
 16 |      33 | 83
 17 |      35 | 78
 18 |      36 | 83
 19 |      37 | 78
 20 |      38 | 83
 21 |      39 | 83
 22 |      40 | 89
 23 |      41 | 78
 24 |      42 | 83
 25 |      43 | 78
 26 |      44 | 83
 27 |      45 | 83
 28 |      46 | 89
 29 |      47 | 78
 30 |      49 | 83
 30 |      48 | 83
 30 |      50 | 83
(50 rows)
```

# find path from 0 to 30
```{sql}
mydatabase=> 
WITH recursive search (next_id, id, reward, length, id_path, cycle) AS (
		-- root node
        SELECT g.next_id, g.id, reward, 1, ARRAY[g.id, g.next_id], FALSE
        FROM graph AS g
        WHERE g.id = 0
    UNION ALL
		-- child node to leaf node
        SELECT g.next_id, g.id, g.reward, s.length + 1, id_path || g.next_id, g.next_id = ANY(id_path)
        FROM graph AS g, search AS s
        WHERE g.id = s.next_id AND NOT cycle
)
SELECT id, next_id, reward, length, id_path FROM search WHERE next_id = 30 ORDER BY id_path;

 id | next_id | reward | length |    id_path    
----+---------+--------+--------+---------------
 14 |      30 | 83     |      4 | {0,2,6,14,30}
(1 row)
```
