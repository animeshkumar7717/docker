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

============================================================================================================

<!-- @format -->

## Docker Compose

This is the most important thing for docker, it is useful for managing the container, we won't do the same thing again and again via commands to connect with the containers and all, it is very easily do with the docker compose file.

It can be possible, just with one command:

1. docker compose up

docker also provide with CLI which will generates these files for us.

1. docker init

It will ask some question to create a perfect yml file for you.

1. ? What application platform does your project use? Node
2. ? What version of Node do you want to use? (20.11.0)

3. ? What version of Node do you want to use? 20.11.0
4. ? Which package manager do you want to use? npm
5. ? Do you want to run "npm run build" before starting your server? No
6. ? What command do you want to use to start the app? [tab for suggestions] npm run dev

7. ? What command do you want to use to start the app? npm run dev
8. ? What port does your server listen on? 5173

9. ? What port does your server listen on? 5173

It will create 4 files for us.

✔ Created → .dockerignore
✔ Created → Dockerfile
✔ Created → compose.yaml
✔ Created → README.Docker.md

here, the compose.yaml file is the most important file.

After that the next step is to run the below command.

1. docker compose up (now, it is starts building)

but even this won't solves our whole issues and this is not optimal for the developers, that when there is some changes in the file we have to re-ren the docker compose again and again, that's where the new docker features comes in.

## Docker Compose Watch

As the name suggest, it watches to our chnages and do something like:
-> Rebuilding our app
-> Rerunning our container and more!

It automatically updates our service container
We can do 3 main thing with the docker watch

1. sync: it moves from our computer to the right place, making sure everything is upto-date in the real time.
2. rebuild: it starts with the new creation of containers and then it updates the service, it is benificial for rolling out the changes production, gurenteen then more recent version of our code in production.
3. sync-restart: it merge the sync and rebuild process, it starts with the sync from the host file system to the container path and restarting the container. This would be benificial for development and testing application.

In simple words, docker compose watch will make sure to update the recent version of the code while development.

how does it work?

first we have to write the text in the compose.yaml file and then run, whatever we write in the develop: it will be in the docker watch.

Ex:
develop:
watch: - path: ./package.json
action: rebuild

1. docker compose up.
   After that if we changes some codes, it won't effect in the UI.
2. docker compose watch
   run the below command in another terminal
   It will watch the changes and packages which will specify in the compose.yaml file, if anything changes it automatically re-run or re-build the container.

## The next concept is docker scout

It actually checks the vernability of our docker images, we can check in
-> Docker Desktop
-> Docker Hub
-> CLI

## Dockerize the next.js application

Same as the React and Node

============================================================================================================

<!-- @format -->

# Learning Docker with docker command

we dont need to install the packages, because we will handle everything with docker itself.
-> we have to create a Dockerfile and write the instructions.

after that we have to build the images

1. docker build -t react-docker .

2. docker run react-docker (for running the docker).

but it won't work because the docker container runs in the isolated environment, so the port is not accessable for outside the container.
we have to use the PORT mapping, it is the bridge between the host machine and docker container.

3. docker run -p 5173:5173 react-docker

now, when we do some changes in the code, it won't affect in the UI, so we have to run the build again and again but this won't be the good approch. It happens because in the container there is still a previous code. so we have to update the container again and again via some network operations.

4. docker run -p 5173:5173 -v "${pwd}:/app" -v /app/node_modules react-docker (here, pwd is the current directory and app is in the container)

## play with docker images and container

1. docker ps (to check the docker conatiner)
2. docker ps -a (to check the all docker conatiner)

3. docker container prune (stopped all container which is not running)
4. docker rm d20 --force (only need 3 digit of conatiner id)

## publish a docker images in the host service provider.

1. docker login (Login succeeded -> means you are logged in)

now, we can publish the image by using the following command.

2. docker tag react-docker animeshkumar7717/react-docker (username/name-of-image)

after that lets publish our image by using the following command.

3. docker push animeshkumar7717/react-docker

============================================================================================================

<!-- @format -->

## Docker in MERN project

In this project we have 3 different services or container, with the help of
docker compose.yaml file, we have to manage the container.

below is the code for the compose.yaml file:

<!-- ---------------------------------------------------- -->

version: "3.8" (this is the version of docker)

# define the services/containers to be run

services: (how many services are there, here is 3 web (frontend), api for (backend), db for (database))

# define the frontend service

# we can use any name for the service. A standard naming convention is to use "web" for the frontend

# web: (for frontEnd)

we use depends_on to specify that service depends on another service # in this case, we specify that the web depends on the api service # this means that the api service will be started before the web service

# depends_on: - api (it depends on api, means api will run first)

specify the build context for the web service # this is the directory where the Dockerfile for the web service is located

# build: ./frontend (this is the directory)

specify the ports to expose for the web service # the first number is the port on the host machine # the second number is the port inside the container

# ports: - 5173:5173 (specifies the port first one is for the hub port and second one is for the local)

specify the environment variables for the web service # these environment variables will be available inside the container

# environment:

# VITE_API_URL: http://localhost:8000

    # this is for docker compose watch mode
    # anything mentioned under develop will be watched for changes by docker compose watch and it will perform the action mentioned

# develop: ( whatever we write inside the develop, it goes to the docker compose watch mode )

      # we specify the files to watch for changes
      watch:
        # it'll watch for changes in package.json and package-lock.json and rebuild the container if there are any changes
        - path: ./frontend/package.json
          action: rebuild
        - path: ./frontend/package-lock.json
          action: rebuild
        # it'll watch for changes in the frontend directory and sync the changes with the container real time
        - path: ./frontend
          target: /app
          action: sync

# define the api service/container

# api: (this is for the backend)

api service depends on the db service so the db service will be started before the api service

# depends_on: - db (the depends on db, that means db will run first)

    # specify the build context for the api service

# build: ./backend (this is the backedn directory)

    # specify the ports to expose for the api service
    # the first number is the port on the host machine
    # the second number is the port inside the container

# ports: (specifies the post, first one is for the hub and second one is for the local)

      - 8000:8000

    # specify environment variables for the api service
    # for demo purposes, we're using a local mongodb instance

# environment: (this url for the database)

      DB_URL: mongodb://db/anime

    # establish docker compose watch mode for the api service

# develop: (whatever we write inside the develop it goes to the docker compose watch)

      # specify the files to watch for changes
      watch:
        # it'll watch for changes in package.json and package-lock.json and rebuild the container and image if there are any changes
        - path: ./backend/package.json
          action: rebuild
        - path: ./backend/package-lock.json
          action: rebuild

        # it'll watch for changes in the backend directory and sync the changes with the container real time
        - path: ./backend
          target: /app
          action: sync

# define the db service

# db:

specify the image to use for the db service from docker hub. If we have a custom image, we can specify that in this format # In the above two services, we're using the build context to build the image for the service from the Dockerfile so we specify the image as "build: ./frontend" or "build: ./backend". # but for the db service, we're using the image from docker hub so we specify the image as "image: mongo:latest" # you can find the image name and tag for mongodb from docker hub here: https://hub.docker.com/_/mongo
image: mongo:latest

    # specify the ports to expose for the db service
    # generally, we do this in api service using mongodb atlas. But for demo purposes, we're using a local mongodb instance
    # usually, mongodb runs on port 27017. So we're exposing the port 27017 on the host machine and mapping it to the port 27017 inside the container
    ports:
      - 27017:27017

    # specify the volumes to mount for the db service
    # we're mounting the volume named "anime" inside the container at /data/db directory
    # this is done so that the data inside the mongodb container is persisted even if the container is stopped
    volumes:
      - anime:/data/db

# define the volumes to be used by the services

volumes:
anime:

## Now

After that we have to run the

1. docker compose up
   to start the compose file, but when you do some changes in the file it won't do anything, that's the reason you have to run the following command to watch.
2. docker compose watch
   It watches the changes which will specifies in the yaml file.

We have to run the 2nd command in the next terminal.

============================================================================================================

<!-- @format -->

## Everything is same
