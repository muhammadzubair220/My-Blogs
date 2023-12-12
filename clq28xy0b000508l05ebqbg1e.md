---
title: "Understanding and Configuring Layered Security in an AWS VPC"
datePublished: Tue Dec 12 2023 11:15:39 GMT+0000 (Coordinated Universal Time)
cuid: clq28xy0b000508l05ebqbg1e
slug: understanding-and-configuring-layered-security-in-an-aws-vpc
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702379682993/7ba3e0b5-9faf-4daf-8647-bd611b7ec10a.png
tags: awssecurity, aws-amazonwebservices-cloudcomputing-scalability-5-innovation-businesstransformation-datasecurity-8-costeffective-techblog-awsservices-cloudtechnology-awsbenefits-digitaltransformation-awssecurity-awsforbusiness-cloudstorage-machinelearning-awsanalytics-awsnetworking-awscomputing, whizlabs

---

# **Lab Steps**

## **Task 1: Sign in to AWS Management Console**

1. Click on the **Open Console** button, and you will get redirected to AWS Console in a new browser tab.
    
2. On the AWS sign-in page,
    
    * Leave the Account ID as default. Never edit/remove the 12 digit Account ID present in the AWS Console. otherwise, you cannot proceed with the lab.
        
    * Now copy your **User Name** and **Password** in the Lab Console to the **IAM Username and Password** in AWS Console and click on the **Sign in** button.
        
3. Once Signed In to the AWS Management Console, Make the default AWS Region as **US East (N. Virginia) us-east-1.**
    

     **Note: There is no Validation function for this lab.**

## **Task 2: Creating a new VPC**

In this task, we are going to create a new VPC with the required configurations such as name, IPv4 CIDR block.

1. Make sure to choose the **N.Virginia** region in the AWS Management Control dashboard, which is present in the top right corner.
    
2. Navigate and click on  **VPC** which will be available under the **Networking & Content Delivery** section of **Services**
    
3. Click on **Your VPCs** from the left menu and Click on **Create VPC** button.
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1171_47_43.png align="left")

      4. In **Create VPC** page fill the following details,

* Select **VPC Only**
    
* Name tag: Enter ***whizlabs\_VPC***
    
* IPV4 CIDR Block: Enter ***10.0.0.0/16***
    
* IPV6 CIDR block:  Select **No IPV6 CIDR block**
    
* Tenancy:  **Default**
    
* Click on **Create** **VPC** button**.**  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1172_49_27.png align="left")

## **Task 3: Creating and attaching an Internet gateway**

In this task, we are going to create an internet gateway and will attach it to the created VPC.

1. Click on **Internet Gateways** from the left menu and click on **Create internet gateway** button and enter the following details:
    

* Name tag: Enter ***whizlabs\_IGW*** 
    
* Click on **Create** **internet gateway** button.  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1173_50_54.png align="left")

1. **Select** the Internet gateway you created from the list.
    

* Click on **Actions** button.
    
* Click on **Attach to VPC** button.  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1174_52_33.png align="left")

* **Select** MyVPC from the drop-down and click on **Attach internet gateway** button.  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1175_54_43.png align="left")

## **Task 4: Creating two Subnets**

1. You will create **2 Subnets,** one for public and another for private resources. First, we will create a **public subnet**. 
    
2. For the Public Subnet**,** click on **Subnets** from the left menu and click on **Create subnet** button. 
    

* VPC ID: Select **whizlabs\_VPC** (Select the VPC which you created from the dropdown) 
    
* Name tag: Enter ***public\_subnet***
    
* Availability zone: Select **No Preference**
    
* IPv4 CIDR block: Enter ***10.0.1.0/24***
    
* Click on **Create subnet** button
    

1. For Private Subnet**,** click on **Create Subnet** again. 
    

* VPC ID: Select **whizlabs\_VPC** (Select the VPC which you created from the dropdown) 
    
* Name tag: Enter ***private\_subnet***
    
* Availability zone: Select **No Preference**
    
* IPv4 CIDR block: Enter ***10.0.2.0/24***
    
* Click on **Create subnet** button.  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1176_59_41.png align="left")

## **Task 5: Creating Route tables, configuring routes and associating them with Subnets** 

1. You will create **2 route tables,** one for public routes and another for private routes.
    
2. Go to **Route Tables** from the left menu and click on **Create route table** button. 
    

* Name tag: Enter ***public\_route***
    
* VPC: Select **whizlabs\_VPC** (Select the VPC you created from the dropdown)
    
* Click on **Create** **route table** button**.**  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1177_01_42.png align="left")

1. Similarly, go to **Route Tables** from the left menu and click on **Create route table.**
    

* Name tag: Enter ***private\_route***
    
* VPC: Select **whizlabs\_VPC** (Select the VPC you created from the dropdown)
    
* Click on **Create** **route table** button.
    

1. Now, you need to **add routes to the Route Tables**. 
    

* Select **public\_route.**
    
* Go to the **Routes** tab. Click on **Edit routes**. On the next page, click on **Add route.**
    
* Specify the following values: 
    
    * **Destination:** Enter ***0.0.0.0/0***
        
    * **Target:** Select **Internet Gateway** from the dropdown menu to select **whizlabs\_IGW**.
        
    * Click on **Save changes** button.  
         
        

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1178_06_32.png align="left")

1. Next, you need to associate the **public\_subnet** with this **public\_route**. Select the **public\_route** and go to the **Actions** and in that go to **Edit Subnet Associations** tab.
    
    * Click on **Edit Subnet Associations**.
        
    * Select **public\_subnet** from the list.
        
    * Click on **Save Associations** button. 
        

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/public_subnet_association.jpg align="left")

1. Similarly, you need to associate the **private\_subnet** with this **private\_route**. Select the **private\_route** and go to the **Actions** and in that go to **Edit Subnet Associations** tab.
    
    * Click on **Edit Subnet Associations**.
        
    * Select **private\_subnet** from the list.
        
    * Click on **Save Associations** button.
        

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/private_subnet_association.jpg align="left")

## **Task 6: Creating Security Group**

In this task, we are going to create a security group for the EC2 Instance. 

1. Go to **Security Group** from the left menu and click on **Create security group** button and then provide the following details**:**
    

* Security group name: Enter ***whizlabs\_securitygroup***
    
* Description: Enter ***Security group for multilayered VPC***
    
* VPC: Select **whizlabs\_VPC** (select from the dropdown)
    
* Under **Inbound Rules,** click on **Add Rule** button.
    
* To add **SSH**,
    
    * Choose Type: Select **SSH** 
        
    * Source: **Custom - 0.0.0.0/0**
        
* To add **All ICMP - IPv4,**
    
    * Click on **Add Rule**
        
    * Choose Type: Select **All ICMP - IPv4** 
        
    * Source: **Anywhere IPv4**
        
* Click on **Create security group** button.  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1179_14_10.png align="left")

## **Task 7: Creating and configuring Network ACL**

Network Access Control Lists (ACLs) in AWS are used to control inbound and outbound traffic at the subnet level. They act as virtual firewalls that provide an additional layer of security for your Amazon Virtual Private Cloud (VPC). In this task, we are going to create and configure Network ACL by adding required inbound and outbound rules.

1. Go to **Network ACLs** from the left menu and click on **Create network ACL**. Provide the following details:
    

* Name tag: Enter ***whizlabs\_NACL***
    
* VPC: Select **whizlabs\_VPC** (Select the VPC which you created from the dropdown)
    
* Click on **Create network ACL** button.  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1180_16_08.png align="left")

1. Select **whizlabs\_NACL** and go to **Inbound rules tab.** Click on **Edit inbound rules** and then click on the **Add new rule.** 
    
2. Add the following rules:
    

* For **SSH**, click on **Add new rule**,
    
    * Rule number : Enter ***100***
        
    * Type: Choose ***SSH (22)*** 
        
    * Source: Enter ***0.0.0.0/0***
        
    * Allow / Deny: Select **Allow**
        
* For **ALL ICMP- IPv4**, click on **Add new rule**,
    
    * Rule number : Enter ***200***
        
    * Type: Choose ***ALL ICMP - IPv4*** 
        
    * Source: Enter ***0.0.0.0/0***
        
    * Allow / Deny: Select **Allow**
        
* Click on **Save changes** button.
    

1. NACLs are stateless. You need to add the rules in Outbound rules too. 
    
2. Select **whizlabs\_NACL** and go to **Onbound rules tab.** Click on **Edit onbound rules** and then click on the **Add Rule** button.
    

* For **ALL ICMP- IPv4**, click on **Add new rule**,
    
    * Rule# : Enter ***100***
        
    * Type: Choose ***ALL ICMP - IPv4*** 
        
    * Destination: Enter ***0.0.0.0/0***
        
    * Allow / Deny: Select **Allow**
        
* For **Custom TCP Rule**, click on **Add new rule**,
    
    * Rule# : Enter ***200***
        
    * Type: Choose ***Custom TCP Rule*** 
        
    * Port Range: Enter ***1024 - 65535***
        
    * Destination: Enter ***0.0.0.0/0***
        
    * Allow / Deny: Select **Allow**
        
* Click on **Save changes** button.  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/24.png align="left")

1. You need to associate both public and private subnets with the NACL. 
    
2. Select **whizlabs\_NACL** and go to the **Subnet associations tab.** Click on **Edit subnet associations.**
    
3. Choose all the available subnets and then click on **Save changes** button.
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1181_20_21.png align="left")

## **Task 8: Launching 2 EC2 Instances**

1.  Navigate to **Services** and choose **EC2** under **Compute**
    
2. Navigate to **Instances** on the left panel and click on **Launch Instances** button. 
    
3. Name : Enter ***public\_instance***
    
4. **For Amazon Machine Image (AMI):** Search for **Amazon Linux 2 AMI** in the search box and click on the **select** button.  
     
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_1161_21_19.png align="left")

* **Note: if there are two AMI's present for Amazon Linux 2 AMI, choose any of them.**
    

1. **For Instance Type:** Select ***t2.micro***
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/ec2_instance_48_06.png align="left")

1. **For Key pair:** Select **Create a new key pair** Button
    
    1. Key pair name: **WhizKey**
        
    2. Key pair type: **RSA**
        
    3. Private key file format: **.pem**
        
2. Select **Create key pair** Button.
    
3.  In Network Settings Click on **Edit** button:
    
    * VPC: Select **whizlabs\_VPC** 
        
    * Subnet: Select **public\_subnet** 
        
    * Auto-assign public IP: **Enable**
        
    * Choose **Select an existing security group** and remove default one then select **whizlabs\_securitygroup**
        

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/ec2instance_27_38.gif align="left")

1. Keep Rest thing Default and Click on **Launch Instance** Button.
    
2. Select **View all Instances** to View Instance you Created
    
3. Similar to the above, launch **another EC2 instance:**
    

* **Name** the instance as ***private\_instance*** 
    
* Key pair : Select the existing one
    
* VPC: Select **whizlabs\_VPC** 
    
* Subnet: Select **private\_subnet** 
    
* Auto-assign public IP: **Disable**
    
* Choose **Select an existing security group** and remove default one then select **whizlabs\_securitygroup**
    

1. Keep Rest thing Default and Click on **Launch Instance** Button.
    
2. Select **View all Instances** to View Instance you Created.
    

## **Task 9: Testing the EC2 instances**

1. Select the **publc\_instance** from the EC2 dashboard and copy the public IPv4 address.
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/public_ip_ec2.jpg align="left")

1. Similarly, copy the **Private IPv4 Address** of the **private\_instance**.
    
2. SSH into **public\_instance** EC2 Instance.
    

* Please follow the steps in [SSH into EC2 Instance](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance).
    

1. **Ping** the **private IP** of your **private\_instance** by using the below command:
    
    * **ping &lt;your Private EC2 IPv4 address&gt;**
        
2. Once you execute this command, you will receive a response from the IP.
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/screenshot_17.png align="left")

1. Press **\[Ctrl\] + C** to cancel the process.
    

> ### **Do you know?**
> 
> Security groups are applied at the instance level and provide stateful control over traffic, while NACLs are applied at the subnet level and provide stateless control over traffic.

## **Task 10 : Validation of the Lab**

1. Once the lab steps are completed, please click on the **Validation** button on the left side panel.
    
2. This will validate the resources in the AWS account and displays whether you have completed this lab successfully or not.
    
3. Sample output : 
    

![](https://labresources.whizlabs.com/dd7eb642ac8aa27ce96bca9efdd35186/3_40_36.gif align="left")

# **Completion and Conclusion** 

1. You have successfully created a new VPC.
    
2. You have successfully created and attached an Internet Gateway.
    
3. You have successfully created two subnets for public and private AWS instances.
    
4. You have successfully created and configured the Route Table.
    
5. You have successfully created a Security Group.
    
6. You have successfully created and configured Network ACL. 
    
7. You have successfully launched 2 EC2 instances (one in a public subnet and one in a private subnet).
    
8. You have successfully tested the EC2 instance.
    

# **End Lab**

1. Sign out from the AWS Account.
    
2. You have successfully completed the lab.