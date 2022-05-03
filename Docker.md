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
  - [Data Management](#data-management)
    - [Volumes](#volumes)
      - [Volumes Common CLI commands](#volumes-common-cli-commands)
    - [Bind Mounts](#bind-mounts)
      - [Bind Mounts Common CLI commands](#bind-mounts-common-cli-commands)
    - [tmpfs mounts](#tmpfs-mounts)
  - [Docker Networking](#docker-networking)
    - [Network Drivers](#network-drivers)
      - [Bridge](#bridge)
      - [Host](#host)
      - [None](#none)
      - [overlay](#overlay)
      - [ipvlan](#ipvlan)
      - [macvlan](#macvlan)
      - [3rd-party networks](#3rd-party-networks)
    - [Network Common CLI commands](#network-common-cli-commands)
  - [Docker compose](#docker-compose)

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

## Data Management

- Docker has two options for containers to store files on the host machine, so that the files are persisted even after the container stops: **volumes**, and **bind mounts**.
- Docker also supports containers storing files in-memory on the the host machine. Such files are not persisted.
  - If you’re running Docker on Linux, **tmpfs** mount is used to store files in the host’s system memory.
  - If you’re running Docker on Windows, named pipe is used to store files in the host’s system memory.
- No matter which type of mount you choose to use, the data looks the same from within the container. It is exposed as either a directory or an individual file in the container’s filesystem.
- Bind mounts and volumes can both be mounted into containers using the `-v` or `--volume` flag, but the syntax for each is slightly different. For tmpfs mounts, you can use the `--tmpfs` flag. We recommend using the `--mount` flag for both containers and services, for bind mounts, volumes, or tmpfs mounts, as the syntax is more clear.

### Volumes

- They are stored in a part of the host filesystem which is created and managed by Docker (/var/lib/docker/volumes/ on Linux).
- Non-Docker processes *should not modify* this part of the filesystem.
- Volumes are the best way to persist data in Docker.
- A given volume can be mounted into multiple containers simultaneously.
- Volumes also support the use of volume drivers, which allow you to store your data on remote hosts or cloud providers, among other possibilities.

#### Volumes Common CLI commands

- `docker volume create [OPTIONS] [VOLUME]`: Creates a new Volume
- `docker volume prune [OPTIONS]`: Removes unused Volumes
- `docker volume inspect [OPTIONS] VOLUME [VOLUME...]`: Display detailed information on one or more volumes
- `docker volume ls`: List volumes
- `docker volume rm [OPTIONS] VOLUME [VOLUME...]`: Remove one or more volumes. You cannot remove a volume that is in use by a container.
- `docker run -v [VOLUME_NAME:]CONTAINER_STORAGE_PATH IMAGE`: Mount a volume to a container.

### Bind Mounts

- Available since the early days of Docker.
- They may be stored anywhere on the host system.
- They may even be important system files or directories.
- Non-Docker processes on the Docker host or a Docker container can modify them at any time.
- Bind mounts have limited functionality compared to volumes.
- When you use a bind mount, a file or directory on the host machine is mounted into a container.
- The file or directory is referenced by its full path on the host machine.
- The file or directory does not need to exist on the Docker host already. It is created on demand if it does not yet exist.
- You can’t use Docker CLI commands to directly manage bind mounts.

#### Bind Mounts Common CLI commands

- `docker run -v LOCAL_PATH:CONTAINER_STORAGE_PATH IMAGE`: Bind mount to a container.

### tmpfs mounts

- They are stored in the host system’s memory only, and are never written to the host system’s filesystem.
- It can be used by a container during the lifetime of the container, to store non-persistent state or sensitive information.

## Docker Networking

- Docker networking is primarily used to establish communication between Docker containers and the outside world via the host machine where the Docker daemon is running.

### Network Drivers

-Docker’s networking subsystem is pluggable, using drivers. Several drivers exist by default, and provide core networking functionality.

#### Bridge

- The default driver.
- Bridge networks are usually used when your applications run in standalone containers that need to communicate with each others.

#### Host

- Disables Docker's network isolation.
- It means that containers see and use exactly the same network as the host.

#### None

- The none network driver does not attach containers to any network.
- Containers do not access the external network or communicate with other containers.

#### overlay

- Overlay networks connect multiple Docker daemons together and enable swarm services to communicate with each other.
- You can also use overlay networks to facilitate communication between a swarm service and a standalone container, or between two standalone containers on different Docker daemons.

#### ipvlan

- IPvlan networks give users total control over both IPv4 and IPv6 addressing.
- The VLAN driver builds on top of that in giving operators complete control of layer 2 VLAN tagging and even IPvlan L3 routing for users interested in underlay network integration.

#### macvlan

- Macvlan networks allow you to assign a MAC address to a container, making it appear as a physical device on your network.
- The Docker daemon routes traffic to containers by their MAC addresses.
- Using the macvlan driver is sometimes the best choice when dealing with legacy applications that expect to be directly connected to the physical network, rather than routed through the Docker host’s network stack.

#### 3rd-party networks

- You can install and use third-party network plugins with Docker.
- Third-party network plugins allow you to integrate Docker with specialized network stacks.
- These plugins are available from Docker Hub or from third-party vendors.

### Network Common CLI commands

- `docker network create [OPTIONS] NETWORK` : Create a network
- `docker network connect [OPTIONS] NETWORK CONTAINER` : Connect a container to a network
- `docker network disconnect [OPTIONS] NETWORK CONTAINER` : Disconnect a container from a network
- `docker network inspect [OPTIONS] NETWORK [NETWORK...]` : Display detailed information on one or more networks
- `docker network inspect [OPTIONS] DRIVER [DRIVER...]` : Display detailed information on one or more network drivers
- `docker network ls` : List networks
- `docker network prune` : Remove all unused networks
- `docker network rm NETWORK [NETWORK...]` : Remove one or more networks
- `docker run --network=NETWORK IMAGE` : Run a container and connect it to NETWORK network

## Docker compose

- It enables managing an application that uses more than one container at the same time. So, you will be able to create, start, stop, and remove them with a single command.
- They can be created according to the instructions in a file called `docker-compose.yml`.
- The Compose file is a YAML file defining services, networks, and volumes for a Docker application.
- The daemon or CLI command is `docker-compose` compared to `docker`.
