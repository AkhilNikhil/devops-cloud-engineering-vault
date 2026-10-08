# 📝 docker exp

```text
docker exp


/*

# Docker on EC2 - Step by Step Summary

---

## 1. Apache HTTPD Container

### Dockerfile

```dockerfile
FROM httpd:latest
COPY ./index.html /usr/local/apache2/htdocs/
EXPOSE 80
```

### index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Docker Web Page</title>
</head>
<body>
    <h1>Hello from Docker + Apache!</h1>
    <p>Your container is running successfully 🚀</p>
</body>
</html>
```

### Build & Run

```bash
docker build -t myhttpd .
docker run -d -p 8080:80 --name cmyhttpd myhttpd
```

### Notes

* Test inside EC2: `curl localhost:8080`
* Open in browser: `http://<EC2-PUBLIC-IP>:8080`
* Ensure Security Group allows **port 8080** inbound.

---

## 2. Nginx Container

### Dockerfile

```dockerfile
FROM nginx:latest
COPY ./index.html /usr/share/nginx/html/
EXPOSE 80
```

### index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Nginx Docker Page</title>
</head>
<body>
    <h1>Hello from Docker + Nginx!</h1>
    <p>Your Nginx container is running successfully 🚀</p>
</body>
</html>
```

### Build & Run

```bash
docker build -t mynginx .
docker rm -f cnginx   # remove old container if exists
docker run -d -p 8081:80 --name cnginx mynginx
```

### Notes

* Test inside EC2: `curl localhost:8081`
* Browser access: `http://<EC2-PUBLIC-IP>:8081`
* Security Group: allow **port 8081** inbound.

---

## 3. Tomcat Container

### Dockerfile

```dockerfile
FROM tomcat:9.0
COPY ./index.html /usr/local/tomcat/webapps/ROOT/index.html
EXPOSE 8080
```

### index.html

```html
<!DOCTYPE html>
<html>
<head>
    <title>Tomcat Docker Page</title>
</head>
<body>
    <h1>Hello from Docker + Tomcat!</h1>
    <p>Your Tomcat container is running successfully 🚀</p>
</body>
</html>
```

### Build & Run

```bash
docker build -t mytomcat .
docker run -d -p 8082:8080 --name cmytomcat mytomcat
```

### Notes

* Test inside EC2: `curl localhost:8082`
* Browser access: `http://<EC2-PUBLIC-IP>:8082`
* Security Group: allow **port 8082** inbound.
* Important: Map host port to container 8080 because Tomcat listens on 8080 by default.

---

## 4. General Notes

* Always check **Security Group** inbound rules for the ports you use.
* Use `docker ps` to check running containers.
* Use `docker logs <container_name>` for debugging.
* Multiple containers (Apache, Nginx, Tomcat) can run on **different ports** on same EC2.
* Folder structure recommendation:

```
project/
 ├── apache/
 │    ├── Dockerfile
 │    └── index.html
 ├── nginx/
 │    ├── Dockerfile
 │    └── index.html
 └── tomcat/
      ├── Dockerfile
      └── index.html
```

*/

```
