### DOCKER BUILD 
* ```docker build - < Dockerfile``` - no access to files except Dockerfile
* ```docker build - < context.tar.gz``` - data injected from tar file
* ```docker build http://github``` - data injected from git
* ```docker build . -t <image-tag>``` - build from local store

### DOCKERFILE
* RUN - default wrapping [sh -c “”]
  * ```RUN <command>```
  * ```RUN [“executable”, “param1”, “param2”]```
  * ```RUN apt-get update && apt-get install -y curl```
  * ```RUN [“/bin/bash”, “-c”, “echo Hello”]```
* CMD - default commend
  * ```CMD [<command> <param1> <param2>]```
  * ```CMD [“param1”, “param2”]``` - requires an ENTRYPOINT
  * ```CMD nginx -g ‘daemon off’```
  * ```CMD [“nginx”, “-g”, “daemon off”]```
  * ```docker run –rm -it <docker-id> sh``` - overriding cmd with “sh”
* EXPOSE - container listening port
  * ```EXPOSE <port>[/<protocol>]```
  * ```EXPOSE 80``` - listening 80 TCP
  * ```EXPOSE 3030/udp``` - listening 3030 UDP
* ENV
  * ```ENV <key>=<value>```
  * ```ENV env=staging```
  * ```ENV first=staging second=staging_2```
  * ```RUN VARIABLE=value env``` - variable accessible only for this line 
  * ```RUN export VARIABLE=value && env``` - variable for using only during docker build image
* COPY
  * ```COPY <src>[, <src>, …] <dest>```
  * ```COPY index.html /var/www```
  * ```COPY *.png /var/www/static```
  * ```COPY –chown-usr1:usr1 . /var/www``` - changing user and group to usr1
  * ```COPY –chown=101 index* /srv/``` - changing to user 101
* ENTRYPOINT - main command
  * ```ENTRYPOINT [“/entrypoint.sh”] + CMD [“some] -> /entrypoint.sh some```
* VOLUME - mount point
  * ```VOLUME [“/dir”, “/path”]``` - create anonymous volume and data will be available on volume folder
* USER - sets user name (group name) or UID for running image
  * ```USER <user>[:<group>]```
  * ```USER <UID>[:<GID>]```
  * ```USER root```
  * ```USER www-data:www-data```
* WORKDIR - create and change working dir for RUN, CMD, ENTRYPOINT, COPY, ADD
  * ```WORKDIR /a/b/c```
* ARG - defines variable that user can pass at build-time
  * ```ARG VERSION``` - argument added to Dockerfile
  * ```RUN apk add nginx~$VERSION``` - passing argument to RUN command
  * ```docker build –build-arg VERSION=1.18``` passing VERSION 1.18 during build

### COPY FILES TO DOCKER (DOCKERFILE)
* COPY
  * many sources and one destination 
  * recommended approach is to use COPY instead of using ADD
  * unpacking and getting data from url are not good practice 
* ADD
  * extension of COPY instruction 
  * can use “url” source 
  * can unpack files from local source to folder destination 
* .dockerignore 
  * ignore file which does not use for docker build 

### MULTISTAGE

### DOCKERFILE BEST PRACTICE
* Collapsing layer -> chaining shell commands
* Squash the image - experimental feature - squash all layers to one
* ‘’’hadolint’’’ - tool for static code analysis 
* ‘’’docker build –squash .’’’
* order of instructions
  * FROM
  * static instructions - EXPOSE, VOLUME, CMD, ENTRYPOINT, WORKDIR
  * dynamic instructions - ENV, ARG, 
  * RUN
  * ADD or COPY

### DOCKER BUILDER
* legacy build
* BuildKit
* BuildX




