<img width="1349" height="681" alt="image" src="https://github.com/user-attachments/assets/99b324e4-a2b5-4b4e-b23f-73f28e705fdb" />

<img width="1338" height="636" alt="image" src="https://github.com/user-attachments/assets/c3240a86-16b3-4dcf-bb25-6814cf891b90" />

<img width="1338" height="638" alt="image" src="https://github.com/user-attachments/assets/fbb71b89-44ec-4f9d-bae1-1be0448368ad" />

<img width="1346" height="681" alt="image" src="https://github.com/user-attachments/assets/f2412fcc-a85f-4594-a89c-ceadfcd6e5c3" />

<img width="1353" height="640" alt="image" src="https://github.com/user-attachments/assets/8a19d161-77fb-4586-b50d-338112d10763" />

<img width="1348" height="625" alt="image" src="https://github.com/user-attachments/assets/c793446f-1811-48c6-8b46-95b2c1bb9277" />

<img width="1353" height="663" alt="image" src="https://github.com/user-attachments/assets/6e060c65-ee21-4514-95dc-19c6db5ff7d3" />

# Prerequisites
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


# VProfile: Multi-Tier Kubernetes Application

## Overview

**VProfile** is a full-stack web application demonstrating a **multi-tier architecture** deployed using **Docker** and **Kubernetes**.  

It includes:  
- **Application Tier** – Java web app running on Tomcat  
- **Database Tier** – MySQL  
- **Cache Tier** – Memcached  
- **Message Queue** – RabbitMQ  
- **Web Tier** – Nginx for frontend and reverse proxy  
- **Ingress** – Handles routing external traffic to the application  

This project is ideal for learning **containerization**, **orchestration**, and **Kubernetes basics**.


## Project Structure

Kube-Project/

├── Docker-files/ # Dockerfiles for each tier

├── kubedefs/ # Kubernetes deployment, services, ingress

├── src/ # Java application source code

├── target/ # Compiled application (WAR file)

├── pom.xml # Maven project file

├── docker-compose.yml # Local Docker Compose setup

└── README.md # Project documentation


## Key Concepts

1. **Docker**: Containerizes each component (app, database, cache, web).  
2. **Multi-stage builds**: Compile Java app in one image, run it in Tomcat image for smaller size.  
3. **Kubernetes**: Orchestrates deployment, scaling, and networking of all containers.  
4. **Ingress**: Exposes the application externally without needing a domain name.  


## How to Run

### Using Docker Compose (Local Testing)

docker compose build
docker compose up -d
Access the app at http://localhost:8080

Nginx frontend at http://localhost:80

## Using Kubernetes

kubectl apply -f kubedefs/

kubectl get pods

kubectl get svc

kubectl get ingress

Use the Ingress LoadBalancer external IP to access the app in a browser

## Learning Points

Understand multi-tier architecture

Learn containerization with Docker

Deploy applications on Kubernetes

Configure services, volumes, and ingress

Use multi-stage Docker builds for optimized images

# Author
Javed Shaik

DevOps Project | Kubernetes | Docker | Java | DevOps



