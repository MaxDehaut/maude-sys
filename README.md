# Running the Maude Docker Container

This document describes how to build and run a Docker container for the Maude system, and how to interact with the Maude console.

## Prerequisites

You need to have Docker and Docker Compose installed on your machine. Please refer to the official Docker documentation for instructions on how to install Docker:

- Install Docker
- Install Docker Compose

## Building and Running the Container

The Docker Compose configuration file (docker-compose.yml) provided in the project root directory can be used to build and run the Maude container. Here's what you need to do:

1. Navigate to the project directory that contains the Dockerfile and docker-compose.yml.
1. Run docker-compose up. This command will start the Maude container in interactive mode.
   Here's the command sequence:

```
cd /path/to/project/directory
docker-compose up
```

The docker-compose up command will build an image for the Maude system (if it hasn't been built yet) and start a container based on that image.

## Interacting with the Maude Console

Once the Maude Docker container is up and running, you'll automatically be dropped into an interactive session with the Maude console. This is due to the stdin_open: true and tty: true configurations in the docker-compose.yml file.

In this interactive session, you can start typing Maude commands directly into the console.

## Detaching and Reattaching to the Console

If you need to detach from the Maude console but want to keep it running, you can use the CTRL-p CTRL-q sequence. This will detach your terminal from the container but keep the container running in the background.

To reattach to the console, use the docker attach command followed by the container ID or name:

```
docker attach <container_id>
```

You can get the <container_id> by running the docker ps command, which lists all running containers.

Please note that if you start the container in detached mode (docker-compose up -d), the docker attach command won't give you an interactive shell. To get an interactive session again, you would need to stop and remove the container (docker-compose down) and then run docker-compose up again (without the -d flag).

## Hello, World! in Maude

```
Maude> fmod HELLO-WORLD is
    pr STRING .
    op helloWorld : -> String .
    eq helloWorld = "Hello, World!" .
endfm
```

This module, HELLO-WORLD, imports the predefined STRING module, defines an operation helloWorld that requires no arguments (-> String), and equates this operation to the string "Hello, World!".

To test this module, we can reduce helloWorld:

```
Maude> reduce in HELLO-WORLD : helloWorld .
```
