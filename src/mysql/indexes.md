# INDEXES #
* types
    * B-tree 
        * default (almost all databases)
        * most popular
        * leaf rows are stored 
        * supports single lookups
        * supports range lookups
        * supports scanning in order (sorted access)
    * Hash
        * special purpose
        * supports single lookups
        * does not support ordered access, bulk access, scanning
    * Log-Structure Merge
    * Other (full-text, spatial, skiplist)
 

* goals
    * read less data
    * read in bulk
    
### IMPORTANT COMMANDS ###
* show indexes
```bash
SHOW INDEX FROM statement_of_work_snapshots;
```

* drop indexes with name 'account_id'
```bash
ALTER TABLE statement_of_work_snapshots DROP INDEX account_id;
```

* explain command
```bash
EXPLAIN SELECT * FROM statement_of_work_snapshots where account_id = '0000000001';
```

* explain command with more data 
```bash
EXPLAIN FORMAT=JSON SELECT * FROM statement_of_work_snapshots where account_id = '0000000001';
```

### MULTI COLUMNS INDEX ###
https://dev.mysql.com/doc/refman/8.0/en/multiple-column-indexes.html    