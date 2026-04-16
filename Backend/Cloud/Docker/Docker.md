![Docker Logo](https://i.imgur.com/7J7c4Az.png)
# What Docker is used for ?

**Docker enables developers to package applications into containers, which are lightweight, standalone, and executable software packages that include everything needed to run an application: code, runtime, system tools, libraries, and settings.**

Docker's key components:
1. **Docker Engine**: The core part of Docker that creates and runs containers.
2. **Docker Hub**: A public repository where you can share and access Docker images.
3. **Docker Compose**: A tool for defining and running multi-container Docker applications.
4. **Docker Swarm**: A native clustering and orchestration tool for Docker containers.

---
# Docker Commands

`Docker -v` : To check docker installed version

`Docker run -it <image_name>` : To create docker container from the specified Docker image in **Interactive Mode**
>e.g. , `Docker run -it Ubuntu`

- `-i` (interactive): Keeps STDIN open even if not attached.
- `-t` (tty): Allocates a pseudo-TTY, allowing you to have an interactive shell session.

`Docker exec <container_name> <command>`: Executing a command inside an already running container. 
> e.g. , `Docker exec -it stupefied_wozniak bash`
> e.g. , `Docker exec stupefied_wozniak ls`

The above command will download the Image from [Docker Hub](https://hub.docker.com/), if the image is not present in the local machine. From that moment same image will be used whenever this same command is executed. Although the image might be same but instances of every created from this command will always be different. 

```bash
Docker container ls
```
Will lists only running containers at the moment

![[Pasted image 20241225190519.png]]
`Docker container ls -a` : Will list all the containers, even those containers which are not running
![[Pasted image 20241225190535.png]]

`Docker images`: will lists all the docker images available in the local system 

`Docker start <container_name>`: Will start  the mentioned container
> e.g. , `Docker start stupefied_wozniak`

`Docker stop <container_name>`: Will stop the mentioned container
> e.g. , `Docker stop stupefied_wozniak`


---
# Docker Images v/s Containers

**A simple analogy:** `A Docker image is like a recipe, and a Docker container is the prepared dish. You can use the same recipe to make multiple dishes, just like you can use a Docker image to create multiple containers.`

| **Feature**      | **Docker Image**                                                                 | **Docker Container**                              |
| ---------------- | -------------------------------------------------------------------------------- | ------------------------------------------------- |
| **Definition**   | A read-only, standalone file with all the necessary software for an application. | A runtime instance of a Docker image.             |
| **Immutability** | Immutable (cannot be changed).                                                   | Mutable (can be changed while running).           |
| **Purpose**      | Acts as a blueprint for creating containers.                                     | An isolated environment for running applications. |
| **Layers**       | Built in layers that stack on top of each other.                                 | Runs as a single unit of an image.                |
| **State**        | Static (doesn't change once created).                                            | Dynamic (changes with each run).                  |

---

# Custom Docker Images


---

# Port Mapping 

Port mapping is a key concept in Docker that allows us to map network ports of a Docker container to ports on the host machine. This way, we can access the services running inside a container from outside the container.

**Syntax**: `Docker run -p <host_port>:<container_port> <image_name>`
> e.g. , `Docker run -p 3000:1025 mailhog/mailhog 

**To Run in interactive mode**: `Docker run -it -p <host_port>:<container_port> <image_name>

Let's consider this situation that our container is running an image for node.js and is directing to PORT: 8000 but when we go to `http://localhost:8000` it shows us nothing this is because we are running the port inside the container, not in the host machine. 

For a PORT to become accessible we need to expose the *container's PORT* to the *host machine*. This way we can expose the container's PORT and access it through any browser or postman.

---

# Containerize an Application

Let's actually start using Docker by containerizing our application. For the instance, consider we ehave created a simple Express.js app with Node.js version 22.11.0 

![[Pasted image 20241225204135.png]]

Now we have to create a Docker file inside the the application with name **Dockerfile** (remember, it should be written in the exact manner and with no extension). 

Inside that file we will have:
### 1. Base Image

The base image is the starting point for your Docker image. Since we're working with a Node.js application, we'll use a Node.js base image. This image includes Node.js and NPM, which are required to run your application.

### 2. Working Directory

The working directory is the directory inside the container where the application code will reside. This helps organize the container's filesystem.

### 3. Copy Application Code

We need to copy the application code from the host machine into the container.

### 4. Install Dependencies

Run the necessary commands to install the application's dependencies.

### 5. Expose Port

Expose the port that the application will use, so it can be accessed from outside the container.

### 6. Command to Run the Application

Specify the command that should be executed to start the application when the container is run.

> e.g. , Provided screen shot is an example of a simple [Express.js](https://expressjs.com/) application containerized with BASE_IMAGE of **ubuntu** and using [Fast Node Manager](https://github.com/Schniz/fnm) for installing and Managing [Node.js](https://nodejs.org/en) version.
![[Pasted image 20241225221351.png]] 

After this run command `Docker build -t docker-node .` from the root of your application
