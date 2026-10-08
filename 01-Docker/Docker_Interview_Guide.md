# 📖 Docker Interview Guide
> *Converted from `Docker Interview Guide.pdf` for high-readability on GitHub.*

---
## Page 1

Complete Docker Interview Guide
1. Basics of Docker
Q1. What is Docker?  - Docker is an open-source platform for automating the deployment of applications
inside lightweight, portable containers.
Q2. Why use Docker?  - Provides consistent environments across development, testing, and production -
Faster deployment - Lightweight and resource-efficient compared to virtual machines - Application isolation
and easier scaling
Q3.  Difference  between  Docker  and  Virtual  Machine |  Feature  |  Docker  |  Virtual  Machine  |
|---------|--------|----------------| | OS virtualization | Shares host OS kernel | Full OS virtualization | | Resource
usage | Lightweight | Heavy | | Boot time | Seconds | Minutes | | Isolation | Application-level | OS-level |
| Performance | High | Medium |
2. Docker Architecture
Docker Engine: Core component that runs containers
Docker Client: CLI tool to interact with Docker
Docker Daemon: Background service running on host
Docker Image: Read-only template for container
Docker Container: Running instance of an image
Docker Registry: Storage for Docker images (Docker Hub, Nexus, private registry)
3. Basic Docker Commands
Command Description
docker --version Check Docker version
docker pull <image> Pull image from Docker Hub
docker images List images
docker run -it <image> Run a container interactively
docker ps List running containers
docker ps -a List all containers
docker stop <container> Stop container
• 
• 
• 
• 
• 
• 
1

## Page 2

Command Description
docker start <container> Start container
docker rm <container> Remove container
docker rmi <image> Remove image
docker logs <container> View container logs
docker exec -it <container> bash Access container shell
4. Docker Image & Container Lifecycle
Pull image: docker pull nginx
Run container: docker run -d -p 8080:80 --name mynginx nginx
Check container: docker ps
Stop container: docker stop mynginx
Remove container: docker rm mynginx
Remove image: docker rmi nginx
5. Dockerfile & Custom Images
Example Dockerfile:
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y python3
COPY app.py /app/app.py
WORKDIR /app
CMD ["python3", "app.py"]
Build image: docker build -t mypythonapp .  Run container: docker run -d -p 5000:5000 
mypythonapp
6. Docker Compose (Multi-container)
Example docker-compose.yml:
version: '3'
services:
1. 
2. 
3. 
4. 
5. 
6. 
2

## Page 3

web:
image: nginx
ports:
- "8080:80"
db:
image: mysql
environment:
MYSQL_ROOT_PASSWORD: root
Start: docker-compose up -d  Stop: docker-compose down
7. Docker Volumes
Persist data outside containers 
docker run -d -v /host/data:/container/data nginx
8. Docker Networking
Bridge, Host, Overlay networks
Commands: 
docker network ls
docker network create mynetwork
docker network connect mynetwork mycontainer
9. Docker Registry (Docker Hub/Nexus)
Push image: docker login , docker tag mypythonapp username/mypythonapp:latest , 
docker push username/mypythonapp:latest
Pull image: docker pull username/mypythonapp:latest
Private registry like Nexus can also be used
• 
• 
• 
• 
• 
• 
3

## Page 4

10. Common Docker Interview Questions &
Answers
Q1. What is Docker and why use it?  - Open-source platform to package applications in containers for
consistency, portability, and isolation.
Q2. Difference between Docker and VM? - Docker shares host OS and is lightweight; VM virtualizes full OS
and consumes more resources.
Q3. Explain Docker architecture.  - Docker Client interacts with Docker Daemon which runs containers
from Images; images stored in Registries.
Q4.  How  do  you  create  a  Docker  image?  -  Use  a  Dockerfile  with  instructions,  then  run
docker build -t <imagename> .
Q5. How to run and stop a container?  - Run:  docker run -it <image>  - Stop:  docker stop 
<container>
Q6. What is a Dockerfile? Provide example.  - Script containing instructions to build Docker images (see
example above).
Q7.  What  is  Docker  Compose? -  Tool  to  define  and  run  multi-container  Docker  applications  using
docker-compose.yml
Q8. How do you persist data in Docker containers? - Use Docker volumes or bind mounts
Q9. How to push and pull images from Docker Hub or Nexus?  - Push: docker login , docker tag , 
docker push  - Pull: docker pull
Q10. Explain Docker networking and types of networks.  - Bridge (default), Host, Overlay, and Macvlan
networks for container communication
Q11. Difference between docker run  and docker exec ? - docker run  creates and starts a new
container; docker exec  runs a command inside an existing container
Q12. How to view logs and access shell inside a container? - Logs: docker logs <container>  - Shell:
docker exec -it <container> bash
This guide covers Docker basics, commands, image/container lifecycle, Dockerfile, Compose, volumes,
networking, registry, and answers to common interview questions for Docker preparation.
4

