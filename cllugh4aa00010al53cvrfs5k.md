---
title: "Day 8 : Jenkins: Automating Your Software Delivery Pipeline ✨🚀 Part 1"
datePublished: Mon Aug 28 2023 05:45:32 GMT+0000 (Coordinated Universal Time)
cuid: cllugh4aa00010al53cvrfs5k
slug: day-8-jenkins-automating-your-software-delivery-pipeline-part-1
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693201525923/adfb1859-e644-480d-9f83-e5e064dabbc7.png
tags: jenkins, devops90days, freestyle-jenkins-project, declarative-pipeline-jenkins

---

Jenkins is a powerful open-source automation tool that enables Continuous Integration (CI) and Continuous Delivery (CD) of software projects. It streamlines the software development process by automating repetitive tasks and providing a framework for building, testing, and deploying code changes. Here's a step-by-step guide to setting up Jenkins for your project:

### **Installation and Setup** 🛠️🔧

1. Update package list:
    
    ```plaintext
    sudo apt update
    ```
    
2. Install OpenJDK 17 (Java Runtime Environment):
    
    ```plaintext
    sudo apt install openjdk-17-jre
    ```
    
3. Check Java version:
    
    ```plaintext
    java -version
    ```
    
4. Add Jenkins repository key and source to package manager:
    
    ```plaintext
    curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    ```
    
5. Install Jenkins:
    
    ```plaintext
    sudo apt-get install jenkins
    ```
    
6. Check Jenkins status:
    
    ```plaintext
    systemctl status jenkins
    ```
    
7. Retrieve the initial admin password:
    
    ```plaintext
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```
    
8. Access Jenkins on your browser and follow the setup wizard.
    

### **Docker Integration** 🐳

Install Docker:

1. ```plaintext
    sudo apt install docker.io
    ```
    
2. Add Jenkins to the Docker group:
    
    ```plaintext
    sudo usermod -aG docker jenkins
    ```
    
3. Restart Jenkins:
    
    ```plaintext
    sudo systemctl restart jenkins
    ```
    

### **Creating a Basic Pipeline** 🚀🔍

1. Create a new pipeline job:
    
    * Name: YourJobName
        
    * Type: Pipeline
        
2. Configure the pipeline stages:
    
    ```plaintext
    pipeline {
       agent any
       stages {
          stage("Code") {
             steps {
                echo "Code Cloned"
             }
          }
          stage("Build") {
             steps {
                echo "Code Built"
             }
          }
          stage("Test") {
             steps {
                echo "Code Tested"
             }
          }
          stage("Deploy") {
             steps {
                echo "Code Deployed"
             }
          }
       }
    }
    ```
    
3. Save and run the pipeline job.
    

### **Troubleshooting** 🛠️🔍

* Check ports in use:
    
    ```plaintext
    sudo lsof -i:8001
    ```
    
* Using Docker Compose:
    
    ```plaintext
    docker-compose down
    docker-compose up -d
    ```
    

### **Benefits of Jenkins Pipelines** 💡🌐

* **Automation**: Jenkins automates repetitive tasks, reducing manual errors.
    
* **Speed**: Continuous Integration shortens feedback loops, accelerating development.
    
* **Reliability**: Automated testing ensures code quality and stability.
    
* **Consistency**: Pipelines enforce consistent processes across teams.
    
* **Traceability**: Each pipeline run is recorded, aiding troubleshooting and audits.
    

### **Conclusion** 🎉🚀

With Jenkins, you can build, test, and deploy software efficiently and reliably. By setting up pipelines, you establish a structured approach to software delivery, enhancing collaboration and quality. Embrace Jenkins to streamline your development lifecycle and deliver outstanding software with confidence! 🌟🚀