# 📖 Docker_Complete_Notes_with_Commands
> *Converted from `Docker_Complete_Notes_with_Commands.pdf` for high-readability on GitHub.*

---
## Page 1

■ Docker — Complete Notes with Commands
1■■ What is Docker?
Docker is a containerization platform that packages applications and dependencies into lightweight,
portable containers.
2■■ Docker Architecture
Client, Daemon, Images, Containers, Registry.
3■■ Basic Commands
docker --version
docker ps
docker ps -a
docker images
docker pull image_name:tag
docker rm container_id
docker rmi image_id
docker system prune -a
4■■ Run Containers
docker run image_name
docker run -it ubuntu:latest
docker run -d nginx
docker run -itd --name mynginx -p 8080:80 nginx:latest
docker run -itd -v /home/user/html:/usr/share/nginx/html nginx
5■■ Manage Containers
docker start/stop/restart container_name
docker exec -it container_name bash
docker logs container_name
docker cp container:/src /dest
docker inspect container
6■■ Images
docker build -t image:tag .
docker tag image:tag user/repo:tag
docker push user/repo:tag
docker save/load images
7■■ Dockerfile Example
FROM openjdk:11
WORKDIR /app
COPY target/myweb.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
8■■ Volumes
docker volume create myvol
docker run -itd -v myvol:/data ubuntu
9■■ Networks
docker network create mynet
docker run -itd --name cont1 --network mynet nginx

## Page 2

■ Docker Compose Example
version: '3'
services:
web:
image: nginx
ports:
- "8080:80"
db:
image: mysql:5.7
environment:
MYSQL_ROOT_PASSWORD: root123
MYSQL_DATABASE: mydb
Commands:
docker-compose up -d
docker-compose down
11■■ Docker Hub
docker login
docker tag myapp:v1 username/myapp:v1
docker push username/myapp:v1
12■■ System Commands
docker stats, docker top, docker history, docker events, docker system df
13■■ Clean-up
docker rm -f $(docker ps -aq)
docker rmi -f $(docker images -aq)
docker system prune -a
14■■ Lifecycle
docker create, start, run, stop, restart, rm, exec
15■■ Port Mapping
-p 8080:80, -p 3306:3306 etc.
16■■ Communication
docker network create mynet
docker run -itd --network mynet --name web nginx
docker run -itd --network mynet --name db mysql
17■■ Troubleshooting
docker logs container
docker inspect container
docker exec -it container bash

