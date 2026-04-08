# Dockerized Website Deployment with AWS Load Balancer

## Project Overview

This project demonstrates how to deploy a containerized static website on multiple cloud servers and distribute traffic using a load balancer to achieve high availability and scalability.

The website is packaged using Docker and deployed on two EC2 instances. An AWS Application Load Balancer distributes incoming traffic across both servers.

---

## Architecture

User
↓
Application Load Balancer
↓
EC2 Instance 1 (Docker + Nginx)
EC2 Instance 2 (Docker + Nginx)

---

## Technologies Used

* AWS EC2
* AWS Application Load Balancer
* Docker
* Nginx
* GitHub
* Linux

---

## Project Implementation

### 1. Launch EC2 Instances

* Created two EC2 instances
* Configured security groups to allow HTTP traffic (port 80)
* Installed Docker on both servers

### 2. Containerize Website

Created a Dockerfile to serve the static website using Nginx.

Dockerfile:

```
FROM nginx:alpine
COPY dist/ /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

This copies the website files into the Nginx web directory inside the container.

---

### 3. Build Docker Image

```
docker build -t agency-website .
```

---

### 4. Push Image to Docker Hub

```
docker tag agency-website <dockerhub-username>/agency-website
docker push <dockerhub-username>/agency-website
```

---

### 5. Run Container on EC2

```
docker run -d -p 80:80 <dockerhub-username>/agency-website
```

The container serves the website using Nginx.

---

### 6. Configure Application Load Balancer

Steps performed:

* Created a target group
* Registered both EC2 instances
* Configured HTTP listener on port 80
* Attached the target group to the load balancer

The load balancer distributes traffic between the two servers.

---

## Testing

Access the application using the Load Balancer DNS:

```
http://<load-balancer-dns>
```

Refresh the page multiple times to confirm traffic is served by different instances.

---


Examples:

* EC2 instances running
* Docker container running
* Load balancer configuration
* Target group health status
* Website output

---

## Key DevOps Concepts Demonstrated

* Containerization using Docker
* Reverse proxy web server using Nginx
* Cloud infrastructure using AWS EC2
* Load balancing for high availability
* Multi-instance deployment

---

## Outcome

Successfully deployed a Dockerized website on multiple EC2 instances and implemented load balancing using AWS Application Load Balancer to ensure high availability and reliability.

---

## Future Improvements

* Add CI/CD pipeline using GitHub Actions
* Automate deployment with Infrastructure as Code (Terraform)
* Use Auto Scaling Group for dynamic scaling
