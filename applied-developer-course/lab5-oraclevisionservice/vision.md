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
| async API/jobs/startImageAnalysisjob/jobs/start | Analyze multiple images or multi-page PDFs | <p>* JPG, PNG (PDF and Tiff for analyzeDocument)<br>* Up to 2000 images input<br> * Supports multi-page PDF<br></p>| 


## Task 2: Upload Data to Object Storage 

1. Create an Object Storage Bucket (This step is optional in case the bucket is already created)

a. First, From the OCI Services menu, click Object Storage.

![](images/cloud-storage-bucket.png " ")

b. Then, Select Compartment from the left dropdown menu. Choose the compartment matching your name or company name.

![](images/compartment.png " ")

c. Next click Create Bucket

![](images/bucket.png " ")

d. Next, fill out the dialog box:

* Bucket Name: Provide a name
* Storage Tier: STANDARD

e. Then click Create

![](images/createBucket.png " ")

2. Upload image files into Storage Bucket

a. Switch to OCI Window and click the Bucket Name.
b. Bucket detail window should be visible. Click Upload

![](images/upload.png " ")

c. Click on Upload and then browse to file which you desire to upload.

![](images/uploaded.png " ")

More details on Object storage can be found on this page. [Object Storage Upload Page](https://oracle-livelabs.github.io/oci-core/object-storage/workshops/freetier/index.html?lab=object-storage) to see how to upload.

## Task 3: Demo Vision Service using the OCI Console

1. Navigate to the Vision Page of OCI Console

![](images/navigate-to-ai-vision-menu.png " ")

2. Use Document AI features

a. On the Vision page, select “Document AI” on the left navigation menu and provide a document or image from OCI object storage. You can also upload from local storage. In order to upload image from Object Storage Bucket, you will need image's URL Path.

![](images/template.png " ")

b. Image URL path can be found in the Object Storage Bucket where your image resides. Navigate to the bucket to locate object details that has the image URL path, as shown below. 

![](images/obj-details.png " ")
![](images/path.png " ")


c.  This invokes analyzeDocument API after the image is provided. Raw text extracted by our pre-trained multi-tenant model is displayed on the right.

![](images/document-ai.png " ")


| Feature | Description | Details on Console |
| -------- |:-------:| -----:|
| OCR (Optical Character Recognition) |Locates and digitizes text information from images |Text will appear under the "raw text" header of the results pane of the console [Reference](images/raw-text.png)|
| Document Image Classification |Classifies documents into different types based on their visual appearance, high-level features, and extracted keywords |Classification along with confidence score appears directly under "Results" pane [Reference](images/results.png)|
|Language Classification|Classifies the language of document based on visual features |Classification along with confidence score appears under document classification in Results pane [Reference](images/results.png)|
|Table extraction|Extracts content in tabular format, maintaining row/column relationships of cells| Toggle to the Table tab to get table information |
|Searchable PDF output|Embeds a transparent layer on top of document image in PDF format to make it searchable by keywords|You need to test on a PDF document to use this feature. When you've selected a PDF, the searchable PDF button will be clickable. Clicking on it will download an OCR PDF to your computer. [Reference](images/pdf.png)|


3. Use Image Analysis Features

a. On the Vision page, select “Image Classification” or "Object Detection" on the left navigation menu and provide an image from local storage or OCI object storage. This invokes analyzeImage API after the image is provided.


![](images/img-classification.png " ")


b. Features you can test out:

| Feature | Description | Details on Console |
| -------- |:-------:| -----:|
| Image classification | Categorizes object(s) within an image | Select "Image Classification." Labels and confidence scores will appear under the Results pane. [Reference](images/img-detection.png)|
| Object detection | Locates and identifies objects within an image | Select "Object Detection." Objects, confidence score, and highlighted bounding box will all appear under the Results pane. Clicking on one of the labels on the results pane will also highlight where on the image that object was detected.|

Congratulations on completing this lab!

Proceed to the next section. 




