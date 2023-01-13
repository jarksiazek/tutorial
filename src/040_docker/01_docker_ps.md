Docker PS
* ```docker ps``` - list of running containers sorted by creation time 
* ```docker ps -a``` - list of all containers sorted by creation time 
* ```docker ps -l``` - last started container 
* ```docker ps -q``` - list of id’s for running containers docker rm $(docker ps -q) 
* ```docker ps -qf name=web*``` - list of id’s for running containers plus filter for name
