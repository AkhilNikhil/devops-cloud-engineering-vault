# 🐳 Docker Container Engineering: The Definitive Master Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Container Architecture, Linux Namespaces & cgroups, Dockerfile Mastery, Multi-Stage Optimization (Node.js & Python), Compose v2 Orchestration, Storage Volumes & Maintenance (`prune`), Networking Topologies, Modern Tooling (Docker Scout & Docker Init), Security Hardening, and Production Troubleshooting.

---

## 📑 Table of Contents
- [1. Container Architecture & Kernel Fundamentals](#1-container-architecture--kernel-fundamentals)
- [2. Virtual Machines vs Docker Containers](#2-virtual-machines-vs-docker-containers)
- [3. Complete Dockerfile Instruction Reference](#3-complete-dockerfile-instruction-reference)
- [4. Execution Mechanics: RUN vs CMD vs ENTRYPOINT](#4-execution-mechanics-run-vs-cmd-vs-entrypoint)
- [5. Storage Systems: Volumes, Bind Mounts, & tmpfs](#5-storage-systems-volumes-bind-mounts--tmpfs)
- [6. Docker Maintenance & Cleanup (`system prune`)](#6-docker-maintenance--cleanup-system-prune)
- [7. Networking Architecture & Topologies](#7-networking-architecture--topologies)
- [8. Modern Tooling: Docker Scout & Docker Init](#8-modern-tooling-docker-scout--docker-init)
- [9. Multi-Stage Optimization (Node.js & Python)](#9-multi-stage-optimization-nodejs--python)
- [10. Docker Compose v2 Production Orchestration](#10-docker-compose-v2-production-orchestration)
- [11. Essential Docker CLI Command Reference](#11-essential-docker-cli-command-reference)
- [12. Production Troubleshooting Playbook](#12-production-troubleshooting-playbook)
- [13. Security Hardening Checklist](#13-security-hardening-checklist)
- [14. Senior DevOps Interview Q&A](#14-senior-devops-interview-qa)

---

## 1. Container Architecture & Kernel Fundamentals

### System Architecture Overview
```text
┌─────────────────────────────────────────────────────────────┐
│                       Docker Client                         │
│   (CLI commands: docker build, docker run, docker scout)    │
└──────────────────────────────┬──────────────────────────────┘
                               │ REST API / UNIX Socket (/var/run/docker.sock)
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                       Docker Daemon                         │
│                    (dockerd Engine)                         │
│                                                             │
│  ┌──────────────────┐  ┌──────────────────┐  ┌───────────┐  │
│  │ Image Management │  │ Container Engine │  │ Network & │  │
│  │ (Build & Cache)  │  │   (containerd)   │  │  Storage  │  │
│  └──────────────────┘  └────────┬─────────┘  └───────────┘  │
└─────────────────────────────────┼───────────────────────────┘
                                  │ CRI / OCI Spec
                                  ▼
┌─────────────────────────────────────────────────────────────┐
│                     containerd-shim                         │
│   • Decouples container process from the daemon             │
│   • Keeps container running during dockerd restarts         │
└─────────────────────────────────┬───────────────────────────┘
                                  │ Invokes
                                  ▼
┌─────────────────────────────────────────────────────────────┐
│                          runc                               │
│   • Low-level OCI reference runtime                         │
│   • Talks directly to Linux Kernel to spawn containers      │
└─────────────────────────────────┬───────────────────────────┘
                                  │ Configures
                                  ▼
┌─────────────────────────────────────────────────────────────┐
│                       Linux Kernel                          │
│   • Namespaces (Isolation)      • cgroups (Resource Limits) │
│   • Overlay2 (Storage)          • Netfilter / iptables      │
└─────────────────────────────────────────────────────────────┘
```

### The Two Linux Kernel Pillars
Containers are **not virtual machines**; they are standard Linux processes running in isolated environments powered by two specific kernel features:

#### 1. Linux Namespaces (What a Container Can See)
* **PID Namespace (Process ID)**:
  * Isolates the process ID tree.
  * The main container process becomes PID 1 inside the container, but appears as a normal unprivileged PID (e.g., PID 84920) on the host kernel.
* **NET Namespace (Networking)**:
  * Gives the container its own virtual network interfaces (e.g., `eth0`), loopback interface, IP address, and private routing/iptables rules.
* **MNT Namespace (Mount / Filesystem)**:
  * Provides an isolated filesystem view rooted at `/`.
  * The container cannot see or access host paths unless explicitly mounted.
* **IPC Namespace (Inter-Process Communication)**:
  * Isolates shared memory segments, semaphores, and POSIX message queues from other containers and the host.
* **UTS Namespace (Hostname & Domain)**:
  * Allows the container to have its own unique hostname (e.g., container ID or custom name).
* **USER Namespace (User & Group IDs)**:
  * Maps UID 0 (root) inside the container to a non-privileged UID on the host, preventing host root takeovers.

#### 2. Control Groups (cgroups) (What a Container Can Use)
* **CPU Limiting**: Controls maximum CPU share and execution bandwidth (e.g., `--cpus="1.5"` or `--cpu-shares=1024`).
* **Memory Limiting**: Sets hard memory caps (e.g., `--memory="512m"`). If exceeded, the Linux Kernel OOM killer terminates the process (Exit Code 137).
* **Block I/O (blkio)**: Throttles read/write disk I/O rates to prevent noisy-neighbor storage saturation.
* **PIDs Limiting**: Limits the maximum number of child processes (`--pids-limit=100`) to completely eliminate fork bomb attacks.

---

## 2. Virtual Machines vs Docker Containers

### Point-by-Point Comparison

| Feature | Virtual Machine (VM) | Docker Container |
| :--- | :--- | :--- |
| **Architecture** | Runs a complete Guest OS on top of a Hypervisor | Runs as an isolated process on the shared Host OS Kernel |
| **Hypervisor** | Requires Type 1 (ESXi, KVM) or Type 2 (VirtualBox) | Requires only container runtime (`containerd`, `runc`) |
| **Boot Time** | Minutes (boots BIOS, kernel, system services) | Milliseconds to seconds (spawns single process) |
| **Resource Footprint** | Heavy (Gigabytes of RAM & storage for Guest OS) | Extremely light (Megabytes, shares host kernel memory) |
| **Storage Overhead** | Large virtual disk images (`.vmdk`, `.qcow2`) | Layered Overlay2 union filesystem sharing base layers |
| **Isolation Level** | Strong hardware-level isolation via hypervisor | Process-level isolation via kernel namespaces and cgroups |
| **Portability** | Heavy to export and move across environments | Ultra-portable OCI images run identically anywhere |
| **Density** | Low (tens of VMs per physical host) | High (hundreds of containers per physical host) |

---

## 3. Complete Dockerfile Instruction Reference

A Dockerfile is a step-by-step blueprint for building an OCI container image. Every line creates an immutable layer cached by the build engine.

### Detailed Point-by-Point Instruction Guide

#### 1. `FROM`
* **Purpose**: Defines the parent base image. Must be the very first non-comment instruction (except `ARG`).
* **Best Practice**: Always pin to a specific, minimal version (e.g., `FROM node:18.19-alpine` instead of `FROM node:latest`).
* **Multi-Stage Syntax**: `FROM <image> AS <stage_name>` enables naming stages for intermediate builds.

#### 2. `WORKDIR`
* **Purpose**: Sets the working directory for all subsequent `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions.
* **Best Practice**: Always use absolute paths (e.g., `WORKDIR /app`). Automatically creates directories if they do not exist.
* **Anti-Pattern**: Avoid chaining `RUN cd /app && npm start`—directory changes do not persist across separate `RUN` layers!

#### 3. `COPY` vs `ADD`
* **`COPY` (Preferred)**:
  * Copies local files/directories from the build context into the container filesystem.
  * Predictable, transparent, and supports ownership flags: `COPY --chown=node:node . .`.
* **`ADD` (Specialized)**:
  * Can unpack compressed archives automatically (e.g., `ADD rootfs.tar.gz /`).
  * Can fetch files from remote URLs (not recommended due to cache invalidation).
  * **Rule**: Use `COPY` for all standard files; use `ADD` only when auto-extracting local tarballs.

#### 4. `RUN`
* **Purpose**: Executes shell commands during the image build phase to install packages and compile code.
* **Layer Caching Rule**: Chain dependent commands using `&&` to minimize intermediate image layers:
  ```dockerfile
  RUN apt-get update && apt-get install -y --no-install-recommends       curl       ca-certificates       && rm -rf /var/lib/apt/lists/*
  ```

#### 5. `ENV` vs `ARG`
* **`ARG` (Build-Time Only)**:
  * Available only while `docker build` is executing (e.g., `--build-arg VERSION=1.2.0`).
  * Never baked into the running container environment.
* **`ENV` (Runtime Available)**:
  * Sets environment variables available during build **and** inside the running container.
  * Example: `ENV NODE_ENV=production PORT=3000`.

#### 6. `EXPOSE`
* **Purpose**: Documents the port on which the container application listens.
* **Important Note**: `EXPOSE` **does not** actually publish or open ports to the host! It serves purely as documentation. You must still pass `-p host_port:container_port` at runtime.

#### 7. `VOLUME`
* **Purpose**: Creates an anonymous mount point and marks it as holding externally mounted storage.
* **Behavior**: Any data written to a `VOLUME` path bypasses the container writable layer and is stored directly on host storage.

#### 8. `USER`
* **Purpose**: Switches the active UID/GID for all subsequent instructions and container runtime.
* **Security Critical**: **Never run containers as root in production!** Always create and switch to an unprivileged user (e.g., `USER 10001` or `USER node`).

#### 9. `HEALTHCHECK`
* **Purpose**: Instructs Docker how to test if the container application is actually healthy and responding.
* **Syntax**:
  ```dockerfile
  HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3     CMD curl -f http://localhost:3000/health || exit 1
  ```

---

## 4. Execution Mechanics: RUN vs CMD vs ENTRYPOINT

Understanding the exact difference between these three instructions is a top-tier interview drill.

```text
┌─────────────────┬────────────────────────────────────────────────────────┐
│ Instruction     │ When Does It Execute? / What Does It Do?               │
├─────────────────┼────────────────────────────────────────────────────────┤
│ RUN             │ Executes during BUILD phase; commits a new layer       │
│ ENTRYPOINT      │ Configures the fixed executable at RUNTIME             │
│ CMD             │ Provides default arguments to ENTRYPOINT or default app│
└─────────────────┴────────────────────────────────────────────────────────┘
```

### The Two Syntax Forms
1. **Exec Form (Preferred & Production Standard)**:
   * Syntax: `["executable", "param1", "param2"]`
   * Runs directly as PID 1 without invoking a shell.
   * **Receives OS signals (`SIGTERM`, `SIGINT`) properly**, enabling clean container shutdown.
2. **Shell Form (Discouraged)**:
   * Syntax: `executable param1 param2`
   * Docker wraps this command as `/bin/sh -c "executable param1 param2"`.
   * The shell runs as PID 1; your application runs as a child process and **does not receive `SIGTERM`**, causing Docker to forcibly kill it after a 10s timeout (`SIGKILL`).

### How `ENTRYPOINT` and `CMD` Work Together

```dockerfile
ENTRYPOINT ["node", "server.js"]
CMD ["--port", "3000"]
```
* **Default execution**: `node server.js --port 3000`
* **Overriding arguments (`docker run myimage --port 8080`)**: `node server.js --port 8080` (replaces `CMD`, keeps `ENTRYPOINT`).
* **Overriding executable (`docker run --entrypoint /bin/sh myimage`)**: Completely overrides `ENTRYPOINT`.

---

## 5. Storage Systems: Volumes, Bind Mounts, & tmpfs

Docker uses a layered storage driver (**Overlay2**) for container images. Any changes made inside a running container are written to a thin, temporary **Container Read-Write Layer**. When the container is deleted, that layer is destroyed.

To persist data, Docker provides three external storage mechanisms:

```text
┌─────────────────────────────────────────────────────────────────────────┐
│                              HOST MACHINE                               │
│                                                                         │
│  ┌───────────────────────────┐         ┌─────────────────────────────┐  │
│  │    Named Docker Volume    │         │      Host Bind Mount        │  │
│  │ (/var/lib/docker/volumes) │         │    (/home/user/project)     │  │
│  └─────────────┬─────────────┘         └──────────────┬──────────────┘  │
│                │                                      │                 │
│                ▼                                      ▼                 │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │                        DOCKER CONTAINER                           │  │
│  │                                                                   │  │
│  │  ┌─────────────────────────────────────────────────────────────┐  │  │
│  │  │                 tmpfs Mount (Host RAM Only)                 │  │  │
│  │  └─────────────────────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

### 1. Named Volumes (Best for Production & Databases)
* **Location**: Fully managed by Docker inside `/var/lib/docker/volumes/<volume_name>/_data`.
* **Key Advantages**:
  * Completely independent of host directory structure and OS file permissions.
  * Can be backed up, migrated, and managed via Docker CLI (`docker volume ls`, `docker volume inspect`).
  * Supports volume drivers for cloud storage (AWS EBS, NFS, Ceph).
* **CLI Syntax**:
  ```bash
  # Create named volume
  docker volume create mysql_data

  # Mount volume to container
  docker run -d -v mysql_data:/var/lib/mysql mysql:8.0
  ```

### 2. Bind Mounts (Best for Local Development)
* **Location**: Maps any arbitrary folder on the host machine directly into the container.
* **Key Advantages**:
  * Great for hot-reloading code during active local development.
* **Risks**:
  * Binds container security directly to host file permissions.
  * Breaks portability if the specified host path does not exist on another machine.
* **CLI Syntax**:
  ```bash
  docker run -d -v /home/user/code:/app node:18-alpine
  ```

### 3. tmpfs Mounts (In-Memory Ephemeral Storage)
* **Location**: Stored strictly in the host machine's RAM; never written to disk.
* **Key Advantages**:
  * Ultra-fast read/write operations.
  * High security for sensitive tokens, passwords, and encryption keys that must never touch permanent storage.
* **CLI Syntax**:
  ```bash
  docker run -d --tmpfs /app/secrets myapp:latest
  ```

---

## 6. Docker Maintenance & Cleanup (`system prune`)

Over time, unused images, dead containers, dangling build caches, and orphan volumes silently consume hundreds of gigabytes of disk space.

### The `docker system prune` Command Suite

* **Standard Prune**:
  ```bash
  docker system prune
  ```
  * Removes stopped containers.
  * Removes all unused networks.
  * Removes dangling images (untagged `<none>` layers).
  * Removes dangling build cache.
  * **Does NOT delete named volumes** by default (safe from data loss).

* **Aggressive Production Cleanup**:
  ```bash
  docker system prune -a --volumes
  ```
  * `-a` (`--all`): Removes **all** unused images, not just dangling ones.
  * `--volumes`: Prunes **all unused anonymous and named volumes** (Warning: deletes database data if containers are stopped!).

* **Selective Pruning by Age (Safe Periodic Cron Job)**:
  ```bash
  # Prune containers stopped more than 24 hours ago
  docker container prune --filter "until=24h"

  # Prune images created more than 7 days ago
  docker image prune -a --filter "until=168h"
  ```

---

## 7. Networking Architecture & Topologies

Docker creates virtual network interfaces on the host and manages packet routing using Linux bridges and `iptables`.

### The 5 Core Network Drivers

| Driver | Scope | How It Works | Primary Use Case |
| :--- | :--- | :--- | :--- |
| **`bridge`** | Single Host | Default private virtual bridge (`docker0`). Containers get private IPs (e.g. `172.17.0.x`). | Standard standalone containers & local compose |
| **`host`** | Single Host | Bypasses container network isolation; container shares host network stack directly. | Ultra-low latency, high-throughput apps |
| **`none`** | Container | Disables all networking; only loopback (`127.0.0.1`) interface exists. | High-security air-gapped jobs, batch crypto jobs |
| **`overlay`**| Multi-Host | Enables cross-host container networking across Swarm or Kubernetes clusters. | Distributed multi-host clusters |
| **`macvlan`**| Physical LAN| Assigns a real MAC address to the container, making it appear as a physical device on LAN. | Legacy apps needing direct physical subnet IPs |

### User-Defined Bridge Networks vs Default Bridge
* **Default Bridge (`docker0`)**:
  * Containers can only communicate with each other using raw IP addresses.
  * **No automatic DNS resolution**!
* **User-Defined Bridge Network (Production Standard)**:
  * Has built-in embedded DNS server (`127.0.0.11`).
  * Containers resolve each other **by container name or service name**!
  * **Commands**:
    ```bash
    # Create isolated user bridge
    docker network create -d bridge app-network

    # Connect containers to network
    docker run -d --name db --network app-network mysql:8.0
    docker run -d --name web --network app-network -e DB_HOST=db mywebapp:latest
    ```

---

## 8. Modern Tooling: Docker Scout & Docker Init

Modern enterprise DevOps requires continuous security scanning and automated container scaffolding.

### 1. Docker Scout (Vulnerability & CVE Analysis)
Docker Scout scans container image layers, discovers software dependencies (SBOM - Software Bill of Materials), and identifies known vulnerabilities (CVEs) without requiring third-party tools.

* **Quick Layer Summary**:
  ```bash
  docker scout quickview <image_name>:<tag>
  ```
  * Displays high-level vulnerability breakdown: Critical, High, Medium, Low.
* **Full CVE Vulnerability Log**:
  ```bash
  docker scout cves <image_name>:<tag>
  ```
  * Lists exact CVE IDs, affected software packages, CVSS severity scores, and recommended fixed package versions.
* **Base Image Recommendations**:
  ```bash
  docker scout recommendations <image_name>:<tag>
  ```
  * Suggests safer alternative base images that eliminate known vulnerabilities.

### 2. Docker Init (Automated Project Scaffolding)
`docker init` is a modern CLI utility that automatically analyzes your source code repository and writes optimized Docker configuration files.

* **Workflow**:
  1. Open your terminal inside your project directory.
  2. Run:
     ```bash
     docker init
     ```
  3. Select your application programming language (Go, Python, Node, Java, Rust, etc.).
  4. Specify package manager, port, and main entrypoint file.
* **Generated Assets**:
  * `.dockerignore` (pre-configured to exclude git, tests, and local caches).
  * `Dockerfile` (optimized multi-stage build following security best practices).
  * `compose.yaml` (starter Compose specification configured with unprivileged ports).

---

## 9. Multi-Stage Optimization (Node.js & Python)

Multi-stage builds allow you to use heavy SDKs, compilers, and development tools during the build phase, and then copy **only the compiled artifacts and production dependencies** into a minimal, stripped-down runtime image.

### Production Pattern 1: Node.js Multi-Stage Build
```dockerfile
# ==========================================
# STAGE 1: Builder (Compiles TypeScript & Installs Dependencies)
# ==========================================
FROM node:18-alpine AS builder
WORKDIR /app

# Optimize layer caching: Only reinstall modules if package manifests change
COPY package*.json ./
RUN npm ci

# Copy application source and build production bundle
COPY . .
RUN npm run build

# Prune development dependencies to keep production footprint minimal
RUN npm prune --production

# ==========================================
# STAGE 2: Production Runner (Lean, Clean, & Hardened)
# ==========================================
FROM node:18-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production

# Security: Create and switch to non-root user
USER node

# Copy only production dependencies and compiled dist from builder
COPY --from=builder --chown=node:node /app/node_modules ./node_modules
COPY --from=builder --chown=node:node /app/dist ./dist
COPY --from=builder --chown=node:node /app/package.json ./package.json

EXPOSE 3000
CMD ["node", "dist/index.js"]
```

### Production Pattern 2: Python Multi-Stage Build
```dockerfile
# ==========================================
# STAGE 1: Builder (Compiles Wheels & C-Extensions)
# ==========================================
FROM python:3.11-slim AS builder
WORKDIR /build

RUN apt-get update && apt-get install -y --no-install-recommends     build-essential     gcc     && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir --user -r requirements.txt

# ==========================================
# STAGE 2: Production Runner (Minimal Slim Runtime)
# ==========================================
FROM python:3.11-slim AS runner
WORKDIR /app

# Create non-root system user
RUN useradd -u 10001 -m -s /bin/bash appuser

# Copy installed python packages from builder stage
COPY --from=builder /root/.local /home/appuser/.local
COPY --chown=appuser:appuser . .

ENV PATH=/home/appuser/.local/bin:$PATH
ENV PYTHONUNBUFFERED=1

USER appuser

EXPOSE 8000
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

## 10. Docker Compose v2 Production Orchestration

Docker Compose v2 (`compose.yaml`) manages multi-container application stacks declaratively.

### Production `compose.yaml` Blueprint
```yaml
version: '3.8'

services:
  # Database Service
  database:
    image: mysql:8.0
    container_name: taskflow_mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: ${DB_ROOT_PASSWORD}
      MYSQL_DATABASE: taskflow_db
      MYSQL_USER: taskflow_user
      MYSQL_PASSWORD: ${DB_USER_PASSWORD}
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - internal_network
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-u", "root", "-p${DB_ROOT_PASSWORD}"]
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 30s

  # Backend API Service
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile
    container_name: taskflow_backend
    restart: always
    environment:
      DB_HOST: database
      DB_PORT: 3306
      DB_NAME: taskflow_db
      DB_USER: taskflow_user
      DB_PASSWORD: ${DB_USER_PASSWORD}
    ports:
      - "5000:5000"
    depends_on:
      database:
        condition: service_healthy
    networks:
      - internal_network
      - edge_network

  # Frontend Web Service
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile
    container_name: taskflow_frontend
    restart: always
    ports:
      - "80:80"
    depends_on:
      - backend
    networks:
      - edge_network

# Persistent Named Volumes
volumes:
  db_data:
    driver: local

# Isolated Network Topologies
networks:
  internal_network:
    driver: bridge
    internal: true  # Completely blocks direct internet inbound/outbound access
  edge_network:
    driver: bridge
```

---

## 11. Essential Docker CLI Command Reference

### Image Management
* `docker build -t app:v1 .` — Build image from current directory Dockerfile.
* `docker images` — List all local images.
* `docker rmi <image_id>` — Remove local image.
* `docker tag app:v1 username/app:v1` — Tag image for Docker Hub registry.
* `docker push username/app:v1` — Push image to remote registry.

### Container Lifecycle
* `docker run -d -p 80:3000 --name web app:v1` — Run container in detached mode with port mapping.
* `docker ps` — List running containers.
* `docker ps -a` — List all containers (running and stopped).
* `docker stop <id>` — Send `SIGTERM` followed by `SIGKILL` after 10s.
* `docker rm -f <id>` — Force remove running container.
* `docker restart <id>` — Restart container.

### Inspection & Diagnostics
* `docker logs -f --tail 100 <id>` — Tail live container stdout/stderr logs.
* `docker exec -it <id> sh` — Open interactive shell inside running container.
* `docker inspect <id>` — Return complete low-level JSON configuration (IP, mounts, env).
* `docker stats` — Stream live CPU, Memory, Network, and Block I/O usage for all containers.
* `docker top <id>` — Display running processes inside container.

### Networks & Volumes
* `docker network ls` — List all networks.
* `docker network inspect <net_name>` — Inspect connected containers and subnet details.
* `docker volume ls` — List all named volumes.
* `docker volume inspect <vol_name>` — View exact storage mount path on host.

---

## 12. Production Troubleshooting Playbook

### Scenario 1: Container Exits Immediately with Exit Code 137
* **Root Cause**: Linux Kernel **OOM (Out Of Memory) Killer** terminated the container process because it exceeded its allocated memory limit (`--memory`), or host ran out of RAM.
* **Diagnosis**:
  * Run `docker inspect <container_id> --format '{{.State.OOMKilled}}'`. Returns `true` if OOM killed.
  * Check kernel logs: `dmesg -T | grep -i oom`.
* **Remediation**:
  * Increase container memory limit (`--memory="1g"`).
  * Profile application memory leaks using heap dump analysis.

### Scenario 2: Container Exits with Exit Code 0
* **Root Cause**: The foreground process (PID 1) finished execution and exited naturally (e.g., CMD was `echo "hello"` or a background daemon spawned without keeping a foreground process alive).
* **Remediation**:
  * Ensure the main process runs in the foreground (e.g., `nginx -g 'daemon off;'` or `tail -f /dev/null` for testing).

### Scenario 3: Container Cannot Reach Database on User-Defined Bridge
* **Root Cause**: Trying to use `localhost` or default bridge without DNS.
* **Remediation**:
  * Ensure both containers are on the **same user-defined bridge network**.
  * Use the **container service name** as the database host (e.g., `DB_HOST=database`), never `127.0.0.1` or `localhost`.

---

## 13. Security Hardening Checklist

* [ ] **Run as Non-Root**: Always specify `USER <non-root-uid>` in Dockerfile.
* [ ] **Use Minimal Base Images**: Prefer `alpine` or `distroless` to eliminate attack surface and package vulnerabilities.
* [ ] **Scan Images for CVEs**: Automate `docker scout cves` in CI/CD before pushing to registry.
* [ ] **Drop Linux Capabilities**: Run containers with `--cap-drop=ALL --cap-add=NET_BIND_SERVICE`.
* [ ] **Make Filesystem Read-Only**: Use `--read-only` with explicit tmpfs mounts for temporary directories.
* [ ] **Do Not Expose Docker Socket**: Never mount `/var/run/docker.sock` inside untrusted containers (grants full root host access!).
* [ ] **Use Secret Managers**: Never bake passwords, tokens, or private keys into `ENV` or image layers.

---

## 14. Senior DevOps Interview Q&A

### Q1: What happens under the hood when you run `docker run -d -p 80:80 nginx`?
* The Docker CLI validates command syntax and sends a REST API request to the `dockerd` daemon over the UNIX socket (`/var/run/docker.sock`).
* `dockerd` checks local storage for the `nginx` image; if missing, it downloads image layers from Docker Hub.
* `dockerd` instructs `containerd` to prepare the image root filesystem using the `Overlay2` storage driver.
* `containerd` uses `containerd-shim` to invoke the OCI runtime (`runc`).
* `runc` makes Linux kernel system calls to configure **namespaces** (PID, NET, MNT, IPC, UTS) and **cgroups** (CPU, memory).
* `dockerd` configures a virtual Ethernet pair (`veth`), attaches one end to the `docker0` bridge and the other inside the container's NET namespace as `eth0`.
* An `iptables` NAT port-forwarding rule is injected on the host: `Host:80 -> Container:80`.
* The `nginx` process starts as PID 1 inside the container namespace.

### Q2: Why is the order of instructions in a Dockerfile critical?
* Docker evaluates instructions top-to-bottom and caches intermediate layers.
* If a layer changes, that layer and **every single layer below it** must be rebuilt from scratch.
* **Golden Rule**: Place stable, infrequently changing layers (OS packages, dependency manifests `package.json`, `requirements.txt`) at the top, and volatile, frequently changing layers (source code) at the very bottom.

### Q3: What is the difference between a bind mount and a named volume?
* **Named Volume**: Managed completely by Docker inside `/var/lib/docker/volumes`. Portable, backed up easily, supports storage plugins, and works across operating systems.
* **Bind Mount**: Directly maps an absolute host directory into the container. Dependent on the host machine filesystem structure; best for local development code reloading.

### Q4: How do you shrink a 1.2GB Docker image down to 50MB?
* Switch from full OS distributions (e.g., `ubuntu`, `debian`) to an Alpine or Distroless base image.
* Implement a multi-stage Dockerfile to separate the compilation toolchain from the runtime container.
* Clean package manager caches within the same `RUN` command (e.g., `apt-get clean && rm -rf /var/lib/apt/lists/*`).
* Ensure a comprehensive `.dockerignore` file prevents `.git`, `node_modules`, test files, and local build outputs from entering the build context.
