---
title: "AWS Access control alerts with CloudWatch and CloudTrail"
datePublished: Mon Dec 18 2023 06:59:45 GMT+0000 (Coordinated Universal Time)
cuid: clqakfyn3000j08jr31schu2r
slug: aws-access-control-alerts-with-cloudwatch-and-cloudtrail
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702882733045/bc8a78b9-5ee0-4f2d-b080-3bec2ada4148.png
tags: security, aws-cloudtrail, aws-management, log-group

---

# **Lab Steps**

## **Task 1: Sign in to AWS Management Console**

1. Click on the **Open Console** button, and you will get redirected to AWS Console in a new browser tab.
    
2. On the AWS sign-in page,
    
    * Leave the Account ID as default. Never edit/remove the 12 digit Account ID present in the AWS Console. otherwise, you cannot proceed with the lab.
        
    * Now copy your **User Name** and **Password** in the Lab Console to the **IAM Username and Password** in AWS Console and click on the **Sign in** button.
        
3. Once Signed In to the AWS Management Console, Make the default AWS Region as **US East (N. Virginia) us-east-1.**
    
4. Select Maybe later in New AWS Console Home page pop-up 
    

## **Task 2: Creating a CloudTrail**

1. Make sure to choose the **N.Virginia** region in the AWS Management console dashboard (present in the top right corner).
    
2. Navigate and click on **CloudTrail,** which will be available under the  **Management & Governance** section of **Services**.
    
3. Click on **Create Trail** on the right side.
    
4. Under Create Trail, enter these details:
    
    * Trail name: Enter ***My\_cloudtrail***.
        

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/image_55_37.png align="left")

5. Select the trail you have created, click on it. Scroll down you can see Cloudwatch logs section. 

    Click on the **Edit** button.

* CloudWatch Logs  :  **Check** Enabled
    
    * Log group : Leave it as default (i.e New and default log group name)
        
    * IAM Role : Select **New** and give the Role name as ***whiz\_role.***
        
    * Click on **Save changes** button 
        

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/image_57_18.png align="left")

* Tags-optional:
    
    * Key: Enter ***Name***
        
    * Value: Enter ***my\_logs***
        
* Click on **Save changes** button
    

          6.    A CloudTrail instance that delivers logs to an S3 bucket has now been created.

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/task_2_step_5.jpg align="left")

## **Task 3: Creating Metric Filters for Log Groups in Cloudwatch**

1. Make sure you are in the **N.Virginia** Region.
    
2. Click on **Services** and navigate to the **CloudWatch** dashboard under **Management & Governance**.
    
3. Click on **Log groups** under **Logs** in the left panel.
    
4. Click on the log group we just created and click on the **Actions.**
    
5. Click on **create metric filter** as shown below:
    
6. Under **Create filter pattern,** provide the pattern you need to filter on. For this lab, we are **going to filter for stopped instances**.
    

* Filter pattern                 : Enter the pattern ***{ $.eventName= "StopInstances" }***
    
* Select log data to test  : Select the **cloudtrail log**  in drop-down.
    

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/image28_50_52.png align="left")

* After completing the above steps, click on **Next**.
    

1. Next we will create a filter using the following details:
    

* Filter name: Enter ***stoppedInstancecount***
    
* Metric details:
    
    * Metric namespace  : Enter ***CloudTrailMetrics***
        
    * Metric name            : Enter ***EC2stoppedInstanceEventCount***
        
    * Metric value            : Enter ***1***
        
    * Default value           : Leave default
        
* Finally, click on and **Next** review the given details. Click on **Create metric filter** to complete the metric filter creation.
    

## **Task 4: Creating an Alarm**

1. In CloudWatch, select the log group created for our CloudTrail and then click on **metric filters** at the bottom.
    
2. Select the Metric filter created in the above step and then click on **create alarm** as shown below:
    

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/image2_53_48.png align="left")

1. Specify the metric conditions as follows:
    

* Namespace : **CloudTrailMetrics (default)**
    
* Metric name : **EC2stoppedInstanceEventCount (default)**
    
* Statistic        : **sum (default)**
    
* Period          : **5 minute (default)**
    
* Conditions:
    
    * Threshold type: Select **Static**
        
    * Whenever EC2stoppedInstanceEventCount is :    than ***1***.
        
* Click on **Next**.
    

1. Next we'll **configure actions**
    

* Alarm state trigger                                              : Select **in alarm**
    
* Select an SNS topic                                            : select **Create new topic**
    
* Create a new topic                                              : Enter the topic name as ***My\_Ec2count\_topic***
    
* Email endpoints that will receive the notification :  Enter your Email address to receive the alert
    
* Once you provide these details, click on **create topic**.
    
    * AWS will send a confirmation email to the Email address provided above. You will need to confirm the email subscription 
        
    * **Note:** If you are not getting any mail from AWS confirmation, Please check your spam
        

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/subcription_topic.png align="left")

* Click on the **next** button to complete the alarm creation.
    

1. Give the name for your alarm and complete the steps as shown below:
    

* Alarm name : Enter ***My\_stopped\_ec2\_alarm***
    
* Alarm description        : Enter ***Alarm to count the stopped instances count***
    
* Review the details and click on **create alarm**.
    

1. Navigate to the CloudWatch dashboard and click on alarms. You should see the alarm created in the above step under **insufficient data** as shown below:
    

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/clt1_07_50.png align="left")

## **Task 5: Creating an EC2 Instance to Trigger our Alarm**

1. Make sure you are in the **N.Virginia** Region.
    
2. Navigate to **EC2** by clicking on the **services** menu in the top, then click on **EC2** in the **Compute** section
    
3. Navigate to **Instances** on the left panel and click on **launch instances**
    
4. Name : Enter ***MyEC2Server***
    

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/myec2server.png align="left")

1. **For Amazon Machine Image (AMI):** Select **Amazon Linux 2 AMI** in the search box.
    
    ![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/image_13_45.png align="left")
    

**Note: if there are two AMI's present for Amazon Linux 2 AMI, choose any of them.**

1. **For Instance Type:** select ***t2.micro***
    

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/ec2_instance.png align="left")

1. **For Key pair:** Select **Create a new key pair** Button
    
    1. Key pair name: **WhizKey**
        
    2. Key pair type: **RSA**
        
    3. Private key file format: **.pem**
        
2. Select **Create key pair** Button.
    
3.  In Network Settings Click on **Edit**:
    

* Auto-assign public IP: **Enable**
    
* Select **Create new Security group**
    
* Security group name : Enter ***MyEC2Server\_SG***
    
* Description : Enter ***Security Group to allow traffic to EC2***
    

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/ec2_network.png align="left")

* Check **Allow SSH from** and Select **Anywhere** from dropdown
    
    * To add **SSH**,
        
        1. Choose Type: **SSH**
            
        2. Source: Select **Anywhere**
            

1. Keep Rest thing Default and Click on **Launch Instance** Button.
    
2. Select **View all Instances** to View Instance you Created
    
3. **Launch Status:**Your instance is now launching, Click on the instance ID and wait for complete initialization of instance.
    

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/ec2.jpg align="left")

    13.Once the EC2 instance launches successfully, **start and stop the instance 2 to 3 times** as shown in the below screenshot:

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/stop.jpg align="left")

    14.Navigate to the CloudWatch console and click on **In alarm** under **Alarms** on the left side panel to see the newly-created alarm. It should show the state as **In alarm**, as shown below:

![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/image23.png align="left")

> ### **Do you know?**
> 
> AWS Access Control Alerts with CloudWatch and CloudTrail are mechanisms provided by Amazon Web Services (AWS) to monitor and track access and authorization events within your AWS environment. They help detect and notify you about potential security issues, unauthorized access attempts, and unusual activity.

## **Task 6: Validation Test**

1. Once the lab steps are completed, please click on the **Validate** button on the Right side panel.
    
2. This will validate the resources in the AWS account and display whether you have completed this lab successfully or not.
    
3. Sample output : 
    
    ![](https://labresources.whizlabs.com/1d3160c3978dc813a7100919c1660008/55_36_30.gif align="left")
    

# **Completion and Conclusion**

1. You have successfully created a CloudTrail and an S3 bucket to store logs.
    
2. You have created CloudWatch log groups and a metric filter for stopped EC2 instances.
    
3. You have successfully created SNS topic to receive the alert from CloudWatch.
    
4. You have successfully launched an EC2 instance.
    
5. You successfully stopped the instance a few times to check the working of the alarm.
    

# **End Lab**

1. Sign out of AWS Account.
    
2. You have successfully completed the lab.