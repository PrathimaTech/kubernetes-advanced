> there are many docker images available on hub.docker.com, we can just pull them & start running containers
```
docker search <image name>    # to search the docker images from command line
docker pull <image name>      # to pull a docker image from docker hub	
docker images                 # to display the images on your local machine
docker history < image name > # to know the changes done to the image
docker inspect < image name > # to view the detaied information in JSON output
docker rmi <image name>       # to remove a image from local machine
docker image prune            # to remove all unused images from local machine
```

## how to run containers from a docker image 

### two ways we can run the images 
	1) interative mode ( -it )
	2) detached mode  ( -d )

```	
  docker run -d nginx ( always creates new container & detaches from the terminal you are working on ( goes in background process )) 
  docker run -it nginx bash ( always creates new container & gets inside the container )
  docker ps -- to check all running containers 
  docker ps -a -- to check all running + exited/stopped containers
	
  docker stop <container id> -- to stop a container 
  docker start <container id> -- to start a stopped container 
  docker restart <container id> -- to restart a container 
  docker inspect <container id> -- to view detailed information about the continaer in JSON format
  docker rm <container id> -- to remove a stopped/exited container
  docker rm -f <container id> -- to remove a container forcefully though it is in running state 
  docker container prune -- to remove all stopped/exited containers
```
### how to get inside a running container
```
  docker run -d nginx ( creates a new container in detached mode )
  docker ps  -- displays the running containers, note down the container id
  docker exec -it <container id> bash 
```
### how to come out of a container
```
  ctrl pq ( it is mandatory to use this command always )
```  
### how to access the applications running inside the container from external world ( browser )
	
> services running inside a container can never be accessed direcltry, we always need to 
> publish/expose them on to docker host while we create the containers 
	
> we need to publish/expose the services using -P (capital) OR -p (small) with in the docker run command  

```	
ex: 
  -P ( capital ) -- docker will publish/expose the port number dynamically on docker host & maps with port running inside the cont

  docker run -d -P nginx  # which create a new port mapping from docker host to the service inside the container 
  docker ps # to check the container port 

  to access : in the browser http://<docker host IP>:<exposed port>  ex: http://52.14.62.88:32768
  

  -p ( small ) -- we need to assign a port on docker host & map to the port inside the container 
		
  docker run -d -p 1234:80 nginx ( always port-on-docker-host : process-port-inside-container )
  docker ps # to check the container port 
		
  to access : in the browser http://<docker host IP>:<exposed port>  ex: http://52.14.62.88:1234
```
