# AWS EC2 Deployment — V3

This guide explains how to deploy the **My Tasks (Todo Management System) V3** application on an AWS EC2 instance using Docker.

The application uses:

- **Frontend:** React + Vite, served by Nginx
- **Backend:** Python Flask + Gunicorn
- **Database:** PostgreSQL on Supabase
- **Authentication:** JWT with Admin/User roles
- **Container Registry:** Docker Hub
- **Cloud Platform:** AWS EC2
- **Operating System:** Ubuntu Server
- **Deployment:** Docker containers on a single EC2 instance

> **Note:** This document describes the AWS EC2 deployment path. The same V3 application is also deployed on Render; see the main deployment documentation for the Render workflow.

---

## 1. Architecture

![AWS EC2 V3 Architecture](images/aws-ec2-v3-architecture.png)

### AWS deployment flow

```text
User
  |
  | HTTP :80
  v
AWS EC2 Instance
  |
  +-----------------------------+
  | Docker                      |
  |                             |
  | Frontend Container          |
  | React build + Nginx         |
  | Port 80                     |
  |                             |
  | Backend Container           |
  | Flask + Gunicorn            |
  | Port 5000                   |
  +-----------------------------+
              |
              | PostgreSQL / SSL
              v
        Supabase PostgreSQL
```

Docker images are pulled from Docker Hub:

```text
akhilbm/todo-frontend:3.1
akhilbm/todo-backend:3.0
```

The application code remains the same; AWS EC2 provides the compute environment and Docker runs the application containers.

---

## 2. AWS Resources

For this deployment we use:

| Resource | Configuration |
|---|---|
| EC2 | `t3.micro` |
| OS | Ubuntu Server |
| Storage | 8 GiB gp3 |
| Public IP | Enabled |
| VPC | Default VPC |
| Database | Supabase PostgreSQL |
| Containers | Frontend + Backend |
| Container Registry | Docker Hub |

No AWS IAM role is required for the application containers in this deployment because the backend connects to Supabase using the database connection string supplied through environment variables.

---

## 3. Security Group

Configure the EC2 Security Group with the following inbound rules:

| Type | Port | Source | Purpose |
|---|---:|---|---|
| SSH | 22 | My IP recommended | SSH administration |
| HTTP | 80 | `0.0.0.0/0` | Public frontend |
| Custom TCP | 5000 | `0.0.0.0/0` | Public backend API |

For a production deployment, port `22` should be restricted to trusted IP addresses and the backend port should preferably not be exposed publicly.

> The port `5000` rule is used here because this deployment exposes the Flask API directly from the EC2 instance. A future production improvement would place Nginx in front of both services and expose only ports `80/443`.

### Screenshot

Add:

```text
docs/images/aws-01-security-group.png
```

Show the inbound rules, but do not include credentials or private information.

---

## 4. Launch the EC2 Instance

In the AWS Console:

1. Open **EC2**.
2. Choose **Launch Instance**.
3. Select **Ubuntu Server**.
4. Select instance type:
   ```text
   t3.micro
   ```
5. Configure the default VPC/subnet.
6. Enable public IP assignment.
7. Select/create an SSH key pair.
8. Attach the Security Group described above.
9. Use an approximately 8 GiB gp3 root volume.
10. Launch the instance.

### Screenshot

Add:

```text
docs/images/aws-02-ec2-instance.png
```

Capture the running EC2 instance showing the instance type, public IP/DNS, and running state.

---

## 5. Connect to EC2 Using SSH

From Git Bash:

```bash
ssh -i "todo-key.pem" ubuntu@<EC2_PUBLIC_IP>
```

Example format:

```bash
ssh -i "todo-key.pem" ubuntu@<EC2_PUBLIC_IP>
```

Do not commit the `.pem` file to GitHub.

If required on Linux/macOS:

```bash
chmod 400 todo-key.pem
```

### Screenshot

Add:

```text
docs/images/aws-03-ssh.png
```

Capture the successful SSH connection and terminal prompt.

Do not show private key contents.

---

## 6. Update the Ubuntu Server

After connecting:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 7. Install Docker

Install Docker and Docker Compose:

```bash
sudo apt install -y docker.io
sudo apt install -y docker-compose-v2
```

Start Docker:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

Allow the current user to run Docker:

```bash
sudo usermod -aG docker $USER
newgrp docker
```

Verify:

```bash
docker --version
docker compose version
```

Expected versions may differ over time.

### Screenshot

Add:

```text
docs/images/aws-04-docker-installation.png
```

Show the Docker and Docker Compose version output.

---

## 8. Configure Environment Variables

The backend requires:

- `DATABASE_URL`
- `JWT_SECRET_KEY`

Create the environment file:

```bash
nano .env
```

Add:

```env
DATABASE_URL=<your Supabase PostgreSQL connection string>
JWT_SECRET_KEY=<your JWT secret>
```

Save the file.

### Security

**Never commit `.env` to GitHub.**

Do not put the actual values in documentation, screenshots, Dockerfiles, or Git history.

The `.gitignore` should contain:

```text
.env
```

### Screenshot

Do **not** take a screenshot showing the actual `.env` values.

If you want to document this step visually, use a screenshot of the terminal showing:

```text
nano .env
```

with the secret values hidden/redacted.

---

## 9. Pull the Docker Images

Pull the V3 images from Docker Hub:

```bash
docker pull akhilbm/todo-backend:3.0
docker pull akhilbm/todo-frontend:3.1
```

Verify:

```bash
docker images
```

You should see:

```text
akhilbm/todo-backend    3.0
akhilbm/todo-frontend   3.1
```

### Screenshot

Add:

```text
docs/images/aws-05-docker-images.png
```

Show the `docker images` output.

---

## 10. Start the Backend Container

Run:

```bash
docker run -d \
  -p 5000:5000 \
  --env-file .env \
  --name backend \
  akhilbm/todo-backend:3.0
```

Check:

```bash
docker ps
```

Check backend logs if required:

```bash
docker logs backend
```

---

## 11. Start the Frontend Container

Run:

```bash
docker run -d \
  -p 80:80 \
  --name frontend \
  akhilbm/todo-frontend:3.1
```

Check:

```bash
docker ps
```

Expected:

```text
backend     ...   0.0.0.0:5000->5000/tcp
frontend    ...   0.0.0.0:80->80/tcp
```

### Screenshot

Add:

```text
docs/images/aws-06-containers-running.png
```

Capture:

```bash
docker ps
```

showing both containers running.

---

## 12. Verify the Backend

From inside the EC2 instance:

```bash
curl http://localhost:5000/api/health
```

Expected:

```json
{"status":"healthy"}
```

Also test:

```bash
curl -v http://localhost:80/
```

### Screenshot

Add:

```text
docs/images/aws-07-health-check.png
```

Show the successful health check.

---

## 13. Verify Public Access

From your local computer:

```bash
curl -v http://<EC2_PUBLIC_IP>/
```

Backend health:

```bash
curl -v http://<EC2_PUBLIC_IP>:5000/api/health
```

Open the frontend in a browser:

```text
http://<EC2_PUBLIC_IP>/
```

Then verify:

- Registration
- Login
- Task creation
- Task update
- Complete/Undo
- Delete
- Logout/login persistence
- User task isolation
- Admin functionality

### Screenshot

Add:

```text
docs/images/aws-08-application.png
```

Capture the deployed application running through the EC2 public IP.

---

## 14. Deployment Verification Checklist

- [ ] EC2 instance is running
- [ ] Security Group allows required ports
- [ ] SSH connection works
- [ ] Docker is installed
- [ ] Backend image pulled successfully
- [ ] Frontend image pulled successfully
- [ ] Backend container is running
- [ ] Frontend container is running
- [ ] Backend health endpoint returns `200`
- [ ] Frontend is reachable from the public IP
- [ ] Registration works
- [ ] Login works
- [ ] Tasks can be created and updated
- [ ] Tasks persist after logout/login
- [ ] User task isolation works
- [ ] Admin features work
- [ ] Supabase PostgreSQL connectivity works

---

## 15. Troubleshooting

### Container is not running

```bash
docker ps -a
```

Then:

```bash
docker logs backend
```

or:

```bash
docker logs frontend
```

---

### Backend health check fails

Check:

```bash
docker logs backend
```

Verify that `.env` contains valid:

```text
DATABASE_URL
JWT_SECRET_KEY
```

Also verify the Supabase database is reachable.

---

### Frontend is not accessible

Check:

```bash
docker ps
```

Then verify the Security Group allows:

```text
TCP 80
```

Also test inside EC2:

```bash
curl http://localhost:80
```

---

### Backend is not accessible externally

Check:

```bash
curl http://localhost:5000/api/health
```

If this works inside EC2 but not externally, verify the Security Group allows:

```text
TCP 5000
```

---

### SSH connection fails

Check:

- EC2 instance is running
- Correct public IP
- Correct SSH username (`ubuntu`)
- Correct `.pem` file
- Security Group allows TCP 22 from your IP

---

## 16. Managing the Deployment

Stop containers:

```bash
docker stop backend frontend
```

Start them again:

```bash
docker start backend frontend
```

View logs:

```bash
docker logs backend
docker logs frontend
```

Remove containers when no longer needed:

```bash
docker rm backend frontend
```

---

## 17. AWS Cost Management

For a personal/demo deployment:

- Stop the EC2 instance when it is not being used.
- Remember that stopping and starting an instance without an Elastic IP can change its public IP.
- Monitor AWS billing and set a budget/alert.
- Avoid leaving unnecessary instances running.

Stopping the instance stops compute usage, although attached storage can still incur a small charge.

---

## 18. Current V3 Docker Images

The AWS deployment uses the finalized V3 Docker images:

```text
akhilbm/todo-backend:3.0
akhilbm/todo-frontend:3.1
```

These images are published to Docker Hub and can be pulled directly from the EC2 instance.

---

## 19. Deployment Flow Summary

```text
GitHub
   |
   v
Docker Images
   |
   v
Docker Hub
   |
   +-----------------------------+
   |                             |
   v                             v
Render                       AWS EC2
   |                             |
Frontend + Backend          Frontend + Backend
   |                             |
   +-------------+---------------+
                 |
                 v
        Supabase PostgreSQL
```

The application code and database remain the same. The deployment platform changes.

---

## 20. Screenshots to Add

Recommended screenshot order:

| File | What to capture |
|---|---|
| `aws-01-security-group.png` | EC2 Security Group inbound rules |
| `aws-02-ec2-instance.png` | Running EC2 instance |
| `aws-03-ssh.png` | Successful SSH connection |
| `aws-04-docker-installation.png` | Docker version + Compose version |
| `aws-05-docker-images.png` | Pulled V3 images |
| `aws-06-containers-running.png` | `docker ps` |
| `aws-07-health-check.png` | `/api/health` returning healthy |
| `aws-08-application.png` | Application running via EC2 public IP |

### Screenshot safety checklist

Before committing screenshots to GitHub:

- Hide `.env` values.
- Hide JWT secrets.
- Never show private key contents.
- Do not upload `.pem` files.
- Redact passwords and database credentials.
- Public IPs can be documented, but using `<EC2_PUBLIC_IP>` in documentation keeps the guide reusable.
