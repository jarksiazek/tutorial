# DOCKER POSTGRES #

* start postgres - password secret
```bash
docker run --name postgres -e POSTGRES_PASSWORD=secret -e POSTGRES_USER=user -e POSTGRES_DB=assessment_tool -p 5432:5432 -d postgres:12
``` 

* connecting to remote database postgres
```bash
docker run -it --rm postgres bash -c "psql  -hassessment-tool-db-dev.ctzigj6l6m5w.eu-west-2.rds.amazonaws.com -U postgres -p 5432"
```

* connecting to local database postgres 
```bash
docker exec -it <container_name> bash
```
```bash
docker exec -it ff3 bash
```
