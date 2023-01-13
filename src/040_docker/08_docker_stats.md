### DOCKER STATS
CPU, memory, Network i/o, block i/o 
```docker stats``` - list of dockers with basic usages 
```docker stats –no-stream -f ‘{{ .Name }}\t{{ .CPUPerc}} ’``` - no stream, just snapshot
```docker top <docker-name>``` - list of processes in the docker
