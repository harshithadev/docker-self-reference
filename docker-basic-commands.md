=================================================================

docker run <image_name>
//starts and runs a new container from the image mentioned

docker start <container_name>
//starts a (preexisiting) container 

docker stop <container_name>
//stops a spinning container 

docker rm <container_name>
//removes a stopped container 

====================================================================

docker ps 
//lists all running containers

docker ps -a
//lists all conainers, running and stopped ones

=====================================================================

docker log 

docker inspect 

=====================================================================

docker run <image_name> -d -p <host_port>:<container_port>

=====================================================================

docker run -v <host_directory>:<container_directory> -d <image_name>

=====================================================================

docker image ls

docker <image_name> pull

docker run --rm -it -p 8082:80 <image_name>

    The -it switch allows me to stop the container using Ctrl-C from the command-line
    The –rm switch ensures that the container is deleted once it has stopped

docker rmi <image_name>
=====================================================================


docker run -d -p 80 --restart always <image_name>
    Docker host itself restart, the container will restart so that it has a high uptime. But it actually works too well; if you try to stop the container using the docker stop command, it will not stop.

docker run -d -p 80 --restart unless-stopped <imge_name>
    That way, your container will almost always be up, except when you don’t want it to - explicilty give stop.
=====================================================================


docker stats
     views the information about the running containers and the resources they consume and such. 
     This will output a live list of running containers plus information about how many resources they consume on the host machine. Like a docker ps extended with live resource usage data.
     including, cpu usage, memory usage ect. 

=====================================================================
the following can be used to reclaim disk space : 

docker container prune -f
docker volume prune -f
docker image prune -f


docker image prune --all
=====================================================================


