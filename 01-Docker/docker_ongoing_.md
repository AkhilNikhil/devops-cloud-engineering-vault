# 📝 docker ongoing 

```text
docker 

📘 Docker – Table of Contents

1. Introduction to Docker
   1.1 What is Docker?
   1.2 Why use Docker?
   1.3 Docker Architecture (Client, Daemon, Registry, Images, Containers)
   1.4 Docker vs Virtual Machines

2. Installation & Setup
   2.1 Installing Docker on Linux
   2.2 Installing Docker on Windows
   2.3 Installing Docker on macOS
   2.4 Verifying installation

3. Docker Images
   3.1 What is a Docker Image?
   3.2 Pulling images
   3.3 Inspecting images
   3.4 Building custom images (Dockerfile)
   3.5 Image layers & caching
   3.6 Tagging images
   3.7 Removing images

4. Docker Containers
   4.1 What is a container?
   4.2 Running containers
   4.3 Viewing container logs
   4.4 Executing commands in containers
   4.5 Starting, stopping, restarting
   4.6 Removing containers
   4.7 Container lifecycle

5. Dockerfile
   5.1 Basic structure
   5.2 Common instructions (FROM, RUN, COPY, ADD, CMD, ENTRYPOINT)
   5.3 EXPOSE, ENV, WORKDIR, VOLUME
   5.4 Multi-stage builds
   5.5 Best practices for Dockerfile

6. Docker Volumes & Storage
   6.1 Types of volumes (host, anonymous, named)
   6.2 Creating and managing volumes
   6.3 Mounting volumes
   6.4 Backing up and restoring volumes

7. Docker Networking
   7.1 Docker network types (bridge, host, none, overlaying, mackvlan explain all)
   7.2 Creating custom networks
   7.3 Connecting containers
   7.4 Port mapping
   7.5 DNS inside Docker
	commands for docker networking 

8. Docker Compose
   8.1 What is Docker Compose?
   8.2 docker-compose.yml file format
   8.3 Running multi-container applications
   8.4 Environment variables in Compose
   8.5 Networking in Compose
   8.6 Scaling services
   8.7 Common Compose commands

9. Docker Registry & Repositories
   9.1 Docker Hub
   9.2 Private registries
   9.3 Logging into registry
   9.4 Pushing & pulling images
   9.5 Managing image tags

10. Docker Security
   10.1 Container isolation
   10.2 Scanning images for vulnerabilities
   10.3 Managing secrets securely
   10.4 Least privilege principle

11. Docker Swarm (Optional)
   11.1 Introduction to Swarm
   11.2 Initializing cluster
   11.3 Deploying services
   11.4 Scaling containers
   11.5 Rolling updates

12. Docker with CI/CD
   12.1 Using Docker in Jenkins pipelines
   12.2 Docker build & push automation
   12.3 Deploying to AWS/EKS/Kubernetes

13. Troubleshooting Docker
   13.1 Common errors
   13.2 Inspecting logs
   13.3 Cleaning unused resources (prune)
   13.4 Debugging containers

14. Real-time DevOps Use Cases
   14.1 Deploying apps using Docker
   14.2 Docker for Microservices
   14.3 Blue-Green deployments using Docker

15. Important Docker Commands Cheat Sheet
   15.1 Image commands
   15.2 Container commands
   15.3 Network commands
   15.4 Volume commands
   15.5 Compose commands





1. Introduction to Docker
   1.1 What is Docker?
   1.2 Why use Docker? (Benefits)
   1.3 Docker Architecture (Client, Daemon, Registry, Images, Containers)
   1.4 Docker vs Virtual Machines
   1.5 Docker Architecture Diagram (Text)
   1.6 Summary






====================================================================
1.1 What is Docker?
====================================================================
Docker is an open-source containerization platform that allows applications 
and their dependencies to run inside lightweight, isolated containers. 
These containers ensure consistent execution across 
different environments (dev, QA, prod, cloud).

Key points:
- OS-level virtualization (no separate OS per container)
- Packages app + dependencies together
- Runs consistently on any machine
- Fast, portable, efficient





====================================================================
1.2 Why use Docker? (Benefits)
====================================================================
1. Consistency Across Environments  
   Runs the same everywhere because app + dependencies are packaged together.

2. Lightweight  
   Containers share host OS kernel → faster & smaller than VMs.

3. Faster Deployment  
   Launch in seconds, easy rollback, versioning.

4. Portability  
   Works on Linux, Windows, macOS, On-prem, AWS, Azure, GCP.

5. Isolation  
   Each container has its own filesystem, process space, network.

6. Scalability  
   Perfect for microservices & Kubernetes.

7. DevOps Friendly  
   Works well with CI/CD tools (Jenkins, GitLab, GitHub Actions).





====================================================================
1.3 Docker Architecture (Client, Daemon, Registry, Images, Containers)
====================================================================
Docker uses a client-server architecture.

                          ┌───────────────────────────┐
                          │       Docker Client       │
                          │  (CLI: docker run/build)  │
                          │  (REST API / HTTP calls)  │
                          └───────────────┬───────────┘
                                          │
                                          │ Sends Commands via
                                          │ REST API (Unix socket/TCP)
                                          ▼
                         ┌────────────────────────────────────┐
                         │          Docker Daemon             │
                         │            (dockerd)               │
                         │────────────────────────────────────│
                         │  • Handles container lifecycle     │
                         │  • Manages images, networks        │
                         │  • Builds images from Dockerfile   │
                         │  • Pulls/pushes from registry      │
                         │  • Exposes Docker Engine REST API  │
                         └───────────┬───────────┬───────────┘
                                   	  │           │
                                  	  │           │
                   ┌────────────────┘           └───────────────────┐
                   ▼                                               	       ▼

        ┌──────────────────────────────┐                 ┌────────────────────────────┐
        │        Docker Images       		    │                 │      Docker Containers      │
        │  (Read-only templates)     		    │                 │ (Running instances of image)│
        │  • Stored locally          		    │                 │  • Isolated processes       │
        │  • Pulled from registry     		    │                 │  • Uses host OS kernel      │
        └──────────────────────────────┘                 └────────────────────────────┘

                                      │
                                      │ Pull/Push Images
                                      ▼

                     ┌──────────────────────────────────────────┐
                     │   		   	         Docker Registry                 │
                     │  		   	  (Docker Hub, AWS ECR, Azure ACR, GCR)  │
                     │ 			    • Stores versioned Docker images         │
                     │ 				 • Public or private                     │
                     └──────────────────────────────────────────┘


1. Docker Client
   - Provides the user interface to interact with Docker using CLI commands or REST API.
   - Sends all requests (build, run, pull) to Docker Daemon for execution.

2. Docker Engine REST API
   - A HTTP/JSON API used by Client → Daemon communication.
   - Allows remote automation tools and services to control Docker operations.

3. Docker Daemon (dockerd)
   - The core Docker engine that builds images, runs containers, and manages networks/volumes.
   - Executes all tasks requested by the client and interacts with registries.

4. Docker Images
   - Read-only application blueprints containing code, dependencies, and environment.
   - Used to create containers quickly and consistently.

5. Docker Containers
   - Lightweight runtime instances created from images, sharing the host OS kernel.
   - Provide isolated environments for running applications.

6. Docker Registry
   - A storage service for Docker images (public or private).
   - Pull images to run containers or push custom images for deployment.



1. Docker Client  
   - CLI tool where you run commands  
   - Sends instructions to Docker Daemon  
   - Example commands: docker build, docker run, docker pull

2. Docker Daemon (dockerd)  
   - The core engine  
   - Listens to API requests from client  
   - Responsible for:
     • Managing containers  
     • Managing images  
     • Managing networks  
     • Managing volumes  

3. Docker Registry  
   - Stores Docker images  
   - Public: Docker Hub  
   - Private: AWS ECR, Azure ACR, Google GCR  

4. Docker Images  
   - Read-only templates  
   - Created using Dockerfile  
   - Example: nginx:latest, ubuntu:22.04

5. Docker Containers  
   - RUNNING instances of images  
   - Isolated but share host OS  
   - Fast, lightweight, portable





===============================
VIRTUAL MACHINES vs CONTAINERS
===============================

Virtual Machines (VMs)                                   | Containers
---------------------------------------------------------|---------------------------------------------------------
1. Each VM runs with its own full OS                     | 1. Containers share the host OS kernel
2. Heavyweight (GBs in size)                             | 2. Lightweight (MBs in size)
3. Slow boot time (seconds to minutes)                   | 3. Very fast boot time (ms to seconds)
4. High resource usage (CPU, RAM, Disk)                  | 4. Low resource usage
5. Strong hardware-level isolation                       | 5. Process-level isolation
6. Lower performance due to virtualization overhead      | 6. Near-native performance
7. Moderate portability (large VM images)                | 7. Highly portable (small images)
8. Difficult to scale quickly                            | 8. Easy to scale using Docker/Kubernetes
9. Used for legacy apps, full OS environments            | 9. Used for microservices, CI/CD, cloud-native apps
10. Requires OS maintenance (patching, updates)          | 10. Minimal maintenance; only app + dependencies
11. Best when strong isolation or multi-OS needed        | 11. Best when fast deployment and efficiency needed



====================================================================
1.4 Docker vs Virtual Machines
====================================================================
Feature                | Docker Containers              | Virtual Machines
-----------------------|--------------------------------|-----------------------------
Isolation              | Process-level isolation        | Full OS isolation
Performance           | High                           | Lower (heavy)
Boot Time             | Seconds                        | Minutes
Size                  | MBs                            | GBs
OS Kernel             | Shared with host               | Separate OS per VM
Resource Usage        | Low                            | High
Scalability           | Very high                      | Lower
Best Use Case         | Microservices, CI/CD           | Full OS, legacy apps

Summary:
- Docker is lightweight & fast.
- VMs are heavy but provide complete isolation.





====================================================================
1.6 Summary
====================================================================
- Docker uses OS-level virtualization.
- Containers are lightweight, fast, and portable.
- Architecture includes Client → Daemon → Images → Containers → Registry.
- Docker is better than VMs for modern DevOps workloads.
- Ideal for CI/CD, microservices, cloud-native apps.





===============================
CONTAINERS – SIMPLE DEFINITION
===============================
A container is a lightweight, portable, and isolated environment that packages
an application along with all its dependencies so it can run consistently on any system.
 It shares the host OS kernel, making it much faster and smaller than virtual machines.

===============================
MAIN POINTS ABOUT CONTAINERS
===============================
1. Lightweight – Uses very little CPU, RAM, and storage.
2. Fast Startup – Containers start in milliseconds.
3. Portable – Same container runs anywhere (local, cloud, server).
4. Isolated – Each container runs separately from others.
5. Consistent – Eliminates “works on my machine” issues.
6. Easy to Scale – Perfect for microservices and Kubernetes.
7. Uses Images – Containers are created from Docker images.
8. Secure – Provides process-level isolation.
9. Efficient – Shares host OS kernel, no full OS required.
10. Ideal for DevOps – Works well with CI/CD pipelines.

===============================
SHORT SUMMARY
===============================
Containers = Fast, lightweight, isolated environments to run applications reliably anywhere.


AWS → EC2 → Install Docker → Run Containers



========================================
DOCKER LAYERS (BOTTOM → TOP OVERVIEW)
========================================

Layer 1: Host Operating System  
--------------------------------
• This is the actual OS installed on your machine/server (Linux, Windows, macOS).  
• Docker uses this OS kernel to run all containers.

----------------------------------------

Layer 2: Docker Engine (Docker Daemon)  
----------------------------------------
• The core service that manages images, containers, volumes, and networks.  
• Communicates using Docker REST API and executes all Docker commands.

----------------------------------------

Layer 3: Docker Images  
----------------------------------------
• Read-only blueprints used to create containers.  
• Contains app code + dependencies + runtime environment.  
• Built using Dockerfile.

----------------------------------------

Layer 4: Image Layers (Union File System)  
----------------------------------------
• Each instruction in Dockerfile creates a new layer (e.g., FROM, RUN, COPY).  
• Layers are cached, shared, and reused to save space and speed up builds.

----------------------------------------

Layer 5: Docker Containers  
----------------------------------------
• Running (live) instances created from images.  
• Lightweight, isolated, and share the host OS kernel.  
• Containers run the application with its required environment.

----------------------------------------

Layer 6: Applications Inside Containers  
----------------------------------------
• Your actual app (Node.js, Java, Python, Nginx, MySQL, etc.).  
• Runs independently inside each container.


========================================
FULL DOCKER STACK (TEXT DIAGRAM)
========================================

                 ┌─────────────────────────────┐
                 │     Applications (App)      │
                 │ (Running inside container)  │
                 └───────────────▲─────────────┘
                                 │
                 ┌───────────────┴─────────────┐
                 │        Containers            │
                 │ (Live, isolated runtimes)    │
                 └───────────────▲─────────────┘
                                 │
                 ┌───────────────┴─────────────┐
                 │        Image Layers          │
                 │ (FROM, RUN, COPY steps)      │
                 └───────────────▲─────────────┘
                                 │
                 ┌───────────────┴─────────────┐
                 │        Docker Images         │
                 │ (Blueprints for containers)  │
                 └───────────────▲─────────────┘
                                 │
                 ┌───────────────┴─────────────┐
                 │       Docker Engine          │
                 │  (Daemon + REST API)         │
                 └───────────────▲─────────────┘
                                 │
                 ┌───────────────┴─────────────┐
                 │      Host Operating System   │
                 │        (Linux/Windows)       │
                 └─────────────────────────────┘


========================================
SIMPLE SUMMARY
========================================
Host OS  
 → Docker Engine  
   → Docker Images  
     → Image Layers  
       → Containers  
         → Applications

Containers sit **at the top**, running your app, and depend on all layers below them.





Docker:
Docker is a containerization platform that packages and runs applications inside isolated, 
lightweight containers. It ensures the application works the same on any system.

Docker Image:
A Docker Image is a read-only template that contains the application code, libraries, 
dependencies, and environment settings. Containers are created from images.

Dockerfile:
A Dockerfile is a simple text file containing step-by-step instructions on how to build 
a Docker Image. It defines the base image, packages, commands, ports, and final app setup.

Docker Registry:
A Docker Registry is a storage and distribution system for Docker Images. It allows 
you to push (upload) and pull (download) images. Example: Docker Hub, AWS ECR, 
GitHub Container Registry.





# 2.1 Installing Docker on AWS Linux (Amazon Linux 2)

# Step 1: Connect to your AWS EC2 Instance
ssh -i "your-key.pem" ec2-user@your-ec2-public-ip

# Step 2: Update package repository
sudo yum update -y

# Step 3: Install Docker
sudo amazon-linux-extras install docker -y

# Step 4: Start Docker service
sudo service docker start

# Step 5: Enable Docker to start on boot
sudo systemctl enable docker

# Step 6: Add your user to Docker group (run Docker without sudo)
sudo usermod -a -G docker ec2-user
# Note: Log out and log back in or run: newgrp docker

# Step 7: Verify Docker installation
docker --version
docker run hello-world





# 3. Docker Images

# 3.1 What is a Docker Image?
# A Docker image is a lightweight, standalone, and executable package 
# that includes everything needed to run a piece of software: code, 
   runtime, libraries, environment variables, and configuration files.
# Images are read-only templates used to create Docker containers.



# 3.2 Pulling images

# Download an image from Docker Hub (or any registry)
	docker pull <image_name>:<tag>
# Example:
	docker pull amazonlinux:2

# 3.3 Inspecting images
# View detailed information about an image
	docker images          # List all images on your system
    docker inspect <image_name>:<tag>   # Inspect metadata of a specific image



# 3.4 Building custom images (Dockerfile)
# 1. Create a Dockerfile

# Example Dockerfile for AWS Linux 2:

# -------------------
# FROM amazonlinux:2
# RUN yum update -y && yum install -y python3
# CMD ["python3", "--version"]
# -------------------


# 2. Build the image
  docker build -t <your_image_name>:<tag> .
# Example:
  docker build -t my-python-app:1.0 .


# 3.5 Image layers & caching
# - Each instruction in a Dockerfile creates a new layer.
# - Layers are cached, so Docker reuses unchanged layers to speed up builds.
# - Helps reduce storage usage and improve build efficiency.


# 3.6 Tagging images
# Assign a friendly name or version to an image
docker tag <image_id_or_name> <repository>:<tag>
# Example:
docker tag my-python-app:1.0 akhil/my-python-app:v1



# 3.7 Removing images
# Delete images you no longer need
docker rmi <image_name>:<tag>
# Example:
docker rmi my-python-app:1.0


# Optional: Force remove if image is in use
docker rmi -f <image_name>:<tag>


# Docker Containers - Common Commands


# 1. List all Docker images on the system
docker images
# OR
docker image ls


# 2. Create and run a container in interactive mode (attach terminal)
docker run -it <image_name>:<tag> /bin/bash
# Example:
docker run -it ubuntu:latest /bin/bash
# -it opens an interactive terminal inside the container


# 3. Run a container in detached mode (background)
docker run -d <image_name>:<tag>
# Example:
docker run -d nginx:latest
# -d runs the container in the background


# 4. Run a container with a name (interactive or detached)
# Interactive with name:
docker run --name <container_name> -it <image_name>:<tag> /bin/bash
# Detached with name:
docker run --name <container_name> -d <image_name>:<tag>
# Examples:
docker run --name my-ubuntu -it ubuntu:latest /bin/bash
docker run --name my-nginx -d nginx:latest


# 5. Run a container in both interactive and detached mode
docker run -dit --name <container_name> <image_name>:<tag>
# Example:
docker run -dit --name my-ubuntu ubuntu:latest
# -d → detached, -i → keep STDIN open, -t → allocate pseudo-TTY


# 6. List running containers only
docker ps


# 7. List all containers (running + stopped)
docker ps -a


# 8. Enter into a running container (interactive terminal)
docker exec -it <container_name_or_id> /bin/bash
# Example:
docker exec -it my-nginx /bin/bash


# 9. Start a stopped container
docker start <container_name_or_id>


# 10. Stop a running container
docker stop <container_name_or_id>


# 11. Remove a container
docker rm <container_name_or_id>







# Docker Container Lifecycle

# Lifecycle Diagram (text-editor friendly)

           +---------------------+
           |    Docker Image     |
           +----------+----------+
                      |
                      v
           +---------------------+
           |   Container Created  |
           +----------+----------+
                      |
           +----------+----------+
           |     Running         |
           +----------+----------+
           | - Use containerized |
           |   app or exec shell |
           +----------+----------+
          /            |            \
         v             v             v
   Paused State     Stopped State   Killed
     (docker pause)  (docker stop)  (docker kill)
         |             |             |
         v             v             v
     Unpaused        Start Again   Removed
   (docker unpause)  (docker start) (docker rm)




# Docker Container Lifecycle Commands

# 1. Create a container (does not start by default)
docker create --name <container_name> <image_name>:<tag>
# Example:
docker create --name my-container ubuntu:latest

# 2. Start a container
docker start <container_name_or_id>
# Example:
docker start my-container

# 3. Stop a running container (graceful shutdown)
docker stop <container_name_or_id>
# Example:
docker stop my-container

# 4. Pause a running container (suspend all processes)
docker pause <container_name_or_id>
# Example:
docker pause my-container

# 5. Unpause a paused container (resume all processes)
docker unpause <container_name_or_id>
# Example:
docker unpause my-container

# 6. Kill a running container (forceful termination)
docker kill <container_name_or_id>
# Example:
docker kill my-container

# 7. Remove a container
docker rm <container_name_or_id>
# Example:
docker rm my-container

# 4.3 Viewing container logs
# View logs of a running container:
docker logs <container_name_or_id>
# Follow logs in real-time:
docker logs -f <container_name_or_id>



# 4.6 Removing containers
# Remove a stopped container:
docker rm <container_name_or_id>
# Force remove a running container:
docker rm -f <container_name_or_id>



# Quick One-Line Difference Between stop and kill
# docker stop → graceful shutdown (sends SIGTERM, then SIGKILL after timeout)
# docker kill → immediate forceful shutdown (sends SIGKILL)




# Docker Containers - Removal Scenarios

# Important: You cannot remove a container unless it is stopped.
# Node: "Without stopping a container, we cannot remove it"

# Scenarios:
# 1. Container is running → docker rm fails → need stop or kill first
# 2. Container is running → force remove: docker rm -f <container_name_or_id>
# 3. Container is stopped → docker rm <container_name_or_id> works
# 4. Remove all containers (stopped or running):
docker rm -f $(docker ps -aq)



# Removing Images
# Remove a single image:
	docker rmi <image_name_or_id>
# Remove multiple images:
	docker rmi <image1> <image2> <image3>


# Docker System Prune (cleanup)
# Remove stopped containers, unused networks, dangling images:
	docker system prune
# Remove all unused images, not just dangling:
	docker system prune -a
# Force prune without confirmation prompt:
	docker system prune -a -f



# Port Mapping
# - Maps a host machine port to a container port
# - Allows external access to containerized services
# - Syntax: -p <host_port>:<container_port>
# Example:
docker run -d -p 8080:80 nginx:latest



# Dockerfile
# - Text file with instructions to build a Docker image
# - File name: Dockerfile (no extension)
# Main points:
# 1. Defines base image
# 2. Installs dependencies
# 3. Copies application code
# 4. Sets environment and default command



# Common Dockerfile Instructions:
# - FROM <image>            → base image
# - RUN <command>           → execute command in image
# - COPY <src> <dest>       → copy files into image
# - ADD <src> <dest>        → copy files, extract archives
# - CMD ["executable"]      → default command when container runs
# - ENTRYPOINT ["executable"] → default executable
# - ENV <key>=<value>       → environment variable
# - WORKDIR <dir>           → set working directory
# - EXPOSE <port>           → declare port for container
# - USER <username>         → run container as specific user



# How to Run a Dockerfile
# 1. Navigate to directory containing Dockerfile
# 2. Build image from Dockerfile:
	docker build -t <image_name>:<tag> .
# Example:
	docker build -t my-app:1.0 .

# 3. Run container from built image:
	docker run -dit --name <container_name> -p 8080:80 <image_name>:<tag>
# Example:
	docker run -dit --name my-app-container -p 8080:80 my-app:1.0






# 5. Dockerfile Guide

# 5.1 Basic Structure of a Dockerfile

# - Dockerfile is a text file that contains instructions to build a Docker image
# - No file extension; simply named "Dockerfile"

# - Typical structure:

#   FROM <base_image>
#   RUN <commands>
#   COPY/ADD <src> <dest>
#   ENV <key>=<value>
#   WORKDIR <dir>
#   EXPOSE <port>
#   CMD/ENTRYPOINT <command>



# Example:
# -------------------
# FROM ubuntu:20.04
# RUN apt-get update && apt-get install -y python3
# WORKDIR /app
# COPY . /app
# EXPOSE 8080
# CMD ["python3", "app.py"]
# -------------------


# 5.2 Common Instructions
# - FROM <image>            → sets base image
# - RUN <command>           → executes commands during image build
# - COPY <src> <dest>       → copy files/folders into image
# - ADD <src> <dest>        → copy files/folders and auto-extract archives
# - CMD ["executable"]      → default command when container runs
# - ENTRYPOINT ["executable"] → sets the main executable



# 5.3 Additional Useful Instructions
# - EXPOSE <port>           → declares port the container listens on
# - ENV <key>=<value>       → sets environment variable
# - WORKDIR <dir>           → sets working directory for subsequent instructions
# - VOLUME <path>           → defines a mount point for persistent data



# 5.4 Multi-Stage Builds
# - Allows using multiple FROM statements to reduce final image size
# - Useful for building code in one stage and copying only necessary artifacts to final image

# Example:
# -------------------
# FROM golang:1.20 as builder
# WORKDIR /app
# COPY . .
# RUN go build -o myapp
#
# FROM alpine:latest
# WORKDIR /app
# COPY --from=builder /app/myapp .
# CMD ["./myapp"]
# -------------------



# 5.5 Best Practices for Dockerfile
# 1. Use official base images when possible
# 2. Minimize number of layers (combine RUN commands)
# 3. Order instructions to maximize caching
# 4. Avoid installing unnecessary packages
# 5. Use .dockerignore to reduce build context size
# 6. Always specify versions for dependencies






# Docker Containers & Dockerfile - Extended Guide

# Note: We can create a Docker image from a running or stopped container using `docker commit`.

# 1. Create an image from a running container
# Syntax:
docker commit <container_name_or_id> <new_image_name>:<tag>
# Example:
docker commit my-running-container my-custom-image:1.0

# 2. Dockerfile → Image → Container → New Image Diagram

           +----------------+
           |   Dockerfile   |
           +--------+-------+
                    |
                    v
           +----------------+
           |     Image      |
           +--------+-------+
                    |
                    v
           +----------------+
           |   Container    |
           +--------+-------+
                    |
                    v
           +----------------+
           |  New Image     |
           +----------------+

# Explanation:
# - Dockerfile builds an image
# - Image runs as a container
# - Container changes can be saved as a new image

# 3. Push Image to Docker Hub
# Step 1: Login to Docker Hub
docker login
# Enter Docker Hub username and password

# Step 2: Tag the image with your repository
docker tag <image_name>:<tag> <dockerhub_username>/<repository>:<tag>
# Example:
docker tag my-custom-image:1.0 akhil/my-custom-image:1.0

# Step 3: Push the image to Docker Hub
docker push <dockerhub_username>/<repository>:<tag>
# Example:
docker push akhil/my-custom-image:1.0

# Step 4: Pull the image from Docker Hub (to verify or use on another machine)
docker pull <dockerhub_username>/<repository>:<tag>
# Example:
docker pull akhil/my-custom-image:1.0






# Deploying an Application Using Docker - Simplified Flow

1. **Clone the Code**
   - Get the application source code from repository
   - Example:
     git clone <repository_url>

2. **Build the Application (if required)**
   - Compile/build the app depending on the language/framework
   - Example: mvn package, npm install, pip install -r requirements.txt

3. **Create a Dockerfile**
   - Define base image, dependencies, copy code, expose ports, set CMD/ENTRYPOINT

4. **Build Docker Image**
   - Navigate to directory with Dockerfile
   - Command:
     docker build -t <image_name>:<tag> .
   - Example:
     docker build -t my-app:1.0 .

5. **Run Container**
   - Run container from image
   - Map ports and use detached mode:
     docker run -dit --name <container_name> -p <host_port>:<container_port> <image_name>:<tag>
   - Example:
     docker run -dit --name my-app-container -p 8080:80 my-app:1.0

6. **Push Image to Docker Hub (Optional)**
   - Login: docker login
   - Tag image: docker tag <image_name>:<tag> <dockerhub_user>/<repo>:<tag>
   - Push: docker push <dockerhub_user>/<repo>:<tag>





# Docker Deployment Flow Diagram (Text-Editor Friendly)

  +----------------+
  |  Clone Code    |
  +--------+-------+
           |
           v
  +----------------+
  |   Build App    |
  +--------+-------+
           |
           v
  +----------------+
  |   Dockerfile   |
  +--------+-------+
           |
           v
  +----------------+
  |   Docker Image |
  +--------+-------+
           |
           v
  +----------------+
  |   Container    |
  +--------+-------+
           |
           v
  +----------------+
  |  Docker Hub    |
  +----------------+



Clone Code → Build → Dockerfile → Docker Image → Container → Docker Hub









# Deploying an Application Using Docker and Jenkins


# 1. Clone the Code (Jenkins will do this automatically)
# Jenkins pulls the application from GitHub/GitLab/Bitbucket
# Example Git URL used inside Jenkins job:
# https://github.com/user/repository.git


# 2. Jenkins Pipeline Starts
# Jenkinsfile or Freestyle Job triggers stages:
# - Pull code
# - Build application
# - Build Docker image
# - Run tests (optional)
# - Push Docker image
# - Deploy container


# 3. Build the Application (Jenkins stage)
# Example commands inside Jenkins:
# mvn package
# npm install
# pip install -r requirements.txt


# 4. Dockerfile
# Dockerfile should be present in repo
# Jenkins will use it to build Docker image


# 5. Jenkins Builds Docker Image
# Example commands in Jenkins pipeline:
# docker build -t <image_name>:<tag> .

# Example:
# docker build -t my-app:1.0 .


# 6. Jenkins Runs Docker Container
# Jenkins deploys the application using Docker:
docker run -dit --name my-app-container -p 8080:80 my-app:1.0


# 7. Jenkins Pushes Docker Image to Docker Hub (Optional)
docker login -u <dockerhub_user> -p <password>
docker tag my-app:1.0 <dockerhub_user>/<repo>:1.0
docker push <dockerhub_user>/<repo>:1.0


# 8. Deployment to Servers (Production / Staging)
# On the target server, Jenkins or script:
docker pull <dockerhub_user>/<repo>:1.0
docker run -dit -p 8080:80 <dockerhub_user>/<repo>:1.0







# Deployment Flow Diagram (Docker + Jenkins)

      +----------------+
      |    Developer   |
      |   Push Code    |
      +--------+-------+
               |
               v
      +----------------+
      |    Git Repo    |
      +--------+-------+
               |
               v
      +----------------+
      |    Jenkins     |
      |  CI Pipeline   |
      +--------+-------+
               |
    +----------+-----------+
    |                      |
    v                      v
+-----------+       +--------------+
|  Build    |       |  Dockerfile  |
|  App      | ----> |  Build Image |
+-----------+       +--------------+
                          |
                          v
                  +----------------+
                  |   Docker Image |
                  +--------+-------+
                          |
                          v
                +--------------------+
                | Run Container      |
                | Deploy App         |
                +--------------------+
                          |
                          v
                +--------------------+
                | Push to Docker Hub |
                +--------------------+




# Jenkins Pipeline Example (Declarative) for Docker Deployment

pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/user/repository.git'
            }
        }

        stage('Build App') {
            steps {
                sh 'mvn package'     # or npm install / python build
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app:1.0 .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -dit --name my-app-container -p 8080:80 my-app:1.0'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker login -u $USER -p $PASS'
                sh 'docker tag my-app:1.0 $USER/my-app:1.0'
                sh 'docker push $USER/my-app:1.0'
            }
        }
    }
}








# 8. Docker Compose

# FIRST NOTE:
# Docker Compose is used for:
# 1. Creating and managing MULTIPLE CONTAINERS
# 2. Building MULTIPLE IMAGES using build context in compose file
# 3. Running multi-container applications with one command

# -----------------------------------------
# 8.1 What is Docker Compose?
# -----------------------------------------
# - A tool to define and run multi-container Docker applications.
# - Uses a YAML file (docker-compose.yml)
# - With one command (docker compose up) → it creates networks, volumes, images, and containers.

# -----------------------------------------
# 8.2 docker-compose.yml File Format
# -----------------------------------------
# Basic Syntax:
# --------------------
# version: "3"
# services:
#   service_name:
#       image: <image_name> OR build: <path>
#       ports:
#       - "<host_port>:<container_port>"
#       environment:
#       - KEY=value
#       depends_on:
#       - another_service
# volumes:
#   volume_name:
# networks:
#   network_name:
# --------------------

# Example:
# --------------------
# version: "3"
# services:
#   web:
#     build: .
#     ports:
#       - "8080:80"
#     depends_on:
#       - db
#
#   db:
#     image: mysql:8
#     environment:
#       - MYSQL_ROOT_PASSWORD=pass123
# --------------------


# -----------------------------------------
# 8.3 Running Multi-Container Applications
# -----------------------------------------
docker compose up
docker compose up -d   # detached mode
docker compose down

# -----------------------------------------
# 8.4 Environment Variables in Compose
# -----------------------------------------
# Syntax:
# --------------------
# environment:
#   - KEY=value
# --------------------

# Example:
environment:
  - MYSQL_USER=root
  - MYSQL_PASSWORD=test123

# You can also use a separate .env file (KEY=value format)

# -----------------------------------------
# 8.5 Networking in Compose
# -----------------------------------------
# - All services automatically join a default network.
# - Services communicate using service names.

# Example:
#   web connects to db using:
#   db:3306

# Manual network:
# --------------------
networks:
  custom-net:
# --------------------

# Assign service to network:
# --------------------
services:
  web:
    networks:
      - custom-net
# --------------------

# -----------------------------------------
# 8.6 Scaling Services
# -----------------------------------------
docker compose up --scale <service>=<count>
# Example:
docker compose up --scale web=3 -d

# -----------------------------------------
# 8.7 Common Docker Compose Commands
# -----------------------------------------
docker compose up                 # Start all services
docker compose up -d              # Detached
docker compose down               # Stop & remove containers
docker compose ps                 # List containers
docker compose logs               # View logs
docker compose build              # Build images
docker compose restart            # Restart services
docker compose stop               # Stop services
docker compose rm                 # Remove stopped containers

# -----------------------------------------
# ADDITION: SYNTAX FOR CREATING IMAGES USING COMPOSE
# -----------------------------------------
# Compose can create MULTIPLE IMAGES using 'build:' key

# Syntax:
# --------------------
services:
  service_name:
    build:
      context: <path_of_source_code>
      dockerfile: <Dockerfile_name>
      args:
        KEY: value
    image: <image_name>:<tag>
# --------------------

# Example:
# --------------------
version: "3"
services:
  app:
    build:
      context: ./app
      dockerfile: Dockerfile
    image: myapp:v1
    ports:
      - "8080:80"

  worker:
    build:
      context: ./worker
    image: worker-image:v2
# --------------------
# This example builds TWO images (myapp:v1 and worker-image:v2)
# from two different folders using one compose file.






# Docker Volumes & Storage

## 📌 6.0 What is a Docker Volume? (Definition & Key Points)
- Docker Volume is a **persistent storage mechanism** for containers.
- Data remains **even after the container is deleted**.
- Preferred over bind mounts (Docker‑managed, secure, portable).
- Allows **data sharing** between multiple containers.
- Ideal for **databases, logs, configurations, backups**.
- Keeps container images **small & stateless**.
- Useful for both **development and production** setups.

------------------------------------------------------------

## 📌 6.1 Types of Docker Volumes

### **1. Anonymous Volume**
- Auto‑created when container runs.
- No name → hard to reuse or manage.
```
docker run -v /app/data nginx
```

### **2. Named Volume**
- Manually created and easy to identify, reuse.
```
docker volume create myvol
```

### **3. Host (Bind) Mount**
- Maps a folder from host → container.
- Most useful during development.
```
docker run -v /host/path:/app/data nginx
```

------------------------------------------------------------

## 📌 6.2 Creating & Managing Volumes
### **Commands**
```
docker volume create myvol      # Create volume

docker volume ls               # List volumes

docker volume inspect myvol    # Inspect volume

docker volume rm myvol         # Remove volume

docker volume prune            # Remove all unused volumes
```

------------------------------------------------------------

## 📌 6.3 Mounting Volumes (Two Methods)

### ✅ Method 1: Mount Using Docker Run Command

#### **Named Volume**
```
docker run -d -v myvol:/app/data nginx
```

#### **Anonymous Volume**
```
docker run -d -v /app/data nginx
```

#### **Host (Bind) Mount**
```
docker run -d -v /home/user/project:/app nginx
```

---

### ✅ Method 2: Mount Using Dockerfile
#### **Using VOLUME Instruction**
```
VOLUME ["/app/data"]
```
- Automatically creates an **anonymous volume**.
- Good for making a directory always persistent.

#### **Example Dockerfile**
```
FROM alpine
WORKDIR /app
VOLUME ["/app/data"]
CMD ["sh"]
```

------------------------------------------------------------

## 📌 6.4 Backing Up & Restoring Volumes

### **Backup a Volume**
```
docker run --rm -v myvol:/data -v $(pwd):/backup \
  alpine tar czvf /backup/myvol_backup.tar.gz /data
```

### **Restore a Volume**
```
docker run --rm -v myvol:/data -v $(pwd):/backup \
  alpine tar xzvf /backup/myvol_backup.tar.gz -C /
```

------------------------------------------------------------

## 📌 Diagram – How Docker Volumes Work
```
+-----------------------+        +------------------------+
|   Docker Container    | <----> |      Volume Storage    |
|  (/app/data)          |        |   (Managed by Docker)  |
+-----------------------+        +------------------------+
             ^                            ^
             |                            |
 Named Volume or Host Mount     Persistent Across Restarts
```

------------------------------------------------------------

## 📌 EXTRA: When Should You Use Volumes?
- When you need **persistent** application data.
- When multiple containers need access to the same data.
- For production DBs like **MySQL, MongoDB, PostgreSQL**.
- To avoid losing logs after container deletion.
- For backup/restore and migration tasks.

------------------------------------------------------------

## 📌 EXTRA: Why Volumes Are Better than Bind Mounts?
| Feature | Volumes | Bind Mounts |
|--------|---------|--------------|
| Docker‑managed | ✔ | ✖ |
| Secure | ✔ | ✖ (depends on host) |
| Portable | ✔ | ✖ |
| Works anywhere | ✔ | Requires same host path |
| Best for production | ✔ | ✖ |

------------------------------------------------------------




## 📌 6.5 Connecting Multiple Containers to a Single Volume (New Content)


### Step 1: Create a Named Volume
```
docker volume create sharedvol
```


### Step 2: Start First Container with Volume
```
docker run -d --name container1 -v sharedvol:/app/data alpine sh -c "while true; do echo hello > /app/data/hello.txt; sleep 5; done"
```


### Step 3: Start Second Container Using Same Volume
```
docker run -d --name container2 -v sharedvol:/app/data alpine sh -c "tail -f /app/data/hello.txt"
```


### Explanation:
- `container1` writes to `/app/data`.
- `container2` reads from the **same named volume**.
- This allows **real-time data sharing** between multiple containers.


### Diagram – Connecting Containers via Volume
```
+-------------------+ 	     +-------------------+ 	  +-------------------+
| Container 1	    | 	     | Docker Volume 	 | 	  | Container 2       |
| (/app/data) 	    | <----> | sharedvol 	 | <----> | (/app/data)       |
+-------------------+ 	     +-------------------+ 	  +-------------------+
```







# Docker Networking

## 7.1 Docker Network Types

### 1. Bridge Network

* Default network for standalone containers.
* Containers can communicate within the same bridge network.
* Isolated from the host network.
* Example: docker network create mybridge

  * Purpose: Create a bridge network to connect multiple containers isolated from host.

### 2. Host Network

* Container shares host network stack.
* No isolation; container uses host IP.
* Faster networking but less secure.
* Example: docker run --network host nginx

  * Purpose: Run container using host network directly.

### 3. None Network

* Container has no network.
* Used for completely isolated containers.
* Example: docker run --network none alpine

  * Purpose: Run container without network access.

### 4. Overlay Network

* Used for multi-host container communication.
* Requires Docker Swarm.
* Connects containers across different Docker hosts.
* Example: docker network create -d overlay myoverlay

  * Purpose: Enable multi-host container communication using Swarm.

### 5. Macvlan Network

* Assigns a MAC address to container.
* Container appears as a physical device on the network.
* Useful for legacy apps needing direct L2 network access.
* Example: docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 mymacvlan

  * Purpose: Make container appear as separate device on network.

---

## 7.2 Creating Custom Networks

* Create network: docker network create --driver bridge mycustomnetwork

  * Purpose: Create custom bridge network for containers.
* List networks: docker network ls

  * Purpose: Show all Docker networks.
* Inspect network: docker network inspect mycustomnetwork

  * Purpose: Get details of network including connected containers.
* Remove network: docker network rm mycustomnetwork

  * Purpose: Delete unused network.

---

## 7.3 Connecting Containers

* Connect container to network: docker network connect mycustomnetwork container_name

  * Purpose: Attach container to an existing network.
* Disconnect container: docker network disconnect mycustomnetwork container_name

  * Purpose: Detach container from network.
* Run container on custom network: docker run -d --network mycustomnetwork nginx

  * Purpose: Start container directly attached to a specific network.

---

## 7.4 Port Mapping

* Maps host port to container port: <host_port>:<container_port>
* Example: docker run -d -p 8080:80 nginx

  * Purpose: Access container service via host port.
* Bind to localhost only: docker run -d -p 127.0.0.1:8080:80 nginx

  * Purpose: Restrict container access to localhost.

---

## 7.5 DNS inside Docker

* Docker provides internal DNS for containers.
* Containers can reach each other by container name.
* Works automatically on user-defined networks.
* Useful for service discovery in multi-container setups.

  * Purpose: Enable containers to communicate by name instead of IP.

---

## Useful Docker Networking Commands

* docker network create --driver bridge mynetwork  # Create custom network
* docker network ls                               # List all networks
* docker network inspect mynetwork               # Inspect network details
* docker network rm mynetwork                    # Remove network
* docker network connect mynetwork container    # Connect container to network
* docker network disconnect mynetwork container # Disconnect container from network
* docker run -d --network mynetwork nginx       # Run container on a specific network




# Multi-Stage Dockerfile Notes

# 1. Definition
# A Multi-stage Dockerfile uses multiple FROM instructions, allowing you to build
# and package applications efficiently with smaller final images.

# 2. Main Points
# - Reduces final image size
# - Keeps build tools out of the final image
# - Each stage can have a different base image
# - Final stage contains only required app files
# - Improves security and performance

# 3. Advantages
# ✔ Smaller & cleaner images
# ✔ Faster deployments
# ✔ Same Dockerfile for build & run
# ✔ No build tools like gcc, npm in final image
# ✔ Reduced attack surface

# 4. Syntax Example
# --------------------------------------------------------
# FROM <base-image> AS builder
# RUN build commands
#
# FROM <runtime-image>
# COPY --from=builder <source> <destination>
# CMD ["executable"]
# --------------------------------------------------------


# 5. Full Example (Node.js App)
# --------------------------------------------------------
# Stage 1: Build Stage
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Production Stage
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
# --------------------------------------------------------


# 6. Go Application Example
# --------------------------------------------------------
# Stage 1 - Build
FROM golang:1.20 AS builder
WORKDIR /src
COPY . .
RUN go build -o myapp

# Stage 2 - Final Image
FROM alpine
COPY --from=builder /src/myapp /usr/local/bin/myapp
CMD ["myapp"]
# --------------------------------------------------------


# 7. Commands Used With Multi-Stage Builds
# Build Image
# docker build -t myapp .

# Build With Specific Target Stage (debugging)
# docker build --target builder -t myapp-builder .

# List Layers
# docker history myapp

# Run Container
# docker run -p 8080:80 myapp



# 8. Diagram — Multi-Stage Build Flow
# --------------------------------------------------------
# +------------------------+     +------------------------+
# |   Stage 1: Builder     |     |   Stage 2: Final Image |
# |  (Node/Golang/etc)     |     |    (Nginx/Alpine/etc)  |
# +------------------------+     +------------------------+
# | build tools installed  |     | lightweight runtime    |
# | compilers              | --> | only required output   |
# | dependencies           |     | copied from builder    |
# +------------------------+     +------------------------+


```
