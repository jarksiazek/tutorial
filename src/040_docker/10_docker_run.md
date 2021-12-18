# DOCKER RUN #
https://docs.docker.com/engine/reference/run/
```bash
docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
docker run hello-world
docker run -a stdin -a stdout -i -t ubuntu /bin/bash
```

* ```-d``` detached mode  
* ```-p``` <host-port><container-port>  
* ```--name``` name  
* ```-rm``` clean up after docker success  
* ```--restart``` setting restart option
    * ```no``` (default) no restart 
    * ```on-failure``` if container fails
    * ```always``` after success or failure
    * ```unless stopped``` after success or failure, and after container stop
* ```-memory``` a hard limit of the memory
* ```-memory-reservation``` a soft limit of the memory 

