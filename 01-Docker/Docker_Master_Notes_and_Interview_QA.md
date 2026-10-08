# 📖 Docker_Master_Notes_and_Interview_QA
> *Converted from `Docker_Master_Notes_and_Interview_QA.pdf` for high-readability on GitHub.*

---
## Page 1

■ Docker Master Notes & Interview Q&A;
Complete Intermediate + Advanced Notes with Syntax, Examples
& 40+ Interview Questions
■ PART 1: Docker Complete Notes
1■■ What is Docker?
Docker is a containerization platform that packages applications and dependencies into lightweight,
portable containers.
2■■ Docker Architecture
- Docker Client: Sends commands to Docker Daemon.
- Docker Daemon: Manages images, containers, networks, volumes.
- Docker Registry: Stores and distributes images (e.g., Docker Hub).
- Docker Images: Read-only templates used to create containers.
- Docker Containers: Running instances of Docker images.
-------------------------------------------------------
■ BASIC DOCKER COMMANDS
Syntax: docker [COMMAND] [OPTIONS]
Examples and Explanation:
1. Check Docker version
Syntax: docker --version
Example: docker --version
→ Displays installed Docker version.
2. List running containers
Syntax: docker ps
Example: docker ps
→ Shows currently running containers.
3. List all containers (including stopped)
Syntax: docker ps -a
Example: docker ps -a
→ Lists all created containers with their status.
4. List images
Syntax: docker images
Example: docker images
→ Displays available images locally.
5. Pull an image from Docker Hub
Syntax: docker pull image_name:tag
Example: docker pull nginx:latest

## Page 2

→ Downloads the latest NGINX image from Docker Hub.
-------------------------------------------------------
■ CONTAINER CREATION & MANAGEMENT
1. Run a simple container
Syntax: docker run image_name
Example: docker run ubuntu
→ Creates and starts a container using Ubuntu image.
2. Run interactively with terminal
Syntax: docker run -it image_name
Example: docker run -it ubuntu bash
→ Starts an Ubuntu container and opens a shell.
3. Run in detached mode
Syntax: docker run -d image_name
Example: docker run -d nginx
→ Runs container in background.
4. Run with name and port mapping
Syntax: docker run -itd --name container_name -p host_port:container_port image_name:tag
Example: docker run -itd --name webapp -p 8080:80 nginx
→ Runs nginx and maps host port 8080 to container port 80.
5. Start/Stop/Restart containers
docker start container_name
docker stop container_name
docker restart container_name
6. Access running container shell
Syntax: docker exec -it container_name bash
7. View container logs
Syntax: docker logs container_name
8. Copy files
docker cp container_name:/path/in/container /host/path
docker cp /host/path container_name:/path/in/container
-------------------------------------------------------
■ IMAGE MANAGEMENT
1. Build image from Dockerfile
Syntax: docker build -t image_name:tag .
Example: docker build -t myapp:v1 .
2. Tag an image
Syntax: docker tag image_name:tag username/repo:tag
3. Push image to Docker Hub
docker login
docker push username/repo:tag
4. Remove image or container
docker rm container_id

## Page 3

docker rmi image_id
-------------------------------------------------------
■ DOCKERFILE EXAMPLE
FROM openjdk:11
WORKDIR /app
COPY target/myweb.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
→ Build and Run:
docker build -t myweb:v1 .
docker run -itd -p 8080:8080 myweb:v1
-------------------------------------------------------
■ DOCKER VOLUMES
1. Create a volume
docker volume create myvol
2. List volumes
docker volume ls
3. Use volume in container
docker run -itd -v myvol:/data ubuntu
4. Bind host directory
docker run -itd -v /home/user/data:/var/lib/mysql mysql
-------------------------------------------------------
■ DOCKER NETWORKS
1. List networks
docker network ls
2. Create custom network
docker network create mynet
3. Run container on that network
docker run -itd --name cont1 --network mynet nginx
4. Connect existing container
docker network connect mynet cont2
-------------------------------------------------------
■■ DOCKER COMPOSE
docker-compose.yml Example:
version: '3'
services:
web:
image: nginx
ports:
- "8080:80"

## Page 4

db:
image: mysql:5.7
environment:
MYSQL_ROOT_PASSWORD: root123
MYSQL_DATABASE: mydb
Commands:
docker-compose up -d
docker-compose down
docker-compose ps
docker-compose logs
-------------------------------------------------------
■ DOCKER SWARM (Advanced)
1. Initialize Swarm
docker swarm init
2. Add worker node
docker swarm join --token
3. Deploy stack
docker stack deploy -c docker-compose.yml mystack
4. List services
docker service ls
-------------------------------------------------------
■ TROUBLESHOOTING COMMANDS
docker logs container_name
docker inspect container_name
docker exec -it container_name bash
docker ps -a
docker start -a container_name
docker system prune -a
-------------------------------------------------------
■ BEST PRACTICES
- Use minimal base images (e.g., alpine).
- Keep Dockerfile simple and layer-efficient.
- Use `.dockerignore` file.
- Tag images properly (v1, latest, etc.).
- Clean unused containers regularly.

## Page 5

■ PART 2: Docker Interview Questions & Answers
1. What is Docker?
→ Docker is a platform for developing, shipping, and running applications inside containers.
2. Difference between container and virtual machine?
→ VM virtualizes hardware; container virtualizes OS. Containers are lightweight and faster.
3. What is a Docker image?
→ A read-only template used to create containers.
4. What is a Docker container?
→ A running instance of a Docker image.
5. What is Docker Hub?
→ A public registry where images are stored and shared.
6. Difference between docker run, start, and exec?
→ run = create + start, start = start stopped container, exec = run command in running container.
7. What is the default Docker network?
→ bridge network.
8. What is port mapping in Docker?
→ Links container port to host port using -p option (e.g., -p 8080:80).
9. How to share data between containers?
→ Use Docker volumes or --volumes-from option.
10. What is Dockerfile?
→ A text file with instructions to build an image.
11. What are layers in Docker image?
→ Each command in Dockerfile creates a new layer to optimize builds.
12. Explain Docker Compose.
→ A tool to define and run multi-container applications using docker-compose.yml.
13. Explain Docker Swarm.
→ Docker’s native clustering and orchestration tool.
14. Difference between CMD and ENTRYPOINT?
→ CMD provides default args; ENTRYPOINT defines executable.
15. What is COPY vs ADD in Dockerfile?
→ COPY only copies local files; ADD can also download from URLs or extract archives.
16. How to check logs of a container?
→ docker logs container_name
17. How to see container’s IP address?
→ docker inspect container_name | grep IPAddress
18. How to clean up unused resources?

## Page 6

→ docker system prune -a
19. How to copy file from host to container?
→ docker cp /host/path container:/path
20. How to list all images?
→ docker images
21. What is difference between -d, -it, -itd flags?
→ -d = detached, -it = interactive terminal, -itd = both (interactive + detached).
22. Explain docker volume usage.
→ Volumes store persistent data independent of container lifecycle.
23. How to persist data after container deletion?
→ Use Docker volumes.
24. How to connect containers together?
→ Using Docker networks.
25. Explain Docker architecture components.
→ Client, Daemon, Images, Containers, Registry.
26. How to check resource usage of containers?
→ docker stats
27. How to export and import image?
→ docker save -o file.tar image_name:tag
docker load -i file.tar
28. What happens when container exits?
→ It stops, but data remains unless removed.
29. How to run multiple containers on same image?
→ Run docker run command multiple times with different names/ports.
30. How to remove all stopped containers?
→ docker container prune
31. What is difference between docker pause and stop?
→ pause = freezes processes, stop = stops processes gracefully.
32. Can containers communicate without exposing ports?
→ Yes, if they’re on same user-defined network.
33. Explain docker commit.
→ Creates a new image from a container’s changes.
34. What are Dangling Images?
→ Unused image layers not tagged or associated with containers.
35. Difference between docker attach and exec?
→ attach reconnects to container’s main process, exec starts a new process.
36. What is ENTRYPOINT used for?
→ Define the executable to run when container starts.

## Page 7

37. Can we use multiple FROM statements?
→ Yes, for multi-stage builds.
38. How to update running container?
→ Commit changes or rebuild image and redeploy.
39. How to see environment variables of container?
→ docker inspect container | grep Env
40. How to check Docker version and server info?
→ docker version
docker info

