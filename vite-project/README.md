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
