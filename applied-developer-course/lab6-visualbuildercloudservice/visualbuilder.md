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

1. Log in to the Oracle Cloud at cloud.oracle.com. Cloud Account Name is howarduniversity. Click “Next”.
2. Click on “Direct Sign-In” and enter your Cloud Account email and password.
3. Once you are logged in, you are taken to the cloud services dashboard where you can see all the services available to you. Click the navigation menu in the upper left to show top level navigation choices.
4. Click **Developer Services --> Visual Builder**.

   ![](images/1.png " ")

5. Select the **CareClinics** compartment and then click create.

   ![](images/2.png " ")

6. Type in the name for your VBCS instance. For example: **CareClinicVB**. Then click create.

   ![](images/3.png " ")

7. It will take a couple of minutes to create the instance. Once the status changes to active, click on the **Service Homepage** button.

   ![](images/4.png " ")

8. This will take you to the landing page for Visual builder cloud service. Then click on **New Application** to create an application.

   ![](images/5.png " ")

9. Enter an application name and click **Finish**. This will create your application and take you to the application builder landing page.

   ![](images/6.png " ")

## Task 2: Configure Service Connections

In this task, we will create 4 service connections. Prior to creating service connections to OCI services, you first have to get details to generate OCI signature like tenancy OCID, user OCID, fingerprint and key.

### Service Connection Pre-requisite: Build OCI Signature

1. Log in to the Oracle Cloud at cloud.oracle.com. Cloud Account Name is howarduniversity. Click “Next”.
2. Click on “Direct Sign-In” and enter your Cloud Account email and password.
3. Once you are logged in, click on the avatar icon on the top right corner.
   ![](images/8.png " ")

4. Click on **API Keys** and then Add API Key.
   ![](images/9.png " ")

5. Click on **Generate API Key Pair**.
6. Download the keys to your system and store them at a secure location.
7. Click Add.
   ![](images/10.png " ")

8. Copy the Configuration File Preview and paste this in a notepad text file. We will use this while adding a service connection to OCI services.
   ![](images/11.png " ")

### Service Connection 1: Object Storage

This is a service connection to the Object Storage Service. We built this bucket in the "Introduction to OCI" workshop. We will need the "namespaceName" & "bucketName" from that lab for later portions of this lab.

Go to this page to know more about Object Storage REST endpoints [Object Storage API](https://docs.oracle.com/en-us/iaas/api/#/en/objectstorage/20160918/Object/PutObject)

We will use following API to upload Object to Object Storage.

```copy
https://objectstorage.us-{region}-1.oraclecloud.com/n/{namespaceName}/b/{bucketName}/o/{objectName}
```

1. Click on **services** in left panel and then click on **plus sign** to add new service connection

   ![](images/7.png " ")

2. Select Define by Endpoint to add REST endpoints
   ![](images/12.png " ")

3. Enter the Object Storage URL. Method will be **PUT** since we will uplload image to Object Storage. Click **Next**
   ![](images/13.png " ")

4. By default you will be in **Overview** tab. Change **Service Name**
   ![](images/14.png " ")

5. Click on **Server**, under Server Variables change region variable to your region, here we are using ashburn and we will change the authentication to `Oracle Cloud Infrastructire API signature 1.0`
   ![](images/15.png " ")

6. Click on **pencil icon** to add API key ( < tenancyocid >/< userocid >/< fingerprint >) and Private Key. Click **Save**
   ![](images/16.png " ")

7. Click on **Request > Body** and change Media Type to `application/octet-stream`
   ![](images/17.png " ")

### Service Connection 2: ORDS Autonomous Database

This is a service connection to the Autonomous Database. We built this API in the "Oracle Apex and ADW" workshop (REST Apis for POST - Patient_Insurance and GET - Patient tables). No authentication for these APIs.

Repeat the above process to create another service connection to fetch user information.

1. Here we will have get method and hint will be get one. Click **Next**.

   ![](images/18.png " ")

2. Rename the service if you want and go to test, and enter id value and click on send request. Once we get 200 response, save the example response and then click create.

   ![](images/19.png " ")

   ![](images/20.png " ")
   ![](images/21.png " ")

### Service Connection 3: Vision Service

This is a service connection to the OCI Vision Service. The APIs are available out of the box. OCI Signature is the authentication scheme for these APIs (similar to what we did in Service Connection 1).

Go to this page to know more about OCI Vision REST endpoints [OCI Vision APIs](https://docs.oracle.com/en-us/iaas/api/#/en/vision/20220125/AnalyzeDocumentResult/AnalyzeDocument)

We will use following API to extract text from the insurance cards.

```copy
https://vision.aiservice.us-ashburn-1.oci.oraclecloud.com/20220125/actions/analyzeDocument
```

1. Repeat Steps **1-2** from the "Service Connection 1: Object Storage". Enter the Vision Service URL. Method will be **POST**.

2. Repeat Steps **4-6 for authentication** from the "Service Connection 1: Object Storage". Click on **Request > Body** and paste the following:

```copy
{
     "features" : [ {
    "featureType" : "TEXT_DETECTION"
  } ],
  "language" : "ENG",
      document: {
        source: "OBJECT_STORAGE",
        namespaceName: "EXAMPLE-namespaceName-Value",
        bucketName: "EXAMPLE-bucketName-Value",
        objectName: "EXAMPLE-objectName-Value"
      }
}
```

![](images/59.png " ")

## Task 3: Create Mobile Application

In this task we will now actually create mobile application that end users can interact with.

### Page 1: main-start

1. Click on **Mobile Applications** in left panel and then click on **plus sign**.
   ![](images/task3/20.png " ")

2. Give name to application, select **none** as Navigation Style and click **Next**.
   ![](images/task3/21.png " ")

3. Click **Custom** as template and Click Create.
   ![](images/task3/22.png " ")

4. Once page is loaded you can see the structure in left panel, by defauly main-start is landing page. In canvas you can see components where we can filter different components and drag and drop in our canvas. Also elements in canvas can be seen under structure.

   ![](images/task3/23.png " ")

5. Search for input and drag and drop to Input Text to canvas
   ![](images/task3/24.png " ")

6. On right hand side under properties, rename **Label hint** to Enter Id and check the required field. Also add class of `oj-sm-padding-5x` which make it look bit nicer.
   ![](images/task3/25.png " ")
   ![](images/task3/26.png " ")

7. Repeat the same process to add Button.

8. Under structure, click on **Flex Container** and then under properties click on **Center** in Justify and again **Center** in Align
   ![](images/task3/27.png " ")

9. Click on Input Text and then under **Properties** go to **Data** and next to value click on **down arrow** and finally click **Create Variable**

   ![](images/task3/28.png " ")

10. Give variable name and then click **Create**
    ![](images/task3/29.png " ")

11. Click on Button and then under events in Properties click on New Event and on ojAction.
    ![](images/task3/30.png " ")

12. This will take you to Action page and create new action rename ID to `LoginButtonActionChain` and then drag and drop Call REST to canvas
    ![](images/task3/31.png " ")

13. Select Call Rest and under Properties click on Select next to Endpoint
    ![](images/task3/32.png " ")

14. Select getUser endpoint and click Select.
    ![](images/task3/33.png " ")

15. Under Properties now you should see Input Parameters and click on Assign
    ![](images/task3/34.png " ")

16. Drag userId from Sources to id under Target.
    ![](images/task3/35.png " ")

17. Now if our REST call is success we want to Navigate to other page, fo that drag and drop Navigate. Under Properties click Create next to Page.
    ![](images/task3/36.png " ")

18. Give name to page and select Custom, click Create.
    ![](images/task3/37.png " ")

### Page 2: main-cardImage

1. In the left navigation pane, find the newly created page and click on "main-cardimage".
   ![](images/task3/page-2/01.png " ")

2. In the main-cardpage, go to **types** and click on +type and then "From Endpoint".
   ![](images/task3/page-2/02.png " ")

3. Select the getUser under services.
   ![](images/task3/page-2/03.png " ")

4. Select the fields you want the type to have, in this example we are going to display only the first and last name but we also need the id for the REST calls to update the database table. Therefore select those three fields.  
   ![](images/task3/page-2/04.png " ")
5. Then go to **Variables** and click "+Variable", name it **userDetails** and select the type as the one you created in step 4. Then click create. Create another variable "image" of type Any.  
   ![](images/task3/page-2/05.png " ")
   ![](images/task3/page-2/06.png " ")

6. Choose the option "Required" under the input parameters on the right side of the screen.
   ![](images/task3/page-2/07.png " ")

7. Go back to the "main-start" page and open the action chain that will be called on click of the login button. Click on the "navigate to main-cardimage" activity. You should now see under input parameters the newly created input paramater for main-cardimage page i.e. userDetails. Click on Assign.
   ![](images/task3/page-2/08.png " ")

8. Assign the userDetails on the right side the following code:

`{ "patient_id": $chain.results.callRestGetPatientId.body.patient_id, "first_name": $chain.results.callRestGetPatientId.body.first_name, "last_name": $chain.results.callRestGetPatientId.body.last_name }`

Then click Save.

Note: callRestGetPatientId could be different for you if you changed the rest call id step right above the navigate step. The idea is to assign the returned fields from the rest call to your next page's input parameter.
![](images/task3/page-2/09.png " ")

9. Go back to your "main-cardimage" page, drag and drop a form layout to the canvas.
10. Also add **oj-sm-padding-4x-horizontal** class on the right side properties panel.
    ![](images/task3/page-2/010.png " ")

11. Next drag and drop an "Input Text" inside the form layout and on the right properties panel goto data.
12. For the value field under the data tab, hover over the field and you will see an arrow on the far right. Click on that arrow and select "first_name" under the userDetails variable.
13. Repeat step 12 for the "Last Name" field.
    ![](images/task3/page-2/011.png " ")

14. Drag and drop a camera component under the form layout in the canvas. In the properties panel on the right, deselect video as the app will only accept images. Also align it centrally.
    ![](images/task3/page-2/012.png " ")

15. Then in the properties panel, go to "events" tab and click on "+New Event" and select "On Selected Files". This will open up an action chain.
    ![](images/task3/page-2/013.png " ")

16. Drag and drop an assign varibale option to the canvas. Then click Assign.
    ![](images/task3/page-2/014.png " ")

17. From the left assign Files.item[0] to the image variable and make sure to select expression and click save.
    ![](images/task3/page-2/015.png " ")

18. After the assign variable, drag and drop a "fire notification activity" and in the properties panel on the right update the details accordingly.  
    ![](images/task3/page-2/016.png " ")

19. Drag and drop button in canvas. Change Label and align center. Add class oj-sm-margin-2x-top

![](images/task3/page-2/017.png " ")

20. Click on Events, and then click on New Event -> ojAction

![](images/task3/page-2/018.png " ")

21. Drag and drop Call Rest in canvas and click on Select Endpoint in properties.
    ![](images/task3/page-2/019.png " ")

22. Select PUT endpoint for uploading image to Object Storage.
    ![](images/task3/page-2/020.png " ")

23. Enter Bucket Name, Namespace in target and for objectName we will use firstname_lastname.jpeg. Click Save
    ![](images/task3/page-2/021.png " ")
    ![](images/task3/page-2/026.png " ")

24. Drag and drop Fire Notification, enter Summary and change display mode to Transient and Notification Type to confirmation
    ![](images/task3/page-2/022.png " ")

25. Drag and drop Call rest after Fire Notification. Select analyzeDocument API an dthen click on Body.
    ![](images/task3/page-2/023.png " ")

26. Paste the Body as follow, and replace fields like namespace and bucketname with yours. For objectName copy the syntax we used above for uploading image to Object Storage.
    ![](images/task3/page-2/024.png " ")

27. Drag and drop Call Function. Here we will write our own javascript function to parse the output we get after analyzing image.

    ![](images/task3/page-2/028.png " ")

    <!-- ![](images/task3/page-2/025.png " ") -->

28. Click on JavaScript Tab and paste the following function inside PageModule class.

    ![](images/task3/page-2/029.png " ")

29. Go back to Actions. and then select the Function Name that we just added.

    ![](images/task3/page-2/030.png " ")

30. We need to pass the output from endpoint to function, click on Assign next to Input Parameters and expand results, look for Lines array and map it to arrOfLines in target

    ![](images/task3/page-2/031.png " ")

31. Add another Rest Call and select patient_insurance endpoint to update patient insurace details in DB.

    ![](images/task3/page-2/032.png " ")

32. Replace all the fields in body. Member id and Group Number we will get from our JS function and patient id is already there in variable. Contruct the URL for image URL

    ![](images/task3/page-2/033.png " ")

33. Add Navigate at the end in Success fork, and select the main-success page.

    ![](images/task3/page-2/034.png " ")

### Page 3: main-success

1. Click on Flex Container and on the right properties panel, select the following:
   ![](images/task3/53.png " ")

2. Drag and drop a icon component onto the canvas and click on the icon option in the properties panel.
   ![](images/task3/54.png " ")

3. Search for success and select the "Success S" option and then click on select.
   ![](images/task3/55.png " ")

4. Add the **oj-icon-color-success** class to the icon.
   ![](images/task3/56.png " ")

5. Go to the "All tab" for the icon properties and then search for style. Then add "font-size:100px;".
   ![](images/task3/57.png " ")

6. Drag and drop a text right under the icon component.
7. Change the value to "Success! You can now return to the Chatbot"
   ![](images/task3/58.png " ")

## Task 4: Publish Application and test

## Troubleshoot Tips

    If you are having problems with any of the labs, please visit the Need Help? tab.
