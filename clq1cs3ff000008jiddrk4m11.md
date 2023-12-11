---
title: "How to setup an AWS Site-to-Site (S2S) VPN Connection"
datePublished: Mon Dec 11 2023 20:15:19 GMT+0000 (Coordinated Universal Time)
cuid: clq1cs3ff000008jiddrk4m11
slug: how-to-setup-an-aws-site-to-site-s2s-vpn-connection
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702325672112/e87cf973-7cca-4642-ba77-bc460c7d92a8.png
tags: devops, awssecurity, awsdevops

---

## **Task 1: Sign in to AWS Management Console**

1. Click on the **Open Console** button, and you will get redirected to AWS Console in a new browser tab.
    
2. On the AWS sign-in page,
    
    * Leave the Account ID as default. Never edit/remove the 12 digit Account ID present in the AWS Console. otherwise, you cannot proceed with the lab.
        
    * Now copy your **User Name** and **Password** in the Lab Console to the **IAM Username and Password** in AWS Console and click on the **Sign in** button.
        
3. Once Signed In to the AWS Management Console, Make the default AWS Region as **US East (N. Virginia) us-east-1.**
    

## **Task 2: Create a VPC in the Mumbai Region**

1. Make sure you are in the **Mumbai Region**. 
    
2. Navigate to **VPC** by clicking on the **Services** menu in the top, then click on **VPC** in the **Network & Content Delivery** section.
    
3. Navigate to **Your VPC's** on the left panel and click on the **Create VPC**.
    
    * Select **VPC only**
        
    * Name tag : Enter ***On\_Premises\_Network*** 
        
    * IPv4 CIDR block : Enter ***10.0.0.0/16***
        
        ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_task2_02_13.png align="left")
        
4. Leave everything else as default and click on the **Create VPC**.
    
5. You have successfully created the VPC
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image23.png align="left")

## **Task 3: Create a Public subnet**

1. Navigate to **Subnets** from the left side menu and click on **Create Subnet**.
    
    * VPC ID : Select the **On\_Premises\_Network** VPC from the list.
        
    * Subnet name : Enter ***Public\_subnet***
        
    * Availability Zone : Select **ap-south-1a**
        
    * IPv4 CIDR block : Enter ***10.0.1.0/24***
        
        ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_task3_04_09.png align="left")
        

**Note** : In the **Mumbai** region select **ap-south-1a**, because in other regions t2.micro EC2 launch may **fails**.

1. Now click on the **Create Subnet** 
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image27.png align="left")

## **Task 4: Create and attach an Internet Gateway**

1. Navigate to the **Internet Gateways new** from the left side menu and click on the **Create Internet Gateway** 
    
    * Name tag : Enter ***On\_Premises\_IGW***
        
2. Click on the **Create Internet Gateway** 
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_task4_06_58.png align="left")

1. Now click on the **Actions** and select **Attach to VPC**.
    
    * Available VPCs :  select **On\_Premises\_Network** from the list.
        
2. Now click on the **Attach Internet Gateway** 
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image87.png align="left")

## **Task 5: Create a Public Route Table and associate it with the subnet**

1. Navigate to **Route Tables** on the left side panel and click on the **Create route table** button.
    
    * Name tag : Enter ***PublicRT***
        
    * VPC\* : Select the **On\_Premises\_Network** from the list.
        
2. Now click on the **Create route table** button.
    
3. Now click on **Route Tables** in the left panel and select the **PublicRT** from the list and go to the **Subnet associations** tab in below.
    
4. Click on the **Edit subnet associations** button.
    
5. Now select the subnet **Public\_subnet** and click on the **Save associations** button.
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/task_5_step_5.jpg align="left")

## **Task 6: Add public Route in the Route table**

1. Navigate to **Route Tables** on the left side panel and select the **PublicRT** from the list.
    
2. Go to the **Routes** tab in below and click on the **Edit routes** button.
    
3. Now click on the **Add route** button.
    
    * Destination : Enter ***0.0.0.0/0***
        
    * Target : select **Internet Gateway** and then select the **Internet Gateway id.**
        

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/task_6_step_3.jpg align="left")

1. Click on the **Save changes** button.
    

## **Task 7: Launch an EC2 instance**

1. Make sure you are in the **Mumbai Region.**
    
2. We will be launching this EC2 instance to act as an Public Router in On-Premises Network, for that we will be installing **Openswan** later in this lab.
    
3. Navigate to **EC2** by clicking on the **Services** menu in the top, then click on **EC2** in the **Compute** section.
    
4. Navigate to **Instances** from the left side menu and click on **Launch Instances** 
    
5. Enter Name as ***On\_Premises\_Router***
    
6. **Choose an Amazon Machine Image (AMI):** Search for **Amazon Linux 2 AMI** in the search box and click on the **select** button.  
      
    
7. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_251.png align="left")
    
8. Choose an Instance Type: select **t2.micro  
      
    **
    
9. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_252.png align="left")
    
10. Key Pair : Choose **Create a new key Pair** from the dropdown list.
    
    * Key pair name : Enter ***Router-key***
        
    * Key Pair Type: Select **RSA**
        
    * Click on **Create key pair** button to download the key to your local machine.  
        
11. Under **Network Settings,** click on **Edit** button. 
    
    * Network : Select **On\_Premises\_Network**
        
    * Subnet : leave as default
        
    * Auto-assign Public IP : Select **Enable  
        **
        
        ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_253.png align="left")
        

13. Configure Security Group:
    
    * Firewall(security groups) : Select **Create a new security group**
        
    * Security group name : Enter ***On\_Premises\_Router\_SG***
        
    * Description : Enter ***Security group for public Router***
        
    * To add **SSH**,
        
        * Choose Type: **SSH**
            
        * Source: **Anywhere** (From ALL IP addresses accessible).
            
    * For **All TCP,** 
        
        * Click on **Add Security group rule** button.
            
        * Choose Type: **All TCP** 
            
        * Source: **Custom** and Enter ***30.0.0.0/16*** in the textbox.
            
    * For **IPv4 ICMP,**
        
        * Click on **Add Security group rule** button.
            
        * Choose Type: **All ICMP - IPv4**
            
        * Source: **Custom** and Enter ***30.0.0.0/16*** in the textbox.  
              
            
14. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/2022-08-01_17_47_07-ec2_management_console.png align="left")
    
    * **Note** : we will be allowing SSH port from anywhere (Lab practice) and we are allowing all TCP and ICMP AWS side VPC in N.Virginia Region which we will create next. (**30.0.0.0/16** will be the VPC CIDR)  
          
        
    
15. Click on **Launch Instance** button.
    
16. **Launch Status:** Your instance is now launching, Click on the instance ID and wait for complete initialization of instance till status change to **Running**.
    
17. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image55.png align="left")
    
18. Note down the sample **IPv4 Public IP** Address of the EC2 instance and place it in your text editor. A sample is shown in the screenshot below.
    
19. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image40.png align="left")
    

## **Task 8: Create a VPC in N.Virginia Region**

1. Click on this link [https://console.aws.amazon.com/console/home?region=us-east-1#](https://console.aws.amazon.com/console/home?region=us-east-1#) to open the N.Virginia region.
    
2. Make sure you don't close the **Asia Pacific (Mumbai)** Region. Maintain both regions on different tabs in your browser.
    
3. Navigate to **VPC** by clicking on the **Services** menu in the top, then click on **VPC** in the **Network & Content Delivery** section.
    
4. Navigate to **Your VPC new** on the left panel and click on the **Create VPC** 
    
    * Select **VPC Only**
        
    * Name tag : Enter ***AWS\_Network***
        
    * IPv4 CIDR block : Enter ***30.0.0.0/16***
        
5. Leave everything else as default and click on the **Create VPC** 
    
    ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_task8_07_41.png align="left")
    
6. You have successfully created the VPC
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image48.png align="left")

## **Task 9: Create a Private subnet**

1. Navigate to **Subnets new** from the left side menu and click on **Create Subnets** 
    
    * VPC ID : Select the **AWS\_Network** VPC from the list.
        
    * Subnet name : Enter ***Private\_subnet***
        
    * Availability Zone : select **us-east-1a**
        
    * IPv4 CIDR block : Enter ***30.0.1.0/24***
        
        ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_task9_08_14.png align="left")
        
2. Now click on the **Create Subnet** 
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image99.png align="left")

## **Task 10: Launch an EC2 instance**

1. Make sure you are in the **N.Virginia Region**.
    
2. Navigate to **EC2** by clicking on the **Services** menu in the top, then click on **EC2** in the **Compute** section.
    
3. Navigate to **Instances new** from the left side menu and click on **Launch Instances** 
    
4. Enter Name as ***AWS\_EC2***
    
5. **Choose an Amazon Machine Image (AMI):** Search for **Amazon Linux 2 AMI** in the search box and click on the **select** button.  
      
    
6. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_251.png align="left")
    
7. **Choose an Instance Type:** select **t2.micro  
      
    **
    
8. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_252.png align="left")
    
9. **Key Pair :** Choose **Create a new key Pair** from the dropdown list.
    
    * Key pair name : Enter ***public-key***
        
    * Key Pair Type: Select **RSA**
        
    * Click on **Create key pair** button to download the key to your local machine.
        
10. Under **Network Settings,** click on **Edit** button. 
    
    * Network : Select **AWS\_Network**
        
    * Subnet : leave as default
        
    * Auto-assign Public IP : Select **Disable**
        
11. Configure Security Group:
    
    * Firewall(security groups) : Select **Create a new security group**
        
    * Security group name : Enter ***AWS\_EC2\_SG***
        
    * Description : Enter ***Security group for public Router***
        
        * To add **SSH**,
            
            * Choose Type: **SSH**
                
            * Source: **Anywhere** (From ALL IP addresses accessible).
                
        * For **All TCP,** 
            
            * Click on **Add Security group rule** button.
                
            * Choose Type: **All TCP** 
                
            * Source: **Custom** and Enter***10.0.0.0/16*** in the textbox.
                
        * For **IPv4 ICMP,**
            
            * Click on **Add Security group rule** button.
                
            * Choose Type: **All ICMP - IPv4**
                
            * Source: **Custom** and Enter***10.0.0.0/16*** in the textbox.  
                  
                
12. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/2022-08-01_17_47_07-ec2_management_console.png align="left")
    
13. Click on **Launch Instance** button.
    
14. **Launch Status:** Your instance is now launching, Click on the instance ID and wait for complete initialization of instance till status change to **Running**.  
      
    
15. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image58.png align="left")
    
16. Since this EC2 is created in a private subnet, the machine will only have Private IP so, note down the sample **IPv4 Private IP** Address of the EC2 instance. A sample is shown in the screenshot below.
    
17. ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image90.png align="left")
    

## **Task 11: Create a Customer Gateway in N.Virginia Region**

1. Now navigate to the other browser tab, in which **N.Virginia region** is used.
    
2. Navigate to **VPC** by clicking on the **Services** menu in the top, then click on **VPC** in the **Network & Content Delivery** section.
    
3. Now scroll down and select **Customer Gateway** under **Virtual Private Network (VPN)**.
    
4. Click on the **Create Customer Gateway**
    
    * Name : Enter ***On\_Premises\_Network\_Gateway***
        
    * IP Address : Enter **On-premises EC2 instance IPv4 Public IP (EC2 act as the Public Router in Mumbai Region)**
        
    * Leave everything else as default.
        

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_255.png align="left")

1. Click on the **Create Customer Gateway** 
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_256.png align="left")

## **Task 12: Create a Virtual Private Gateway in N.Virginia Region**

1. Now scroll down and select **Virtual Private Gateways** under **Virtual Private Network (VPN)**.
    
2. Click on the **Create Virtual Private Gateway** 
    
    * Name tag : Enter ***AWS\_Network\_VPG***
        
    * ASN : Leave as Default
        
3. Now click on the **Create Virtual Private Gateway**
    
4. Now the state will be **detached** for the Virtual Private gateway that you have created.
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_258.png align="left")

1. Now you need to attach the VPG to the VPC that you have created in the same region.
    
2. Select the **Virtual Private gateway** that you just created, click on the **Actions** button and select **Attach to VPC.**
    
    * VPC : Select **AWS\_Network** from the list.
        
    * Now click on the **Attach to VPC** 
        
3. Now wait for a few seconds and refresh the aws console by clicking on the **Refresh** button and the state will be attached.
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_260.png align="left")

## **Task 13: Create a Site-to-Site VPN connection**

1. Now scroll down and select **Site-to-Site VPN Connections** under **Virtual Private Network(VPN)**.
    
2. Click on the **Create VPN Connection** 
    

**Note** : If you see any error in this page, kindly neglect it.

* Name tag : Enter ***AWS\_On\_Premises\_Connection***
    
* Virtual Private Gateway\* : Select **AWS\_Network\_VPG** from the list.
    
* Customer Gateway ID\* : Select **On\_Premises\_Network** from the list.
    
* Routing Options : Select **Static**
    
* Static IP Prefixes : Enter ***10.0.0.0/16*** in the textbox (Your On-Premises VPC CIDR)
    
* Tunnel Options :
    
    * Leave as default.
        
    * **Info** : The VPN creates 2 tunnels for High Availability and it uses IPSec Secure protocol to establish the connection. AWS will generate a pre shared key or you can add your own key. In this lab we will be using the key generated by AWS.
        

1. Now click on the **Create VPN Connection**  
    
2. Now it will take 3 to 4 Minutes to set up the VPN Connection.
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_262.png align="left")

1. Select the VPN Connection and on top, click on the **Download the configuration** to download the config file which you need to add to the EC2 instance which you're using as **Public Router in Mumbai Region**.
    
    * Vendor : Select **Openswan**
        
    * Platform : Select **Openswan**
        
    * Software : Leave default.
        

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/screenshot_263.png align="left")

1. Now click on the **Download** button and the configuration file will be downloaded to your local machine and note down the file name. Once done click on the close or cancel button.
    
2. Now Navigate to the **Tunnel Details** tab and you will be able to see that both tunnels are in down state, Next we are going to make the status as **UP.**
    

## **Task 14: Configure On-Premises Router**

1. You need to SSH into the EC2 instance (**On\_Premises\_Router**) that you have created in the **On\_Premises\_Network** VPC that you have created in the Mumbai Region. This EC2 will act as the Public Router of On-Premises Network.
    
2. Previously when the EC2 instance was launched, you have noted down the public IPv4 IP and if not navigate to the Mumbai region browser tab and copy the public IPv4 address.
    
3. Key Pair name as per the lab :  **Router-key**
    
4. Please follow the steps in [SSH into EC2 Instance](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance).
    
5. Once you have successfully SSH in to EC2, run the following commands :
    
    * Switch to root user :
        
        ```plaintext
        sudo -s
        ```
        
6. Install Openswan
    
    ```plaintext
    yum install openswan -y
    ```
    
7. Next make sure the last line in **/etc/ipsec.conf** is not commented. (NO **#** in the beginning)
    
    ```plaintext
    nano /etc/ipsec.conf
    ```
    
    * Scroll to the end and make sure the last line include **/etc/ipsec.d/\*.conf** has no hash **(#)** in the beginning.
        

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image100.png align="left")

* Click **\[Control\] + X** or **\[Ctrl\] + X** to exit the file.
    

1. Update **/etc/sysctl.conf** file
    
    ```plaintext
    nano /etc/sysctl.conf
    ```
    
    * Add the below 3 lines in end of this file with no hash (#) in the beginning and add each in new lines
        

<table><tbody><tr><td colspan="1" rowspan="1"><p>net.ipv4.ip_forward = 1</p></td></tr></tbody></table>

  
 

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image12.png align="left")

* Click **\[Control\] + X** or **\[Ctrl\] + X** to exit the file.
    
* Save modified buffer?  (Answering "No" will DISCARD changes.) : Enter **Y**
    
* File Name to Write: /etc/sysctl.conf : Hit **\[Enter\]** Key
    

1. Restart Network Service
    
    ```plaintext
    service network restart
    ```
    
2. Next we need to configure IPSec and pre-shared keys in Openswan.
    
3. For that you have **downloaded** a **configuration file** from the Site-to-site VPN page to your **local system**. Open that file in your text editor.
    
4. Create or open **/etc/ipsec.d/aws.conf** file
    
    ```plaintext
    vi /etc/ipsec.d/aws.conf
    ```
    
    * In the Configuration file, look for **point number 4**  under **IPSEC Tunnel #1** and copy the entire code below **point number 4**.
        

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/task_14_step_12.2.jpg align="left")

* Press " **i "** button in your keyboard to edit the file you have created.
    
* Paste the code in the file we opened.
    
* **Note: While pasting the code please remove white spaces at end of each line as well as replace the white spaces in the beginning of each line with tab space. If this is not followed the ipsec service won’t work**
    
* **Remove** the line **auth=esp** from the file (else the connection won't work)  
      
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/task_14_step_12.6.jpg align="left")

* Update **leftsubnet** and **rightsubnet**
    
    * leftsubnet= Enter ***10.0.0.0/16*** (On-premises VPC CIDR)
        
    * rightsubnet= Enter ***30.0.0.0/16*** (AWS VPC CIDR)  
          
        

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/task_14_step_12.7.jpg align="left")

* Click **\[Esc\]** button in the keyboard to exit the editing mode.
    
* Now type **:wq** and hit **\[Enter\]** Key to save the file.
    

1. Create or open **/etc/ipsec.d/aws.secrets** file
    
    ```plaintext
    vi /etc/ipsec.d/aws.secrets
    ```
    
    * In the Configuration file, look for **point number 5**  under **IPSEC Tunnel #1** and copy the entire code below.
        

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/task_14_step_13.2.jpg align="left")

* Press " **i "** button in your keyboard to edit the file you have created.
    
* Paste the secret key in the file you opened.
    
      
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/task_14_step_13.4.jpg align="left")

* Click **\[Esc\]** button in the keyboard to exit the editing mode.
    
* Now type **:wq** and hit **\[Enter\]** Key to save the file.
    

1. **Note** : we will not be using **IPSEC Tunnel #2** in this lab because Openswan only supports 1 tunnel. If you're using Cisco, Palo Alto, Fortinet Routes you will have an option to add the Tunnel 2. 
    
2. Now Navigate to **N.Virginia** Region and goto **VPC Console**.
    
3. Navigate to **Route Table** from the left side menu.
    
4. Now select the **RouteTable**, where VPC is mentioned as **AWS\_Network**.
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/task_14_step_17.jpg align="left")

1. Now Goto the **Route propagation** tab below and click on the **Edit route propagation** button.
    
2. Check the **Enable** checkbox and click on the **Save** button.
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/task_14_step_19.jpg align="left")

1. In case if your EC2 Session gets timed out. please follow the steps to [SSH into EC2 Instance](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance) again.
    
    * Switch to root user :
        
        ```plaintext
        sudo -s
        ```
        
2. Start IPSec service
    
    ```plaintext
    systemctl start ipsec
    ```
    
3. Check the status of IPSec
    
    ```plaintext
    systemctl status ipsec
    ```
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image53.png align="left")

## **Task 15: Test the connectivity between two Networks**

1. Now you have already copied the **Private IPv4** address of the **EC2** instance (**AWS\_EC2**) that you created in the **Private Subnet** of **N.Virginia** Region VPC.
    
2. In case if your EC2 Session gets timed out. please follow the steps to [SSH into EC2 Instance](https://business.whizlabs.com/labs/support-document/ssh-into-ec-instance) again.
    
3. Ping the private EC2 from the Public EC2 Instance which acts as Public Router in Mumbai Region.
    
    * Syntax : **ping** &lt;Private IPv4 Address&gt;
        
    * Example : **ping 30.0.1.31**
        
4. Now You can see we are able to ping an EC2 in a Private subnet from a Public Subnet where both EC2’s are in different VPC(Network).
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/image102.png align="left")

1. If you are able to ping the private EC2 instance in a different VPC, that means a connection is established between both VPC's. i.e VPN.
    
2. Now scroll down and select **Site-to-Site VPN Connection** under **Virtual Private Network(VPC)**.
    
3. Check the **Tunnel Details** and you will be able to see that **Tunnel 1** is **UP**. Tunnel 2 is Down because in Openswan only one tunnel can be configured and we only used Tunnel 1. (If the status is still DOWN wait for a few minutes to reflect the status in the AWS Management console). **Wait till the Tunnel is UP.**
    
4. **Note** : if no traffic is flowing from On-premises network to AWS Cloud network, then the **VPN tunnel will go down**. So always use a keep alive, wait or something else to keep the connection active.
    

> ### **Do You Know ?**
> 
> When setting up a Site-to-Site VPN connection between your on-premises network and your Amazon Virtual Private Cloud (VPC), AWS allows you to use BGP for dynamic routing over the VPN tunnel. BGP is an exterior gateway protocol widely used in the networking industry for exchanging routing information between different autonomous systems (AS).

## **Task 16: Validation Test**

1. Once the lab steps are completed, please click on the **Validation** button on the right side panel.
    
2. This will validate the resources in the AWS account and displays whether you have completed this lab successfully or not.
    
3. Sample output : 
    
    ![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/2_49_51.gif align="left")
    

## **Task 17: Delete AWS Resources**

## **Deleting EC2 Instance in N.Virginia region**

1. Make sure you are in the **US East (N. Virginia)** Region. 
    
2. Navigate to **EC2** by clicking on the **Services** menu in the top, then click on **EC2** under **Compute** section.
    
3. Now select the EC2 instance that you have created, click on **Instance State** and click on the **Terminate** **instance** option.
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/terminate_ec2.jpg align="left")

     4. Click on **Terminate** button and your EC2 will start terminating.

## **Deleting EC2 Instance Mumbai region**

1. Make sure you are in the **Asia Pacific  (Mumbai)** Region.
    
2. Navigate to **EC2** by clicking on the **Services** menu in the top, then click on **EC2** under **Compute** section.
    
3. Now select the EC2 instance that you have created, click on **Instance State** and click on the **Terminate instance** option.
    

![](https://labresources.whizlabs.com/16b946592707a2ad9ff58e2c0491a2b5/terminate_ec2.jpg align="left")

     4. Click on **Terminate** button and your EC2 will start terminating.

# **Completion and Conclusion**

1. You have successfully created a VPC in the Mumbai Region.
    
2. You have successfully created a Public subnet.
    
3. You have successfully created and attached an Internet Gateway.
    
4. You have successfully created a Public Route Table and associated it with the subnet.
    
5. You have successfully added the public Route in the Route table.
    
6. You have successfully launched an EC2 instance.
    
7. You have successfully created a VPC in N.Virginia Region.
    
8. You have successfully created a Private subnet.
    
9. You have successfully launched an EC2 instance.
    
10. You have successfully created a Customer Gateway in N.Virginia Region.
    
11. You have successfully created a Virtual Private Gateway in N.Virginia Region.
    
12. You have successfully created a Site-to-Site VPN connection.
    
13. You have successfully configured On-Premises Router.
    
14. You have successfully tested the connectivity between two Networks.
    

# **End Lab**

1. Sign out of AWS Account.
    
2. You have successfully completed the lab.