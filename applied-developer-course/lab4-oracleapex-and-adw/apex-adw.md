<!-- Updated June 15, 2022 -->

# Build APEX Application on ATP

## Introduction

This lab walks you through the steps to quickly provision an Autonomous Transaction Processing instance on Oracle Cloud. In this lab we will create web application which will take medical documents and store them in the Autonomous Database. Further we will also use Oracle Text to allow users to filter, search, and view those documents with one-click.

Estimated lab time: 2 hours

### Objectives

- Create a new APEX workspace 
- Build a web application
- Explore Oracle Text 

### Prerequisites

- This lab requires completion of the **Get Started** section in the Contents menu on the left.

## Task 1: Create Autonomous Transaction Processing Database
1.  Login to your Oracle Cloud Tenancy and open the side menu

![](images/image1.png  " ")

2.  Navigate Autonomous Transaction Processing

![](images/image2.png  " ")

3.  Select the correct compartment (Ex: Care Clinic) and click **Create an Autonomous Database**

![](images/image3.png  " ")

4.  Give a prefered Display Name (Ex: CareClinicsDB) and click **Transaction Processing** for the workload type

![](images/image4.png " ")

5.  Create the ADMIN password for the DB, following the database password requirements. Leave everything else as default

    *Note:* Make sure to save this password, you will need it later in this lab

![](images/image5.png  " ")

6.  Click **Create Autonomous Database**

![](images/image6.png  " ")

7.  Database provisioning will take about 5 minutes. Once the Lifecycle State is ***Available***, you can continue to the next task

![](images/image7.png " ")

## Task 2: Create an APEX Workspace
1.  Under Tools, click **Oracle APEX**

![](images/image8.png " ")

2.  Enter ADMIN password (Step 5) and sign in

![](images/image9.png " ")

3. Create a new Workspace

![](images/image10.png " ")

4. Create a Database User and new password for this user (Ex: CareClinic)

    *Note:* Make sure to save this database user password, you will need it later

![](images/image11.png " ")

5. After creating the workspace, click **CARECLINIC** to sign out of the admin(internal) workspace and into the workspace that you have just created

![](images/image12.png " ")

## Task 3: Upload Sample Data and Create a new Application

1. Enter password for new dabase user (Ex: CareClinic) and sign into the workspace

![](images/image13.png " ")

2. This is the oracle apex workspace running on inside the database you created. Let's visit the SQL Workshop!

![](images/image14.png " ")

3. Inside the SQL Workshop > Object Browser to view any objects in the databse. 

    *Note:* It should be empty i.e no tables currently in the databse. Uploading a DDL script will create the table structure you need, and then you can inset the data from .csv files

![](images/image15.png " ")

4. Go to SQL Scripts and upload the contents of the <a href="files/Create_Tables.sql">Create\_Tables.sql</a> file. This will build the table structure of the tables required. 


![](images/image16.png " ")

5. First upload the script

![](images/image17.png " ")

6. Once uploaded, run the script

![](images/image18.png " ")

7. Ensure there are ***19*** Statements processed with 0 errors **Replace Screen Capture HERE down**

![](images/image19.png " ")

8. You are now able to view all 8 tables that were just created. You will need to upload the data into them

![](images/image20.png " ")

9. Click **Load Data** and upload the respective .csv file for HEALTHCARE\_FACILITY

![](images/image21.png " ")

10. Repeat this step 5 more tables (Exclude PATIENT\_DOCUMENTS and PATIENT\_INSURANCE)

![](images/image22.png " ")­­

11. There should now be data in 6/8 tables

![](images/image23.png " ")

12. Let's create a new application using the Healthcare\_Facility Table

![](images/image24.png " ")

13. Give your application a name, and click create application. You can leave everything else as defult!

![](images/image25.png " ")

14. Run the application and sign in with your database user (Step 11)!

![](images/image26.png " ")

15. These are two sample application pages created for you. Let's click Application 100 and create a page to upload our sample documents to our Patients Documents Table!

![](images/image27.png " ")

## Task 4: Add Pages to Application

1. Create new Page!

![](images/image28.png " ")

2. Select Form!

![](images/image29.png " ")

3. Select Report with Form!

![](images/image30.png " ")

4. Give the report and form a unique name. Use a classic report with a Modal Dialog Page.!

![](images/image31.png " ")

5. Create a new navigation menu entry

![](images/image32.png " ")

6. Select the Patient\_Documents table!

![](images/image33.png " ")

7. Select Primary Key Column as "ID (Number)" and create page!

![](images/image34.png " ")

8. Let's hide some columns we do not want showing in the report. You can Ctrl+Click these columns and change their type to Hidden Column!

![](images/image35.png " ")

9. Select the DOCUMENT Column and in the right side pannel change the Mime Type, Filename Column, and Last Updated Column to match the column in our Patient\_Documents table!

![](images/image36.png " ")

10. We will need to repeat the same steps for Page 6. Change the unneeded columns to type Hidden!

![](images/image37.png " ")

11. Select the P6\_Documents page item, and change the MIME Type, Filename Column, and BLOB Last Updated Column, and Save. (You will need to type these out to match exactly to the database columns.!

![](images/image38.png " ")

12. Let's create a Popup LOV on our P6\_PATIENT\_VISIT\_ID help us assign the correct Patiend ID visit for the document we are uploading.!

![](images/image39.png " ")

13. Change the Type to SQL Query and add this code. 'Select PV.PATIENT\_VISIT\_ID \|\| \' - \' \|\| P.FIRST\_NAME \|\| \' \' \|\| P.LAST\_NAME d, PATIENT\_VISIT\_ID r from PATIENT\_VISIT PV, PATIENT P where PV.PATIENT\_ID = P.PATIENT\_ID'\

![](images/image40.png " ")

14. Go to Page 5 and run the application (Modal Pages cannot be run directly from the page designer i.e Page 6)!

![](images/image41.png " ")

15. Sign Into the application, if prompeted, and click create to inset new record into Patient\_Documents Table!

![](images/image42.png " ")

16. Upload all 6 PDF documents ensuring that the Patient Visit ID matches the document that is being uploaded!

![](images/image43.png " ")

17. Now there will be 6 documents in the Patient\_Document Table. 

![](images/image44.png " ")

18. This will also be reflected in the SQL Workshop -\> Object Browser -\> Patient\_Document !

![](images/image45.png " ")

## Task 5: Explore Oracle Text

1. Return to the Cloud Console, and inside the ATP you have created, click Database Actions!

![](images/image46.png " ")

2. Click Database Users!

![](images/image47.png " ")

3. Edit the new user you have created!

![](images/image48.png " ")

4. Under Granted Roles, search for "CTX" and check "CTXAPP" and apply changes.!

![](images/image49.png " ")

5. To verify the role was granted, return to Database Actions.!

![](images/image50.png " ")

6. Under Development Click SQL!

![](images/image51.png " ")

7. Execute the query, ensuring to chage the code to match your database user that was created (Step 11)!

![](images/image52.png " ")

8. Return to Database Actions -\> Database Users. Enable REST on the Databse User you created by clicking the more actions and enabling rest!

![](images/image53.png " ")

9. Open a new window by clicking below and sign in with the user that was created (Step 11)!

![](images/image54.png " ")

10. Open SQL Web Developer!

![](images/image55.png " ")

11. Enable REST on both PATIENT and PATIENT\_INSURANCE tables by right clicking them. Leave all settings as defult!

![](images/image56.png " ")

12. Ensure are both enables, you will need this later for the other labs.!

![](images/image57.png " ")

13. Now visit thew APEX workspace. Go to SQL Commands under SQL Workshop!

![](images/image58.png " ")

14. Create an Index on the Patient\_Documents Table, where the visit summaries are stored!

![](images/image59.png " ")

15. Core query inside the document to see if it contains a keyword. In this first example we are looking for all documents who have the work MRN inside the after visit summary. A score greater than 0 means the text is found inside the document.

![](images/image60.png " ")

16. Find all documents that have the word ABC with a score \> 1 and also contains the word Medical Center.!

![](images/image61.png " ")

17. This is a proximity search to look for the word ADULT near the word EXERCISES!

![](images/image62.png " ")

18. Fuzzy Search on a term, this gives the ability to find the work medications in the document without correct spelling. !

![](images/image63.png " ")

19. Soundex Search on a term, giving the ability to find words that sound like the term provided, in this case "pressure". !

![](images/image64.png " ")

20. Stem search on a term. For example if we are looking for documents with that stem of Jounal, then it will return words like Journaling.!

![](images/image65.png " ")

21. Accumulation Search on two or more terms. This is looking for both terms in the document and assigning a score. Higher if both terms are present.!

![](images/image66.png " ")

22. You can also weight each term as seen here. The word phyiscal carries 3x the weight of the work exercises. !

![](images/image67.png " ")

23. Construct Themes Tables: To build themes for your documents you will first need to create a table to hold the themes.Run each statement individually by highlingting the the statement then clicking Run.!

![](images/image68.png " ")

24. Create Themes index for the documents currently in the PATIENT\_DOCUMENTS table.!

![](images/image69.png " ")

25. Query all themes. Show all themes with weight over 25!

![](images/image70.png " ")

26. Repeat for the Gist Table. Note: Run each of the 3 statements individually. !
![](images/image71.png " ")

27. Repeat for the Filtered Docs Table. Note: Run each of the 3 statements individually. ![Graphical user interface, text Description automatically generated]![](images/image72.png " ")

28. Finally repeat for the Full Themes tables. Note: Run each of the 3 statements individually. !

![](images/image73.png " ")

29. We can vertify all 4 tables were created by visitng the Object Browser. !

![](images/image74.png " ")

## Task 6: Implement Oracle Text for End Users

1. Now let's create a new page to let end users view document gists with 1 click. Create Page -\> Report -\> Classic Report!

![](images/image75.png " ")

2. Give the Classic Report a name, and select Modal Dialog (this will allow the page to be a pop-up instead of a redirect)!

![](images/image76.png " ")

3. Finally select the source as SQL Query and enter the query as shown.

![](images/image77.png " ")

4. On the new page, create two page items (P7\_QUERY\_ID and P7\_TITLE) by right-clicking on the content body region. 

![](images/image78.png " ")

5. Set the Type of both new page items to "Hidden"

![](images/image79.png " ")

6. Return to page 5. Right-Click Columns and Create Virual Column on this "Report 1"!

![](images/image80.png " ")

7. While Selecting the new virtual column you created, change the Heading to Document Gist. Under Link, click "No Link Defined" to define a new link for this virtual column. Set the link to page 7. Under Set Items, ensure you add both P7\_Query\_ID and P7\_TITLE, with values of \#ID\# and \#TITLE\# respectivly. Note: Use the menu to the right of the text box makes this easier.

![](images/image81.png " ")

8. Add a Link Text by expanding the menu and selecting any of the defult optoions shown.

![](images/image82.png " ")

9. Save and Run the application. Test this new feature by clicking on the pencil icon under Document Gist.

![](images/image83.png " ")

10. You now have a gist of the PDF documents with just one click. Now lets see how we can replicate this to add Fildered Docs in plain text to the table as well.

![](images/image84.png " ")

11. Navigate to Page 7 using the developent tool bar below. Choose the "+" icon and select Page as Copy. Select "Page in this application"!

![](images/image85.png " ")

12. Select the new page as page 8, and provide a new page name. On the next page select "Do not associate with a navigation menu entry"!

![](images/image86.png " ")

13. Give the Page Region a new name 

![](images/image87.png " ")

14. You now have a new page (Page 8) where you can alter the SQL query to reflect that of Full Text. Let's create another virtual column link to this page.

![](images/image88.png " ")

15. Save and return to Page 5. Right- Click columns and Create Virtual Column

![](images/image89.png " ")

16. Make changes similar to before, but instead redirecting to Page 8

![](images/image90.png " ")

17. Change the link text to a defult icon. Save and run the page.!

![](images/image91.png " ")

18. By clicking the manifying glass icon we can see the full text for that individual document.!

![](images/image92.png " ")
## Task 7: Create Calendar Page for Patient Appointments 

1. Click Edit App 100 down in the development tool bar. Let's create one more page for our patients appointments.This time we will create a Calandar page

![](images/image93.png " ")

2. Give the new page a name, and select Next. 

![](images/image94.png " ")

3. Select "Create a new nagivation menu entry" and enter a naviagation menu entry name!

![](images/image95.png " ")

4. Enter the source and a SQL Query and paste the code provided. Click Next.!

![](images/image96.png " ")

5. For Display Column select Last\_Name, and for Start Data Column select Date\_Time.!

![](images/image97.png " ")

6. Lastly under attributed for the Patient Appointments Region. Activate Show time, and add some supplemental information for each of the events on the calendar.Save and Run.

![](images/image98.png " ")

7. Use this navigation to return to the end of 2021/start of 2022 where data is present in out tables. Note you can hover over the appointments to view the supplemental information about each one. !

![](images/image99.png " ")

Congratulations! You have successfully completed this lab.

## Homework: Create a New Page 

