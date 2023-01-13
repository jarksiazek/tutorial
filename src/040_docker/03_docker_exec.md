### DOCKER EXEC 
```docker exec <docker-name> <command>``` - run new process inside existing docker 
```docker exec -it -u 0<docker-name> <command>``` - enter container with root user 
```docker exec <docker-name> sh -c “ls && ps”``` - couple commands in one query
```sudo nsenter``` - alternative program on the host machine   
```sudo cntr attach <docker-name>``` - alternative program on the host machine 
