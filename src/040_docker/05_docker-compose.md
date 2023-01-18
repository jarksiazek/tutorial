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
* ```-/var/lib/mysql```
