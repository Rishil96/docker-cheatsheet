# Docker Commands

## Table of Contents

| Sr. No. | Topic |
|:---:|:---:|
| 1 | [Basic Commands](#1) |
|  |  |
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
