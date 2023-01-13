
### DOCKER PS
* ```docker ps``` - list of running containers sorted by creation time 
* ```docker ps -a``` - list of all containers sorted by creation time 
* ```docker ps -l``` - last started container 
* ```docker ps -q``` - list of id’s for running containers docker rm $(docker ps -q) 
* ```docker ps -qf name=web*``` - list of id’s for running containers plus filter for name


### DOCKER EXEC 
* ```docker exec <docker-name> <command>``` - run new process inside existing docker 
* ```docker exec -it -u 0<docker-name> <command>``` - enter container with root user 
* ```docker exec <docker-name> sh -c “ls && ps”``` - couple commands in one query
* ```sudo nsenter``` - alternative program on the host machine   
* ```sudo cntr attach <docker-name>``` - alternative program on the host machine 

### DOCKER INSPECT
* ```docker inspect <docker-name>``` - docker details
* ```docker inspect –format ‘{{ json .State.Status  }}’ <docker-name>``` - docker details
