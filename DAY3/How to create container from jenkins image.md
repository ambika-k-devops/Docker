# how to create contianer from jenkins image

To **create a container from the Jenkins image**, follow these simple steps:

---

### ✅ Step-by-Step (Using Docker CLI)

#### 🔹 **1. Pull the Jenkins image (optional, auto-pulled on run)**

```bash
docker pull jenkins/jenkins:lts
```

#### 🔹 **2. Run the Jenkins container**

```bash
docker run -d \
  --name jenkins \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
```

---

### 🔍 Explanation of Options:

| Option                              | Meaning                                |
| ----------------------------------- | -------------------------------------- |
| `-d`                                | Run container in background (detached) |
| `--name jenkins`                    | Name the container `jenkins`           |
| `-p 8080:8080`                      | Expose Jenkins web UI on port 8080     |
| `-p 50000:50000`                    | For connecting agents/slaves           |
| `-v jenkins_home:/var/jenkins_home` | Save Jenkins data persistently         |

---

### 🚀 Access Jenkins

After container starts, open:

```
http://localhost:8080
```

Initial password (for first login):

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

---

Let me know if you want:

* Jenkins with plugins
* Docker-in-Docker for Jenkins
* Custom Jenkinsfile setup

I can guide you accordingly.
