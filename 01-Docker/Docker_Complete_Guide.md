# 📖 Docker Complete Guide
> *Converted from `Docker Complete Guide.pdf` for high-readability on GitHub.*

---
## Page 1

Docker Complete Guide
1. Docker Overview
Docker is a platform to develop, ship, and run applications in containers. - Containers are lightweight,
portable, and isolated. - Docker uses images to create containers.
2. Docker Installation & Version Check
Install Docker: sudo yum install docker  or sudo apt install docker.io
Start Docker: sudo systemctl start docker
Enable on boot: sudo systemctl enable docker
Check Version: 
docker --version
docker version
docker info
3. Docker Images
Commands:
Command Description Example
docker pull <image> Pull image from
registry docker pull nginx:latest
docker build -t <name>:<tag> 
<path>
Build image from
Dockerfile docker build -t myapp:v2 .
docker images List local images
docker rmi <image> Remove image docker rmi myapp:v2
docker tag <source> 
<target> Tag image docker tag myapp:v2 myrepo/
myapp:v2
docker push <image> Push image to
registry docker push myrepo/myapp:v2
docker history <image> Show image layers
docker inspect <image> Detailed image info
• 
• 
• 
• 
1

## Page 2

Command Description Example
docker save -o <file.tar> 
<image> Save image to tar docker save -o nginx.tar 
nginx:latest
docker load -i <file.tar> Load image from tar
docker image prune Remove dangling
images
4. Docker Containers
Commands:
Command Description Example
docker run <image> Run container docker run ubuntu
docker run -it <image> Interactive shell docker run -it ubuntu 
bash
docker run -d -p 
<host>:<container> <image>
Detached with port
mapping
docker ps List running containers
docker ps -a List all containers
docker stop <container> Stop container
docker start <container> Start container
docker restart <container> Restart container
docker rm <container> Remove container
docker rm -f <container> Force remove running
container
docker logs <container> Show logs
docker logs -f <container> Follow logs in real-time
docker exec -it <container> bash Access shell inside
container
docker attach <container> Attach to container
stdin/stdout
docker inspect <container> Detailed container info
2

## Page 3

Command Description Example
docker diff <container> Show file system
changes
docker cp <container>:<path> 
<host> Copy from container docker cp cont:/app/
file.txt ./
docker commit <container> <image> Save container as
image
docker update --cpus 2 --memory 1g 
<container>
Update container
resource limits
5. Docker Volumes
Commands:
Command Description Example
docker volume create <name> Create a volume
docker volume ls List volumes
docker volume inspect <name> Inspect volume
docker volume rm <name> Remove volume
docker run -v <volume>:<path> Mount volume
docker run -v <host_path>:<container_path> Bind mount host directory
docker volume prune Remove all unused volumes
6. Docker Networks
Commands:
Command Description Example
docker network ls List networks
docker network create <name> Create network
docker network inspect <name> Inspect network
docker network rm <name> Remove network
docker run --network <net> <image> Connect container to network
3

## Page 4

Command Description Example
docker network connect <net> <container> Connect existing container
docker network disconnect <net> 
<container>
Disconnect container from
network
docker network prune Remove unused networks
7. Docker Compose
Commands:
Command Description Example
docker-compose up Start all services
docker-compose up -d Detached mode
docker-compose down Stop & remove containers
docker-compose build Build services
docker-compose logs Show logs
docker-compose logs -f Follow logs
docker-compose ps List running services
docker-compose exec <service> bash Access shell in service container
docker-compose restart Restart all containers
docker-compose rm Remove stopped services
8. Docker System Management
docker system df  → Disk usage
docker system prune  → Remove unused containers, images, networks, cache
docker system prune -a  → Remove all unused images
docker stats  → Live resource usage
docker top <container>  → Processes inside container
docker events  → Live events stream
• 
• 
• 
• 
• 
• 
4

## Page 5

9. Dockerfile Instructions
Instruction Description
FROM Base image
RUN Run commands during build
COPY Copy files
ADD Copy files/URLs
WORKDIR Set working directory
ENV Set environment variables
EXPOSE Open container ports
CMD Default command
ENTRYPOINT Container entry
VOLUME Declare mount point
USER Set user
LABEL Metadata
ARG Build-time variable
10. Docker Advanced Options
docker run --rm  → Remove container after exit
docker run --privileged  → Full host privileges
docker run --cpus <num>  → CPU limit
docker run --memory <size>  → Memory limit
docker run --restart <policy>  → Restart automatically
docker network create --driver overlay <name>  → Swarm overlay network
docker swarm init  → Initialize swarm
docker service create  → Deploy service in swarm
11. Docker Interview Q&A
Q1: Difference between image and container? A: Image is a template; container is a running instance.
Q2: Difference between Docker and VM? A: Docker shares OS kernel, lighter; VM has full OS.
Q3: How do you persist data in Docker? A: Using volumes or bind mounts.
• 
• 
• 
• 
• 
• 
• 
• 
5

## Page 6

Q4: What is Docker Compose? A: Tool to define multi-container apps using YAML.
Q5: How to reduce image size? A: Use smaller base image, clean cache, multi-stage builds.
Q6: Difference  between  CMD  and  ENTRYPOINT ?  A: CMD  sets  default  args;  ENTRYPOINT  defines
executable.
Q7: How do you link containers? A: Using Docker networks or --link  (deprecated).
Q8: How to check container logs? A: docker logs <container>
Q9: How to stop and remove all containers? A: docker stop $(docker ps -aq)  then docker rm $
(docker ps -aq)
Q10: What is a multi-stage build? A: Build smaller final images by using intermediate stages.
End of Docker Complete Guide
6

