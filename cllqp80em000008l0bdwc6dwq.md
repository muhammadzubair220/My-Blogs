---
title: "Day 7: Package Management - Docker Advanced"
datePublished: Fri Aug 25 2023 14:39:19 GMT+0000 (Coordinated Universal Time)
cuid: cllqp80em000008l0bdwc6dwq
slug: day-7-package-management-docker-advanced
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1692974197369/2fc8fc65-d7fc-46b1-8cc5-c53523e03ce9.png
tags: docker, docker-volume, 90daysofdevops, two-tier-application-using-docker-compose

---

### 📁 **Volumes**

In the world of Docker, managing data persistence across containers is a puzzle we all face. Docker volumes offer a solution by allowing us to store and handle data externally. Here's how you can dive into the realm of Docker volumes:

* List Docker volumes:
    
    ```plaintext
    docker volume ls
    ```
    
* Create a volume with customized options:
    
    ```plaintext
    docker volume create --name django-app-volume --opt type=none --opt device=/home/ubuntu/django-app/volumes/django-app-volume --opt o=bind
    ```
    

### 📂 **Mounting Volumes:**

After crafting your volume, the next step is to mount it within containers. This empowers your applications with seamless data sharing and persistence. Here's how to go about it:

1. Identify the volume ID, like `c1cb9e66374b`.
    
2. Launch a container with the volume mounted:
    
    ```plaintext
    docker run -d --mount source=django-app-volume,target=/data -p 8000:8000 django-app:latest
    ```
    
3. Execute commands within the container:
    
    ```plaintext
    docker exec -it 557628d790c6 bash
    ```
    

### 🚀 **Compose for Multi-Container Applications**

As our projects grow in complexity, managing individual containers becomes a juggling act. Docker Compose comes to the rescue, enabling you to wrangle multi-container applications effortlessly, particularly in a microservices architecture:

* **Docker Compose Essentials:**
    
    * Docker Compose masters multiple containers.
        
    * It's the key to harmonizing microservices.
        
* **Unveiling the Docker Compose Pattern:**
    
    ```plaintext
    Version: '3'
    Services: 
       Backend:
          Build:
             Context:
          Port: 
             5000:5000
          
       Mysql:
          Image: mysql:5.7
          Volume:mysql-data:/
    ```
    

### 🔄 **Unified Actions with Docker Compose**

Ah, the power of one-click actions! Docker Compose orchestrates tasks across containers, simplifying your life with every click. Let's create our symphony of commands:

* A configuration file in YAML is your ticket.
    
* YAML stands for "Yet Another Markup Language."
    
* A sneak peek at a YAML structure:
    
    ```plaintext
    yaml Key: Value
    Name: Zubair
    Hobbies:
       Personal:
          - Teaching
          - Workout
       Professional:
          - Coding
          - Documentation
    ```
    

🔧 **Multi-Stage Docker Builds**

Crafting the ideal Docker images for production often involves a dance of multi-stage builds. These streamlined maneuvers yield efficient, compact images while maintaining an organized building process. Unveil the magic of multi-stage builds:

* **Behold, the Multi-Stage Dockerfile:**
    
    ```plaintext
    DockerfileCopy code# Stage 1
    FROM python:3.9 AS big-stage
    WORKDIR app
    COPY . .
    
    # Stage 2
    FROM python:3.9-slim-bullseye
    COPY --from=big-stage /app /app
    RUN pip install flask
    CMD ["python", "app.py"]
    ```
    

🚀 **Pushing Images to Docker Hub**

Sharing is caring, especially in the world of Docker images. Docker Hub is your go-to stage for showcasing and disseminating these images. Let's take your images to the world:

1. Initiate a graceful entrance into Docker Hub:
    
    ```plaintext
    docker login
    ```
    
2. Give your image the spotlight it deserves:
    
    ```plaintext
    docker image tag multi-flask-app:latest muhammadzubair220/multi-flask-app:latest
    ```
    
3. Raise the curtains and push your image:
    
    ```plaintext
    docker push muhammadzubair220/multi-flask-app:latest
    ```
    

### 🌟 **In Conclusion**

Docker is a universe of possibilities, and understanding its key concepts is your spaceship to smoother development. From volumes that defy data limitations to orchestration with Docker Compose and the art of efficient builds, you're now equipped to conquer containerized challenges with confidence.

📚 **Keep Learning**

Connect with me on LinkedIn to stay updated on the latest tech adventures: [**Muhammad Zubair**](https://www.linkedin.com/in/muhammadzubair220/)