# Docker Cheat sheet

- [Docker Cheat sheet](#docker-cheat-sheet)
  - [What Docker is](#what-docker-is)
    - [Docker Benefits](#docker-benefits)
    - [The underlying technology](#the-underlying-technology)

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