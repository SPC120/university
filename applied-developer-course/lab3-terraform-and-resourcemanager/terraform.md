<!-- Updated June 29, 2022 -->
# Introduction to Terraform and Oracle Resource Manager (ORM)

## Introduction

**Estimated lab time: 120 minutes**

### Objectives

-   Create a VCN using the Quick Start Template
-   Create a Compute Instance using the Quick Start Template
-   Download the ORM Stack for the Compute Instance and Enhance it
-   Create an ORM Stack using the Discover Feature
-   Explore Advance Features of Terrafrom and Oracle Resource Manager (ORM)
-   Destroy all OCI Resources 

### Prerequisites

-   Access to an OCI tenancy.
-	Compartment **CareClinic**
-	SSH Public/Private Key Pair

## Task 1: Login in to the Oracle Cloud 

1. Log in to the Oracle Cloud from <https://www.oracle.com> , click on **View Accounts** then **Sign in to Cloud**

	![](./images/task1/image1.png " ")

2. Enter the **Cloud Account Name** and click **Next**

	![](./images/task1/image2.png " ")

3. Select **oracleidentitycloudservice** as the Identity Provider and click **Continue**

	![](./images/task1/image3.png " ")

4. Enter your **username** (this may be your email address) and **password** and click on **Sign In**

	![](./images/task1/image4.png " ")

5. You are now on the **Get Started** page of the Oracle Cloud Infrastructure (OCI) Console

	![](./images/task1/image5.png " ")


## Task 2: Access Oracle Resource Manager

1.  From Oracle Cloud Infrastructure (OCI) Console click on the navigation menu in the upper left to display the OCI Service Groupings

	![](./images/task2/image1.png " ")

2.  Select **Developer Services** then **Overview** under the **Resource Manager** group

	![](./images/task2/image2.png " ")

3.  You are now presented with the **Resource Manager Overview** page

	![](./images/task2/image3.png " ")

## Task 3: Create a VCN using the Quick Start Template

1.  From the **Resource Manager Overview** page, scroll down to the **Create** section and click on the **Provision a VCN that includes....** option

	![](./images/task3/image1.png " ")

2.  Enter the name **VCN-Terraform** and select the Compartment **CareClinics** and click **Next**

	![](./images/task3/image2.png " ")

3.  Accept the defaults on this page and click **Next**

	![](./images/task3/image3.png " ")

4.  Accept the defaults and click **Create**

	![](./images/task3/image4.png " ")

5.  The **VCN-Terraform** Resource Manager Stack is now created

	![](./images/task3/image5.png " ")

6.  Click **Plan** then **Plan** again on the pop-out to execute a Plan against the Resource Manager Stack

	![](./images/task3/image6.png " ")

7.  The Plan is now executed, once complete, it will change to green and have a **Succeeded** status

	![](./images/task3/image7.png " ")

	![](./images/task3/image8.png " ")

8.  You can scroll through the **Logs** for the Plan execution and see what resources will be added. You can also click on **Download Logs**. You will see that **6** resources will be created in OCI when this stack is applied. The resources created are

	-   Default Route Table
	-   Internet Gateway
	-   Default Subnets for AD1, AD2, AD3 (AD = Availability Domain)
	-   Default Security List
	-   Default DHCP Options
	-   Virtual Cloud Network (VCN)

	![](./images/task3/image9.png " ")

9.  To execute this Stack and create the OCI Services listed in the Plan, scroll back up and click on **Stack Details** then click on **Apply** then **Apply** in the pop-out.

	![](./images/task3/image10.png " ")

	![](./images/task3/image11.png " ")

10. The Stack is now **IN PROGRESS**, once completed, the status will change to **SUCCEEDED** .

	![](./images/task3/image12.png " ")

	![](./images/task3/image13.png " ")

11. Let's examine the **Logs** to see what was created. You can see from the **Logs** the 6 OCI resources were created.

	![](./images/task3/image14.png " ")

12. You can also click on **Outputs** the resources listed along with their corresponding OCIDs are listed.

	![](./images/task3/image15.png " ")

13. To see the VCN resources created within the OCI Console, click on the navigation menu in the upper left, select **Networking**, **Virtual Cloud Networks**

	![](./images/task3/image16.png " ")

14. You are presented with the VCN Page where you will see the **testVCN** created by the Oracle Resource Manager (ORM) Stack. Be sure your compartment is **CareClinics.** Click on the **testVCN** name to see the details.

	![](./images/task3/image17.png " ")

15. Here you will see can see all the information related to the VCN **testVCN**. You can also see and access all the resources that make up this VCN. Feel free to click around and explore.

	![](./images/task3/image18.png " ")


## Task 4: Create a Compute Instance using the Quick Start Template

## Task 4: Download an ORM Stack and Enhance it

## Task 5: Create an ORM Stack using the Discover Feature

## Task 6: Explore Advance Features

## Task 7: Destroy all OCI Resources

## Homework: Create an OCI Service Using Terraform - ORM

## Additional Resources