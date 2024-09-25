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
