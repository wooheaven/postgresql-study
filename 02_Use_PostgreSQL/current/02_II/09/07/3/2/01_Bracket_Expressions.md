# grep other char by [^char]
```{sql}
test_database=# select regexp_replace('/firstStr/secondstr/test/values', '[^/]+', '', 'g');
 regexp_replace
----------------
 ////
(1 row)

test_database=# select regexp_replace('/firstStr/secondstr/test/values', '[/]+', '', 'g');
       regexp_replace
-----------------------------
 firstStrsecondstrtestvalues
(1 row)
```
