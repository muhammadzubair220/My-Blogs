---
title: "Day 2  Linux Fundamentals and Architecture"
datePublished: Thu Aug 03 2023 08:13:05 GMT+0000 (Coordinated Universal Time)
cuid: clkuvqjxo000009l48218gs1r
slug: day-2-linux-fundamentals-and-architecture
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691050498610/42391dee-c8a0-4431-bbc7-487893a7c72e.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691050356194/ca626895-0f4d-4e5c-8976-3750a56c80c0.jpeg
tags: linux, cybersecurity-1, linux-for-beginners, 90daysofdevops

---

Understanding the Linux architecture is crucial for a comprehensive grasp of its functionality. It operates from the top down, encompassing various layers:

1. **Application**:
    
    * **Description**: This is where user-facing software runs and interacts.
        
2. **Shell**:
    
    * **Description**: The interface through which users interact with the system, executing commands.
        
3. **Kernel**:
    
    * **Description**: The core component managing hardware resources and providing essential services.
        
4. **Hardware**:
    
    * **Description**: The physical machinery that Linux operates on.
        

---

**Global Infrastructure and AWS Billing:**

Managing AWS billing involves understanding the global infrastructure, including regions and availability zones, which play a pivotal role. AWS offers a comprehensive overview of their infrastructure at: [**Global Infrastructure Overview**](https://aws.amazon.com/about-aws/global-infrastructure/regions_az/).

**Favorite AWS Region - North Virginia**:

* **Description**: Among the available regions, North Virginia stands out as a personal favorite due to its merits and offerings.
    

---

**EC2 (Elastic Compute Cloud) Setup:**

Setting up an EC2 instance involves a step-by-step process:

1. **Login**:
    
    * **Description**: Access your AWS account and select your preferred region.
        
2. **Launch Instance**:
    
    * **Description**: Search and choose your instance name. Select the operating system and architecture, such as 64bit (x86) or 64bit (arm), making use of the 1-year free tier with 1,000 hours of usage, preferably on a t2.micro instance.
        
3. **Key Pair**:
    
    * **Description**: Provide a name for your key pair, choose RSA as the encryption type (utilizing RSA encryption keys), and generate a key pair file in the .pem format, widely used in the Linux ecosystem for enhanced career prospects.
        
4. **Network Settings**:
    
    * **Description**: Establish a security group to allow essential traffic, such as SSH, HTTPS, and HTTP.
        

By following these steps, you will successfully create a launch instance, resulting in a fully operational machine image tailored to your requirements.

Title: **Mastering Basic Linux Commands: A Comprehensive Guide**

Introduction:

* Briefly introduce the importance of command-line skills in Linux.
    
* Highlight the efficiency and versatility of using the terminal.
    
* Set the tone for the article as an essential resource for beginners.
    

### **Section 1: Getting Started with the Terminal**

1.1 **The Terminal Interface**

* Introduce the terminal and its significance in Linux.
    
* Explain how to open the terminal on different Linux distributions.
    
* Discuss the terminal prompt and its meaning.
    

### **Section 2: Navigating the File System**

2.1 **pwd and ls**

* Explain the `pwd` command to print the current working directory.
    
* Describe the `ls` command for listing files and directories.
    
* Introduce common options like `-l`, `-a`, and `-h`.
    

2.2 **cd and mkdir**

* Explain how to change directories using `cd`.
    
* Describe creating new directories with the `mkdir` command.
    

### **Section 3: Working with Files**

3.1 **Creating and Touching Files**

* Describe how to create new files using `touch`.
    
* Explain the purpose of `echo` for writing content to files.
    

3.2 **Viewing File Content**

* Introduce `cat`, `more`, and `less` for displaying file content.
    
* Highlight their differences and interactive features.
    

3.3 **Copying, Moving, and Renaming**

* Describe the `cp` command for copying files and directories.
    
* Explain how to use `mv` to move and rename files.
    

3.4 **Removing Files and Directories**

* Introduce the `rm` command for deleting files and directories.
    
* Emphasize caution and introduce the `-r` and `-f` options.
    

### **Section 4: Searching and Filtering**

4.1 **Searching with grep**

* Explain how to use `grep` to search for patterns in files.
    
* Provide examples of basic usage and options.
    

### **Section 5: System Monitoring and Management**

5.1 **Viewing Running Processes**

* Introduce the `ps` command to list running processes.
    
* Explain the `aux` option for detailed process information.
    

5.2 **Terminating Processes**

* Describe how to use the `kill` command to terminate processes.
    

### **Section 6: Disk Usage and Management**

6.1 **Checking Disk Space**

* Introduce the `df` command for checking disk space usage.
    
* Describe the `-h` option for human-readable sizes.
    

6.2 **Checking Folder Sizes**

* Explain how to use the `du` command to check sizes of files and folders.
    
* Discuss the `-h` option for human-readable sizes.
    

### **Section 7: Additional Resources**

7.1 **Using the Manual**

* Explain how to access command documentation using `man`.
    
* Encourage readers to explore more commands and options.