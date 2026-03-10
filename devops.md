# 🔧 DevOps — Interview Questions & Answers

> Top DevOps interview questions with answers and code/command examples.
> Source: [Intellipaat — DevOps Interview Questions](https://intellipaat.com/blog/interview-question/devops-interview-questions/)

---

### Q1. What is DevOps?

**DevOps** is a culture and set of practices that brings together **Development** and **Operations** teams to automate and integrate the software delivery process. It emphasizes CI/CD, automation, monitoring, and collaboration.

---

### Q2. CI/CD Pipeline

| Concept                         | Description                                                     |
| ------------------------------- | --------------------------------------------------------------- |
| **CI** (Continuous Integration) | Developers frequently merge code; automated builds & tests      |
| **CD** (Continuous Delivery)    | Code is always deployment-ready; manual approval for production |
| **CD** (Continuous Deployment)  | Every change automatically deployed to production               |

```yaml
# Example: GitHub Actions CI/CD
name: CI/CD Pipeline
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm install
      - run: npm test
      - run: npm run build
  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying to production..."
```

---

### Q3. DevOps vs Agile

| Feature    | DevOps                   | Agile                  |
| ---------- | ------------------------ | ---------------------- |
| Focus      | Development + Operations | Development + Customer |
| Goal       | Continuous delivery      | Iterative development  |
| Feedback   | From monitoring/ops      | From customers         |
| Automation | Primary focus            | Not primary            |

---

### Q4. Infrastructure as Code (IaC)

```hcl
# Terraform example
resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "WebServer"
  }
}
```

```yaml
# Ansible playbook
- hosts: webservers
  become: yes
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
    - name: Start nginx
      service:
        name: nginx
        state: started
```

---

### Q5. Containers vs Virtual Machines

| Feature   | Containers        | Virtual Machines |
| --------- | ----------------- | ---------------- |
| OS        | Share host kernel | Full guest OS    |
| Size      | MBs               | GBs              |
| Startup   | Seconds           | Minutes          |
| Isolation | Process-level     | Hardware-level   |

```dockerfile
# Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

```bash
# Docker commands
docker build -t myapp .
docker run -d -p 3000:3000 myapp
docker ps
docker logs <container_id>
docker stop <container_id>
```

---

### Q6. Git — Version Control

```bash
# Branch management
git checkout -b feature/login
git add .
git commit -m "Add login feature"
git push origin feature/login

# Merge vs Rebase
git merge feature/login   # Creates merge commit
git rebase main            # Replays commits on top of main

# Resolve merge conflicts
git merge feature-branch
# Fix conflicts in files, then:
git add .
git commit

# Revert a bad commit
git revert <commit_hash>   # Creates new commit undoing changes
git reset --hard <commit>  # Destructive — removes commits

# Squash last 3 commits
git rebase -i HEAD~3  # Then change 'pick' to 'squash'
```

---

### Q7. Jenkins Pipeline

```groovy
// Jenkinsfile (Declarative Pipeline)
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            when { branch 'main' }
            steps {
                sh 'npm run deploy'
            }
        }
    }
    post {
        failure {
            mail to: 'team@company.com', subject: 'Build Failed!'
        }
    }
}
```

---

### Q8. Kubernetes Basics

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
        - name: web
          image: myapp:latest
          ports:
            - containerPort: 3000
---
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  type: LoadBalancer
  selector:
    app: web
  ports:
    - port: 80
      targetPort: 3000
```

```bash
kubectl apply -f deployment.yaml
kubectl get pods
kubectl get services
kubectl scale deployment web-app --replicas=5
kubectl logs <pod-name>
```

---

### Q9. Monitoring & Logging

| Tool           | Purpose                                          |
| -------------- | ------------------------------------------------ |
| **Prometheus** | Metrics collection and alerting                  |
| **Grafana**    | Visualization dashboards                         |
| **ELK Stack**  | Elasticsearch + Logstash + Kibana (log analysis) |
| **Datadog**    | Full-stack monitoring                            |
| **Nagios**     | Infrastructure monitoring                        |
| **PagerDuty**  | Incident management                              |

---

### Q10. DevOps KPIs

| KPI                      | Description                       |
| ------------------------ | --------------------------------- |
| **Deployment Frequency** | How often code is deployed        |
| **Lead Time**            | Commit to production time         |
| **MTTR**                 | Mean Time to Recovery             |
| **Change Failure Rate**  | % of deployments causing failures |

---

### Q11. Security in DevOps (DevSecOps)

- **Shift-left security**: Integrate security early in the pipeline
- **SAST/DAST**: Static & Dynamic Application Security Testing
- Container scanning (Trivy, Snyk)
- Secret management (Vault, AWS Secrets Manager)
- RBAC in Kubernetes

---

### Q12. Configuration Management Tools

| Tool          | Language   | Architecture    | Key Feature                |
| ------------- | ---------- | --------------- | -------------------------- |
| **Ansible**   | YAML       | Agentless (SSH) | Simple, no agent needed    |
| **Chef**      | Ruby       | Client-Server   | Code-based "recipes"       |
| **Puppet**    | Puppet DSL | Client-Server   | Declarative, mature        |
| **Terraform** | HCL        | Agentless       | IaC for cloud provisioning |

---
