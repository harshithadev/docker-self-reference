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

docker-compose --help 

docker-compose build    
//will build images from its dockerfile, if image linked and not dockerfile, process skipped

docker-compose images
//lists the images build

docker-compose run
//build containers from the images(have to be images, would not build from dockerfile)

docker-compose up
//builds and runs the containers and their dependencies

'' --build
//switch force builds a new image, even if image already exsists

docker-compose stop 
//stops all the containers mentioned in the compose file

docker-compose start 
//starts any stopped containers 

docker-compose restart
//does exactly what it says, restarts all of the containers

docker-compose ps   
//This lists all the containers for services mentioned in the current docker-compose file. 
//The containers can either be running or stopped.

docker-compose down 
//stops and deletes

docker system prune 
//stops, cleans up the containers, networks, and images used

docker-compose logs
//prints logs of all containers and services involved
=====================================================================

docker swarm 
//checks and returns if docker is present

docker swawrm init
//initialises a 'swawrm' 

returns something like this : 
＄ docker swarm init
Swarm initialized: current node (ayxwwpio1sksk5hi2bdqxanf4) is now a manager.
To add a worker to this swarm, run the following command:
    docker swarm join --token SWMTKN-1-19vn56bmfcc2l20jmts9gg9b152vkn47ruu6vtfwgsl3646ha2-8lcseq2vaegpjqytnnw1xgksn 192.168.65.3:2377
To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.

docker service create <service name> 
//allows us to create a service on swarm with a defined number of containers in it.
example : docker service create --name web_app -p 5000:5000 venky8283/flask_app:3.0.
another service exmaple : docker service create --name database --env-file [.env file location] --mount type=bind,src=[location of init.sql],dst=/docker-entrypoint-initdb.d/init.sql mysql/mysql-server:5.7

we need to create a overlay network for the nodes in the swarm to communaicate.
> docker network create --driver=overlay app
and then add the services to the network
> docker service update --network-add app web_app
> docker service update --network-add app database

docker service scale <service ID/Name>=Replicas_number
//to scale up or down 

=============================================================================

after writing a stack file, 

docker stack deploy <stack name> --compose-file=<location of docker-compose.yml file>

docker service ls
