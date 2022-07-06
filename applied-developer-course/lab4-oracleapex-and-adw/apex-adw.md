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
1.  Login to Oracle Cloud Tenancy and click the menu in the top left![Graphical user interface, application, Teams Description automatically generated
![](images/image1.png " ")

2.  ![](images/image2.png)Access Autonomous Transaction Processing

3.  Select the correct compartment (Ex: Care Clinic)

4.  ![](images/image3.png)Give a prefered Display Name (Ex: DB-Username-CareClinic) and select Transaction Processing![Graphical user interface, application Description automatically generated](images/image4.png)

5.  Create the ADMIN password for the DB, following Password Requirements. Leave everything else as default.![Graphical user interface, text, application, Teams Description automatically generated](images/image5.png){width="6.493121172353455in" height="3.54in"}

6.  Create Autonomous Database![Graphical user interface, application, Teams Description automatically generated](images/image6.png)

7.  Provisioning will take about 5 minutes![Graphical user interface, text, application, email Description automatically generated](images/image7.png)

8.  Under Tools, open Oracle APEX ![Graphical user interface, text, application, email Description automatically generated](images/image8.png)

9.  Enter ADMIN password and Sign In![Graphical user interface, application Description automatically generated](images/image9.png)

10. Create Workspace ![Graphical user interface, website Description automatically generated](images/image10.png)

11. Create a Database User and new password for user (Ex: CareClinic)![A screenshot of a computer Description automatically generated](images/image11.png)

12. After creating click here to sign out of the admin(internal) workspace and into the workspace that was just created![Graphical user interface, website Description automatically generated](images/image12.png)

13. Enter Password for new dabase user (Ex: CareClinic) and Sign in![Graphical user interface, application Description automatically generated](images/image13.png)

14. This is the oracle apex workspace for the DB that was created. Visit the SQL Workshop![A screenshot of a computer Description automatically generated with medium confidence](images/image14.png)

15. Visit the SQL Workshop -\> Object Browser to view any objects in the databse. Note: It should be empty. Uploading a Script will create the tables we need.![Graphical user interface, text, application Description automatically generated](images/image15.png)

16. Go to SQL Scripts and upload the contents of the ***Create\_Tables.sql*** file ![Graphical user interface, application, Teams Description automatically generated](images/image16.png)

17. Upload the Script![A screenshot of a computer Description automatically generated with medium confidence](images/image17.png)

18. Run th Script![Graphical user interface, application Description automatically generated](images/image18.png)

19. Ensure there are 19 Statements processed with 0 errors![Graphical user interface, application Description automatically generated](images/image19.png)

20. You are now able to view all 7 tables that were just created. Just need to upload the data into them.![A screenshot of a computer Description automatically generated](images/image20.png)

21. Click Load Data and upload the .csv file for HEALTHCARE\_FACILITY. ­­![Graphical user interface, application Description automatically generated](images/image21.png)

22. Repeat for 5 more tables (Exclude PATIENT\_DOCUMENTS)![A screenshot of a computer Description automatically generated](images/image22.png)­­

23. There should now be data in 6/7 tables.![Graphical user interface Description automatically generated](images/image23.png)

24. Let's create a new application using the Healthcare\_Facility Table![A screenshot of a computer Description automatically generated with medium confidence](images/image24.png

25. Give your application a name, and click create application. You can leave everything else as defult![A screenshot of a computer Description automatically generated with medium confidence](images/image25.png)

26. Run the application and sign in with your database user (Step 11)![A screenshot of a computer Description automatically generated with medium confidence](images/image26.png)

27. These are two sample application pages created for you. Let's click Application 100 and create a page to upload our sample documents to our Patients Documents Table![Graphical user interface, application Description automatically generated](images/image27.png)

28. Create new Page![A screenshot of a computer Description automatically generated with medium confidence](images/image28.png)

29. Select Form![Graphical user interface, application Description automatically generated](images/image29.png)

30. Select Report with Form![A screenshot of a computer Description automatically generated with medium confidence](images/image30.png)

31. Give the report and form a unique name. Use a classic report with a Modal Dialog Page.![A screenshot of a computer Description automatically generated with medium confidence](images/image31.png)

32. Create a new navigation menu entry![](images/image32.png)

33. Select the Patient\_Documents table![A screenshot of a computer Description automatically generated with medium confidence](images/image33.png)

34. Select Primary Key Column as "ID (Number)" and create page![A screenshot of a computer Description automatically generated with medium confidence](images/image34.png){width="6.494917979002625in" height="3.55in"}

35. Let's hide some columns we do not want showing in the report. You can Ctrl+Click these columns and change their type to Hidden Column![A screenshot of a computer Description automatically generated with medium confidence](images/image35.png){width="6.507341426071741in" height="3.57in"}

36. Select the DOCUMENT Column and in the right side pannel change the Mime Type, Filename Column, and Last Updated Column to match the column in our Patient\_Documents table![A screenshot of a computer Description automatically generated with medium confidence](images/image36.png)

37. We will need to repeat the same steps for Page 6. Change the unneeded columns to type Hidden![Graphical user interface, application Description automatically generated](images/image37.png)

38. Select the P6\_Documents page item, and change the MIME Type, Filename Column, and BLOB Last Updated Column, and Save. (You will need to type these out to match exactly to the database columns.![A screenshot of a computer Description automatically generated](images/image38.png)

39. Let's create a Popup LOV on our P6\_PATIENT\_VISIT\_ID help us assign the correct Patiend ID visit for the document we are uploading.![A screenshot of a computer Description automatically generated with medium confidence](images/image39.png)

40. Change the Type to SQL Query and add this code. 'Select PV.PATIENT\_VISIT\_ID \|\| \' - \' \|\| P.FIRST\_NAME \|\| \' \' \|\| P.LAST\_NAME d, PATIENT\_VISIT\_ID r from PATIENT\_VISIT PV, PATIENT P where PV.PATIENT\_ID = P.PATIENT\_ID'\
    ![Graphical user interface, application Description automatically generated](images/image40.png)

41. Go to Page 5 and run the application (Modal Pages cannot be run directly from the page designer i.e Page 6)![A screenshot of a computer Description automatically generated](images/image41.png)

42. Sign Into the application, if prompeted, and click create to inset new record into Patient\_Documents Table![Graphical user interface, text, application, Word Description automatically generated](images/image42.png)

43. Upload all 6 PDF documents ensuring that the Patient Visit ID matches the document that is being uploaded![Graphical user interface, application Description automatically generated](images/image43.png)

44. Now there will be 6 documents in the Patient\_Document Table. ![Graphical user interface, text, application Description automatically generated](images/image44.png)

45. This will also be reflected in the SQL Workshop -\> Object Browser -\> Patient\_Document ![Graphical user interface Description automatically generated](images/image45.png)

46. Return to the Cloud Console, and inside the ATP you have created, click Database Actions![Graphical user interface, text, application, email Description automatically generated](images/image46.png)

47. Click Database Users![Graphical user interface, application Description automatically generated](images/image47.png)

48. Edit the new user you have created![Graphical user interface, application, Teams Description automatically generated](images/image48.png)

49. Under Granted Roles, search for "CTX" and check "CTXAPP" and apply changes.![Graphical user interface, application, Teams Description automatically generated](images/image49.png)

50. To verify the role was granted, return to Database Actions.![Graphical user interface, application, Teams Description automatically generated](images/image50.png)

51. Under Development Click SQL![Graphical user interface, application, Teams Description automatically generated](images/image51.png)

52. Execute the query, ensuring to chage the code to match your database user that was created (Step 11)![Graphical user interface, text, application, email Description automatically generated](images/image52.png)

53. Return to Database Actions -\> Database Users. Enable REST on the Databse User you created by clicking the more actions and enabling rest![Graphical user interface, application, Teams Description automatically generated](images/image53.png)

54. Open a new window by clicking below and sign in with the user that was created (Step 11)![Graphical user interface, application Description automatically generated](images/image54.png)

55. Open SQL Web Developer![Graphical user interface, application, Teams Description automatically generated](images/image55.png)

56. Enable REST on both PATIENT and PATIENT\_INSURANCE tables by right clicking them. Leave all settings as defult![Graphical user interface, text, application, Word Description automatically generated](images/image56.png)

57. Ensure are both enables, you will need this later for the other labs.![Graphical user interface, text, application, Word Description automatically generated](images/image57.png)

58. Now visit thew APEX workspace. Go to SQL Commands under SQL Workshop![Graphical user interface Description automatically generated](images/image58.png)

59. Create an Index on the Patient\_Documents Table, where the visit summaries are stored![A screenshot of a computer Description automatically generated](images/image59.png)

60. Core query inside the document to see if it contains a keyword. In this first example we are looking for all documents who have the work MRN inside the after visit summary. The greater than zero means a score is detected, and therefore the information is inside![A screenshot of a computer Description automatically generated with medium confidence](images/image60.png)

61. Find all documents that have the word ABC with a score \> 1 and also contains the word Medical Center.![A screenshot of a computer Description automatically generated with medium confidence](images/image61.png)

62. This is a proximity search to look for the word ADULT near the word EXERCISES![A screenshot of a computer Description automatically generated with medium confidence](images/image62.png)

63. Fuzzy Search on a term, this gives the ability to find the work medications in the document without correct spelling. ![A screenshot of a computer Description automatically generated](images/image63.png)

64. Soundex Search on a term, giving the ability to find words that sound like the term provided, in this case "pressure". ![A screenshot of a computer Description automatically generated](images/image64.png)

65. Stem search on a term. For example if we are looking for documents with that stem of Jounal, then it will return words like Journaling.![A screenshot of a computer Description automatically generated with medium confidence](images/image65.png)

66. Accumulation Search on two or more terms. This is looking for both terms in the document and assigning a score. Higher if both terms are present.![A screenshot of a computer Description automatically generated](images/image66.png)

67. You can also weight each term as seen here. The word phyiscal carries 3x the weight of the work exercises. ![A screenshot of a computer Description automatically generated](images/image67.png)

68. Construct Themes Tables: To build themes for your documents you will first need to create a table to hold the themes.Run each statement individually by highlingting the the statement then clicking Run.![A screenshot of a computer Description automatically generated](images/image68.png)

69. Create Themes index for the documents currently in the PATIENT\_DOCUMENTS table.![A screenshot of a computer Description automatically generated](images/image69.png)

70. Query all themes. Show all themes with weight over 25![A screenshot of a computer Description automatically generated](images/image70.png)

71. Repeat for the Gist Table. Note: Run each of the 3 statements individually. ![Graphical user interface, text, application Description automatically generated](images/image71.png)

72. Repeat for the Filtered Docs Table. Note: Run each of the 3 statements individually. ![Graphical user interface, text Description automatically generated](images/image72.png)

73. Finally repeat for the Full Themes tables. Note: Run each of the 3 statements individually. ![A screenshot of a computer Description automatically generated](images/image73.png)

74. We can vertify all 4 tables were created by visitng the Object Browser. ![Graphical user interface Description automatically generated](images/image74.png)

75. Now let's create a new page to let end users view document gists with 1 click. Create Page -\> Report -\> Classic Report![Graphical user interface, application, Teams Description automatically generated](images/image75.png)

76. Give the Classic Report a name, and select Modal Dialog (this will allow the page to be a pop-up instead of a redirect)![A screenshot of a computer Description automatically generated with medium confidence](images/image76.png)

77. Finally select the source as SQL Query and enter the query as shown.![](images/image77.png)

78. On the new page, create two page items (P7\_QUERY\_ID and P7\_TITLE) by right-clicking on the content body region. ![Graphical user interface, application Description automatically generated](images/image78.png)

79. Set the Type of both new page items to "Hidden"![Graphical user interface, application Description automatically generated](images/image79.png)

80. Return to page 5. Right-Click Columns and Create Virual Column on this "Report 1"![A screenshot of a computer Description automatically generated](images/image80.png)

81. While Selecting the new virtual column you created, change the Heading to Document Gist. Under Link, click "No Link Defined" to define a new link for this virtual column. Set the link to page 7. Under Set Items, ensure you add both P7\_Query\_ID and P7\_TITLE, with values of \#ID\# and \#TITLE\# respectivly. Note: Use the menu to the right of the text box makes this easier.![Graphical user interface, application Description automatically generated](images/image81.png)

82. Add a Link Text by expanding the menu and selecting any of the defult optoions shown.![A screenshot of a computer Description automatically generated with medium confidence](images/image82.png)

83. Save and Run the application. Test this new feature by clicking on the pencil icon under Document Gist.![Graphical user interface, application Description automatically generated](images/image83.png)

84. You now have a gist of the PDF documents with just one click. Now lets see how we can replicate this to add Fildered Docs in plain text to the table as well.![](images/image84.png)

85. Navigate to Page 7 using the developent tool bar below. Choose the "+" icon and select Page as Copy. Select "Page in this application"![A screenshot of a computer Description automatically generated](images/image85.png)

86. Select the new page as page 8, and provide a new page name. On the next page select "Do not associate with a navigation menu entry"![A screenshot of a computer Description automatically generated with medium confidence](images/image86.png)

87. Give the Page Region a new name ![Graphical user interface, application Description automatically generated](images/image87.png)

88. You now have a new page (Page 8) where you can alter the SQL query to reflect that of Full Text. Let's create another virtual column link to this page.![Graphical user interface, application Description automatically generated](images/image88.png)

89. Save and return to Page 5. Right- Click columns and Create Virtual Column![Graphical user interface, application, Teams Description automatically generated](images/image89.png)

90. Make changes similar to before, but instead redirecting to Page 8![Graphical user interface, application Description automatically generated](images/image90.png)

91. Change the link text to a defult icon. Save and run the page.![A screenshot of a computer Description automatically generated with medium confidence](images/image91.png)

92. By clicking the manifying glass icon we can see the full text for that individual document.![Graphical user interface, text, application Description automatically generated](images/image92.png)

93. Click Edit App 100 down in the development tool bar. Let's create one more page for our patients appointments.This time we will create a Calandar page![](images/image93.png)

94. Give the new page a name, and select Next. ![Graphical user interface, application Description automatically generated](images/image94.png)

95. Select "Create a new nagivation menu entry" and enter a naviagation menu entry name![A screenshot of a computer Description automatically generated with medium confidence](images/image95.png)

96. Enter the source and a SQL Query and paste the code provided. Click Next.![A screenshot of a computer Description automatically generated with medium confidence](images/image96.png)

97. For Display Column select Last\_Name, and for Start Data Column select Date\_Time.![A screenshot of a computer Description automatically generated with medium confidence](images/image97.png)

98. Lastly under attributed for the Patient Appointments Region. Activate Show time, and add some supplemental information for each of the events on the calendar.Save and Run.![Graphical user interface, application Description automatically generated](images/image98.png)

99. Use this navigation to return to the end of 2021/start of 2022 where data is present in out tables. Note you can hover over the appointments to view the supplemental information about each one. ![A screenshot of a computer Description automatically generated](images/image99.png)

