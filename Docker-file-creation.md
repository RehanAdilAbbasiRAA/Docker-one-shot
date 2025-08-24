
# 🚀 Docker Setup Guide

This guide explains step-by-step how to create a `Dockerfile` and build/run your application in a container.  
We’ll use **Node.js** as an example, but the same steps apply for Python, Java, Go, etc.

---

## 1️⃣ Create a Dockerfile

Create a file named **`Dockerfile`** (capital **D**, no extension).

### Example: Node.js Application

```dockerfile
# 1. Base image (this can be Node, Python, Java, etc.)
FROM node:18

# 2. Environment variables (default MongoDB credentials)
ENV MONGO_INITDB_ROOT_USERNAME=admin
ENV MONGO_INITDB_ROOT_PASSWORD=qwerty

# 3. Create a directory inside the container
RUN mkdir /testapp

# 4. Copy everything from current folder → container’s /testapp
COPY . /testapp

# 5. Set working directory (optional but cleaner)
WORKDIR /testapp

# 6. Command to run your app (in array form)
CMD ["node", "/testapp/server.js"]


















Example: Python Application
FROM python:3.11

ENV MONGO_INITDB_ROOT_USERNAME=admin
ENV MONGO_INITDB_ROOT_PASSWORD=qwerty

RUN mkdir /testapp

COPY . /testapp

WORKDIR /testapp

CMD ["python", "/testapp/app.py"]

Example: Java Application
FROM openjdk:17

ENV MONGO_INITDB_ROOT_USERNAME=admin
ENV MONGO_INITDB_ROOT_PASSWORD=qwerty

RUN mkdir /testapp

COPY . /testapp

WORKDIR /testapp

CMD ["java", "-jar", "/testapp/app.jar"]

2️⃣ Build the Docker Image

Run this command inside the folder that has your Dockerfile:

docker build -t my-app .


-t my-app → tags your image with the name my-app

. → tells Docker to use the current directory as build context

3️⃣ Run the Container
docker run -d -p 3000:3000 --name my-container my-app


-d → detached mode (runs in background)

-p 3000:3000 → maps container port 3000 → host port 3000

--name my-container → names the container

my-app → the image you just built

4️⃣ Verify It’s Running

Check running containers:

docker ps


Check logs:

docker logs my-container

5️⃣ Stop & Remove
docker stop my-container
docker rm my-container
docker rmi my-app

🔑 Notes

FROM can be Node, Python, Java, Go, etc. depending on your project.

ENV sets environment variables inside the container.

RUN executes commands at build time.

COPY copies your project files into the container.

CMD specifies the default command to run when the container starts.