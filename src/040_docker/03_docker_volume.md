### VOLUME
* volume
  * ```docker run -d mysql:5.7``` - docker creates anonymous volume
  * ```docker create volume data && docker run -d -v data:/var/lob/data mysql:5.7``` 
* mount 
  * ```docker run -d -v $(pwd):/var/temp mysql:5.7’’’ - mounting file 
* tmpfs
  * RAM disk - temporary file system
