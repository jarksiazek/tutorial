# SETTING UTF8 #
### **NOTE** ###

My sql has default encoding - latin1

* use commend to check it: 
```bash 
mysql> SHOW VARIABLES WHERE Variable_name LIKE 'character\_set\_%' OR Variable_name LIKE 'collation%';

+--------------------------+--------------------+
| Variable_name            | Value              |
+--------------------------+--------------------+
| character_set_client     | latin1             |
| character_set_connection | latin1             |
| character_set_database   | latin1             | <here should be utf8mb4
| character_set_filesystem | binary             | 
| character_set_results    | latin1             |
| character_set_server     | utf8mb4            |
| character_set_system     | utf8               |
| collation_connection     | latin1_swedish_ci  | <here should be utf8mb4_unicode_ci
| collation_database       | latin1_swedish_ci  |
| collation_server         | latin1_swedish_ci  | 
+--------------------------+--------------------+
```

* remember to set correct information when database is being created 

1. Docker
```bash
λ docker run --name sow-mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=StatementOfWorkLocal -p 3306:3306 -d mysql:5.7  --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

2. Change charset after creating database 
* start docker with default latin charset
```bash
docker run --name sow-mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=StatementOfWorkLocal -p 3306:3306 -d mysql:5.7
```

* check current charset and collation
```bash
mysql> USE db_name;
mysql> SELECT @@character_set_database, @@collation_database;
```

* change default charset and collation
```bash
mysql> ALTER DATABASE StatementOfWorkLocal CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
```