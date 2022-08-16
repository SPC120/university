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

    
    ![Welcome to the OCI Dashboard](images/OCI-Dashboard.png  " ")

2.  Navigate Autonomous Transaction Processing

    
    ![Autonomous Transaction Processing](images/Autonomous-Database.png  " ")

3.  Select the correct compartment (Ex: Care Clinic) and click **Create an Autonomous Database**

    
    ![Create ATP Database](images/Initial-Create-Database.png  " ")

4.  Give a prefered Display Name (Ex: CareClinicsDB) and click **Transaction Processing** for the workload type

    
    ![Give new Database a preffered Display Name](images/Input-Display-Name.png " ")

5.  Create the ADMIN password for the DB, following the database password requirements. Leave everything else as default

    *Note:* Make sure to save this password, you will need it later in this lab

    
    ![Set Admin Password](images/Set-Password.png  " ")

6.  Click **Create Autonomous Database**

    
    ![Create Autonomous Database](images/Create-Database.png  " ")

7.  Database provisioning will take about 5 minutes. Once the Lifecycle State is ***Available***, you can continue to the next task

    
    ![Database Provisioning](images/Database-Provisioning.png " ")

## Task 2: Create an APEX Workspace
1.  Under Tools, click **Oracle APEX**

    
    ![Navigate to Oracle APEX](images/Open-APEX.png " ")

2.  Enter ADMIN password (Step 5) and sign in

    
    ![Open the Admin Console](images/Admin-Console.png " ")

3. Create a new Workspace

    
    ![Create a new Workspace](images/Create-Workspace.png " ")

4. Create a Database User and new password for this user (Ex: CareClinic)

    *Note:* Make sure to save this database user/password, you will need it later

    
    ![Create a new Database User](images/Create-Database-User.png " ")

5. After creating the workspace, click **CARECLINIC** to sign out of the admin(internal) workspace and into the workspace that you have just created

    
    ![Sign out of Admin Workspace](images/Navigate-New-Workspace.png " ")

## Task 3: Upload Sample Data and Create a new Application

1. Enter password for new dabase user (Ex: CareClinic) and sign into the workspace

    
    ![Sign into the New Workspace](images/New-Workspace.png " ")

2. This is the oracle apex workspace running on the database you created earlier. Let's visit the SQL Workshop!

    
    ![Navigate to SQL Workshop](images/Workspace-Home.png " ")

3. Inside the SQL Workshop > Object Browser to view any objects in the databse. 

    *Note:* It should be empty i.e no tables currently in the databse. Uploading a DDL script will create the table structure you need, and then you can inset the data from .csv files

    
    ![Object Browser](images/Object-Browser.png " ")

4. Go to SQL Scripts and upload the contents of the <a href="files/Create_Tables.sql">Create\_Tables.sql</a> file. This will build the table structure of the tables required. 


    
    ![Navigate to SQL Scripts](images/SQL-Scripts.png " ")

5. Upload the script

    
    ![Upload the SQL Script](images/Upload-SQL-Script.png " ")

6. Once uploaded, run the script

    
    ![Run the SQL Script](images/Run-Script.png " ")

7. Ensure the statements are processed with no errors 
    
    ![Script Processed](images/Script-Processed.png " ")

8. Return to the object browser. You are now able to view all 8 tables that were just created in the object browser. Now you will need to upload the data into them

    
    ![Tables have been created](images/Tables-Created.png " ")

9. Click **Load Data** and upload the respective .csv file for HEALTHCARE\_FACILITY. The full data set can be found <a href="files/CareClinicData.zip">here.</a>

    
    ![Load Data into HealthCare Facility Table](images/Load-Data-1.png " ")

10. Repeat this step for 5 more tables. All settings can be left as defualt. (Exclude the **PATIENT\_DOCUMENTS** and the **PATIENT\_INSURANCE** tables)

    *Note:* After each load, click view table to return to the object browser

    ![Loading Data into Tables](images/Load-Data-2.png " ")­­

11. There should now be data in 6/8 tables

    
    ![View Data](images/View-Data.png " ")

12. Let's create a new application using the Healthcare\_Facility Table

    
    ![Create new application](images/Create-New-Application.png " ")

13. Give your application a name, and click create application. You can leave everything else as defult!

    
    ![Name your application](images/Application-Name.png " ")

14. Run the application and sign in with your database user (Step 11)!

    
    ![Run your new application](images/Run-Application.png " ")

15. These are two sample pages created for you that show the **Health Care Facility** table. Let's click Application 100 and create a page to upload our sample documents to our **Patients Documents** Table

    
    ![Defult Application Pages](images/Default-Pages.png " ")

## Task 4: Add Pages to Application

1. Create new Page!

    *Note:* This is on version APEX 22.1, it may look slightly different to the current version

    
    ![Create new application page](images/New-Page-1.png " ") 

2. Select **Classic Report**

    
    ![Select Classic Report](images/Classic-Report.png " ")

3. Select **Include Form Page** and give both the classic report and form page unique names. Select the source for this report as the **PATIENT\_DOCUMENTS** table

    *Note:* Its important to note that the report and form are being created on pages 5 and 6 respectivly. These will be referenced later in this lab.

    
    ![Set Classic Report Attributes](images/Classic-Report-Attributes.png " ")

4. Keep the Primary Key Column as ID(Number)

    
    ![Set Primary Key](images/Set-Primary-Key.png " ")

5. Let's hide some columns we do not want showing in the report. You can Ctrl/Cmd+Click these columns and change their type to Hidden Column

    
    ![Hide Report Columns](images/Hide-Report-Columns.png " ")

6. Select the DOCUMENT Column and in the right side pannel change the **Mime Type**, **Filename Column**, and **Last Updated Column** to match the columns in our **Patient\_Documents** table!

    *Note:* Don't forget to save!

    
    ![Update Document Column for Report](images/Update-Document-Column.png " ")

7. You will need to repeat the same steps for the form page (Page 6). Change the unwanted columns to type **Hidden**

    
    ![Hide Form Columns](images/Hide-Form-Columns.png " ")

8. Select the **P6\_Documents** page item, and change the **MIME Type Column**, **Filename Column**, and **BLOB Last Updated Column**, and Save. 

    *Note:* You will need to type these out to match exactly to the database columns.

    
    ![Update Document Column for Form](images/Update-Document-Column-Form.png " ")

9. Let's create a Popup LOV on our **P6\_PATIENT\_VISIT\_ID**. This will help you assign the correct **Patiend Visit ID** for the documents you are going to upload.

    
    ![Change type to Popup LOV](images/Create-Popup-LOV.png.png " ")

10. Scroll down and change the Type to **SQL Query** and add this query under. 
 
    ```
    <copy>
    Select PV.PATIENT_VISIT_ID || ' - ' || P.FIRST_NAME || ' ' || P.LAST_NAME d, PATIENT_VISIT_ID r from PATIENT_VISIT PV, PATIENT P where PV.PATIENT_ID = P.PATIENT_ID
    </copy>
    ```

    
    ![Define List of Values](images/Define-List-Query.png " ")

11. Go back to Page 5 and run the application 

    *Note:* Modal Pages cannot be run directly from the page designer, for example Page 6

    
    ![Run the application to view changes](images/View-Application-Changes-1.png " ")

12. Sign into the application, if prompeted, and click **Create** to inset new record into Patient\_Documents Table. All sample documents can be found <a href="files/Patient_Documents.zip">here.</a>

    
    ![Test Document Upload](images/Test-PDF-Upload.png " ")

13. Upload all 6 PDF documents ensuring that the **Patient Visit ID** matches the document name that is being uploaded

    
    ![Upload all 6 sample documents](images/Upload-Samples.png " ")

14. Now there will be 6 documents in the Patient\_Document Table. 

    
    ![Verify Documents Uploaded Properly](images/Documents-Uploaded.png " ")

15. This will also be reflected in the SQL Workshop -\> Object Browser -\> Patient\_Document !

    
    ![View Table in Object Browser](images/View-Data-Object-Browser.png " ")

## Task 5: Explore Oracle Text

1. Return to the Cloud Console, and inside the ATP DB you created, click **Database Actions**

    
    ![View your cloud console](images/View-Cloud-Console.png " ")

2. Click Database Users!

    
    ![Navigate to Database Users](images/Database-Users.png " ")

3. Edit the new user you have created Ex: CareClinic

    
    ![Edit the new user](images/Edit-New-User.png " ")

4. Under Granted Roles, search for "CTX" and check "CTXAPP" and apply changes

    
    ![Grant User CTXAPP Role](images/Grant-User-Roles.png " ")

5. In order to verify the role was granted, return to Database Actions

    
    ![Navigate to Database Actions](images/Database-Actions.png " ")

6. Under Development, click **SQL**

    
    ![Navigate into SQL Web Developer](images/SQL-Developer.png " ")

7. Execute the following query, ensuring to chage the statement to match your database user that was created in Task 2 

    ```
     <copy>
    Select * From DBA_ROLE_PRIVS WHERE GRANTEE = 'CARECLINIC';
     </copy>
    ```

    
    ![Execute SQL Query](images/Execute-SQL-Query.png " ")

8. Return to **Database Actions**, and click into **Database Users**. Enable REST on the Databse User you created by clicking the more actions and enabling rest

    
    ![Enabling Rest for new Users](images/Enable-REST-1.png " ")

9. Open a new window by clicking below and sign in with the user that was created (Step 11)

    
    ![Switch Database Users](images/Switching-DB-Users.png " ")

10. Open SQL Web Developer

    
    ![Navigate to SQL Web Developer](images/Navigate-SQL-Web-Developer.png " ")

11. Enable REST on both **PATIENT** and **PATIENT\_INSURANCE** tables by right clicking them. Leave all settings as defult!

    
    ![Enable REST for Tables](images/Enable-REST.png " ")

12. Ensure are both tables now have REST Enables, you will need this later for the other labs

    
    ![Verify Last Step](images/Verify-REST-Enabled.png " ")

13. Now visit the APEX workspace. Go to **SQL Commands** under SQL Workshop

    
    ![Visit SQL Commands](images/SQL-Commands.png " ")

14. Create an Index on the Patient\_Documents Table, where the visit summaries are stored

    ```
     <copy>
    CREATE INDEX searchMyDocs ON Patient_Documents(Document) INDEXTYPE IS CTXSYS.CONTEXT PARAMETERS ('DATASTORE CTXSYS.DEFAULT_DATASTORE FILTER CTXSYS.AUTO_FILTER FORMAT COLUMN MIMETYPE sync (every "freq=secondly;interval=60")')
     </copy>
    ```

    
    ![Index Patient Document Table](images/Create-Auto-Index.png " ")

15. Run the following query utilizing Oracle Text. Oracle Text returns all documents (previously indexed) that satisfy the expression along with a relevance score for each document. You can use the scores to order the documents in the result set. If you would like to read more about Oracle Text, more information can be found <a href="https://docs.oracle.com/en/database/oracle/oracle-database/21/ccapp/understanding-oracle-text-application-development.html#GUID-CF13C01A-F5E6-4EF5-839B-C09CF0024D5E">here</a>

    In this first example we are looking for all documents who have the work MRN inside the after visit summary. The CONTAINS operator must always be followed by the > 0 syntax, which specifies that the score value returned by the CONTAINS operator must be greater than zero for the row to be returned.

     ```
     <copy>
    SELECT SCORE(1), ID,PATIENT_VISIT_ID,  TITLE, CREATED_BY  FROM PATIENT_DOCUMENTS WHERE CONTAINS(DOCUMENT, 'MRN', 1) > 0;
     </copy>
    ```

    
    ![Run Basic Query](images/Base-Query.png " ")

16. Find all documents that have the word ABC with a score \> 1 and also contains the word Medical Center.

    ```
     <copy>
    SELECT SCORE(1), ID,PATIENT_VISIT_ID,  TITLE, CREATED_BY   FROM PATIENT_DOCUMENTS WHERE CONTAINS(DOCUMENT, '(ABC > 1) and Medical Center', 1) > 0;
     </copy>
    ```

    
    ![Document Query - Double Word Search](images/ABC-MedicalCenter.png " ")

17. This is a proximity search to look for the word ADULT near the word EXERCISES

    ```
     <copy>
    SELECT SCORE(1), ID,PATIENT_VISIT_ID,  TITLE, CREATED_BY   FROM PATIENT_DOCUMENTS WHERE CONTAINS(DOCUMENT, 'near((ADULT, EXERCISES), 5)', 1) > 0;
     </copy>
    ```

    
    ![Proximity Search](images/Proximity-Search.png " ")

18. Fuzzy Search on a term, this gives the ability to find the work medications in the document without correct spelling. !

    ```
     <copy>
    SELECT SCORE(1), ID,PATIENT_VISIT_ID,  TITLE, CREATED_BY   FROM PATIENT_DOCUMENTS WHERE CONTAINS(DOCUMENT, '?medicatis\', 1) > 0;
     </copy>
    ```

    
    ![Fuzzy Search](images/Fuzzy-Search.png " ")

19. Soundex Search on a term, giving the ability to find words that sound like the term provided, in this case "pressure". !

     ```
     <copy>
    SELECT SCORE(1), ID,PATIENT_VISIT_ID,  TITLE, CREATED_BY   FROM PATIENT_DOCUMENTS WHERE CONTAINS(DOCUMENT, '!prissuer', 1) > 0;
     </copy>
    ```

    
    ![Soundex Search](images/Soundex-Search.png " ")

20. Stem search on a term. For example if we are looking for documents with that stem of Jounal, then it will return words like Journaling

     ```
     <copy>
    SELECT SCORE(1), ID,PATIENT_VISIT_ID,  TITLE, CREATED_BY   FROM PATIENT_DOCUMENTS WHERE CONTAINS(DOCUMENT, '$journal', 1) > 0;
     </copy>
    ```

    
    ![Stem Search](images/Stem-Search.png " ")

21. Accumulation Search on two or more terms. This is looking for both terms in the document and assigning a score. Higher if both terms are present.!

     ```
     <copy>
    SELECT SCORE(1), ID,PATIENT_VISIT_ID,  TITLE, CREATED_BY   FROM PATIENT_DOCUMENTS WHERE CONTAINS(DOCUMENT, 'medications ACCUM Medical', 1) > 0 order by Score(1) desc;
     </copy>
    ```

    
    ![Accumulation Search](images/Accumulation-Search.png " ")

22. You can also weight each term as seen here. The word phyiscal carries 3x the weight of the work exercises. 

    ```
     <copy>
    SELECT SCORE(1), ID,PATIENT_VISIT_ID,  TITLE, CREATED_BY   FROM PATIENT_DOCUMENTS WHERE CONTAINS(DOCUMENT, 'exercises ACCUM physical*3', 1) > 0 order by score(1) desc;
     </copy>
    ```

    
    ![Weighted Accumulation Search](images/Weighted-Accumulation-Search.png " ")

23. Those are some of the basic queries within Oracle Text. 

    Construct Themes Tables: To build themes for your documents you will first need to create a table to hold the themes. Run each statement individually by highlingting the the statement then click Run.

    ```
    <copy>
    create table themes (query_id number, theme varchar2(2000), weight number);
    </copy>
    ```
  
   ![Creating Themes Table](images/Themes-Table.png " ")

24. Create Themes index for the documents currently in the PATIENT\_DOCUMENTS table

    ```
    <copy>
    begin
	for x in (select ID from PATIENT_DOCUMENTS) loop
    ctx_doc.themes ('searchMyDocs', x.ID, 'themes', x.ID, full_themes => false);
    end loop;
    end;
    </copy>
    ```

    
    ![Create Themes Index](images/Themes-Index.png " ")

25. Query all themes. Show all themes with weight over 25

    ```
     <copy>
	select r.title, r.filename, t.theme, t.weight from PATIENT_DOCUMENTS r, themes t
    where r.id = t.query_id and weight > 25
    order by id asc;
     </copy>
    ```

    
    ![Query Themes Table](images/Query-Themes.png " ")

26. Repeat for the Gist Table. 

    *Note:* Run each of the 3 statements individually

    ```
     <copy>
	create table gists (query_id  number, pov  varchar2(80), gist  CLOB);
     </copy>
    ```
    ```
    <copy>
	begin
	for x in (select ID from PATIENT_DOCUMENTS) loop
    ctx_doc.gist('searchMyDocs', x.ID, 'gists',x.ID,'P', pov =>'GENERIC');
    end loop;
    end;
     </copy>
    ```
    ```
     <copy>
	select * from gists;
     </copy>
    ```
    
    ![Create Gist Table and Index](images/Gist-Table.png " ")

27. Repeat for the Filtered Docs Table

    *Note:* Run each of the 3 statements individually

    ```
     <copy>
    create table filtered_docs(QUERY_ID number, DOCUMENT clob);
     </copy>
    ```
    ```
    <copy>
	begin
	for x in (select ID from PATIENT_DOCUMENTS) loop
    	ctx_doc.filter ('searchMyDocs', x.ID, 'filtered_docs', x.ID, plaintext => true);
    end loop;
    end; 
     </copy>
    ```
    ```
    <copy>
	select r.title, f.document as "Plain Text Summary" from PATIENT_DOCUMENTS r, filtered_docs f
    where r.ID = f.query_id
     </copy>
    ```

    
    ![Create Filtered Docs Table and Index](images/Filtered-Docs.png " ")

28. Finally repeat for the Full Themes tables
    
    *Note:* Run each of the 3 statements individually

    ```
    <copy>
    create table full_themes( QUERY_ID	number, THEME   varchar2(2000),WEIGHT   NUMBER);
    </copy>
    ```
    ```
    <copy>
	begin
	for x in (select ID from PATIENT_DOCUMENTS) loop
    	ctx_doc.themes ('searchMyDocs', x.ID, 'full_themes', x.ID, full_themes => true);
    end loop;
    end; 
    </copy>
    ```
    ```
    <copy>
	select r.title, r.filename, t.theme, t.weight from PATIENT_DOCUMENTS r, full_themes t
    where r.ID = t.query_id
    order by ID asc;
    </copy>
    ```

    
    ![Create Full Themes Table and Index](images/Full-Themes.png " ")

29. We can vertify all 4 tables were created by visitng the Object Browser

    
    ![Verify Tables in object browser](images/Verify-Tables-Created.png " ")

## Task 6: Implement Oracle Text for End Users

1. Now let's create a new page to let end users view document gists with 1 click. Create Page, and select **Classic Report**

    
    ![Create Classic New Report for Gist ](images/Create-Classic-Report.png " ")

2. Give the Classic Report a name, and select Modal Dialog, this will allow the page to be a pop-up instead of a redirect. Finally select the source as SQL Query and enter the query as shown

    ```
    <copy>
	select * from gists where query_id = :P7_QUERY_ID;
    </copy>
    ```
    *Note:* Ensure that this new page is page number 7 in-order for the query to populate properly

    ![Document Gist Creation](images/Document-Gist-Creation.png " ")

3. On the new page, rename the Title of the content body on the right pane to 
    **&P7_Title. Gist**.
    Create two page items, **P7\_QUERY\_ID** and **P7\_TITLE**, by right-clicking on the content body region, and selecting **Create Page Item**

    
    ![Adding Page New Items](images/Page-7-Gist-1.png " ")

4. Set the Type of both new page items to **Hidden**

    
    ![Hide Page Unwanted Page Items](images/Page-7-Gist-2.png " ")

5. Save and return to page 5 by using the page navigation. Right-Click Columns and **Create Virual Column** on your report

    
    ![Create a Virtual Column](images/Create-Virtual-Column.png " ")

6. While Selecting the new virtual column you created, change the Heading to **Document Gist**. Under Link, click **No Link Defined** to define a new link for this virtual column. Set the link to page 7. Under Set Items, ensure you add both **P7\_Query\_ID** and **P7\_TITLE**, with values of **\#ID\#** and **\#TITLE\#** respectivly. Note: Use the menu to the right of the text box makes this easier.

    
    ![Creating Column Link](images/Gist-Column-Link.png " ")

7. Add a Link Text by expanding the menu and selecting any of the defult optoions shown.

    
    ![Create A Link Text for New Column](images/Link-Text.png " ")

8. Save and Run the application. Test this new feature by clicking on the pencil icon under Document Gist.

    
    ![Save and Run your Application](images/Test-Link-1.png " ")

9. You now have a gist of the PDF documents with just one click. Now lets see how we can replicate this to add Fildered Docs in plain text to the table as well.

    
    ![View the Modal Page you have created](images/Test-Gist-Link-2.png " ")

10. Navigate to Page 7 using the developent tool bar below. Choose the "+" icon and select Page as Copy. Select **Page in this application**

    
    ![Create a Page Copy](images/Page-Copy.png " ")

11. Select the new page as page 8, and provide a new page name. On the next page select **Do not associate with a navigation menu entry**

    
    ![Enter new Classic Report Attributes](images/Page-Copy-2.png " ")

12. Give the Page Region a new name and copy

    
    ![Name the new Region Copy](images/Region-Copy.png " ")

13. You now have a new page (Page 8) where you can alter the SQL query to reflect that of Full Text. Let's create another virtual column link to this page

    ```
    <copy>
	select r.title, f.document as "Plain Text Summary" from PATIENT_DOCUMENTS r, filtered_docs f
    where r.ID = f.query_id and f.query_id = :P8_QUERY_ID;
    </copy>
    ```

    ![Update SQL Query](images/Full-Text-Query.png " ")

14. Save and return to Page 5. Right- Click columns and Create Virtual Column

    
    ![Create a Virtual Column](images/Second-Virtual-Column.png " ")

15. Make changes similar to before in step 6. Set the link to page 8. Under Set Items, ensure you add both **P8\_Query\_ID** and **P8\_TITLE**, with values of **\#ID\#** and **\#TITLE\#** respectivly.

    
    ![Create Column Link](images/Virtual-Column-Link.png " ")

16. Change the link text to a defult icon. Save and run the page

    
    ![Change Column Link Icon](images/Full-Text-Icon.png " ")

17. By clicking the manifying glass icon we can see the full text for that individual document

    
    ![View Application Changes](images/Completed-Application.png " ")

Congratulations! You have successfully completed this lab.

## Homework: Create a Caledar Page for Patient Appointments  

1. Create a new Calendar page to display patient appointments. Create a new navigation menu entry for this page, and select appropriate colunns for Display column and Start Data column.
You will need to use to following query as the source. This will join 3 tables to ensure the revelant information is displayed.

    ``` 
    <copy>
    select 
        PATIENT_VISIT.DATE_TIME as DATE_TIME,
        PATIENT.FIRST_NAME as FIRST_NAME,
        PATIENT.LAST_NAME as LAST_NAME,
        PRACTITIONER.PRACTITIONER_NAME as PRACTITIONER_NAME,
        HEALTHCARE_FACILITY.FACILITY_NAME as FACILITY_NAME 
    from 
        HEALTHCARE_FACILITY HEALTHCARE_FACILITY,
        PRACTITIONER PRACTITIONER,
        PATIENT PATIENT,
        PATIENT_VISIT PATIENT_VISIT 
    where 
    PATIENT_VISIT.PATIENT_VISIT_ID=PATIENT.PATIENT_ID
    and PATIENT_VISIT.PRACTITIONER_ID=PRACTITIONER.PRACTITIONER_ID
    and PATIENT_VISIT.HEALTHCARE_FACILITY_ID=HEALTHCARE_FACILITY.HEALTHCARE_FACILITY_ID
    </copy>
    ```

2. Lastly you can use the following code to add supplemental information to your page

    ```
    <copy>
    <html>
    <body>
    <p>PATIENT: &FIRST_NAME. &LAST_NAME.</p>  
    <p>PRACTITIONER: &PRACTITIONER_NAME.</p>
    <p>FACILITY: &FACILITY_NAME.</p>
    </body>
    </html> 
    </copy>
    ```

    

    *Note:* Use this navigation to return to the end of 2021/start of 2022 where data already exist in out tables. You can hover over the appointments to view the supplemental information that was added about each one.

    
    ![](images/image99.png " ")

    Congratulations! You have successfully completed the homework



