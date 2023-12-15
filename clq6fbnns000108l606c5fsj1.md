---
title: "Understanding Stateful vs Stateless Firewalls"
datePublished: Fri Dec 15 2023 09:25:21 GMT+0000 (Coordinated Universal Time)
cuid: clq6fbnns000108l606c5fsj1
slug: understanding-stateful-vs-stateless-firewalls
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702632281750/3ccbb384-70ed-4be3-b8c8-5649129bce1a.png
tags: aws, awssecurity, whizlabs, statefull, stateless-firewall

---

# **Lab Steps**

## **Task 1: Sign in to AWS Management Console**

1. Click on the **open console** button, and you will get redirected to AWS Console in a new browser tab.
    
2. On the AWS sign-in page,
    
    * Leave the Account ID as default. Never edit/remove the 12 digit Account ID present in the AWS Console. otherwise, you cannot proceed with the lab.
        
    * Now copy your **User Name** and **Password** in the Lab Console to the **IAM Username and Password** in AWS Console and click on the **Sign in** button.
        
3. Once Signed In to the AWS Management Console, Make the default AWS Region as **US East (N. Virginia) us-east-1.**
    

## **Task 2: Create an Amazon VPC**

1. Make sure you are in the **N.Virginia** Region. 
    
2. Navigate to **VPC** by clicking on the **Services** menu in the top left, then click on **VPC** in the **Networking & Content Delivery** section.
    
3. Navigate to **Your VPCs** on the left panel and click on the **Create VPC** button.
    
    * Name tag : Enter **AWS\_VPC** 
        
    * IPv4 CIDR block : Enter **10.0.0.0/16**
        
4. Leave everything else as default and click on the **Create VPC** button.
    
5. You have successfully created the VPC
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image73.png align="left")

## **Task 3: Create a Public subnet**

1. Navigate to **Subnets** from the left side menu and click on **Create subnet** button.
    
    * VPC ID : Select the **AWS\_VPC** VPC from the list.
        
    * Subnet name : Enter **Public\_subnet**
        
    * Availability Zone : Select **No Preference**
        
    * IPv4 CIDR block : Enter **10.0.1.0/24**
        
2. Now click on the **Create subnet** button.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image72.png align="left")

## **Task 4: Create and attach an Internet Gateway**

1. Navigate to the **Internet Gateways** from the left side menu and click on the **Create Internet Gateway** button.
    
    * Name tag : Enter **AWS\_IGW**
        
2. Click on the **Create Internet Gateway** button.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image77.png align="left")

1. Now click on the **Actions** button and select **Attach to VPC**.
    
    * Available VPCs :  select **AWS\_VPC** from the list.
        
2. Now click on the **Attach internet gateway** button.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image10.png align="left")

## **Task 5: Create a Public Route Table and associate it with the subnet**

1. Navigate to **Route Tables** on the left side panel and click on the **Create route table** button.
    
    * Name tag : Enter **PublicRT**
        
    * VPC : Select the **AWS\_VPC** from the list.
        
2. Now click on the **Create** button and then click on **Close** button.
    
3. Select the **PublicRT** from the list and go to the **Subnet Associations** tab in below.
    
4. Click on the **Edit subnet associations** button.
    
5. Now select the subnet with the name **Public Subnet** and click on the **Save** **associations** button.
    

## **Task 6: Add public Route in the Route table**

1. Navigate to **Route tables** on the left side panel and select the **PublicRT** from the list.
    
2. Go to the **Routes**  tab in below and click on the **Edit routes** button.
    
3. Now click on the **Add route** button.
    
    * Destination : Enter **0.0.0.0/0**
        
    * Target : select **Internet Gateway** and then select the **Internet Gateway id.**
        

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/screenshot_2023-07-20_at_4.58.14_pm_28_39.png align="left")

1. Click on the **Save routes** button and click on **Close**.
    

## **Task 7: Create a security Group**

1. Navigate to **Security Groups** on the left side panel, under **Security**.
    
2. Click on the **Create security group** button.
    
3. We are going to create a Security group with no Inbound and Outbound rules.
    
    * Security group name : Enter **EC2\_SG**
        
    * Description: Enter **Security group for EC2 Instance**
        
    * VPC: Select **AWS\_VPC**
        

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image80.png align="left")

* Under Inbound, leave everything as default
    
* Under **Outbound**, Click on the **Delete** Button to remove the All traffic Route.
    

1. Leave everything as default and click on the **Create security group** button.
    

## **Task 8: Launch an EC2 instance**

1. Navigate to **EC2** by clicking on the **Services** menu in the top left, then click on **EC2** in the **Compute** section.
    
2. Navigate to **Instances** from the left side menu and click on **Launch Instances** button.
    
3. Under the **Name and tags** section :
    

* Name : **MyEC2Instance**
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/2_26_07.png align="left")

1. Under the **Application and OS Images (Amazon Machine Image)** section :
    

* Select **Quick Start** tab and **Amazon Linux** under it
    
* Amazon Machine Image (AMI) : select **Amazon Linux 2 AMI**
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/3_26_45.png align="left")

1. Under the **Instance Type** section **:** 
    
    * Instance Type : Select **t2.micro**
        

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/5_27_04.png align="left")

1. Under the **Key Pair (login)** section **:**
    

* Click on Create new key pair hyperlink
    
* Key pair name: **EC2\_Public\_key**
    
* Key pair type: **RSA**
    
* Private key file format: **.pem** or **.ppk**
    
* Click on Create key pair and select the created key pair
    

1. Under the **Network Settings** section **:**
    

* Click on Edit button
    
* Remove the existing default VPC and add VPC with name **AWS\_VPC**
    
* Auto-assign public IP: select **Enable**
    
* Firewall (security groups) : Select **Select existing security group**
    
* Common security groups : Select Security group with name **EC2\_SG  
      
    **
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/4_27_31.png align="left")

1. Keep everything else as default and click on the **Launch instance** button.
    
2. **Launch Status:** Your instance is now launching, Navigate to **Instances** page from the left menu and wait until the status of the EC2 Instance changes to **running**.
    
3. Note down the sample IPv4 Public IP Address of the EC2 instance and place it in your text editor. A sample is shown in the screenshot below.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image56.png align="left")

## **Task 9: Understand the security group rules**

1. Follow the steps to [SSH into EC2 Instance](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance) but you won't be able to SSH into the EC2 instance because in the Security group you haven’t added any rules.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image28.png align="left")

1. Navigate to **Security Groups** on the left side panel, under **Network & Security**.
    
2. Select the **EC2\_SG** security group from the list, click on **Actions** and select **Edit inbound rules**.
    
3. Click on the **Add rule** button.
    
    * Type select **SSH** and Source select **Custom** and enter **0.0.0.0/0** in the textbox.
        
4. Click on the **Save rules** button.
    
5. Now again try to [SSH into EC2 Instance](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance) and you will be able to successfully SSH into the EC2 Instance.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image79.png align="left")

1. Since you have added the SSH Port in the Inbound of the EC2 Instance, all the SSH requests that originate from client side to server will be allowed.
    
2. Now try to ping [google.com](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance)
    
    ```plaintext
    ping google.com
    ```
    

1. The ping won't work because the security group outbound has no rules added.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/screenshot_2021-02-27_at_8.16.19_pm.png align="left")

1. Navigate to **Security Groups** on the left side panel, under **Network & Security**.
    
2. Select the **EC2\_SG** security group from the list, click on **Actions** and select **Edit outbound rules**.
    
3. Click on the **Add rule** button.
    
    * Type select **All traffic** and Source select **Custom** and enter **0.0.0.0/0** in the textbox.
        
4. Click on the **Save rules** button.
    
5. Now navigate back to the EC2 instance terminal and you can again try to ping the [google.com](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance)
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image31.png align="left")

1. The ping works because now we have enabled all the traffic that initiates from the server to any destination is allowed.
    
2. Stop the ping :
    
    * \[ctrl\] + c or \[control\] + c
        
3. Now close the EC2 terminal.
    

## **Task 10 : Understand the NACL rules**

1. When you create a VPC, a default Network ACL is created that allows both inbound and outbound.
    
2. Navigate to **VPC** by clicking on the **Services** menu in the top, then click on **VPC** in the **Networking & Content Delivery** section.
    
3. Navigate to **Network ACLs** on the left panel.
    
4. Select the **NACL** from the list which says the **VPC ID** as **AWS\_VPC**.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image81.png align="left")

1. Now click on **Actions** and select **Edit inbound rules**.
    
2. Click on the **Remove** button to remove **Rule Number 100** and then click on **Save changes**.
    
3. Similarly select the same NACL and click on **Actions** and select **Edit outbound rules** .
    
4. Click on the **Remove** button to remove **Rule Number 100** and then click on **Save changes**.
    
5. Follow the steps to [SSH into EC2 Instance](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance) but you won't be able to SSH into the EC2 instance because in the NACL you haven’t added any rules.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image28.png align="left")

1. Navigate to **Network ACLs** on the left panel.
    
2. Select the **NACL** from the list which says the **VPC ID** as **AWS\_VPC**.
    
3. Now click on **Actions** and select **Edit inbound rules**.
    
4. Click on the **Add new rule** button.
    
    * Rule Number : Enter **100**
        
    * Type : Select **SSH(22)**
        
    * Source : Enter **0.0.0.0/0**
        
    * Allow/Deny : Select **Allow**
        
5. Click on **Save changes**.
    
6. Now again try to [SSH into EC2 Instance](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance)**,** still the SSH fails because the ssh request reaches the EC2 instances but the response fails because the NACL outbound does not allow any traffic.
    
7. Navigate to **Network ACLs** on the left panel.
    
8. Select the **NACL** from the list which says the **VPC ID** as **AWS\_VPC**.
    
9. Now click on **Actions** and select **Edit outbound rules**.
    
10. Click on the **Add new rule** button.
    
    * Rule Number : Enter **100**
        
    * Type : Select **Custom TCP**
        
    * Port range : Enter **1024-65535**
        
    * Source : Enter **0.0.0.0/0**
        
    * Allow/Deny : Select **Allow**
        
11. Click on **Save changes**.
    
12. Here we are enabling the ephemeral port range because the client request will come from one of these ports.
    
13. Now again try to [SSH into EC2 Instance](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance), and its success.
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image79.png align="left")

1. In Network ACL, if ports are enabled in both inbound and outbound then only the connection will be successful.
    
2. Navigate to **Network ACLs** on the left panel.
    
3. Select the **NACL** from the list which says the **VPC ID** as **AWS\_VPC**.
    
4. Now click on **Actions** and select **Edit inbound rules**.
    
5. Click on the **Add new rule** button.
    
    * Rule Number : Enter **200**
        
    * Type : Select **ALL** **ICMP - IPv4**
        
    * Source : Enter **0.0.0.0/0**
        
    * Allow/Deny : Select **Allow**
        
6. Click on **Save changes**.
    
7. Now click on **Actions** and select **Edit outbound rules**.
    
8. Click on the **Add new rule** button.
    
    * Rule Number : Enter **200**
        
    * Type : Select **ALL** **ICMP - IPv4**
        
    * Source : Enter **0.0.0.0/0**
        
    * Allow/Deny : Select **Allow**
        
9. Click on **Save changes**.
    
10. Now try to ping [google.com](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance)
    
    ```plaintext
    ping google.com
    ```
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/image31.png align="left")

1. Stop the ping :
    
    * \[ctrl\] + c or \[control\] + c
        

> ### **Do You know?**
> 
> NACL rules are evaluated based on their rule numbers in ascending order. The lowest numbered rule that matches the traffic takes precedence. When a rule matches, the action specified in that rule (allow or deny) is applied, and no further rule evaluation occurs for that particular traffic.

## **Task 11: Validation Test**

1. Once the lab steps are completed, please click on the **Validation** button on the left side panel.
    
2. This will validate the resources in the AWS account and displays whether you have completed this lab successfully or not.
    
3. Sample output : 
    

![](https://labresources.whizlabs.com/416aa0eefd1aa5ca94376d05cfc0e248/sss_54_24.gif align="left")

## **Task 12: Delete AWS Resources**

### **Deleting EC2 Instance**

1. Make sure you are in the **US East (N. Virginia)** Region. 
    
2. Navigate to EC2 by clicking on the **Services** menu in the top, then click on **EC2** under the **Compute** [section.Now](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance) select the EC2 instance that you have created, click on the **Instance State** and click on the **Terminate instance** option.
    
3. Click on **Terminate** button and your EC2 will start terminating.
    

# **Completion and Conclusion**

1. You have successfully created an Amazon VPC.
    
2. You have successfully created a Public subnet.
    
3. You have successfully created and attached an Internet Gateway.
    
4. You have successfully created a Public Route Table and associated it with the subnet.
    
5. You have successfully added the public Route in the Route table.
    
6. You have successfully created a Security group.
    
7. You have successfully launched an EC2 instance.
    
8. You have successfully understood security group rules.
    
9. You have successfully created a Network ACL.
    
10. You have successfully understood NACL rules.
    

# **End Lab**

1. Sign out of AWS Account.
    
2. You have successfully completed the lab.