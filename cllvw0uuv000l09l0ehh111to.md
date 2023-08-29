---
title: "Day 9: Setting Up CI/CD Pipeline with Jenkins: A Hands-On Guide 🚀"
datePublished: Tue Aug 29 2023 05:48:34 GMT+0000 (Coordinated Universal Time)
cuid: cllvw0uuv000l09l0ehh111to
slug: day-9-setting-up-cicd-pipeline-with-jenkins-a-hands-on-guide
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693288102629/b8ad5f50-2db9-4211-8925-98be52486900.png
tags: automation, jenkins, pipeline, declarative, devops90days

---

🔧 **Creating and Assigning Jobs to Jenkins Agents**

* Start by writing a description for the job.
    
* Specify the GitHub project repository.
    
* Enable GitHub hook trigger for GITScm polling.
    
* Remember to integrate your Jenkins URL with GitHub and allow necessary ports for seamless integration.
    

### 🌐 **GitHub Integration**

* Add your Jenkins URL to GitHub and configure port settings for smooth communication, just like you would with AWS ECS instances.
    

### 🌱 **Getting Started with the Pipeline**

* Embrace the #grovestntax as you kick off the pipeline setup.
    
* Begin your pipeline with the declaration of the agent. 🛠️
    
* Use a specific agent by adding its name: `Agent {label 'dev-agent'}`.
    

### 🔨 **Defining Pipeline Stages**

* Your pipeline needs to have stages that define the workflow of your CI/CD process.
    
* Start with the 'Code' stage:
    
    * Use the **git** step to fetch code from your GitHub repository.
        
* Move on to the 'Build & Test' stage:
    
    * Employ the **docker build** command to create your Docker image.
        
* Conclude with the 'Deploy' stage:
    
    * Use the **docker-compose** commands to manage container deployment.
        

### 🧩 **Agent Distribution**

* Distribute your Jenkins workload across different agents.
    
* Create multiple agents (e.g., 'agent1', 'agent2') to parallelize tasks.
    

🔧 **Setting Up Agents**

* Configure agents by:
    
    * Naming them appropriately.
        
    * Adding descriptions for clarity.
        
    * Specifying root directories (e.g., /home/ubuntu).
        
    * Assigning labels for categorization (e.g., 'Django', 'Dev').
        
    * Launching them via SSH, configuring IP, private key, and host key verification strategy.
        

🔑 **SSH Key Setup**

* On both the master and agents, generate SSH keys to enable secure communication.
    
* On master: `cd .ssh && ssh-keygen && cat id_rsa.pub`.
    
* On agent: `cd .ssh` (similar steps).
    

🔗 **Connecting Master and Agents**

* Share the public key from the agent with the master for authentication.
    

🚀 **GitHub to DockerHub to AWS**

* The journey begins with GitHub triggering a Docker build.
    
* Through your pipeline, code is packaged and pushed to DockerHub.
    
* From there, AWS EC2 instances pull and deploy the image.
    

📡 **GitHub Integration**

* Enable SCM polling and set up a webhook for smoother GitHub integration.
    

🌐 **DockerHub Login**

* Install the **environment Injector** plugin.
    
* Create global credentials for DockerHub login.
    
* Use the `withCredentials` block to securely log in: `sh "docker login -u ${env.dockerHubUsername} -p ${env.dockerHubPassword}"`.
    

### 📝 **Putting It All Together: Jenkinsfile**

```plaintext
pipeline {
    agent {label 'dev-agent'}
    stages {
        stage('Code') {
            steps {
                git url: 'https://github.com/test12/node', branch: 'master'
            }
        }
        stage('Build & Test') {
            steps {
                sh 'docker build . -t test12/node-todo-app-cicd:latest'
            }
        }
        stage('Login & push image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUsername')]) {
                    sh "docker login -u ${env.dockerHubUsername} -p ${env.dockerHubPassword}"
                    sh "docker push ${env.dockerHubUsername}/node-todo-app-cicd:latest"
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
```

### **Conclusion**

By following these steps, you'll have your CI/CD pipeline up and running, allowing you to seamlessly build, test, and deploy your Node.js application. Now you're ready to automate and streamline your development workflow!

Feel free to connect with me on LinkedIn for more insights and discussions: [**Muhammad Zubair**](https://www.linkedin.com/in/muhammadzubair220/) 👋🌟