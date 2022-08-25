# Hospital Admin Insights from Oracle Analytics Cloud
## Introduction
Up to this point in the course, you have worked with and manipulated all kinds of hospital and patient data. Now, we will perform some data analysis on the patient data gathered into the Autonomous Data Warehouse. In this lab you will learn how to visualization and sharing of data insights through Oracle Analytics Cloud. 

### Objectives

In this lab, you will:
* Create an Oracle Analytics Cloud Instance
* Connect to an Autonomous Data Warehouse data source
* Visualize Hospital Statistics


## Pre-requisites 

* You must have an **IDCS user** set up. If you have completed the "Introduction to OCI" Lab, you already have an IDCS user.


## Task 1: Provision an Oracle Analytics Cloud (OAC) Instance & Enable Auto-Insights

> Note: Provisioning an Oracle Analytics Cloud instance can take over **40 minutes**. In preparatioon, you may watch [this](youtube:ZAqXlhivQCg) short video on provisioning an Oracle Analytics Cloud instance.

0. Navigate to the Oracle Cloud Infrastructure Console accessing from **Oracle Home Page** ([oracle.com](oracle.com)). Click in **View Account** and **Sign in to Cloud**.

    ![View Accounts Sign In](./images/Task-1/0-oracle-com.png)

1. Enter your **Cloud Account Name** (Tenant Name), hit **Next**, and sign in with your cloud login.
    ![Enter Cloud Account](./images/Task-1/1-sign-on.png)

    **Verify that you are logged in as an OCI user** 

    Check that your username is shown as:

    -  oracleidentitycloudservice/&lt;your username&gt;
    
    Then you are **signed in** as a **Single Sign-on** user.

    ![OCI User](./images/Task-1/1-oci-user.png)

    If your user does not contain the identity provider (**oracleidentitycloudservice**) then you are logged in as a **Oracle Cloud Infrastructure** user. In this case, please logout and re-authenticate using **Single Sign On** instead.

    ![Oracle Console SignIn](./images/Task-1/1-console-signin.png)
    To be capable of using **Oracle Analytics Cloud** we need to Sign-On as a **Single Sign-On** (SSO) user.

    ![Oracle Console SSO](./images/Task-1/1-sso.png)

    *For more information about federated users, see [User Provisioning for Federated Users](https://docs.cloud.oracle.com/en-us/iaas/Content/Identity/Tasks/usingscim.htm).*

2. From the **Home Console Page**, navigate to **Analytics & AI**  and select **Analytics Cloud**. This is how you will always navigate to your list of Analytics Cloud instances.

    ![Oracle Cloud Console](./images/Task-1/1-console.png)

    ![Oracle Analytics Console](./images/Task-1/1-console-menu.png)

    > **Note**: You must be connected as a **Single Sign On** (**Federated user**) user to a tenancy, which has available cloud credits to see this menu item. Local OCI users are not able to do this.

3. Select **Create Instance**.

    ![OAC Create Instance](./images/Task-1/3-create-instance.png)

    Complete the form using the following information:

    - **Instance Name**: `WORKSHOPADWOAC`
        ```
        <copy>WORKSHOPADWOAC</copy>
        ```
    - **Compartment**: Select a valid compartment in your tenancy

    - **Description**: &lt;Optional&gt;
        ```
        <copy>Analytics Instance for the cloud</copy>
        ```
    - **Feature Set**: Enterprise Analytics (important)
    
    - **Capacity**: 1 - Non Production
    
    - **License Type**: License Included "Subscribe to a new Analytics Cloud software > license and the Analytics Cloud." (You will use this service as part of the free Oracle Cloud trial that you requested for this workshop).

    - **Edition**: Enterprise Edition "Deploy an instance with enterprise modeling, reporting, and data visualization"

    ![Oracle Analytics Console](./images/Task-1/3-edition.png)


4. Select **Create**.

5. On the **Confirmation** screen, select **Create**.

     The Analytics instance page will be displayed with a status of **CREATING**.

    ![OAC Instance Creating](./images/Task-1/5-creating.png)

    > ***Reminder***: Provisioning an Oracle Analytics Cloud instance can take over **40 minutes**.

6. Once the Analytics instance page displays a status of **ACTIVE** (green), select the **Analytics Home Page**. 

    ![OAC Instance Active](./images/Task-1/6-active.png)

    The home page of your new analytics instance will open in a new tab.

     ![OAC Homepage](./images/Task-1/6-analytics-home-menu.png)

7. To ensure that **Auto Insights** is enabled, select the hamburger menu and navigate to the **Console**.

     ![OAC Homepage](./images/Task-1/7-home-menu.png)

8. From this page you can do anythign from *manage users*, to *create backups*, to *schedyle emails* containing analytics reports. For our purposes, we will choose the **System Settings** page.

     ![OAC Console](./images/Task-1/8-oac-console.png)

9. Select **Performance and Compatibility** from the outline meny, and confirm that **Auto Insights** is **ON** ![ON](./images/on.png)

    ![Auto Insights](./images/Task-1/9-auto-insights.png)

10. Navigate back to the OAC Home Page

    ![Back 1](./images/Task-1/10-back1.png)
    ![Back 2](./images/Task-1/10-back2.png)
    ![Back 3](./images/Task-1/10-back3.png)
    

## Task 2: Connect OAC to Autonomous Data Warehouse (ADW)


## Task 3: Create Data Mapping Between ADW Tables in OAC


## Task 4: Create a Workbook in OAC
## Task 5: Explain & Language Narrative Features for quick insights
## Task 6: Table & Map Visualization
## Task 7: Create dashboards for Patients and Labs Analysis
## Task 8: Use Data Actions to Navigate and Filter

## Task Example: Create a Digital Assistant Instance and Import the Skill
1. Log in to the Oracle Cloud at cloud.oracle.com. Cloud Account Name is howarduniversity. Click “Next”.
2. Click on “Direct Sign-In” and enter your Cloud Account email and password.
3. Once you are logged in, you are taken to the cloud services dashboard where you can see all the services available to you. Click the navigation menu in the upper left to show top level navigation choices.
4. Click **Digital Assistant**

  ![](images/odanav.png " ")

5. Select the CareClinics compartment and create a Digital Assistant instance. 

  ![](images/1-createoda.png " ")

6. After the instance is successfully created. Click on the Service Console to open the ODA console. 

  ![](images/1-servconsole.png " ")

7. Now, select the navigation on the top left menu, select Skills under Development and import the Skill which you downloaded.

  ![](images/1-imp.png " ")
```
    <copy>
    find a doc
    help from doctor
    how can I find the doctor?
    looking for a doctor
    need doctor assistance
    Where is the doc?
    </copy>
    ```
