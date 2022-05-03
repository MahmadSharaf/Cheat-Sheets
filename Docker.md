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

