
### Copy files from and to containter
`docker cp <containerId>:/file/path/within/container /host/path/target`
`docker cp /host/path/target <containerId>:/file/path/within/container`


### stop all containers:
`docker kill $(docker ps -q)`

### remove all containers
`docker rm $(docker ps -a -q)`

### remove all docker images
`docker rmi $(docker images -q)`
