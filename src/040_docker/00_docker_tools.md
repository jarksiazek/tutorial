### HADOLINT
* ‘’’hadolint’’’ - tool for static code analysis
* ```docker run --rm -i hadolint/hadolint < Dockerfile```

### CMD.CAT 
* docker builder
* ```docker run –name curl cmd.cat/curl``` - create docker with curl

### NETSHOOT 
* good container for monitoring other container or host
* ```docker run -it –net container:<container-id> nicolaka/netshoot``` - test other container
* ```docker run -it –net host nicolaka/netshoot``` - test host
