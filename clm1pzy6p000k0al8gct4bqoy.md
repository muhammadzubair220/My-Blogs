---
title: "Day: 11 - Installing Node.js Application on Kubernetes with Helm"
datePublished: Sat Sep 02 2023 07:46:31 GMT+0000 (Coordinated Universal Time)
cuid: clm1pzy6p000k0al8gct4bqoy
slug: day-11-installing-nodejs-application-on-kubernetes-with-helm
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693640748922/19a1441c-3ac9-4aeb-8bc7-42f93da6561a.webp
tags: nodejs, kubernetes, helm, devops90days

---

In this guide, we'll walk through the process of installing a Node.js application on a Kubernetes cluster using Helm, a package manager for Kubernetes. Helm simplifies application deployments by packaging them into charts and providing a consistent way to manage, upgrade, and roll back applications.

## **Prerequisites**

Before we get started, make sure you have the following prerequisites in place:

1. **Kubernetes Cluster**: You should have a Kubernetes cluster up and running.
    
2. **Helm**: Helm should be installed on your local machine. If you haven't already installed Helm, follow the steps below.
    

## **Step 1: Install Helm**

Helm is the tool that will help you manage your Kubernetes applications using charts. Here's how you can install Helm:

### **Linux:**

```plaintext
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor > /usr/share/keyrings/helm-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/helm-archive-keyring.gpg] https://baltocdn.com/helm/stable/debian/ all main" > /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

### **Windows:**

You can download the Windows installer from the [**Helm GitHub Releases**](https://github.com/helm/helm/releases) page and follow the installation instructions.

### **macOS:**

```plaintext
brew install helm
```

Ensure that Helm is successfully installed by running:

```plaintext
helm version
```

## **Step 2: Create a Helm Chart**

Let's create a Helm chart for our Node.js application. Helm provides a `helm create` command to generate a basic chart structure.

```plaintext
helm create node-app
```

This command will generate a `node-app` directory containing the chart files.

## **Step 3: Customize the Helm Chart**

In the `node-app` directory, you'll find various files, including `values.yaml`, `templates`, and `Chart.yaml`. You can customize these files to suit your application's needs. For example, you can specify container image details, environment variables, and resource limits in the `values.yaml` file.

## **Step 4: Install the Helm Chart**

Now, it's time to install your Node.js application using Helm. Run the following command:

```plaintext
helm install node-app ./node-app/
```

This command deploys your Node.js application to the Kubernetes cluster with the name `node-app`.

## **Step 5: Verify the Deployment**

After installation, you can verify the deployment by checking the Kubernetes services:

```plaintext
kubectl get svc
```

This will display the services created by your Helm chart, including the Node.js application service.

## **Step 6: Upgrade or Rollback (if needed)**

As your application evolves, you can easily upgrade or roll back using Helm. Suppose you make changes to your Node.js application or the Helm chart itself. In that case, you can use the following commands:

To upgrade:

```plaintext
helm upgrade node-app ./node-app/
```

To rollback to a previous release:

```plaintext
helm rollback node-app <revision_number>
```

## **Additional Resources**

* To explore more Helm charts and installers, visit the [**Artifact Hub**](https://artifacthub.io/), a repository of Helm charts for various applications and services.
    
* For official Helm documentation and additional information, check out the [**Helm website**](https://helm.sh/).
    

## **Connect with Me**

If you have any questions or need further assistance, feel free to connect with me on LinkedIn: [**Muhammad Zubair**](https://www.linkedin.com/in/muhammadzubair220/).

## **Conclusion**

Helm simplifies the deployment and management of applications on Kubernetes, making it easier to maintain and scale your Node.js applications. With Helm, you can ensure consistency in deployments, upgrades, and rollbacks, simplifying the management of complex Kubernetes workloads.

Now you have a complete guide to installing a Node.js application on Kubernetes using Helm, including the installation of Helm itself. Feel free to customize this guide with your own content and add emojis to make it engaging for your readers.

Happy Helm charting! 🚀🎉