## give me fully featured .md file for all these commands and give me at the end to remembering tip, and few examples, and please dont remove the existing the commands, they are very important to be in this file:
# 🚢 Docker Container Commands Guide

---

## 🛠️ How to Create a Container?

* `docker create` → *Creates* a container (does **not start** it)
* `docker run` → *Creates and starts* the container

```bash
docker create -p 8080:8080 --name javawebapp kkeducation12345/java-web-app
docker start javawebapp
docker run -d -p 8080:8080 --name javawebapp1 kkeducation12345/java-web-app
```

---

## 📋 How to List Containers?

* `docker ps` or `docker container ls` → Running containers
* `docker ps -a` or `docker container ls -a` → All containers

---

## 🔁 Start, Stop, Delete Containers

* Start: `docker start <cid>`
* Stop: `docker stop <cid>`
* Delete stopped: `docker rm <cid>`
* Delete running: `docker rm -f <cid>`
* Delete all running: `docker rm -f $(docker ps -q)`
* Delete all: `docker rm -f $(docker ps -aq)`

---

## 🧹 Clean Up Containers

* Remove only stopped: `docker container prune`
* Remove exited: `docker rm -f $(docker ps --filter status="exited" -aq)`

---

## 🏷️ Rename & Restart

* Rename: `docker rename <cid/name> <new name>`
* Restart: `docker restart <cid/cname>`

---

## ❓ Interview Questions

* **Docker create vs run?**

  * `create`: only creates
  * `run`: creates & starts

* **What is port mapping?**

  * Maps container ports to host: `-p hostPort:containerPort`

* **docker stop vs kill?**

  * `stop`: graceful shutdown (SIGTERM → SIGKILL)
  * `kill`: immediate (SIGKILL)

---

## ⏸️ Pause / Unpause Containers

```bash
docker pause <cid/cname>
docker unpause <cid/cname>
docker rm -f $(docker ps --filter status="paused")
```

---

## 🧪 Test: Ubuntu Example

```bash
docker run --name ubuntucontainer ubuntu
docker ps -a
docker start ubuntucontainer
```

---

## 👨‍💻 Interactive Container (Shell Access)

```bash
docker run -it --name test ubuntu /bin/bash
```

---

## 🧰 Debugging & Logs

```bash
docker logs <cid/cname>
docker logs --tail 10 <cid/cname>
docker logs -f <cid/cname>
```

---

## 🕵️‍♂️ Exec & Inspect Running Container

```bash
docker exec -it <cid/name> /bin/bash
docker exec <cid> ls
docker top <cid/cname>
docker stats <cid/cname>
```

---

## 💾 Allocate Memory to Container

```bash
docker run --memory="512m" -d -p 8082:8080 --name javawebapp2 kkeducation12345/java-web-app:1
```

* Too low memory (e.g. `64m`) may lead to: `OOMKilled`

---

## 📁 File Copying: `docker cp` vs `COPY`

### ✅ `COPY` (Dockerfile Instruction)

* Used **during image build**.
* Adds files to image.

```dockerfile
COPY demo.txt /app/
```

### ✅ `docker cp` (CLI Command)

* Used **after container is running**.
* Copy files to/from container at runtime.

```bash
docker cp demo.txt mycontainer:/app/
docker cp mycontainer:/app/file.txt ./
```

### 💡 Remember:

> 📦 `COPY` = Build time  |  📂 `docker cp` = Runtime

---

## 🕵️‍♀️ docker diff

* `docker diff <cid>` → Shows container file changes since creation

---

## 🧱 docker commit

* `docker commit <cid> image_name:tag`
* Saves current container state as an image

```bash
docker commit mycontainer myimage:1.0
```

---

## 🔍 Inspect Container

```bash
docker inspect <cid/cname>
docker inspect --format "{{.NetworkSettings.IPAddress}}" mavenapp
docker inspect --format "{{.State.Pid}}" <cid>
docker inspect --format "IP: {{.NetworkSettings.Networks.bridge.IPAddress}}, Name: {{.Name}}" mavenapp
```

---

## 🧠 Final Tip for Memory 🧠

```
📦 COPY = image build (Dockerfile)
📂 docker cp = after container is running (CLI)
🚦 stop vs kill = graceful vs immediate
```
