# 🚀 Jenkins Pipeline Using Docker Agent

## 📌 Project Overview

This project demonstrates how to configure **Jenkins to use Docker containers as build agents**.
Instead of running jobs on the Jenkins master node, the pipeline executes inside dynamically created Docker containers.

---

## 🎯 Objective

* Configure Jenkins with Docker integration
* Use Docker containers as Jenkins agents
* Run pipeline stages inside a containerized environment
* Enable parallel execution of stages

---

## 🛠️ Tools & Technologies

* Jenkins
* Docker
* AWS EC2 (Amazon Linux)
* Pipeline (Groovy)

---

## ⚙️ Architecture Diagram
    +----------------------+
    |    Jenkins Server    |
    |   (Master Node)      |
    +----------+-----------+
               |
               | Creates Agent
               ↓
    +----------------------+
    |   Docker Container   |
    | (Jenkins Agent)      |
    +----------+-----------+
               |
               ↓
    +----------------------+
    |   Pipeline Stages    |
    | (Executed Inside)    |
    +----------------------+

 ---   


## ⚙️ Setup Steps

### 1️⃣ Install Java

```bash
sudo yum install java-17-amazon-corretto -y
```

---

### 2️⃣ Install Jenkins

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo \
https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

sudo yum install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

---

### 3️⃣ Install Docker

```bash
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
```

---

### 4️⃣ Configure Permissions

```bash
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
```

---

### 5️⃣ Install Jenkins Plugins

* Blue Ocean
* Pipeline: Stage View Plugin
* Docker Pipeline
* Docker Plugin
  

---

### 6️⃣ Configure Docker Cloud in Jenkins

* Go to: **Manage Jenkins → Clouds → Add Docker**
* Docker Host URI:

```
unix:///var/run/docker.sock
```

---

### 7️⃣ Add Docker Agent Template

* Label: `docker-agent`
* Image: `jenkins/inbound-agent`
* Remote FS: `/home/jenkins/agent`

---

## 🧪 Pipeline Code

```groovy
pipeline {
    agent {
        label 'docker-agent'
    }

    stages {
        stage("Parallel Execution") {
            parallel {
                stage("Task 1") {
                    steps {
                        sh 'echo Running Task 1'
                    }
                }
                stage("Task 2") {
                    steps {
                        sh 'echo Running Task 2'
                    }
                }
            }
        }

        stage("Final Stage") {
            steps {
                sh 'echo Execution Complete'
            }
        }
    }
}
```

---

## 🔍 Output Verification

Run:

```bash
docker ps
```

Example output:

```
jenkins/inbound-agent   Up XX seconds
```

✔ This confirms:

* Docker container is created
* Pipeline is running inside container

---

## 🎯 Key Features

* Dynamic Docker agent creation
* Isolated build environment
* Parallel execution support
* No dependency on Jenkins master

---

## 💬 Conclusion

This setup ensures that Jenkins pipelines run in **containerized environments**, improving scalability, flexibility, and reliability of builds.

---

## 🔥 Author

Mahima Patel
