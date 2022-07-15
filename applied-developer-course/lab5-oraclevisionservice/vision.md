# Oracle Vision Service - Pre-Built models

## Introduction 

Oracle Cloud Infrastructure Vision is an AI service for performing deep-learning-based image analysis at scale, that is accessible using the OCI Console, REST APIs, SDKs and CLI. Vision service features are thematically split between Document AI for document-centric images and Image Analysis for object and scene-based images. 

With pre-built models available out of the box, developers can easily build image recognition and text recognition into their applications without machine learning (ML) expertise.  For industry -specific use cases, developers can automatically train custom vision models using their own data. 

In this session, we will walk through the OCI console to familiarize ourselves with the Vision service. We’ll discuss the data requirements and formats, and show you how to upload to Oracle Object storage for later to train our models. 


***Estimated Time***: 2 hours

### Objectives

In this lab, you will:
- Understand the data requirements and data formats for analyzing images using OCI Vision

- Upload data into OCI (Oracle Cloud Infrastructure) Object Storage

- Get familiar with the OCI console and be able to demo key OCI Vision features  


### Pre-requisites 

-	A free tier or paid tenancy in OCI (Oracle Cloud Infrastructure)
-	Familiarity with OCI Object Storage is desirable, but not required


## Policy Setup

Before you start using OCI Vision, your tenancy administrator should set up the following policies by following below steps:

1. Navigate to Policies

    Log into OCI Cloud Console. Using the Burger Menu on the top left corner, navigate to Identity & Security and click it, and then select Policies item under Identity.


    ![](images/policy1.png " ")


2. Create Policy

   Click Create Policy 

   ![](images/policy2.png " ")

3. Create a new policy with the following statements:

   If you want to allow all the users in your tenancy to use vision service, create a new policy with the below statement:     

    ```
    <copy>
    allow any-user to use ai-service-vision-family in tenancy
    </copy>
    ```

    ![](images/policy3.png " ")

    If you want to limit access to a user group, create a new policy with the below statement:

    ```
    <copy>
    allow group <group-name> to use ai-service-vision-family in tenancy
    </copy>
    ```

    ![](images/policy4.png " ")


## Task 1: Understand the data requirements for OCI AI Vision service

The vision service works with multiple formats of image data in order to detect objects, assign labels to images, extract text, and more. The service accepts data through Object Storage and locally stored images (if using via OCI console).

The service offers sync and async APIs to analyze images, with data requirements for each detailed below:

| API | Description | Supported Input Format |
| -------- |:-------:| -----:|
| sync API (analyzeImage, analyzeDocument) | Analyzes individual images |<p>* JPG, PNG, (PDF and Tiff for analyzeDocument) <br>*Up to 8 MB<br> *Single image input<br></p>|
| async API/jobs/startImageAnalysisjob/jobs/start | Analyze multiple images or multi-page PDFs |<p>* JPG, PNG (PDF and Tiff for analyzeDocument)<br>* Up to 2000 images input<br> * Supports multi-page PDF<br></p>| 


## Task 2: Upload Data to Object Storage 

1. Create an Object Storage Bucket (This step is optional in case the bucket is already created)

a. First, From the OCI Services menu, click Object Storage.

![](images/cloud-storage-bucket.png " ")


## Task 3: Demo Vision Service using the OCI Console
