---
title: "Discover sensitive data present in S3 bucket using Amazon Macie"
datePublished: Fri Dec 22 2023 07:11:26 GMT+0000 (Coordinated Universal Time)
cuid: clqgameja000008jpcyjv3l5q
slug: discover-sensitive-data-present-in-s3-bucket-using-amazon-macie
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1703229034171/6adf6216-2c2a-4b59-9bc0-692c01548a3b.png
tags: sensitive-data, s3-bucket, amazon-macie

---

# **Lab Steps**

## **Task 1: Sign in to AWS Management Console**

1. Click on the **Open Console** button, and you will get redirected to AWS Console in a new browser tab.
    
2. On the AWS sign-in page,
    
    * Leave the Account ID as default. Never edit/remove the 12 digit Account ID present in the AWS Console. otherwise, you cannot proceed with the lab.
        
    * Now copy your **User Name** and **Password** in the Lab Console to the **IAM Username and Password** in AWS Console and click on the **Sign in** button.
        
3. Once Signed In to the AWS Management Console, Make the default AWS Region as **US East (N. Virginia) us-east-1.**
    

## **Task 2: Enable Macie for the account**

1. Make sure you are in the **US East (N. Virginia) us-east-1** Region. 
    
2. Navigate to **Amazon Macie** by clicking on the **Services** menu in the top, then click on  **Amazon Macie** in the **Security, Identity & Compliance** section.
    
3. On the home page, click on the **Get started** button to configure Amazon Macie.
    
    ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma2.png align="left")
    
4. On the Get started page, click on the **Enable Macie** button.
    
    ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma3.png align="left")
    

## **Task 3: Create a Macie job**

1. Macie will try to find out all the details of the account, which may take some time. No need to wait, simply click on the **Create job** button.
    
    ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/macie_35_52.png align="left")
    
2. For Step-1, Choose S3 Bucket,
    
    **Note:** If you are getting any error notification, leave it and continue the rest steps.
    
    * To Select the bucket, click on the **Add filter criteria** field and click on the **Bucket name**.
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/macie_s3_filter_49_04.png align="left")
        
    * Type ***whizlabs*** and select the bucket name starting with **whizlabs**, and click on the **Next** button.
        
        * **NOTE** : If bucket is not listed, wait for 2–5 minutes and **refresh** the page 2–3 times.
            
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma5.png align="left")
        
3. For Step-2, Review S3 buckets
    
    * Keep everything as default and click on the **Next** button.
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma6.png align="left")
        
4. For Step-3, Refine the scope,
    
    * In Sensitive data discover options: Select **One-time job**
        
    * Click on the arrow to expand the window of **Additional settings**
        
    * Let the Object criteria be default as **File name extensions**.
        
    * Write ***csv*** in the textbox and click on the **Include** button.
        
    * Once done, click on the **Next** button to proceed.
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma8.png align="left")
        
5. For Step-4, Select managed data identifiers,
    

* Selection type: Choose **All**
    
* Click on the **Next** button.
    

1. For Step-5, Custom data identifiers,
    
    * Click on the **Manage custom identifiers**, to create one.  
        **Note: This will open in the New tab, please enable a pop-up, if it doesn't open in one click.**
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma9.png align="left")
        
2. Click on the **Create** option present on the top right.
    
    * Fill in the details, as follows:
        
    * Name: Enter ***Whiz***
        
    * Description: Enter ***This identifier finds the data present in the format of AB-01 i.e. two characters, dash and followed by two numbers.***
        
    * Regular expression: Enter ***\[a-z\]{2}-\[0-9\]{2}***
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma12.png align="left")
        
    * Keep all other options as default.
        
    * Click on the **Submit** button to create the **Custom identifier.**
        
    * Go back to the **previous tab** and click on the **refresh** icon to see the newly created Custom identifier.
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma13.png align="left")
        
    * Once refreshed, you will be able to see the Whiz identifier listed here. Click on the **Next** button. 
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma15.png align="left")
        
3. For Step-6 : Select allow lists : Keep it default and click on **Next** button
    
4. For Step-7, In General Setting : Enter a name and description,
    
    * Name: Enter ***WhizJob***
        
    * Description: Enter ***This job scans the bucket with a name starting as whizlabs and gathers its finding based on the regular expression pattern.***
        
    * Click on the **Next** button.
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma16.png align="left")
        
5. For Step-8, Review and create,
    
    * Review everything, click on the **Submit** button present below.
        
6. Job is now created successfully.
    

## **Task 4: Macie job run and findings**

1. Once the job is created, it will start running immediately. 
    
2. The job runs for approximately 10 minutes and gathers the findings.
    
3. After 10 minutes, the status is changed to Complete.
    
    ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma18.png align="left")
    
4. To view the Findings for the job, perform the following:
    
5. Click on the **Job** present there.
    
6. Select **Show results**
    
7. And Choose **Show findings**
    
    ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/findings.png align="left")
    
8. To check the exact results, open the finding.
    
    ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma20.png align="left")
    
9. Perform the following task:
    
    * **Select** the present finding
        
    * Click on the **Actions** button
        
    * And, Choose **Export (JSON)**
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma21.png align="left")
        
    * JSON present here is in Read-only format, you may choose to download the complete report.
        
        ![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/ma22.png align="left")
        

> ### **Do you know?**
> 
> Amazon Macie is an AWS service designed to enhance data security by automatically discovering, classifying, and protecting sensitive data in Amazon S3. It utilizes machine learning and natural language processing techniques to identify various types of sensitive information, such as personally identifiable information (PII), financial data, intellectual property, and more.

## **Task 5: Validation Test**

1. Once the lab steps are completed, please click on the **Validate button** on the Right side panel.
    
2. This will validate the resources in the AWS account and displays whether you have completed this lab successfully or not.
    
3. Sample output : 
    

![](https://labresources.whizlabs.com/c388ab142e7a1817c9459f162e97b746/macie_27_25.gif align="left")

# **Completion and Conclusion**

1. You have successfully enabled Amazon Macie.
    
2. You have successfully created a Macie job.
    
3. You have successfully run the Macie job and retrieved the data.
    

# **End Lab**

1. Sign out of AWS Account.
    
2. You have successfully completed the lab.
    
3.