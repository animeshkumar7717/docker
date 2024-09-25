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
