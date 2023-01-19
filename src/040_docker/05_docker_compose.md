### docker-compose.yaml
```yaml
version: '3'
services: 
  php:
    image: my-application
    build: .
    command: ["php", "/application/index.php"]
    container_name: php-application
    environment:
      - NAME # value not set, will be taken from host
```




### volumes
* ```-/var/lib/mysql``` - anonymousq volume path /var/lib/mysql
* ```/opt/data:/var/lib/mysql``` - /opt/data from host -> /var/lib/mysql on container
* ```./cache:/tmp/cache``` - ./cache on host to /tmp/cache on container
* ```~/cache:/tmp/cache:ro``` - ~/cache on host with read only permission
* ```datavolue:/tmp/cache``` - volume with name datavolue to to /tmp/cache on container
### ports
* ```8080:8080``` - host to container 
* ```8000-8999:8000-8999``` - range of ports
* ```127.0.0.1:80:80``` - loop back interface, only for localhost, no access via the Internet
* ```6060:6060/udp``` - udp protocol

### commends
* ```docker-compose build``` - buid docker-compose based on docker-compose.yaml and Dockerfile both in the same localization
* ```docker-compose up -d``` - start all service from the docker-compose build 
* ```docker-compose -f docker-compose.yaml -f docker-compose.dev,yaml run``` - extend the docker-compose by docker-compose.dev.yaml 

