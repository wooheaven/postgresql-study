# replace string by POSIX regular expression
```{sql}
test_database=# select regexp_replace('/firstStr/secondstr/test/values', '[^/]+', '', 'g');
 regexp_replace
----------------
 ////
(1 row)
```
