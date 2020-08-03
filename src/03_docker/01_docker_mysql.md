# DOCKER MYSQL #

* start mysql - password root
```bash
docker run --name sow-mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=StatementOfWorkLocal -p 3306:3306 -d mysql:5.7  --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
``` 

* start bash > mysql 
```bash
docker exec -it sow-mysql bash
mysql -uroot -p
```

* start mysql
```bash
docker exec -it sow-mysql mysql -uroot -p
``` 

* create dump from docker 
```bash
docker exec sow-mysql /usr/bin/mysqldump -u root --password=root StatementOfWorkLocal > c:/backup.sql
``` 

* create dump from remote docker 
```bash
docker exec sow-mysql /usr/bin/mysqldump -u root --password=root StatementOfWorkLocal > c:/backup.sql
``` 

* connecting to database
```bash
sudo docker run -it --rm mysql /bin/bash -c "mysql -hdevmerchantutilityrds.yell-devqaugc-aws.co.uk -umerchantutility --ssl-mode=DISABLED  -p devmerchantutilityrds "
``` 
