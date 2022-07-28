# Build a Healthcare Portal using Oracle Content Management
## Introduction

What is Oracle Content Management?

Oracle Content Management is a cloud-based content hub to drive omni-channel content management and accelerate experience delivery. It offers powerful collaboration, workflow management, and development capabilities to streamline the creation and delivery of content and improve customer and employee engagement.

In this lab, you will build a website for Care Clinics and integrate a chatbot to help the patients to schedule an appointment online.

Estimated Time: 2 hours

### Objectives

In this lab, you will learn how to:

- Create a website from a Blank Template.
- Build assets and publish them on the website using the Asset Management capability within OCM. 
- Sync the documents in your local machine. 
- Use recommendations and audience attributes feature to show only relavent data to the patients. 
- Integrate Chatbot onto the web page.

## Pre-requisites

Template: 

## Task 1: Create a Oracle Content Management Instance and Import the template

1. Log in to the Oracle Cloud at cloud.oracle.com. Cloud Account Name is howarduniversity. Click “Next”.
2. Click on “Direct Sign-In” and enter your Cloud Account email and password.
3. Once you are logged in, you are taken to the cloud services dashboard where you can see all the services available to you. Click the navigation menu in the upper left to show top level navigation choices.
4. Click **Instances** under **Content Management**
  ![](images/1-Instances.png " ")
5. Select the CareClinics compartment and create an instance.
  ![](images/1-createinstance.png " ")
6. After the instance is successfully created. Click on the *Open Instance* to open the OCM console. 
  ![](images/1-openinstance.png " ")
7. Click on Sites on the left navigation pane, click on *Configure* and *Save* button on the next screen. 
  ![](images/1-configure.png " ")
8. Click on the View all templates in the Developer tab. 
  ![](images/1-createtemplate.png " ")
9. Go ahead and import the template package which you dowloaded. 
  ![](images/1-import.png " ")

10. Upload the file into documents and hit the *OK* button to import a template.
  ![](images/1-createok.png " ")

## Task 2: Create a Site from the template

1. Go ahead and click on the icon to create a site from the template which you just imported.
  ![](images/2-createsite.png " ")

2. Now, select Create a new repository from the drop-down under the Asset Repository sections. 
  ![](images/2-createrepo.png " ")

3. In properties section, enter the following details and hit the *Save* button: 
  - Name: CareClinics
  - Asset Types: Bio, File, Image, NewsArticle, SE2-Story, Videos
  - Taxonomy - PatientInfo(PAT)
    ![](images/2-properties.png " ")

4. Under the configure site section, enter the following details: 
  - Name: CareClinics
  - Assets in Target Repository - Leave it as is (Default - Duplicate Assets)
    ![](images/2-configuresite.png " ")
  - Now hit the *Finish* button.
  
## Task 3: Prepare a Repository

Create a Asset type: 

1. Select *Content* under the *Administration section* in the left navigation pane.  
2. Pick Asset types from the drop down and click on the *Create* button on the top right of the page to create your own Asset type.
3. Now, enter the following details:
  - Name: Specialization
  - Choose Asset Type: Create a Content Item type
  - Click the *Create* button
    ![](images/3-assettype.png " ")
  - Drag and drop the *Text* field under the Content type definition and update the *Text settings* as follows:
  - Provide the display name - *Specialization name* and click the *Next* button.
  ![](images/3-specialization.png " ")
  - *Save* the Asset Type.

Create Taxonomies:

1. Select *Taxonomies* from the drop-down.
  ![](images/3-taxonomy.png " ")
2. Create a taxonomy to display the information regarding CareClinics.
  - Name: CareClinicsInfo
  - Abbreviation: CCI
  ![](images/3-cci.png " ")
  - Add Category - Blogs
  - Add Sibling - Health Talks
  - Add Sibling - Testimonials
  - Select the following checkbox to allow publishing the taxonomy and click the *Done* button.
  ![](images/3-allowpublish.png " ")  

3. Select the Taxonomy (CareClinicsInfo) which you just created and click the *Promote* button.
  ![](images/3-promote.png " ") 

4. Confirm to proceed Promotion. 
  ![](images/3-promoteconfirm.png " ") 

Add the Taxonomy and Content types to the Repository:

1. Edit the repository by adding the Specialization content type and CareClinicsInfo taxonomy to the CareClinics Repository.
  ![](images/3-editrepo.png " ") 
2. Click the *Save* button.

### Task 4: Add Assets to the repository

Oracle Content Management's structure starts with repositories. A repository is a storage location for assets that you need for building web, mobile, or other user experiences in your organization. An asset can be a content item that represents an individual piece of content, such as a blog post, case study, or product information; or a digital asset that represents an image, video, or other type of media that you need in your experiences.


We will now see the process to create the assets in a repository: 

1. Go to the left navigation pane and select *Assets*. You will observe that there are CareClinics repository which already contains a few assets. 
 ![](images/4-assets.png " ")
2. We will select *Create* button and select Create Content Item from the dropdown. 
 ![](images/4-createcontentitem.png " ")
3. Now, we will start creating content items as follows: 

*Specialization:* 

1. Select Specialization from the dropdown. 
 ![](images/4-spec.png " ")
2. Content Item Properties: 
  - Name: Emergency Care
  - Specialization name: Emergency Care
  - Click the *Save* and *Done* button.
 ![](images/4-specer.png.png " ")

3. Repeat step 1 and 2 for the following specializations: 
  - Name: Cardiology, Specialization name: Cardiology
  - Name: Neurology, Specialization name: Neurology
  - Name: Radiology, Specialization name: Radiology
  - Name: Rehabilitation, Specialization name: Rehabilitation
  - Name: Surgery, Specialization name: Surgery
  - Name: Stroke Care, Specialization name: Strxoke Care
  - Name: Spiritual Care, Specialization name: Spiritual Care

*Personal Information:*

*Note: * Use the images from the PatientInfo folder which you downloaded. 

1. Select Bio from the dropdown. 
2. Content Item Properties:
- Name: Health Insurance
- Image: InsuranceCard.jpeg
- Select category (PatientInfo(PAT)>InsuranceCard)
 ![](images/4-ic.png " ") 
- Email: Enter your email- Ex: sp@careclinics.org
3. Repeat step 1 and 2 to create another Content Item: 
- Name: Covid Vaccination Proof
- Image: covidvaccination.jpeg 
- Select category - (PatientInfo(PAT)- VaccinationProof)
- Email: Enter your email- Ex: sp@careclinics.org
4. Ensure the Vaccination Proof and Insurance Card is added to the right category.
 ![](images/4-bioasset.png " ") 

*News Article:*

*Note: * Use the images from the Testimonials folder which you downloaded. 

1. Select NewsArticle from the dropdown. 
2. Content Item Properties: 
  - Name: Justin Lester
  - Author: Justin Lester
  - Date: 07/09/2022
  - Content: Patient with COVID-19, pneumonia and heart failure survives with the help of ECMO.
  - Image: JustinLester.jpg
  - Category: CareClinicsInfo > Testimonials
    ![](images/4-justin.png " ") 
  - Click the *Save* and *Done* button.
3. Repeat step 1 and 2 to create another Content Item: 
  - Name: Kathy Maden
  - Author: Kathy Maden
  - Date: 03/01/2022
  - Content: Kathy came to Clinics Hospital for a total right hip replacement using an anterior approach. The next day, she was able to return home. Within three days of her surge...
  - Image: KathyMaden.jpg
  - Category: CareClinicsInfo > Testimonials
  - Click the *Save* and *Done* button.
4. Ensure the NewsArticle Assets are added to the right category.
  ![](images/4-news.png" ")


*Health Talks*

*Note: * Use the images from the HealthTalks folder which you downloaded. 

1. Select SE2-Story from the dropdown. 
2. Content Item Properties: 
  - Name: Mental Health and Motherhood
  - Summary:  The isolation, loss and fear we’ve experienced during the COVID-19 pandemic has taken its toll on everyone’s mental health. Just ask any mom who’s experienced the weight of the pandemic on top of the everyday stresses of parenthood.
  - Media: motherhood.png | Category (CareClinicsInfo > HealthTalks)
  - Title: Mental Health and Motherhood
  - Content Description: The isolation, loss and fear we’ve experienced during the COVID-19 pandemic has taken its toll on everyone’s mental health. Just ask any mom who’s experienced the weight of the pandemic on top of the everyday stresses of parenthood.
  ![](images/4-motherhood.png " ")
  - Asset Category: CareClinicsInfo > HealthTalks
3. Repeat step 1 and 2 to create another Content Item: 
  - Name: Focusing on Preventive Care During a Pandemic
  - Summary:  Keeping up to date on preventative screenings and wellness visits is the most important thing you can do to stay healthy.
  - Media: preventive.png | Category (CareClinicsInfo > HealthTalks)
  - Title: Focusing on Preventive Care During a Pandemic
  - Content Description: A health care facility is one of the safest places you can go to right now because everyone who's working there is taking safety so seriously.
  - Asset Category: CareClinicsInfo > HealthTalks
4. Ensure the Health Talks Assets are added to the right category.
  ![](images/4-healthtalk.png " ")

*Blogs*

*Note:* Use the images from the HealthTalks folder which you downloaded. 

1. Select SE2-Story from the dropdown. 
2. Content Item Properties: 
  - Name: Decentralized clinical trials - avoiding the snapback
  - Summary:  Winston Churchill was quoted as saying, “Never let a good crisis go to waste”. The on-going pandemic is a global crisis that has forced most physical activities to be made remotely, including clinical trial activities. What we must avoid is the snapback to the pre-pandemic practice of requiring the study participant to physically visit the investigator site location.
  - Media: clinicaltrial.jpg | Category (CareClinicsInfo > Blogs)
  - Title: Decentralized clinical trials - avoiding the snapback
  - Content Description: (Copy the content from here - https://blogs.oracle.com/health-sciences/post/decentralized-clinical-trials-avoiding-the-snapback)
  - CreatedByName: Elvin Thalund
  - CreatedByEmail: et@careclinics.org
  - Asset Category: CareClinicsInfo > Blogs
  ![](images/4-clinic.png " ")
3. Repeat step 1 and 2 to create another Content Item: 
  - Name: The Larger Pandemic - Disparities in Healthcare
  - Summary:  Earlier this year I asked the Oracle Health team if they or someone they love have had a healthcare experience that connects them to our mission. Unsurprisingly, everyone has. Also unsurprising is that many of those experiences could have been improved if those involved had access to better data, tools, and resources. These stories galvanize my desire to explore how the intersection of science, technology, and the HUMAN can improve health equity and create a better healthcare experience for all.
  - Media: pandemic.jpg | Category (CareClinicsInfo > Blogs)
  - Title: The Larger Pandemic: Disparities in Healthcare
  - Content Description: (Copy the content from here - https://blogs.oracle.com/healthcare/post/the-larger-pandemic)
  - CreatedByName: Stephanie Trunzo
  - CreatedByEmail: st@careclinics.org
  - Asset Category: CareClinicsInfo > Blogs
4. Ensure the Blogs Assets are added to the right category.
  ![](images/4-blog.png " ")

