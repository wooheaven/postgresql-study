# Count Number of characters in string
```{sql}
test_database=# select regexp_replace('/firstStr/secondstr/test/values', '[^/]+', '', 'g');
 regexp_replace
----------------
 ////
(1 row)

test_database=# select length(regexp_replace('/firstStr/secondstr/test/values', '[^/]+', '', 'g'));
 length
--------
      4
(1 row)
```
