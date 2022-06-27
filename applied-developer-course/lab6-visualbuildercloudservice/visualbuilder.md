<!-- Updated June 15, 2022 -->

# Provision Visual Builder Cloud Service Instance

## Introduction

This lab walks you through the steps to quickly provision an Visual Builder Cloud Service on Oracle Cloud. In this lab we will create Mobile application which will take photo of ID card and then store it in Object Storage. Further we will also use Vision service to get required detail from the image that user took and store it in Autonomous Database.

Estimated lab time: 2 hours

### Objectives

- Provision a new Visual Builder Cloud Service Instance
- Learn how to connect to your new autonomous database using ORDS and Vision Service.

### Prerequisites

- This lab requires completion of the **Get Started** section in the Contents menu on the left.

## Task 1: Create Visual Builder Cloud Service Instance

![](images/1.png " ")
![](images/2.png " ")
![](images/3.png " ")
![](images/4.png " ")
![](images/5.png " ")
![](images/6.png " ")


## Task 2: Configure Service Connections

In this task, we will create 4 service connections. Prior to creating service connections to OCI services, you first have to get details to generace OCI signature tenancy OCID, user OCID, fingerprint and key.

### OCI Signature details

![](images/8.png " ")
![](images/9.png " ")
![](images/10.png " ")
![](images/11.png " ")

### Object Storage

![](images/7.png " ")
![](images/12.png " ")
![](images/13.png " ")
![](images/14.png " ")
![](images/15.png " ")
![](images/16.png " ")
![](images/17.png " ")

[OCI Rest APIs](https://docs.oracle.com/en-us/iaas/api/)

[Object Storage API](https://docs.oracle.com/en-us/iaas/api/#/en/objectstorage/20160918/Object/PutObject)

```
https://objectstorage.us-{region}-1.oraclecloud.com/n/{namespaceName}/b/{bucketName}/o/{objectName}
```

## Task 3: Create Mobile Application

## Task 4: Publish Application and test

## Troubleshoot Tips

    If you are having problems with any of the labs, please visit the Need Help? tab.
