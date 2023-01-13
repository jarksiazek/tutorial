### DOCKER NETWORKS
* ```docker info | grep Network``` - list of networks
* Network types
  * bridge(default)
    * communication external and internal
    * dockers communicate to each other using docker name
  * none
    * no communication external and internal, only container localhost 
  * host
    * available only for linux
    * not good for docker desktop
    * the host ports and services are reachable
  * container
    * ```docker run –net container:<container-id>```
    * share the namespace with other container
    * good for monitoring, problemating container add to –net parameter
  * overlay- docker swarm

* ```docker network ls``` - list of created docker networks
* ```docker network inspect bridge`` - inspect network with name ‘bridge’
* CMD.CAT  - docker builder 
* ```docker run –name curl cmd.cat/curl``` - create docker with curl 
* ```docker run –name ngrep cmd.cat/ngrep``` - create docker with ngrep 
* NETSHOOT - good container for monitoring other container or host
  * ```docker run -it –net container:<container-id> nicolaka/netshoot``` - test other container
  * ```docker run -it –net host nicolaka/netshoot``` - test host
