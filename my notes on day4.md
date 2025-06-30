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
