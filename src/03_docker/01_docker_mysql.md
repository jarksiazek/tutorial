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

* srat mysql
```bash
docker exec -it sow-mysql mysql -uroot -p
``` 