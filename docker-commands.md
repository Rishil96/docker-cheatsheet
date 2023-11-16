# Docker Commands

## Table of Contents

| Sr. No. | Topic |
|:---:|:---:|
| 1 | [Basic Commands](#1) |
| 2 | [Docker Run](#2) |
| 3 | [Docker Images](#3) |
|  |  |


<a id=1></a>

## Docker Basic Commands
---
- ```docker run container-name```
-  Runs the container-name image if it exists, it not then it pulls down the image from DockerHub and then runs it to create a container (a running instance of an image).
---
- ```docker ps```
- Lists all the running containers with info.
- use **-a** flag to also list previously exited containers.
---
- ```docker stop container-(name/id)```
- to stop a running container use the above command and provide the container id or name to stop.
---
- ```docker rm container-(name/id)```
- removes a previously exited container to free up space taken by the container.
- multiple containers can be provided using space in between.
---
- ```docker images```
- Lists all the images and its sizes in our system.
---
- ```docker rmi image-(name/id)```
- deletes the image name provided.
- for this to work, no containers should be running that was created using this image.
- stop and delete all dependent containers.
---
- ```docker pull image-name```
- pulls the image from DockerHub.
---
- ```docker run ubuntu sleep 5```
- since ubuntu container doesn't have any task to run by itself, for us to keep the container active, we make the container sleep for 5 seconds.
---
- ```docker exec container-name cat /etc/hosts```
- executes a command on a container.
- containers are supposed to run only till a task is running after which the container exits.
- a container hosting an OS will start running and exit instantly as there are no processes in running state inside it.
---
- ```docker run kodecloud/simple-webapp```
- when we run a web server like this, it runs in attached mode (foreground) which means our cmd will act as the standard output of the container and we won't be able to interact on that cmd.
- we will only see the output of the web service on the screen.
- use **-d** to run the container in detached mode (backend), this will give us the prompt back and we can interact on the same prompt again while the container is running in the background.
---
```docker attach container-(name/id)```
- re attaches the docker container's std out to our prompt.
---
- ```docker run -it centos bash```
- **-it** logs in to the container so we can interact in it.
---


<a id=2></a>

## Docker Run

---
- ```docker run image-name:tag```
- provide a tag i.e. version number of the image to specify a certain version instead of just running the latest.
- default tag considered by docker is **latest**.
---
- ```docker run -it kodekloud/simple-prompt-docker```
- **-it** means i for interactive and t for terminal.
- this allows docker to take inputs from Standard input.
---
- ```docker run -p 80:5000 kodekloud/webapp```
- an outside user can only access the docker webserver using the IP address of the docker host machine.
- inside the docker container, the port used is 5000, but since an outside user won't be able to access the server from inside the container, we have to map the container port to the host port.
- **-p** helps us map the port 80:5000 means traffic on port 80 of the docker host machine will be routed to port 5000 inside the docker container.
- So, outside users can access the web server using the IP of host and port such as **http://192.168.1.5:80**
- In this way, multiple instances of the docker image can be run by mapping it to different ports.
---
- ```docker run -v /opt/datadir:/var/lib/mysql mysql```
- docker containers by default have an isolated file system so any changes to it or addition or deletion will be gone after the container is stopped/deleted.
- to actually make use of containers and store data, we need to mount a directory outside the docker container to the folder inside the docker container where the data will be stored.
- in above command, /opt/datadir is the outside location mounted to the /var/lib/mysql location inside the mysql container. 
- Now, any data stored or deleted will be done directly on the outside folder instead of inside the container so it won't be destroyed along with the container.
---
- ```docker inspect container-name```
- gives additional info about a container in JSON format.
---
- ```docker logs container-name```
- gives the logs i.e. all the details that was printed on the standard output of the container when run on detached mode.
---


<a id=3></a>

## Docker Images

---
- ```docker build -f DockerFile -t rishil/my-custom-app```
- Builds an image with respect to the folder and the DockerFile present in it.
- **-f** flag is for specifying the docker file.
- **-t** flag is for giving a tag name for the Image that will be built.
---
- ```docker push rishil/my-custom-app```
- used to push the image to DockerHub. 
- image name is a combination of the DockerHub account name followed by the image name separated by /.
---
- Find a dummy docker file in the flask app demo folder and the basic steps to create an image.
---
- Dockerfile is written as an **INSTRUCTION ARGUMENT** format.
- All docker files must start with a **FROM** command which is a base image of some sort like an OS.
- Check out e.g. Dockerfile below
```
FROM Ubuntu

RUN apt-get update && apt-get -y install python

RUN pip install flask flask-mysql

COPY . /opt/source-code

ENTRYPOINT FLASK_APP=/opt/source-code/app.py flask run
```

1. Ubuntu will act as a base image for this container.
2. Updates package index and install Python in Ubuntu base image.
3. Use pip to install dependencies.
4. COPY source code files to a separate folder inside the image.
5. ENTRYPOINT is the command which will be executed when a container is created off of the image.
---
- ```docker history image-name```
- check the details of a specific image.
- Docker works as a Layered Architecture, so each layer only stores data of the previous layer.
- Makes it easier to run from a specific layer instead of starting over again.
- all layers are cached.
---
---
---