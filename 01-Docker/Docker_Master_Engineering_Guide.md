# 🐳 Docker Containerization: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Container Architecture, Virtual Machines vs Containers, Image Layering, Multi-Stage Builds, Security Hardening, Docker Compose, Production CLI, and Real-World Troubleshooting.

---

## 📑 Table of Contents
- [Docker Architecture & Core Workflow](#docker-architecture--core-workflow)
- [Core Concepts & Foundations](#core-concepts--foundations)
- [Dockerfile Instructions Deep Dive](#dockerfile-instructions-deep-dive)
- [Multi-Stage Production Dockerfile](#multi-stage-production-dockerfile)
- [Docker Networking Deep Dive](#docker-networking-deep-dive)
- [Docker Storage: Volumes vs Bind Mounts](#docker-storage-volumes-vs-bind-mounts)
- [Multi-Container Orchestration with Docker Compose](#multi-container-orchestration-with-docker-compose)
- [Production Command Cheat Sheet](#production-command-cheat-sheet)
- [Production Troubleshooting & Debugging](#production-troubleshooting--debugging)
- [High-Yield Technical Interview Q&A](#high-yield-technical-interview-qa)

---

SECTION 3: DOCKER — COMPLETE GUIDE
Docker Architecture
Docker has three main components:
1. Docker Client — the CLI you use. docker build , docker run , docker push  etc. Sends commands
to the daemon via REST API.
2. Docker Daemon — background service that does all the actual work — building images, running
containers, managing networking and storage.
3. Docker Registry — stores images. Docker Hub (public), Amazon ECR, Azure ACR (private).
Workflow:




You write Dockerfile
→ docker build (client sends to daemon)
→ daemon builds image
→ docker push (push to registry)
→ others pull and run the image
Q1. What is Docker and why does a DevOps engineer use it?
Answer:
Docker is a containerization platform that packages your application, dependencies, and runtime into a
container — a lightweight, isolated environment. Instead of shipping your whole server setup, you ship a
Docker image that runs the same everywhere — laptop, staging, production.
Why better than VMs:
Feature Virtual Machine Docker Container
OS Full OS per VM Shares host OS kernel
Startup Minutes Seconds
Size GBs MBs
Portability Low High
Performance Heavy Lightweight
Key benefit: Eliminates "works on my machine" problem. Same image runs identically everywhere.
Q2. What is the difference between a Docker Image and a Docker
Container?
Answer:
Docker Image — a read-only blueprint/template with all the code, dependencies, and configuration. Built
from a Dockerfile. Stored in a registry.
Docker Container — a running instance of an image. The actual executing process with its own writable
layer.




 
Example:
docker pull nginx                        # pull image from Docker Hub
docker run -d -p 80:80 --name mynginx nginx   # create and run a container from image
docker ps                                # see running containers
You can run multiple containers from one image — they're all isolated from each other.
Q3. What is a Dockerfile and what are the key instructions?
Answer:
A Dockerfile is a text file with instructions to build a Docker image.
Instruction Purpose Example
FROM Base image to start with FROM node:18-alpine
RUN Execute commands during build RUN npm install
COPY Copy files from host into image COPY . /app
WORKDIR Set working directory WORKDIR /app
EXPOSE Declare port the container listens on EXPOSE 3000
CMD Default command when container starts CMD ["node", "app.js"]
ENV Set environment variables ENV NODE_ENV=production
USER Set non-root user for security USER node
Example Dockerfile for a Node.js app:
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000




USER node
CMD ["node", "app.js"]
Q4. What is the difference between COPY and ADD?
Answer:
COPY — simply copies files from host into the image. Nothing extra. Preferred.
ADD — does everything COPY does, plus extracts tar files automatically and can fetch from URLs.
Best practice: Always use COPY. Use ADD only when you need tar extraction.
COPY ./app /app          # preferred - simple and predictable
ADD archive.tar.gz /app  # use only when you need auto-extraction
Q5. What are Docker Layers and why do they matter?
Answer:
Each instruction in a Dockerfile creates a read-only layer. Layers stack on top of each other to form the final
image.
How caching works:
FROM node:18-alpine        # Layer 1 — cached unless base image changes
WORKDIR /app               # Layer 2 — cached
COPY package*.json ./      # Layer 3 — cached unless package.json changes
RUN npm install            # Layer 4 — cached unless layer 3 changes
COPY . .                   # Layer 5 — changes every time code changes
CMD ["node", "app.js"]     # Layer 6
Optimization tip: Put rarely changing instructions at top, frequently changing at bottom. This way npm
install  is cached and doesn't re-run every time you change your code.
Container writable layer: When you run a container, Docker adds a writable layer on top. Multiple containers
from one image each get their own writable layer.




Q6. What is the difference between RUN, CMD, and ENTRYPOINT?
Answer:
Instruction When it runs Can be overridden? Use for
RUN Build time N/A Installing packages
CMD Runtime (container start) Yes, easily Default arguments
ENTRYPOINT Runtime (container start) Only with --entrypoint flag Main executable
Example:
RUN apt-get install -y curl        # runs during build, installs curl
ENTRYPOINT ["python3", "app.py"]   # always runs python3 app.py
CMD ["--debug"]                    # default argument, can be overridden
# Running: docker run myimage --prod
# Result: python3 app.py --prod   (CMD overridden, ENTRYPOINT stays)
Q7. What is Docker Compose?
Answer:
Docker Compose lets you define and run multiple containers together as a single application using a docker-
compose.yml  file.
Example docker-compose.yml (Frontend + Backend + Database):
version: '3.8'
services:
  frontend:
    build: ./frontend
    ports:
      - "80:80"
    depends_on:
      - backend
  backend:
    build: ./backend
    ports:




      - "3000:3000"
    environment:
      - DB_HOST=database
      - DB_PORT=5432
    depends_on:
      - database
  database:
    image: postgres:14
    environment:
      - POSTGRES_DB=myapp
      - POSTGRES_PASSWORD=secret
    volumes:
      - db-data:/var/lib/postgresql/data
volumes:
  db-data:
Key commands:
docker-compose up -d       # start all containers in background
docker-compose down        # stop and remove containers
docker-compose logs -f     # follow logs of all services
docker-compose ps          # list running services
docker-compose build       # rebuild images
Use case: Perfect for local development. In production, use Kubernetes.
Q8. What is Docker Networking?
Answer:
Docker networking controls how containers communicate with each other and the outside world.
Network Type Description Use case
Bridge Default. Containers on same bridge can talk to each other Most common, single host
Host Container uses host machine's network directly High performance, no isolation
Overlay Containers across different machines communicate Docker Swarm, multi-host
None No networking Complete isolation




Commands:
docker network ls                          # list networks
docker network create mynetwork            # create custom bridge network
docker run --network mynetwork myapp       # run container on specific network
docker network inspect mynetwork           # inspect network details
Example: Two containers on same bridge network can communicate by container name:
# Container 1: backend
# Container 2: database
# backend can reach database using: postgres://database:5432
Q9. What is a Docker Volume?
Answer:
A Docker volume is persistent storage that survives even after a container is deleted. Containers are ephemeral
— when they stop, data inside is lost. Volumes store data outside the container.
Types:
Named Volume — managed by Docker, stored in Docker's managed location. Best for production.
Bind Mount — mounts a specific host directory into container. Good for development.
Commands:
docker volume create myvolume              # create named volume
docker volume ls                           # list volumes
docker volume inspect myvolume             # inspect volume details
docker volume rm myvolume                  # remove volume
# Run container with volume
docker run -v myvolume:/var/lib/postgresql/data postgres   # named volume
docker run -v /home/devops/app:/app myapp                   # bind mount
Example: PostgreSQL database with persistent volume:
docker run -d \
  --name postgres \
  -e POSTGRES_PASSWORD=secret \
  -v pgdata:/var/lib/postgresql/data \




  postgres:14
# Even if container is deleted, data in pgdata volume remains
Q10. What is a Docker Registry and types?
Answer:
A Docker registry is a centralized repository to store and manage Docker images.
Registry Type Use case
Docker Hub Public Open source projects, base images
Amazon ECR Private AWS-based projects
Azure ACR Private Azure-based projects
Harbor Self-hosted On-premise enterprise
Commands:
docker login                                    # login to Docker Hub
docker login <registry-url>                     # login to private registry
docker tag myapp:1.0 myrepo/myapp:1.0           # tag image
docker push myrepo/myapp:1.0                    # push to registry
docker pull myrepo/myapp:1.0                    # pull from registry
Q11. What is a Multi-Stage Dockerfile?
Answer:
Multi-stage builds use multiple FROM statements — a build stage and a runtime stage. Build stage compiles
code with all dev tools. Runtime stage copies only the built artifacts, keeping the final image small and secure.
Example:
# Stage 1 - Build
FROM node:18 AS builder
WORKDIR /app




COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
# Stage 2 - Runtime (only artifacts, no dev tools)
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
EXPOSE 3000
CMD ["node", "dist/app.js"]
Result: Final image is tiny — no build tools, no source code, just what's needed to run.
Q12. Docker Security Best Practices
Answer:
# 1. Never run as root — use non-root user
USER node
# 2. Use specific base image versions, not latest
FROM node:18-alpine   # good
FROM node:latest      # bad
# 3. Use .dockerignore to exclude unnecessary files
# .dockerignore file:
node_modules
.git
*.log
.env
# 4. Don't hardcode secrets
ENV DB_PASSWORD=secret123   # BAD — visible in image history
# Use environment variables at runtime instead:
docker run -e DB_PASSWORD=secret123 myapp
# 5. Use multi-stage builds to reduce attack surface
# 6. Scan images for vulnerabilities
docker scan myapp:1.0




# 7. Set resource limits
docker run --memory="256m" --cpus="0.5" myapp
Q13. Docker Troubleshooting Commands
Answer:
# View container logs
docker logs mycontainer              # view logs
docker logs -f mycontainer          # follow logs in real time
docker logs --tail 50 mycontainer   # last 50 lines
# Inspect container
docker inspect mycontainer          # full container details
docker stats                        # live CPU, memory usage of all containers
docker top mycontainer              # processes running inside container
# Debug inside container
docker exec -it mycontainer bash    # open bash shell inside container
docker exec -it mycontainer sh      # use sh if bash not available
# Container lifecycle
docker ps                           # list running containers
docker ps -a                        # list all containers (including stopped)
docker stop mycontainer             # stop container
docker start mycontainer            # start stopped container
docker restart mycontainer          # restart container
docker rm mycontainer               # remove stopped container
docker rm -f mycontainer            # force remove running container
# Image management
docker images                       # list all images
docker rmi myimage:1.0              # remove image
docker image prune                  # remove unused images
docker system prune                 # clean up everything unused
Q14. What is the difference between Docker and containerd?
Answer:




Docker — complete platform. Includes CLI, build tools, image management, networking, storage, and
containerd underneath.
containerd — lightweight container runtime. Just the core engine that runs containers. No CLI, no build
tools.
Docker uses containerd under the hood. Kubernetes moved away from Docker and now uses containerd
directly as its container runtime — simpler, faster, less overhead.
For interviews: Docker is the full toolset for developers. containerd is the leaner runtime that Kubernetes
prefers in production.
Q15. What is Container Orchestration and why do you need it?
Answer:
Container orchestration automates deploying, scaling, and managing containers across multiple machines.
Without it, you'd manually manage each container — impossible at scale.
What orchestration handles:
Deploying containers across multiple nodes
Scaling up/down based on demand
Restarting failed containers (self-healing)
Zero-downtime updates
Load balancing traffic
Networking between containers
Persistent storage management
Tools:
Kubernetes — industry standard, most powerful
Docker Swarm — simpler, built into Docker, less features
For interviews: Always say Kubernetes. It's what enterprise DevOps teams use.
Docker — Deep Dive & Additional Topics
All new content. No duplication with existing Docker section above.




A. VM vs Containers
Virtual Machine (VM)
A VM is a full computer running inside your computer. It has its own OS, kernel, memory, CPU allocation —
everything.
┌─────────────────────────────────────┐
│           Your Machine              │
│  ┌──────────────────────────────┐   │
│  │       Hypervisor             │   │
│  │  (VMware, VirtualBox, KVM)   │   │
│  │                              │   │
│  │  ┌──────────┐ ┌──────────┐  │   │
│  │  │   VM 1   │ │   VM 2   │  │   │
│  │  │ Guest OS │ │ Guest OS │  │   │
│  │  │  App A   │ │  App B   │  │   │
│  │  └──────────┘ └──────────┘  │   │
│  └──────────────────────────────┘   │
│         Host OS + Kernel            │
│              Hardware               │
└─────────────────────────────────────┘
Container
A container shares the host OS kernel. It only packages the app and its dependencies — no full OS needed.
┌─────────────────────────────────────┐
│           Your Machine              │
│  ┌──────────────────────────────┐   │
│  │       Docker Engine          │   │
│  │                              │   │
│  │  ┌──────────┐ ┌──────────┐  │   │
│  │  │Container1│ │Container2│  │   │
│  │  │  App A   │ │  App B   │  │   │
│  │  │  Libs    │ │  Libs    │  │   │
│  │  └──────────┘ └──────────┘  │   │
│  └──────────────────────────────┘   │
│         Host OS + Kernel            │
│              Hardware               │
└─────────────────────────────────────┘
VM vs Container Comparison




Feature Virtual Machine Container
Size GBs (full OS) MBs (just app + libs)
Startup time Minutes Seconds
OS Own full OS Shares host OS kernel
Isolation Strong (hardware level) Good (process level)
Performance Slower (overhead) Near native speed
Portability Less portable Highly portable
Resource usage Heavy Lightweight
Security More isolated Less isolated
Use case Full OS needed, strong isolation Microservices, CI/CD
Pros of VMs:
Strong isolation — one VM crash doesn't affect others
Run different OS (Windows VM on Linux host)
Better security boundaries
Good for stateful, long-running applications
Cons of VMs:
Heavy — each VM needs full OS (GBs)
Slow to start
Wastes resources
Hard to scale quickly
Pros of Containers:
Lightweight — MBs not GBs
Start in seconds
Consistent across environments
Easy to scale
Perfect for microservices and CI/CD
Cons of Containers:
Weaker isolation than VMs
All containers share host kernel — kernel vulnerability affects all
Stateful apps need extra setup (volumes)




Networking more complex at scale
B. Docker Architecture (Detailed)
┌─────────────────────────────────────────────────────┐
│                  Docker Client                       │
│         (docker build, docker run, docker push)      │
└────────────────────────┬────────────────────────────┘
                         │ REST API
┌────────────────────────▼────────────────────────────┐
│                  Docker Daemon (dockerd)             │
│                                                     │
│  ┌─────────────┐  ┌──────────┐  ┌───────────────┐  │
│  │   Images    │  │Containers│  │    Networks    │  │
│  │  (stored    │  │(running  │  │  (bridge,host, │  │
│  │  locally)   │  │instances)│  │   overlay)     │  │
│  └─────────────┘  └──────────┘  └───────────────┘  │
│                                                     │
│  ┌──────────────────────────────────────────────┐   │
│  │         containerd (container runtime)        │   │
│  └──────────────────────────────────────────────┘   │
└────────────────────────┬────────────────────────────┘
                         │ push/pull
┌────────────────────────▼────────────────────────────┐
│                  Docker Registry                     │
│         (Docker Hub, ECR, ACR, Harbor)               │
└─────────────────────────────────────────────────────┘
Three main components:
Docker Client — CLI you use. Sends commands to daemon via REST API.
Docker Daemon (dockerd) — background service. Does all the work — builds images, runs containers,
manages networks and volumes.
Docker Registry — stores and distributes images.
C. Docker Image — Deep Dive
What is a Docker Image?
A Docker image is a read-only template used to create containers. It's built in layers — each instruction in the
Dockerfile creates one layer.




Layer 4: COPY app files        ← your code
Layer 3: RUN npm install       ← dependencies
Layer 2: WORKDIR /app          ← set working dir
Layer 1: FROM node:18          ← base OS + Node
Image Commands:
docker images                          # list all local images
docker images -a                       # include intermediate images
docker pull nginx                      # pull from Docker Hub
docker pull nginx:1.21                 # pull specific version
docker pull myrepo/myapp:1.0          # pull from private registry
docker inspect nginx                   # detailed image info
docker history nginx                   # show layers of image
docker image ls                        # same as docker images
docker image rm nginx                  # remove image
docker rmi nginx                       # same as above
docker rmi -f nginx                    # force remove
docker image prune                     # remove unused images
docker image prune -a                  # remove ALL unused images
docker tag nginx:latest myrepo/nginx:v1  # tag image
docker save nginx > nginx.tar          # save image to file
docker load < nginx.tar                # load image from file
docker export container1 > app.tar     # export container filesystem
docker import app.tar myimage:v1       # import as image
D. Dockerfile — All Instructions
# ─────────────────────────────────────────
# DOCKERFILE COMPLETE INSTRUCTIONS GUIDE
# ─────────────────────────────────────────
# FROM — base image (REQUIRED, must be first)
FROM ubuntu:22.04
FROM node:18-alpine        # alpine = tiny base image
FROM scratch               # empty base (for compiled binaries)
# MAINTAINER — author info (deprecated, use LABEL instead)
MAINTAINER DevOpsEngineer <devops@example.com>
# LABEL — metadata key-value pairs
LABEL maintainer="devops@example.com"




LABEL version="1.0"
LABEL description="My Node.js App"
# RUN — execute command during BUILD time (creates a layer)
RUN apt-get update && apt-get install -y curl    # combine to reduce layers
RUN npm install
RUN mkdir -p /app/logs
# COPY — copy files from host to image
COPY package.json /app/              # copy specific file
COPY src/ /app/src/                  # copy directory
COPY . /app/                         # copy everything
# ADD — like COPY but with extra powers
ADD app.tar.gz /app/                 # auto-extracts tar files
ADD https://example.com/file /app/   # download from URL
# Rule: Use COPY unless you need ADD's extra features
# WORKDIR — set working directory (creates it if doesn't exist)
WORKDIR /app
# All following commands run from /app
# ENV — set environment variables (available at runtime too)
ENV NODE_ENV=production
ENV PORT=3000
ENV DB_HOST=postgres-service
# ARG — build-time variables (NOT available at runtime)
ARG VERSION=1.0
ARG BUILD_DATE
# Usage: docker build --build-arg VERSION=2.0 .
# EXPOSE — document which port the app listens on (doesn't actually publish)
EXPOSE 3000
EXPOSE 80 443
# VOLUME — create mount point for external volumes
VOLUME ["/data"]
VOLUME /var/log/app
# USER — set user for following RUN/CMD/ENTRYPOINT (security best practice)
RUN useradd -m appuser
USER appuser
# Never run as root in production
# CMD — default command when container starts (can be overridden)
CMD ["node", "app.js"]              # exec form (preferred)
CMD node app.js                     # shell form
CMD ["npm", "start"]




# ENTRYPOINT — main executable (harder to override)
ENTRYPOINT ["node"]                 # exec form
ENTRYPOINT node                     # shell form
# Combined with CMD:
ENTRYPOINT ["node"]
CMD ["app.js"]                      # runs: node app.js
# docker run myimage server.js      # runs: node server.js (CMD overridden)
# HEALTHCHECK — how Docker checks if container is healthy
HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
  CMD curl -f http://localhost:3000/health || exit 1
# ONBUILD — trigger instructions for child images
ONBUILD COPY . /app
ONBUILD RUN npm install
# STOPSIGNAL — signal to stop container
STOPSIGNAL SIGTERM
# SHELL — change default shell
SHELL ["/bin/bash", "-c"]
Complete Production Dockerfile Example:
# Stage 1 - Build
FROM node:18 AS builder
LABEL maintainer="devops@example.com"
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
# Stage 2 - Runtime
FROM node:18-alpine
ENV NODE_ENV=production
ENV PORT=3000
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
RUN useradd -m appuser
USER appuser
EXPOSE 3000
HEALTHCHECK --interval=30s CMD curl -f http://localhost:3000/health || exit 1
CMD ["node", "app.js"]




E. Docker Registry — Complete Guide
What is a Docker Registry?
A registry is a server that stores and distributes Docker images. Think of it like GitHub but for Docker images.
Types:
Registry Type URL
Docker Hub Public/Private hub.docker.com
Amazon ECR Private (AWS) AWS Console
Azure ACR Private (Azure) Azure Portal
GitHub Container Registry Private ghcr.io
Harbor Self-hosted Your server
Docker Hub — All Commands:
# Login / Logout
docker login                                    # login to Docker Hub
docker login -u devops -p mypassword            # with credentials
docker login registry.example.com             # login to private registry
docker logout                                  # logout
# Search
docker search nginx                            # search Docker Hub
docker search --filter=stars=100 nginx        # filter by stars
# Pull
docker pull nginx                              # latest tag
docker pull nginx:1.21                         # specific version
docker pull ubuntu:22.04                       # specific OS version
# Tag
docker tag myapp:latest devops/myapp:1.0       # tag for Docker Hub
docker tag myapp:latest 123456.dkr.ecr.us-east-1.amazonaws.com/myapp:1.0  # for ECR
# Push
docker push devops/myapp:1.0                   # push to Docker Hub
docker push 123456.dkr.ecr.us-east-1.amazonaws.com/myapp:1.0  # push to ECR
# Login to AWS ECR
aws ecr get-login-password --region us-east-1 | \




 
  docker login --username AWS --password-stdin \
  123456789.dkr.ecr.us-east-1.amazonaws.com
F. Container Lifecycle
               docker create
                    ↓
             ┌─────────────┐
             │   CREATED   │ ← container created but not started
             └──────┬──────┘
                    │ docker start
                    ↓
             ┌─────────────┐
             │   RUNNING   │ ← container is executing
             └──────┬──────┘
           ┌────────┴────────┐
           │                 │
    docker pause      docker stop/kill
           │                 │
           ▼                 ▼
    ┌──────────────┐  ┌─────────────┐
    │    PAUSED    │  │   STOPPED   │ ← container stopped
    └──────┬───────┘  └──────┬──────┘
           │                 │
    docker unpause    docker start (restart)
           │                 │
           └────────┬────────┘
                    ↓
             ┌─────────────┐
             │   RUNNING   │
             └─────────────┘
                    
             docker rm → DELETED
Lifecycle Commands:
# Create (without starting)
docker create --name mycontainer nginx
# Start
docker start mycontainer
# Run (create + start in one step — most common)




docker run nginx                               # runs in foreground
docker run -d nginx                            # detached (background)
docker run -d --name web nginx                 # with name
docker run -d -p 8080:80 nginx                 # with port mapping
docker run -d -e ENV=production myapp          # with env variable
docker run -d -v myvolume:/data myapp          # with volume
docker run --rm nginx                          # auto-remove when stopped
docker run -it ubuntu bash                     # interactive terminal
# Stop (graceful — sends SIGTERM, waits, then SIGKILL)
docker stop mycontainer
docker stop -t 30 mycontainer                  # wait 30 seconds before kill
# Kill (immediate — sends SIGKILL)
docker kill mycontainer
# Restart
docker restart mycontainer
# Pause / Unpause
docker pause mycontainer
docker unpause mycontainer
# Remove
docker rm mycontainer                          # remove stopped container
docker rm -f mycontainer                       # force remove running container
docker rm $(docker ps -aq)                     # remove ALL stopped containers
docker container prune                         # remove all stopped containers
# View
docker ps                                      # running containers
docker ps -a                                   # all containers (including stopped)
docker ps -q                                   # only IDs
# Inspect and Debug
docker inspect mycontainer                     # full JSON details
docker logs mycontainer                        # logs
docker logs -f mycontainer                     # follow logs
docker logs --tail 50 mycontainer              # last 50 lines
docker exec -it mycontainer bash               # shell inside container
docker exec mycontainer ls /app                # run command without shell
docker top mycontainer                         # processes inside container
docker stats                                   # live resource usage
docker stats mycontainer                       # specific container stats
docker diff mycontainer                        # files changed vs image
docker cp mycontainer:/app/file.txt .          # copy file from container
docker cp file.txt mycontainer:/app/           # copy file to container




G. Port Mapping
Why port mapping?
Containers run in their own isolated network. Port mapping connects a port on your host machine to a port
inside the container.
Host Machine          Container
   :8080    ──────── ▶    :3000
   :8081    ──────── ▶    :3000  (two containers, same container port)
   :5432    ──────── ▶    :5432
# -p hostPort:containerPort
docker run -d -p 8080:3000 myapp           # host 8080 → container 3000
docker run -d -p 80:80 nginx               # host 80 → container 80
docker run -d -p 5432:5432 postgres        # database
docker run -d -p 8080:80 -p 8443:443 nginx # multiple ports
# -P (capital P) — publish ALL exposed ports to random host ports
docker run -d -P nginx
# Check port mappings
docker port mycontainer                    # see all port mappings
docker ps                                  # shows ports in output
# Bind to specific host IP
docker run -d -p 127.0.0.1:8080:80 nginx  # only localhost can access
docker run -d -p 0.0.0.0:8080:80 nginx    # any IP can access (default)
H. Creating Image from a Running Container
Sometimes you make changes inside a running container and want to save that as a new image.
# Step 1 — Run a container and make changes
docker run -it ubuntu bash
# Inside container:
apt-get update && apt-get install -y nginx
exit
# Step 2 — Commit container as new image
docker commit container_name myimage:v1




docker commit -m "Added nginx" -a "DevOpsEngineer" container_name myimage:v1
# Step 3 — Verify
docker images    # you'll see myimage:v1
# Note: This is NOT best practice — always use Dockerfile for reproducibility
# Use commit only for quick debugging or testing
I. Full Deployment Workflow — Docker Only
Scenario: You have a Node.js app. Deploy it using Docker.
# ── STEP 1: Clone your code ──
git clone https://github.com/devops/myapp.git
cd myapp
# ── STEP 2: Write Dockerfile ──
cat > Dockerfile << 'EOF'
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
EOF
# ── STEP 3: Build Docker image ──
docker build -t myapp:1.0 .
docker build -t myapp:1.0 -f Dockerfile.prod .   # specific dockerfile
# ── STEP 4: Test locally ──
docker run -d -p 3000:3000 --name myapp myapp:1.0
curl http://localhost:3000    # verify it works
# ── STEP 5: Tag for Docker Hub ──
docker tag myapp:1.0 devops/myapp:1.0
# ── STEP 6: Login and Push ──
docker login
docker push devops/myapp:1.0
# ── STEP 7: On production server — pull and run ──




docker pull devops/myapp:1.0
docker run -d -p 80:3000 --name myapp devops/myapp:1.0
J. Full Deployment Workflow — Docker + Jenkins Pipeline
Complete Jenkins Pipeline for Docker:
// Jenkinsfile
pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDS = credentials('docker-hub-credentials')
        IMAGE_NAME = "devops/myapp"
        IMAGE_TAG = "${BUILD_NUMBER}"     // use Jenkins build number as tag
        SONAR_TOKEN = credentials('sonar-token')
        NEXUS_CREDS = credentials('nexus-credentials')
    }
    stages {
        // ── STAGE 1: Clone Code ──
        stage('Clone Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/devops/myapp.git'
            }
        }
        // ── STAGE 2: Build Code ──
        stage('Build Code') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        // ── STAGE 3: SonarQube Analysis ──
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=myapp \




                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://sonarqube:9000 \
                        -Dsonar.login=${SONAR_TOKEN}
                    '''
                }
            }
        }
        // ── STAGE 4: Quality Gate ──
        stage('Quality Gate') {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
        // ── STAGE 5: Upload to Nexus ──
        stage('Upload Artifact to Nexus') {
            steps {
                sh '''
                    curl -u ${NEXUS_CREDS_USR}:${NEXUS_CREDS_PSW} \
                    --upload-file target/myapp.jar \
                    http://nexus:8081/repository/myapp-releases/myapp-${BUILD_NUMBER}
                '''
            }
        }
        // ── STAGE 6: Build Docker Image ──
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
                sh "docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${IMAGE_NAME}:latest"
            }
        }
        // ── STAGE 7: Push to Docker Hub ──
        stage('Push Docker Image') {
            steps {
                sh '''
                    echo ${DOCKER_HUB_CREDS_PSW} | \
                    docker login -u ${DOCKER_HUB_CREDS_USR} --password-stdin
                    docker push ${IMAGE_NAME}:${IMAGE_TAG}
                    docker push ${IMAGE_NAME}:latest
                '''
            }
        }
        // ── STAGE 8: Deploy Container ──
        stage('Deploy Container') {
            steps {




 
                sh '''
                    docker stop myapp || true
                    docker rm myapp || true
                    docker pull ${IMAGE_NAME}:${IMAGE_TAG}
                    docker run -d \
                        --name myapp \
                        -p 80:3000 \
                        --restart=always \
                        -e NODE_ENV=production \
                        ${IMAGE_NAME}:${IMAGE_TAG}
                '''
            }
        }
    }
    post {
        success {
            echo "Deployment successful! App running on port 80"
        }
        failure {
            echo "Pipeline failed! Check logs."
            // Send email/Slack notification
        }
        always {
            sh 'docker image prune -f'    // cleanup unused images
        }
    }
}
Pipeline Flow:
Clone Code → Build Code → SonarQube → Quality Gate → Nexus → Docker Build → Docker Pus
K. Docker Compose — Complete Guide
What is Docker Compose?
A tool to define and run multi-container applications using a single YAML file.
Type 1 — Multiple Containers from Existing Images




# docker-compose.yml
version: '3.8'
services:
  # Frontend
  frontend:
    image: nginx:latest
    container_name: frontend
    ports:
      - "80:80"
    volumes:
      - ./frontend:/usr/share/nginx/html
    networks:
      - appnetwork
    depends_on:
      - backend
  # Backend
  backend:
    image: node:18
    container_name: backend
    working_dir: /app
    command: node app.js
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DB_HOST=database
      - DB_PORT=5432
    networks:
      - appnetwork
    depends_on:
      - database
  # Database
  database:
    image: postgres:14
    container_name: database
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - appnetwork




volumes:
  pgdata:          # named volume for database persistence
networks:
  appnetwork:
    driver: bridge
Type 2 — Multiple Containers with Custom Dockerfiles
# docker-compose.yml (builds from Dockerfiles)
version: '3.8'
services:
  frontend:
    build:
      context: ./frontend      # folder containing Dockerfile
      dockerfile: Dockerfile   # Dockerfile name
    container_name: frontend
    ports:
      - "80:80"
    networks:
      - appnetwork
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile.prod    # specific Dockerfile name
      args:
        - NODE_ENV=production         # build arguments
    container_name: backend
    ports:
      - "3000:3000"
    environment:
      - DB_HOST=database
    networks:
      - appnetwork
    depends_on:
      - database
  database:
    image: postgres:14
    container_name: database
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret




    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - appnetwork
volumes:
  pgdata:
networks:
  appnetwork:
    driver: bridge
Docker Compose Commands:
# Start
docker-compose up                      # start all (foreground)
docker-compose up -d                   # start all (background/detached)
docker-compose up --build              # rebuild images before starting
docker-compose up -d --build           # rebuild + detached
# Stop
docker-compose stop                    # stop containers (keep them)
docker-compose down                    # stop + remove containers
docker-compose down -v                 # stop + remove containers + volumes
docker-compose down --rmi all          # remove containers + images too
# View
docker-compose ps                      # list containers
docker-compose logs                    # all logs
docker-compose logs -f                 # follow all logs
docker-compose logs backend            # specific service logs
docker-compose logs -f backend         # follow specific service
# Scale
docker-compose up -d --scale backend=3  # run 3 backend containers
# Execute
docker-compose exec backend bash       # shell into service
docker-compose exec database psql -U admin  # run command in service
# Build only
docker-compose build                   # build all images
docker-compose build backend           # build specific service
# Pull latest images
docker-compose pull                    # pull all images




L. Docker Volumes — Complete Guide
What is a Docker Volume?
Volumes provide persistent storage for containers. Data in volumes survives container restarts and deletions.
Container (ephemeral)
    ↓ writes to
Volume (persistent) ← survives container deletion
Types of Storage
1. Named Volume (Managed by Docker — Recommended)
# Docker manages where data is stored
docker volume create myvolume
docker run -d -v myvolume:/data myapp
# Data lives in: /var/lib/docker/volumes/myvolume/_data
2. Bind Mount (Host directory)
# You control where data lives on host
docker run -d -v /home/devops/data:/data myapp
docker run -d -v $(pwd):/app myapp    # current directory
3. tmpfs Mount (In-memory, not persistent)
docker run -d --tmpfs /tmp myapp      # stored in host memory only
Volume Commands:
# Create
docker volume create myvolume
docker volume create --driver local myvolume
# List
docker volume ls
# Inspect
docker volume inspect myvolume




# Shows mountpoint, driver, labels
# Remove
docker volume rm myvolume
docker volume prune                    # remove all unused volumes
docker volume prune -f                 # force (no confirmation)
# Use in run
docker run -d -v myvolume:/app/data myapp           # named volume
docker run -d -v /host/path:/container/path myapp   # bind mount
docker run -d -v myvolume:/data:ro myapp            # read-only volume
# Backup a volume
docker run --rm \
  -v myvolume:/data \
  -v $(pwd):/backup \
  ubuntu tar cvf /backup/backup.tar /data
# Restore a volume
docker run --rm \
  -v myvolume:/data \
  -v $(pwd):/backup \
  ubuntu tar xvf /backup/backup.tar -C /
M. Docker Networking — All Types
What is Docker Networking?
Docker networking controls how containers communicate with each other and the outside world.
1. Bridge Network (Default)
Host Machine
├── docker0 (bridge interface, 172.17.0.1)
│   ├── container1 (172.17.0.2)
│   ├── container2 (172.17.0.3)
│   └── container3 (172.17.0.4)
└── eth0 (host network, connected to internet)
Default network for all containers
Containers on same bridge can communicate by IP
Containers on custom bridge can communicate by name




Isolated from other bridge networks
# Default bridge
docker run -d nginx                    # uses default bridge
# Custom bridge (recommended — allows DNS by name)
docker network create mybridge
docker run -d --network mybridge --name web nginx
docker run -d --network mybridge --name app myapp
# Now 'app' can reach 'web' by name: http://web:80
2. Host Network
Host Machine (192.168.1.10)
└── Container (shares host network stack)
    └── Uses host's IP and ports directly
Container uses host's network directly
No network isolation
Fastest performance (no NAT overhead)
Container port = host port (no -p needed)
docker run -d --network host nginx
# nginx now accessible on host's port 80 directly
# Cannot use -p with host network
3. None Network
No networking at all
Completely isolated container
Use for maximum security or batch processing
docker run -d --network none myapp
# Container has no network access
4. Overlay Network
Host 1 (Swarm Manager)          Host 2 (Swarm Worker)
├── container1                   ├── container3




└── container2  ←─── overlay ── ▶  └── container4
     (all containers can communicate across hosts)
Used in Docker Swarm for multi-host networking
Containers on different physical hosts communicate seamlessly
Encrypted traffic between hosts
# Create overlay (requires Swarm mode)
docker swarm init
docker network create -d overlay myoverlay
docker service create --network myoverlay nginx
5. Macvlan Network
Assigns a real MAC address to container
Container appears as physical device on network
Direct connection to physical network
Used when containers need to be on physical LAN
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  -o parent=eth0 \
  mymacvlan
docker run -d --network mymacvlan --ip=192.168.1.100 nginx
Networking Commands:
# List networks
docker network ls
# Create network
docker network create mynetwork                          # bridge by default
docker network create --driver bridge mybridge
docker network create --driver overlay myoverlay
docker network create --subnet=172.20.0.0/16 mynet     # custom subnet
# Inspect
docker network inspect mynetwork
docker network inspect bridge                            # default bridge info




# Connect/Disconnect container to network
docker network connect mynetwork mycontainer
docker network disconnect mynetwork mycontainer
# Remove
docker network rm mynetwork
docker network prune                                     # remove unused networks
# Run container on specific network
docker run -d --network mynetwork --name web nginx
docker run -d --network mynetwork --name app myapp
# app can reach web using: http://web (by container name)
Network Comparison:
Network Isolation Communication Use Case
Bridge Yes By IP or name (custom) Default, single host
Host No Shares host network Performance critical
None Complete No networking Batch, security
Overlay Yes Across multiple hosts Docker Swarm
Macvlan Yes Direct to physical LAN Legacy app integration
N. Multi-Stage Dockerfile (Already in Docker Section above — see Section 3
Q11)
Refer to Section 3: Q11 — Multi-Stage Dockerfile for complete explanation and example.


---

## 🚀 Modern 2026 Production Standards & Hardening

### 1. Modern Docker Compose Specification (`compose.yaml`)
*Note: In modern Docker Compose, the top-level `version: '3.8'` attribute is obsolete. Compose now follows the unified Compose Specification:*

```yaml
services:
  web-app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: web-production
    restart: unless-stopped
    ports:
      - "80:8080"
    environment:
      NODE_ENV: production
      DATABASE_URL: postgresql://dbuser:${DB_PASSWORD}@database:5432/appdb
    depends_on:
      database:
        condition: service_healthy
    networks:
      - internal-net

  database:
    image: postgres:16-alpine
    container_name: db-production
    restart: unless-stopped
    environment:
      POSTGRES_DB: appdb
      POSTGRES_USER: dbuser
      POSTGRES_PASSWORD: ${DB_PASSWORD}
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - internal-net
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U dbuser -d appdb"]
      interval: 10s
      timeout: 5s
      retries: 5

volumes:
  postgres_data:

networks:
  internal-net:
    driver: bridge
```

### 2. Multi-Stage Production React / Node.js Template
```dockerfile
# STAGE 1: Build
FROM node:20-alpine AS builder
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci --prefer-offline
COPY . .
RUN npm run build

# STAGE 2: Secure Production Runtime
FROM nginx:1.25-alpine-slim AS runner
RUN addgroup -g 10001 -S appgroup && adduser -u 10001 -S appuser -G appgroup
COPY --from=builder --chown=appuser:appgroup /app/dist /usr/share/nginx/html
USER 10001
EXPOSE 8080
HEALTHCHECK --interval=30s --timeout=5s --retries=3 CMD wget --quiet --tries=1 --spider http://localhost:8080/health || exit 1
CMD ["nginx", "-g", "daemon off;"]
```
