# DOCKER

Docker is a platform that enables developers to create, deploy, and run applications inside containers. Containers are lightweight and portable units of software that can be easily moved from one environment to another, such as from a developer's laptop to a testing environment or from a testing environment to production.

Docker provides a way to package an application with all of its dependencies into a single, portable container that can run on any machine that has Docker installed, regardless of the underlying operating system or hardware. This makes it easier for developers to build, test, and deploy their applications across different environments, and also simplifies the process of deploying applications to cloud platforms like AWS, Google Cloud Platform, and Microsoft Azure.

Docker uses a client-server architecture, with the Docker client sending commands to a Docker daemon, which then carries out those commands. The Docker daemon manages the creation, execution, and deletion of containers, while the Docker client provides a command-line interface for interacting with the daemon. Additionally, Docker provides a registry for storing and sharing container images, which can be used to distribute and deploy applications to different environments.

### Properties of docker:

- Light weight
- Flexible
- Inter changeable
- Scalable
- Stackable

### DOCKER CONTAINER CONTAINS:

- PID
- NATE
- IPC
- Mount
- UTS
- Union file system

### Docker container act as client system architecture:

Docker daemon(server) → RESTAPI → Docker CLI → (Container, Image, Data volumes, Network)
![docker](https://user-images.githubusercontent.com/53580449/227033576-d7dfab03-aabf-4359-93e9-adc7a696391b.png)



### Docker Installation

```jsx
# For Docker Installation
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER && newgrp docker  //This command give permissions 
```

```jsx
singh9765h@docker:~$ docker version
Client:
 Version:           20.10.21
 API version:       1.41
 Go version:        go1.18.1
 Git commit:        20.10.21-0ubuntu1~18.04.2
 Built:             Thu Feb  2 15:03:29 2023
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server:
 Engine:
  Version:          20.10.21
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.18.1
  Git commit:       20.10.21-0ubuntu1~18.04.2
  Built:            Mon Jan 30 21:07:30 2023
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.6.12-0ubuntu1~18.04.1
  GitCommit:        
 runc:
  Version:          1.1.4-0ubuntu1~18.04.1
  GitCommit:        
 docker-init:
  Version:          0.19.0
  GitCommit:
```

### Create container, list container, remove containers

```jsx
docker --help

//sample commands of docker
docker container ls
docker image ls
docker network ls

docker ps //show containers

```

`docker container run <image name>`→ It will search for docker image and download  if not available locally and then install it

`docker container ls -a` → Show all the container that are been stopped

`docker container ls` → Shows the running containers

`docker container rm <id>` → To remove the container with Id

### Create a container  in background, stop, start, detach container

`docker container start <container id>` → To start the container that is present

`docker container stop <container id>` → To stop the running container

`docker container run -d ubuntu sleep 30` → Here -d runs the docker container in detached mode and leave the terminal to do further workings

`docker container run -d -it ubuntu /bin/bash` → To get inside container it will run the ubuntu os as interactive server inside the docker container

`exit()` → To get outside of the ubuntu container

`ctrl + P ctrl + Q` → To keep the ubuntu os container running in background and exiting the interactive server

`docker container rm $(docker conatiner ls -a)` → Command to delete all the containers at once

### Docker container inspect

`docker container run -d nginx` → It will download nginx mage and run the nginx server in detached mode

`docker container inspect <id>` → To inspect the container about it’s network and port on which it is available such details 

### What’s going inside container?

`docker container logs <id>` → To check logs of the container

`docker container top <id>` → To check the processes going inside docker container

`ps -aux` → Command to check the processes on the instance also to match the container process

`docker container stats` → To check container statistics eg, cpu usage, memory usage

### Docker Port mapping, rename container, restart container, exec container

`docker container run -d -p <port to open>:<port of application> <name>` → To port the request of the application IP to machine IP port to make it accessible

`docker container run -d -p <port to open>:<port of application> --name <name> <Container name>` → This will ensure the running container name with IP port

`netstat -nltp`  → To check the ports open on machine

`docker container exec -it <container id>` → To use the running container of server’s terminal to install applications in it

`docker container rename <container id>` <new name> → To change the running containers name

`docker container restart <container id>` → To restart the container

### Attach running container, kill, wait, pause, un-pause, prune, port

`docker container kill <id>` → To kill any docker container

`docker container <id>` → To wait for the stop of docker container it will show exit status on terminal

`docker container pause <id>` → Pause the container and will not accessible

`docker container unpause <id>` → To again make container accessible after paused

`docker container prune` → Remove all the containers that are not in use after creation

`docker container port <id/name>` → Shows the port to which it is mapped

### Create docker container, diff container and copy file into container

`docker container create ubuntu sleep 30` → It will create a container but will not start it

`docker container start <id>` → Now it starts the container

//But in case of docker run it will fetch the image and build a container and also run it

`watch ‘docker container <id>’` → It will watch for the changes in the container going on

`docker container cp <file>/ <container id>: <path>` → This will copy files from running instance inside the container to particular path

### Docker container export / import

1. Create a docker container of ubuntu `docker container run -it ubuntu`. Now in this container install git and tree  as `apt install tree git -y`
2. Now exit the container and then make zip file of the container as `docker container export <container id> > <folder name>.tar`. This will create a tar file and save in the instance
3. Now use this container to send to anyone and to make it run anywhere use `docker image import <filename>.tar <name to be given>`. This will create an Image and then create container as `docker container run -it <image name>`. Check for git and tree they will be installed in it

### How to create docker image from running container

1. Create a container and run it and inside it’s terminal create some files
2. Then exit that terminal and create docker image of that container as `docker container commit --author "Harman" -m "This is test commit" <id> <image name to be made>`
3. This will create image of the running container now delete the container as `docker container rm -f <id>`
4. Now build container from that image as `docker container run -it <image name>`. And check the files created are still there

### Docker image pull, push, tag and docker login

`docker pull ubuntu:tag` → To pull the image of particular docker image

``docker image tag [<account](http://hub.docker.com/<account) name>/<image name>` → To tag the image with name of docker hub repo

docker push <image name with account name tag> → To push the image to docker hub but before that do docker login and enter creds

### Docker image list, image remove, image inspect, image prune
