# DOCKER REVISION CLASS

## Part 1

- What is docker?
- Before Docker and After Docker?
- Containerization vs Virtualization?
- Docker Architecture?
- Docker Flow
- Docker Installation
- Docker Image Related Commands
- Docker Container Related Commands

---

## Practical Session to Understand Docker

### Step 1: Check Docker Installation

### Step 2: Clone the Project
```sh
git clone https://github.com/kkeducation12345/maven-web-app-project-kk-funda.git
cd maven-web-app-project-kk-funda
```

### Step 3: Install Maven & Java
```sh
sudo apt install maven -y
java --version
mvn -version
```

### Step 4: Build the Artifact
```sh
mvn clean package
```

Maven Plugin Configuration:
```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-war-plugin</artifactId>
      <version>3.3.2</version>
    </plugin>
  </plugins>
</build>
```

### Step 5: Create Dockerfile and Build Image
```Dockerfile
FROM tomcat:8.0.21-jre8
COPY target/maven-web-application.war /usr/local/tomcat/webapps/maven-web-application.war
```
```sh
docker build -t kkeducation12345/java-web-app .
```

### Step 6: List Docker Images
```sh
docker images
```

### Step 7: Push to Docker Hub
```sh
docker login -u kkeducation12345 -p password
docker push kkeducation12345/java-web-app
```

### Step 8: Run Container from Image
```sh
docker run -d -p 8080:8080 --name javawebapp kkeducation12345/java-web-app
```

### Step 9: Access the Application
```sh
docker ps -a
```

### Go Inside the Container
```sh
docker exec -it javawebapp /bin/bash
```

---

## Commands

### Docker Info
```sh
docker info
docker --version
```

### Image Related Commands

#### Build Image
```sh
docker build -t <image> <context>
docker build -t kkeducation123456/java-web-app:1 .
docker build -f customName kkeducation123456/java-web-app:1 .
```

#### List Images
```sh
docker images
docker image ls
```

#### Docker Hub Login
```sh
docker login -u <username> -p <password>
cat password | docker login -u <username> --password-stdin
docker logout
docker info
```

#### Push/Pull Image
```sh
docker push <image>
docker pull <image>
```

#### Inspect Image
```sh
docker image inspect <image>
docker history <image>
```

#### Delete Images
```sh
docker rmi <image>
docker rmi <image1> <image2>
docker rmi -f $(docker images -qa)
```

#### Dangling Images
```sh
docker images -f dangling=true
docker rmi -f $(docker images -q -f dangling=true)
```

#### System Cleanup
```sh
docker system prune
docker image prune
docker container prune
docker network prune
docker volume prune
```

#### Tagging Images
```sh
docker tag <existing_image> <new_tag>
```

#### Disk Usage
```sh
docker system df
```

#### Save and Load Image (Move Server to Server)
```sh
docker save -o filename.tar <image>
scp filename.tar user@host:/path
docker load -i filename.tar
```

---

## Container Commands

### Create Containers
```sh
docker create -p 8080:8080 --name javawebapp kkeducation12345/java-web-app
docker run -d -p 8080:8080 --name javawebapp1 kkeducation12345/java-web-app
```

### List Containers
```sh
docker ps
docker ps -a
```

### Start/Stop Containers
```sh
docker start <cid>
docker stop <cid>
```

### Delete Containers
```sh
docker rm <cid>
docker rm -f <cid>
docker rm -f $(docker ps -q)
docker rm -f $(docker ps -aq)
docker container prune
docker rm -f $(docker ps --filter status="exited" -aq)
```

### Rename & Restart
```sh
docker rename <old_name> <new_name>
docker restart <cid>
```

### Pause/Unpause
```sh
docker pause <cid>
docker unpause <cid>
docker rm -f $(docker ps --filter status="paused")
```

---

### Interactive Mode
```sh
docker run -it --name test ubuntu /bin/bash
```

### Debugging
```sh
docker logs <cid>
docker logs --tail <n> <cid>
docker logs -f <cid>
```

### Go Inside Running Container
```sh
docker exec -it <cid> /bin/bash
docker exec <cid> ls
docker top <cid>
```

### Stats and Resource Usage
```sh
docker stats <cid>
docker run --memory="512m" -d -p 8082:8080 --name javawebapp2 kkeducation12345/java-web-app
```

### Copy Files
```sh
docker cp <container>:<path> <local_path>
docker cp <local_file> <container>:<path>
```

### COPY vs docker cp
- **COPY**: Dockerfile instruction, used during image build
- **docker cp**: CLI command, for live containers

### Docker Diff
```sh
docker diff <cid>
```

### Docker Commit
```sh
docker commit <cid> <new_image>
```

---

## Inspect Container
```sh
docker inspect <cid>
docker inspect --format "{{.NetworkSettings.IPAddress}}" <cid>
docker inspect --format "{{.State.Pid}}" <cid>
docker inspect --format "IP Address: {{.NetworkSettings.Networks.bridge.IPAddress}}, Name: {{.Name}}" <cid>
```

---

## Interview Questions (IQ)

- What is the difference between `docker create` and `docker run`?
- What is port publishing or port mapping in Docker?
- What is the difference between `docker stop` and `docker kill`?
- Can memory be limited for containers?
- What is the difference between COPY and docker cp?
  Sure Ambika! Here's a **simple, clear, and interview-friendly explanation** for each of your questions:

---

### ❓1. What is the difference between `docker create` and `docker run`?

✅ **Answer:**

* `docker create`: Only **creates** a container but does **not start** it.
* `docker run`: **Creates and starts** the container immediately.

📌 Example:

```bash
docker create ubuntu         # creates container
docker run ubuntu            # creates + starts container
```

---

### ❓2. What is port publishing or port mapping in Docker?

✅ **Answer:**
Port mapping is used to **expose container ports** to the host machine so you can **access the container app from outside**.

📌 Example:

```bash
docker run -p 8080:80 nginx
```

This maps:

* `80` (inside container) → `8080` (on host)
  So you can open `http://localhost:8080` to access the container.

---

### ❓3. What is the difference between `docker stop` and `docker kill`?

✅ **Answer:**

* `docker stop`: Sends a **graceful shutdown (SIGTERM)**, then **SIGKILL** after timeout.
* `docker kill`: Immediately sends **SIGKILL**, no waiting.

📌 Think of it like:

* `stop` = “Request to stop”
* `kill` = “Force stop now”

---

### ❓4. Can memory be limited for containers?

✅ **Answer:**
Yes, you can **set memory limits** using `--memory` flag.

📌 Example:

```bash
docker run --memory="512m" myapp
```

This ensures the container uses **max 512MB RAM**.
If it exceeds, Docker may **kill** it with `OOMKilled` status.

---

### ❓5. What is the difference between `COPY` and `docker cp`?

✅ **Answer:**

| Feature   | COPY (Dockerfile)           | docker cp (CLI)                     |
| --------- | --------------------------- | ----------------------------------- |
| Usage     | Used **during image build** | Used **after container is running** |
| Direction | From **host → image**       | From **host ↔ container**           |
| When used | In `Dockerfile`             | In command line (`docker cp`)       |

📌 Summary:

* `COPY` = build-time copy into image
* `docker cp` = runtime copy to/from container

---
# Dangling Image
Great question, Ambika! Let’s break this down clearly:

---

### 🔥 **Why `docker rmi -f <IMAGE ID>` didn't work**

```bash
docker rmi -f 7c163b877990
```

➡️ **Error:**

```
conflict: unable to delete 7c163b877990 (cannot be forced) - image is being used by running container 6be86b81285e
```

#### 🧠 **Explanation:**

Even though you used `-f` (force), **Docker does not remove images that are actively in use by running containers** — regardless of whether you use the **image ID** or the **image name**.

In your case:

* `7c163b877990` is the image **ID**.
* It's being used by **container `6be86b81285e`** which is still **running**.

So Docker **protects you** from breaking a running container by not deleting its base image.

---

### ✅ **Why `docker rmi -f ambikadevops/mavenwebapp:1.0.2` worked**

```bash
docker rmi -f ambikadevops/mavenwebapp:1.0.2
```

➡️ This removed **only the tags (name references)**, not the actual image binary (ID).

So even though the **tag** is removed:

* The **image ID** (e.g., `7c163b877990`) is still present in the system.
* It’s just now labeled as `<none>:<none>`, which means **dangling image**.

This is why it looks like only the name worked — but in fact:

> **Docker allowed untagging the image name, but still didn’t remove the image binary because a running container is using it.**

---

### 🧪 To fully delete the image:

You **must first stop and remove the container** using it:

```bash
docker stop 6be86b81285e
docker rm 6be86b81285e
docker rmi -f 7c163b877990
```

---

### 🧠 Summary

| Action                             | What happens                                                                     |
| ---------------------------------- | -------------------------------------------------------------------------------- |
| `docker rmi -f <image-name>`       | Removes the tag reference (untagging). If image is still in use, binary stays.   |
| `docker rmi -f <image-id>`         | Fails if container is running, even with `-f`. Must stop/remove container first. |
| Running container                  | Prevents actual image deletion                                                   |
| `<none>:<none>` in `docker images` | Means image is dangling (no tag) but still used somewhere (or orphaned)          |

---

Let me know if you want a diagram or a cheat sheet for image removal and cleanup commands!

