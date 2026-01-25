<img width="1349" height="681" alt="image" src="https://github.com/user-attachments/assets/99b324e4-a2b5-4b4e-b23f-73f28e705fdb" />

<img width="1338" height="636" alt="image" src="https://github.com/user-attachments/assets/c3240a86-16b3-4dcf-bb25-6814cf891b90" />

<img width="1338" height="638" alt="image" src="https://github.com/user-attachments/assets/fbb71b89-44ec-4f9d-bae1-1be0448368ad" />

<img width="1346" height="681" alt="image" src="https://github.com/user-attachments/assets/f2412fcc-a85f-4594-a89c-ceadfcd6e5c3" />

<img width="1353" height="640" alt="image" src="https://github.com/user-attachments/assets/8a19d161-77fb-4586-b50d-338112d10763" />

<img width="1348" height="625" alt="image" src="https://github.com/user-attachments/assets/c793446f-1811-48c6-8b46-95b2c1bb9277" />

<img width="1353" height="663" alt="image" src="https://github.com/user-attachments/assets/6e060c65-ee21-4514-95dc-19c6db5ff7d3" />

# Prerequisites
#
- JDK 11 
- Maven 3 
- MySQL 8

# Technologies 
- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- Tomcat
- MySQL
- Memcached
- Rabbitmq
- ElasticSearch
# Database
Here,we used Mysql DB 
sql dump file:
- /src/main/resources/db_backup.sql
- db_backup.sql file is a mysql dump file.we have to import this dump to mysql db server
- > mysql -u <user_name> -p accounts < db_backup.sql


Perfect! Based on all the data you’ve shared — your project includes **Docker multi-stage builds, a multi-tier architecture (App, DB, Cache, MQ, Web), Kubernetes manifests, and Ingress setup** — I’ve drafted a **comprehensive `README.md`** for your GitHub repository. You can copy this as-is and tweak if needed.

---

```markdown
# Kubernetes Multi-Tier Application: VProfile

## Overview

**VProfile** is a multi-tier web application built using **Java (Spring/Maven)**, containerized with **Docker**, and orchestrated using **Kubernetes**. This project demonstrates a full-stack deployment including:

- **Application tier** – Tomcat running the Java WAR file
- **Database tier** – MySQL
- **Cache tier** – Memcached
- **Message Queue** – RabbitMQ
- **Web tier / Frontend** – Nginx
- **Ingress** – For routing external traffic

The project uses **multi-stage Docker builds** to optimize image size and **Kubernetes manifests** for deployments, services, volumes, and ingress routing.

---

## Project Structure

```

Kube-Project/
│
├── Docker-files/
│   ├── app/                  # Application Dockerfile (multi-stage)
│   ├── db/                   # MySQL Dockerfile
│   ├── web/                  # Nginx Dockerfile
│
├── kubedefs/                 # Kubernetes manifests
│   ├── appdeploy.yaml        # Deployment for application tier
│   ├── dbdeploy.yaml         # Deployment for database tier
│   ├── cachedeploy.yaml      # Deployment for Memcached
│   ├── mqdeploy.yaml         # Deployment for RabbitMQ
│   ├── appingress.yaml       # Ingress resource
│   ├── services.yaml         # Services for all tiers
│
├── src/                      # Java application source code
├── target/                   # Maven build output
├── pom.xml                   # Maven project file
├── docker-compose.yml        # Local Docker Compose setup
├── Jenkinsfile               # Optional CI/CD pipeline
└── README.md                 # Project documentation

````

---

## Prerequisites

- **Docker** >= 20.x
- **Docker Compose** >= 2.x
- **Minikube / Kind / AWS EKS** for Kubernetes
- **kubectl** CLI
- **Helm** (optional, if using charts)
- **Git** configured with SSH

---

## Docker Setup

### Build all Docker images

```bash
# Build locally using Docker Compose
docker compose build
````

### Run locally with Docker Compose

```bash
docker compose up -d
```

* App runs on: `http://localhost:8080`
* Web (Nginx) runs on: `http://localhost:80`


## Kubernetes Setup

### Apply Kubernetes resources

```bash
# Create namespaces (if needed)
kubectl create namespace vprofile

# Apply deployments
kubectl apply -f kubedefs/

# Check pods
kubectl get pods

# Check services
kubectl get svc

# Check ingress
kubectl get ingress
```

### Ingress Access without DNS

If you don’t have a domain:

1. Use the **external IP** of your ingress controller’s LoadBalancer:

```bash
kubectl get svc -n ingress-nginx
```

2. Open the URL in browser:

```
http://<EXTERNAL-IP>/
```

> Example: `http://aa995e5023b354ce4ab1d6f601956b33-bfa3b4ee87c7dace.elb.us-east-1.amazonaws.com`

---

## Application Architecture

* **vproapp** – Tomcat application container hosting `vprofile-v2.war`
* **vprodb** – MySQL database container
* **vprocache01** – Memcached caching layer
* **vpromq01** – RabbitMQ messaging
* **vproweb** – Nginx container for frontend and reverse proxy
* **Ingress** – Routing external traffic to `vproapp-service`

**Volumes:**

* `vprodbdata` – Persistent volume for MySQL data
* `vproappdata` – Persistent volume for application webapps

---

## Multi-stage Dockerfile

The application Dockerfile uses **Maven build stage** to compile the WAR and **Tomcat runtime stage** to run it:

```dockerfile
FROM maven:3.9.9-eclipse-temurin-21-jammy AS BUILD_IMAGE
RUN git clone https://github.com/hkhcoder/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install

FROM tomcat:10-jdk21
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]
```

---

## Push Docker Images to Registry

```bash
# Login to your registry
docker login <your-registry>

# Tag image
docker tag misterj25/vprofileapp <your-registry>/vprofileapp:latest

# Push image
docker push <your-registry>/vprofileapp:latest
```

## GitHub Repository

This project is configured to be pushed via SSH:

```bash
# Add SSH remote
git remote set-url origin git@github.com:Iam-Javed/Kubernetes-multi-tier-app.git

# Push to GitHub
git push -u origin main
```

## Notes

* Ensure all Kubernetes `Service` names match your **Deployment** `initContainers` for proper DNS resolution.
* The `imagePullPolicy: Always` ensures latest Docker images are pulled when deploying to K8s.
* Remove obsolete `version` from Docker Compose YAML to avoid warnings.

## Author

**Javed Shaik**
VProfile Project | Kubernetes | Docker | Java | DevOps



