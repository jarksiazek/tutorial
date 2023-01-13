
### DOCKER PS
* ```docker ps``` - list of running containers sorted by creation time 
* ```docker ps -a``` - list of all containers sorted by creation time 
* ```docker ps -l``` - last started container
* ```docker ps -s``` - adding 2 cols size (size of writable layer), virtual size (writable layer plus all image layer) 
* ```docker ps -q``` - list of id’s for running containers docker rm $(docker ps -q) 
* ```docker ps -qf name=web*``` - list of id’s for running containers plus filter for name


### DOCKER EXEC 
* ```docker exec <docker-name> <command>``` - run new process inside existing docker 
* ```docker exec -it -u 0<docker-name> <command>``` - enter container with root user 
* ```docker exec <docker-name> sh -c “ls && ps”``` - couple commands in one query
* ```sudo nsenter``` - alternative program on the host machine   
* ```sudo cntr attach <docker-name>``` - alternative program on the host machine 

### DOCKER ATTACH
* ```bash
  docker run -it alpine alpine:3 #run alpine image 
  ^P^Q # detaching docker console, docker stays in daemon mode
  docker attach alpine # attaching to previous running docker 
  ```

### DOCKER INSPECT
* ```docker inspect <docker-name>``` - docker details
* ```docker inspect –format ‘{{ json .State.Status  }}’ <docker-name>``` - docker details

### DOCKER STOP
* ```docker stop``` - graceful stop - SIGTEMR -> 10 sec (default) -> SIGKILL
* ```docker kill``` - (docker rm -f) - force docker stop SIGKILL(default)
* ```docker kill –signal HUB <docker-name>``` - changing default singal to SIGHUB
* ```docker kill –signal TERM <docker-name>``` - changing default singal to SIGTERM


### DOCKER LOGS
default path - /var/lib/docker/containers/…
* ```docker log <docker-name>``` - logs for selected docker
* ```docker log –tail 3 <docker-name>``` - 3 last lines
* ```docker log –tail 3 -f <docker-name>``` - real view of logs

### DOCKER DIFF
* ```docker diff <docker-name>``` - list of removing/adding files on the writable layer 

### DOCKER STATS
* CPU, memory, Network i/o, block i/o 
* ```docker stats``` - list of dockers with basic usages 
* ```docker stats –no-stream -f ‘{{ .Name }}\t{{ .CPUPerc}} ’``` - no stream, just snapshot
* ```docker top <docker-name>``` - list of processes in the docker

### DOCKER COMMIT
* ```docker commit <container-name> <image-name>``` - convert modified container to new image 
* ```docker commit alpine alpine:modified``` - example of docker commit
* ```docker history <image:name>``` - history of docker modification

