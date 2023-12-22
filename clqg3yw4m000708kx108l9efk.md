---
title: "Install CloudWatch Logs Agent on EC2 Instance and View CloudWatch Metrics"
datePublished: Fri Dec 22 2023 04:05:12 GMT+0000 (Coordinated Universal Time)
cuid: clqg3yw4m000708kx108l9efk
slug: install-cloudwatch-logs-agent-on-ec2-instance-and-view-cloudwatch-metrics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703217851140/bbecc8ae-fb50-4f64-a9af-37f0f7fcaaa8.png
tags: monitoring, devops, cloudwatch, cloud-security, ec2server

---

# **Lab Steps**

## **Task 1: Sign in to AWS Management Console**

1. Click on the **Open Console** button, and you will get redirected to AWS Console in a new browser tab.
    
2. On the AWS sign-in page,
    
    * Leave the Account ID as default. Never edit/remove the 12 digit Account ID present in the AWS Console. otherwise, you cannot proceed with the lab.
        
    * Now copy your **User Name** and **Password** in the Lab Console to the **IAM Username and Password** in AWS Console and click on the **Sign in** button.
        
3. Once Signed In to the AWS Management Console, Make the default AWS Region as **US East (N. Virginia) us-east-1.**
    

## **Task 2: Launching an EC2 Instance**

In this task, we are going to launch an EC2 Instance by providing the required configurations like name, instance type, key pair, security group and IAM instance profile.

1. Make sure you are in the **N.Virginia** Region.
    
2. Navigate to **EC2** by clicking on the **Services** menu at the top, then click on **EC2** in the **Compute** section.
    
3. Navigate to **Instances** on the left panel and click on **Launch instances** button. 
    
4. Enter Name as **MyEC2Server**
    
5. Select **Amazon Linux** from the Quick Start and Select **Amazon Linux 2 AMI** from the drop-down.
    
6. Choose **Architecture** as **64-bit(x86)**
    

![](https://labresources.whizlabs.com/a60edf2f6d5d7bfd2c8537f24ebb00c2/screenshot_70.png align="left")

    7. Choose an **Instance Type**: Select ***t2.micro***

![](https://labresources.whizlabs.com/a60edf2f6d5d7bfd2c8537f24ebb00c2/screenshot_71.png align="left")

     8\. **For Key pair:** Select **Create a new key pair** Button

* Key pair name: Enter **WhizKey**
    
* Key pair type: Select **RSA**
    
* Private key file format: Select **.pem  
      
    **
    

    9. Select **Create key pair** Button.

![](https://labresources.whizlabs.com/be95e663a84a7676a4e2b1a5a7eb788e/screenshot_1158_14_52.png align="left")

   10. In Network Settings Click on **Edit** Button:

* Auto-assign public IP: **Enable**
    
* Select **Create new Security group**
    

* Security group name : Enter ***MyEC2Server\_SG***
    
* Description : Enter ***Security Group to allow traffic to EC2***  
     
    

![](https://labresources.whizlabs.com/f472e3578490cdc516691046e475564f/ec2_network.png align="left")

* To add **SSH**, (Ignore if already added by default)
    
    1. Choose Type: Select **SSH** 
        
    2. Source: Select **Anywhere**
        

    11. Scroll Down to **Advanced Settings,** Select **IAM instance profile** already created for you as **task124\_ec2\_&lt;RANDOM\_NUMBER&gt;**

    12. **Leave** the rest of the things as default. Click on **Launch instance** button.

## **Task 4: SSH into the EC2 Instance**

* Please follow the steps in [**SSH into EC2 Instance**](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance)**.**  
     
    

## **Task 5: Download and Install the Cloudwatch Agent**

In this task, we will download and install the CloudWatch agent on the EC2 Instance. 

1.  Download the Cloudwatch Unified Agent
    
    ```plaintext
    wget https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
    ```
    

![](https://labresources.whizlabs.com/be95e663a84a7676a4e2b1a5a7eb788e/image31.png align="left")

1. Install the Cloudwatch Agent
    
    ```plaintext
    sudo rpm -U ./amazon-cloudwatch-agent.rpm
    ```
    

![](https://labresources.whizlabs.com/be95e663a84a7676a4e2b1a5a7eb788e/image30.png align="left")

## **Task 6: Configure and Start the Cloudwatch Agent**

1. Open the setup wizard
    
    ```plaintext
    sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
    ```
    

![](https://labresources.whizlabs.com/be95e663a84a7676a4e2b1a5a7eb788e/image24.png align="left")

1. Enter these values asked during setup:
    
    * On which OS are you planning to use the agent? : Enter ***1***
        
    * Are you using EC2 or On-Premises? : Enter ***1***
        
    * Which user are you planning to run the agent? : Enter ***1***
        
    * Do you want to turn on the StatsD daemon? : Enter ***2***
        
    * Do you want to monitor metrics from CollectD? : Enter **2**
        
    * Do you want to monitor any host metrics? Enter ***1***
        
    * Do you want to monitor CPU metrics per core? Enter ***1***
        
    * Do you want to add ec2 dimensions into all of your metrics if the info is available? : Enter ***1***
        
    * Would you like to collect your metrics at high resolution? : Enter ***1*** (1s)
        
    * Which default metrics config do you want?: Enter ***2***
        
    * Are you satisfied with the above config? Enter ***1***
        
    * Do you have any existing CloudWatch log Agent configuration file to import for migration? : Enter ***2***
        
    * Do you want to monitor any log files? : Enter ***2***
        
    * Do you want to store the config in the SSM parameter store? : Enter ***2***
        

**Note: if you make any mistakes in the above configuration, you can run the configuration setup again whenever you want. The configurations that you make is saved in a JSON File.**

1. Start the Agent:
    
    ```plaintext
    sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
    ```
    

![](https://labresources.whizlabs.com/be95e663a84a7676a4e2b1a5a7eb788e/image38.png align="left")

1. Check Agent Status
    
    ```plaintext
    systemctl status amazon-cloudwatch-agent
    ```
    

![](https://labresources.whizlabs.com/be95e663a84a7676a4e2b1a5a7eb788e/image7.png align="left")

## **Task 7: View the CloudWatch Metrics**

1. Navigate to **CloudWatch** by clicking on the **Services** menu available under the **Management and Governance** section.
    
2. Make sure you are in the **N.Virginia** Region.
    
3. Click on **All** **Metrics** under **Metrics** in the Left Panel.
    
4. You should be able to see **CWAgent** under **All Metrics (Custom Namespaces).** 
    

**Note: If you are not able to see CWAgent, please wait for at least 2 minutes and then refresh the browser page.**

![](https://labresources.whizlabs.com/be95e663a84a7676a4e2b1a5a7eb788e/screenshot_1166_43_16.png align="left")

1. Click on the CloudWatch Agent and you will be able to see visuals for that metric
    

![](https://labresources.whizlabs.com/be95e663a84a7676a4e2b1a5a7eb788e/screenshot_1167_44_31.png align="left")

> ### **Do you know?**
> 
>  The CloudWatch Logs Agent is configured through a JSON-formatted configuration file. This file specifies the log files to monitor, the log group to send the data to, and other parameters such as log rotation settings and timestamps.

## **Task 5 : Validation Test**

1. Once the lab steps are completed, please click on the Validation button on the left side panel.
    
2. This will validate the resources in the AWS account and displays whether you have completed this lab successfully or not.
    
3. Sample output :
    
    ![](https://labresources.whizlabs.com/be95e663a84a7676a4e2b1a5a7eb788e/4_41_26.gif align="left")
    

# **Completion and Conclusion**

1. You have created an EC2 Instance.
    
2. You have successfully accessed the EC2 instance via SSH.
    
3. You have downloaded and installed the CloudWatch Agent.
    
4. You have configured and started the agent.
    
5. You have viewed a cloud metric in CloudWatch.
    

# **End Lab**

1. Sign out of AWS Account.
    
2. You have successfully completed the lab.