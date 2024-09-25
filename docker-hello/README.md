<!-- @format -->

# Docker

it helps to track the version of our application just like a github.
Scalable: hanlde more users to manage.

Devlops integration: it is the bridge between the development and operations from codeing to deployment.

How Docker Works:

Images and container:

## Image:

1. Lightweight
2. Standalone
3. Executable package

The images are includes like:
-> code
-> runtime (like node js)
-> libraries
-> system tools
-> operating system

## container

it is the runable instance of docker image.
represent execution env.
-> it follows the images instruction and implent it.
-> we can create many container with one single images

## volume

-> percestance data storage mechanism.
-> the data between the container and volume.

## docker network

It is a communication channel that enables different docker to talk to each other.
It creates connectivity, while maintaing isolation.

## docker workflow

It consits of three things

1. Docker Client.
2. Docker Host (docker deamon) -> responsible for the docker container to manage in the host system.
3. Docker Registry (docker hub) -> centeralized registry for the docker image (it can be public or private).

## Working with Docker.

Install the docker desktop and start working with it.
Docker hub, you can go to the explore and sees all the public images in it.

## How do we create our own docker images

-> Dockerfile: it is a set of inst. telling to docker what we want.

difference between CMD and ENTRYPOINT

CMD: flexible, and can be overridden (default entrypoint)
ENTRYPOINT: can not be overridden (fixed entrypoint)

## lets intract with ubuntu opereting system.

1. docker pull ubuntu
   (now download the docker ubuntu public images, you can check it in the Docker Desktop images section).
   then you can interact with ubuntu image with:

2. docker run -it ubuntu
   (it creates a container where you can interact with it, you can check it in the Docker Desktop container section).

## now, how to create our own Docker image.

create a folder hello-docker

create a file name as Dockerfile without any extension.

FROM node:20-alpine -> docker base image which is very light weight
COPY . . -> first dot (.) current directory and the second dot (.) the path of current directory within the container.
WORKDIR /app
CMD node hello.js

After creating the Dockerfile, start build the image with the following command.

1. docker build -t hello-docker . (-t is the tag which is optional, when there is no tag, by defalut it accept the latest)

After the build complete, we can check it with the below command.

2. docker images

or we can also check it in the Docker Desktop in the images section.

After the docker images build, we can containerise it or run the images.

3. docker run hello-docker (now, we get the result of our output)

just like, we have stored our value in the docker container, now we can interact with by using the following command. Just like we have used WORKDIR app, that means the files are stored in the app directory of docker container's file.

4. docker run -it hello-docker sh (this put directly to our operating system)

now you can use node hello.js (for directly sees the same result).
