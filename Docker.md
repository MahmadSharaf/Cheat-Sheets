# Docker Cheat sheet

- [Docker Cheat sheet](#docker-cheat-sheet)
  - [What Docker is](#what-docker-is)
    - [Docker Benefits](#docker-benefits)
    - [The underlying technology](#the-underlying-technology)
  - [Docker Architecture](#docker-architecture)
    - [Docker Engine](#docker-engine)
      - [Docker Client](#docker-client)
        - [Docker CLI](#docker-cli)
      - [Docker Daemon](#docker-daemon)
    - [Docker Registry](#docker-registry)
  - [Docker Objects](#docker-objects)
    - [Images](#images)
      - [Image Tags](#image-tags)
      - [Image Layers](#image-layers)
      - [Images Common CLI commands](#images-common-cli-commands)
    - [Containers](#containers)
      - [Containers Common CLI commands](#containers-common-cli-commands)

## What Docker is

- [Docker](https://docker.com) is an open platform for developing, shipping, and running applications.
- Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.
- With Docker, you can package your application with all its dependencies into a single unit called Container.
- Containerized applications enables you to test and build on your convenient local machine, then deploy to any docker-enabled server without the need to re-test or re-adjust to the server environment.
- The core concept is "develop once, run anywhere"

### Docker Benefits

- Saving resources:
  - Hardware resources can be capped within the settings.
  - All containerized applications share the same resources. No need for reserving unnecessary resources.
- Portability:
  - Applications are packages in a platform-agonistic manner, and run in an isolated environment.
  - This enables running applications alongside each other and on any operating system.
- Technology agnostic
  - It is independent of the technology used.
  - Avoids the pain of installing each technology, and its dependencies, used in development and their versions in the local operating system.

### The underlying technology

- Docker is written in the Go programming language and takes advantage of several features of the Linux kernel to deliver its functionality.
- Docker uses a technology called **namespaces** to provide the isolated workspace called the **container**. When you run a container, Docker creates a set of namespaces for that container.
- These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.

## Docker Architecture

- Users interact with Docker through **Docker CLI/CLient** which enables them to manage **Docker objects**.
- **Docker CLI** sends **API requests** to **Docker Daemon** which manages **Docker objects**.
- **Docker registries** acts as a Warehouse for images (*A type of Docker Objects*) which Docker Daemon can store and retrieve images from.

### Docker Engine

- Docker Engine is an open source containerization technology for building and containerizing your applications.
- Docker Engine acts as a client-server application with Docker Daemon and Docker Client.

#### Docker Client

- It is a command line interface (CLI) called `docker` that users interact with.
- It sends all commands to `dockerd` via Docker REST API.
- It can communicate with more than one daemon.

##### Docker CLI

- It consists of 3 parts, `docker` command, docker object, then the action. `docker <object> <action>`
- All commands can be listed by `docker --help`.
- Commands for a specific object can be listed by `docker <object> --help`

#### Docker Daemon
  
- It is a server with a long-running process called `dockerd`.
- It listens for API requests and manages Docker objects such as containers, images, networks, and volumes.
- A daemon can also communicate with other daemons to manage Docker services.

### Docker Registry

- It is used to store (PUSH) and retrieve (PULL) images from.
- **Docker Hub** is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default.
- When you use the `docker pull` or `docker run` commands, the required images are pulled from your configured registry if not found locally. When you use the `docker push` command, your image is pushed to your configured registry.

## Docker Objects

### Images

- It is a read-only template with instructions to create a container.
- An image can be considered as an installation of an application.
- It is often based on another image with additional customization. For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.
- You might create your own images or you might only use those created by others and published in a registry.

#### Image Tags

- They are reference to Docker Images.
- There can be different tags (versions) for the same image with different alterations or even different tags that points to the same image ID/Digest.
- The tag can refer to the version, supported OS, or a customized alteration. Ex: `Latest`, `2.5`, `alpine`, `Sharaf/Ubuntu`.
- `latest` tag is the default one, but it doesn't refer as the most updated version of the image, at least not all the time.
- Common CLI commands:

#### Image Layers

- Image layers are the instructions of building the image.
- You can create your own image by creating a **Dockerfile** with a simple syntax for defining the steps needed to create the image and run it.
- Each instruction in a **Dockerfile** creates a layer in the image. For example, the image have `Ubuntu` as the first layer, then `Apache` as a second layer, and an `App` as the third one.
- When you change the **Dockerfile** and rebuild the image, only those layers which have changed are rebuilt.
  - This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

#### Images Common CLI commands

- `docker image ls`: List available images.
- `docker [image] build [OPTIONS] PATH | URL | -`: Build an image from a Dockerfile.
- `docker [image] history <image name or id>`: It shows the instructions/layers of building the image.
- `docker [image] inspect <image name or id>`: Display detailed information on one or more images.
- `docker [image] push [OPTIONS] NAME[:TAG]`: Push an image or a repository to a registry.
- `docker [image] tag <SOURCE_IMAGE[:TAG]> <[repository/]TARGET_IMAGE[:TAG]>`: It creates a TARGET_IMAGE that refers to SOURCE_IMAGE. EX: `docker tag redis:5.0-alpine mahmadsharaf/redis:dev`

### Containers

- A container is a runnable instance of an image.
- You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.
- By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.
- A container is defined by its image as well as any configuration options you provide to it when you create or start it.
- When a container is removed, any changes to its state that are not stored in persistent storage disappear.

#### Containers Common CLI commands

- `docker container create [OPTIONS] IMAGE [COMMAND] [ARG...]`: Create a new container
- `docker container exec [OPTIONS] CONTAINER COMMAND [ARG...]`: Run a command in a running container
- `docker container inspect [OPTIONS] CONTAINER [CONTAINER...]`: Display detailed information on one or more containers
- `docker container kill [OPTIONS] CONTAINER [CONTAINER...]`: Kill one or more running containers
- `docker container logs [OPTIONS] CONTAINER`: Fetch the logs of a container
- `docker container ls [OPTIONS]`: List containers
- `docker container port CONTAINER [PRIVATE_PORT[/PROTO]]`: List port mappings or a specific mapping for the container
- `docker container prune [OPTIONS]`: Remove all stopped containers
- `docker container restart [OPTIONS] CONTAINER [CONTAINER...]`: Restart one or more containers
- `docker container rename CONTAINER NEW_NAME`: Rename a container
- `docker container rm [OPTIONS] CONTAINER [CONTAINER...]`: Remove one or more containers
- `docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]`: Run a command in a new container
- `docker container start [OPTIONS] CONTAINER [CONTAINER...]`: Start one or more stopped containers
- `docker container stop [OPTIONS] CONTAINER [CONTAINER...]`:Stop one or more running containers
