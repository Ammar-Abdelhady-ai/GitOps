# 🚀 vProfile Application Deployment

<div align="center">

![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring](https://img.shields.io/badge/Spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=apache-maven&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=for-the-badge&logo=helm&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=jenkins&logoColor=white)
![SonarQube](https://img.shields.io/badge/SonarQube-4E9BCD?style=for-the-badge&logo=sonarqube&logoColor=white)

**Full-Stack Application Deployment with CI/CD Pipelines**

[Repository](https://github.com/Ammar-Abdelhady-ai/GitOps) • [Issues](https://github.com/Ammar-Abdelhady-ai/GitOps/issues) • [Wiki](https://github.com/Ammar-Abdelhady-ai/GitOps/wiki)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Application Architecture](#-application-architecture)
- [Technology Stack](#-technology-stack)
- [CI/CD Pipelines](#-cicd-pipelines)
  - [GitHub Actions](#-github-actions)
  - [Jenkins](#-jenkins)
- [Deployment Components](#-deployment-components)
  - [Helm Charts](#-helm-charts)
  - [Kubernetes Manifests](#-kubernetes-manifests)
- [Prerequisites](#-prerequisites)
- [Build & Deploy](#-build--deploy)
- [Quality Assurance](#-quality-assurance)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Overview

The **Deployment Branch** contains the complete application source code and deployment configurations for the **vProfile** project. It integrates a robust CI/CD workflow that builds Java/Spring microservices, containerizes them with Docker, and deploys them to AWS EKS using Helm.

---

## 🏛️ Application Architecture

The vProfile application consists of multiple microservices interacting with data services.

```mermaid
graph TD
    User((User)) -->|Ingress| LB[Load Balancer]
    LB --> FE[Front End<br/>(Tomcat/Java)]
    FE -->|API| BE[Back End Services]
    BE -->|Cache| Memcache[Memcached]
    BE -->|Queue| RMQ[RabbitMQ]
    BE -->|Data| DB[(MySQL Database)]
    
    style FE fill:#6DB33F
    style DB fill:#4479A1
    style Memcache fill:#A32D2E
    style RMQ fill:#FF6600
```

---

## 🛠️ Technology Stack

| Component | Technology | Description |
|-----------|-----------|-------------|
| **Backend** | Java 11 / Spring Boot | Core application logic (Spring MVC, Security, Data JPA) |
| **Database** | MySQL 8 | Relational database for user data |
| **Caching** | Memcached | In-memory caching for performance |
| **Messaging** | RabbitMQ | Message broker for asynchronous tasks |
| **Build Tool** | Apache Maven | Dependency management and build automation |
| **Container** | Docker | Application containerization |
| **Packaging** | Helm | Kubernetes package management |
| **CI Server** | Jenkins / GitHub Actions | Automated build and deployment pipelines |
| **Code Quality** | SonarQube | Static code analysis and security scanning |

---

## 🔄 CI/CD Pipelines

This project supports two CI/CD strategies.

### **🚀 GitHub Actions Workflow**

Configuration: `.github/workflows/deployment.yml`

1. **Test**: Unit tests + SonarQube Analysis
2. **Build**: Maven build + Docker image creation
3. **Publish**: Push Docker image to AWS ECR
4. **Deploy**: Update Helm release on EKS cluster

### **👔 Jenkins Pipeline**

Configuration: `Jenkinsfile`

1. **Build**: `mvn clean install`
2. **Unit Test**: `mvn test`
3. **Integration Test**: `mvn verify`
4. **Analysis**: Checkstyle + SonarQube
5. **Publish**: Artifact upload to Nexus Repository

---

## 🏗️ Deployment Components

### **Helm Charts**

Located in `helm/vprofilecharts/`, our charts manage:

- **Deployment**: ReplicaSets and Pod templates
- **Service**: ClusterIP and LoadBalancer definitions
- **Ingress**: NGINX Ingress rules
- **ConfigMap/Secrets**: Environment configuration

### **Kubernetes Manifests**

Raw manifests in `kubernetes/` for manual deployment or debugging:

- `vproappdep.yml`: Main application deployment
- `vprodbdep.yml`: Database statefulset/deployment
- `vpro-ingress.yaml`: Ingress routing

---

## ✅ Prerequisites

To build and deploy the application locally or via CI:

- **JDK 11**: Required for building source code
- **Maven 3**: Build tool
- **Docker**: For container operations
- **kubectl**: For cluster interaction
- **Helm 3**: For chart deployment

---

## 🚀 Build & Deploy

### **1. Build Local Artifact**

```bash
mvn clean install
```
*Creates `target/vprofile-v2.war`*

### **2. Build Docker Image**

```bash
docker build -t vprofileapp:latest .
```

### **3. Deploy with Helm**

```bash
helm install vprofile-stack ./helm/vprofilecharts \
  --set appimage=vprofileapp \
  --set apptag=latest
```

### **4. Verify Deployment**

```bash
kubectl get pods
# Wait for status 'Running'
```

---

## 🛡️ Quality Assurance

### **SonarQube Integration**

To run code analysis locally:

```bash
mvn sonar:sonar \
  -Dsonar.projectKey=vprofile \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=<token>
```

### **Secrets Management**

Ensure the following secrets are configured in GitHub/Jenkins:

- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `REGISTRY` (ECR URL)
- `SONAR_TOKEN`

---

## 🔧 Troubleshooting

<details>
<summary><b>Database Connection Failed</b></summary>
Check if `db-CIP` service is running and MySQL pod is ready. Verify credentials in `application.properties`.
</details>

<details>
<summary><b>Maven Build Fails</b></summary>
Ensure JDK 11 is selected: `java -version`. Clear local repository: `rm -rf ~/.m2/repository`.
</details>

<details>
<summary><b>Helm Deployment Error</b></summary>
Run with debug/dry-run: `helm install --debug --dry-run ...` to see rendered templates.
</details>

---

## 🤝 Contributing

1. **Fork** the repository.
2. **Clone** `deployment` branch.
3. **Create** feature branch.
4. **Commit** & **Push**.
5. **Open PR**.

---

## 📄 License

This project is licensed under the MIT License.
