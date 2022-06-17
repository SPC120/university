
<!-- Updated June 15, 2022 -->
# Introduction to OCI

## Introduction

This lab will introduce you to Oracle Cloud Infrastructure (OCI), and take you through the console and cover a few of the foundational services that are frequently used with IaaS and PaaS services.  You will also create a Virtual Cloud Network and spin up a compute instance and install and access a web server on that instance.

[](youtube:a6Jm7lYaCWI)

Estimated lab time: 120 minutes

### Objectives

-   Learn how to access and navigate the OCI console.
-   Understand the basic essentials to working with OCI.
-   Create a VCN and compute instance, and install and access a web server.

### Prerequisites

-   Access to an OCI tenancy.  

## Task 1: Access The OCI Console

1. Log in to the Oracle Cloud.  At the time this workshop was being created OCI was updating it's support for federated identity management, and so the log-in screens will be different from these screen shots.  This [blog](https://blogs.oracle.com/cloudsecurity/post/oci-federation-with-oci-iam-identity-domains) and this [whitepaper](https://www.oracle.com/a/ocom/docs/security/what-oci-iam-customers-should-expect.pdf) explains the current (June 2022) and near future approach to federating OCI users and groups, which most developer customers will likely adopt.
2. Once you are logged in, you are taken to the cloud services dashboard where you can see all the services available to you. Click the navigation menu in the upper left to show top level navigation choices.

https://blogs.oracle.com/cloudsecurity/post/oci-federation-with-oci-iam-identity-domains
https://www.oracle.com/a/ocom/docs/security/what-oci-iam-customers-should-expect.pdf


    ![](./images/picture100-36.png " ")

Regions:  https://docs.oracle.com/en-us/iaas/Content/General/Concepts/regions.htm
    
## Task 2: Learn Identity and Access Management Basics

1. Click **Create Autonomous Database** to start the instance creation process.


    ![](./images/picture100-23.png " ")


2.  This brings up the __Create Autonomous Database__ screen where you will specify the configuration of the instance.
3. Provide basic information for the autonomous database:

    - __Choose a compartment__ - Select a compartment for the database from the drop-down list.
   
## Task 3: Learn Networking Basics

Although you can connect to your autonomous database from local PC desktop tools like Oracle SQL Developer, you can conveniently access the browser-based SQL Worksheet directly from your Autonomous Data Warehouse or Autonomous Transaction Processing console.

## Task 4: Learn Storage Basics

Run a query on a sample Oracle Autonomous Database data set.

## Task 5: Learn Compute Basics

## Task 6: Access Cloud Shell


## Troubleshoot Tips

    If you are having problems with any of the labs, please visit the Need Help? tab.


