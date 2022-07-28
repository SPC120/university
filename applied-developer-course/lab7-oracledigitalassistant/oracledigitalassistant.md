# Build a Digital Assistant
## Introduction

In this lab, we will build a Digital Assistant for patients to schedule an appointment online with the Doctor.

Estimated Time: 2 hours
### Objectives

In this lab, you will:

- Create a skill, define intents, utterances, entities.
- Design a conversation flow.
- Create a custom component to update the database from the chatbot.
- Validate, debug and test your skill.

## Pre-requisites 


Before we get started:

- Download the Skill template - <a href="files/CareClinics_Template.zip">download</a> 

- Install your favorite IDE (VScode - preferable)

- Install NodeJS in your local machine.


(Add documentation - ORDS)

## Task 1: Create a Digital Assistant Instance and Import the Skill
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

## Task 2: Create and Test an Intent
Oracle Digital Assistant's underlying natural language processing (NLP) engine doesn't inherently know about the business or task that a skill is supposed to assist with. For the skill to understand what it should react to, you need to define intents and examples (utterances) for how a user would request a specific intent.

You will create intents for finding a doctor and positive health therapy tips. 

Create the Find a Doctor intent: 

1. Click the + Intent button.
2. Next to the Conversation Name field, click the Edit button, and enter *Find Doctor*.
3. In the Name field, type *findDoctor*.
4. Select and copy all of the example sentences below to your clipboard and paste in the *Advance Input Mode* section under Examples

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

    (You'll notice that it's fine for utterances to have inconsistent punctuation and capitalization.)
5. Click the +Create button.

  ![](images/2-intent.png " ")

### Create the Positive Health intent:

1. Click the + Intent button.
2. Next to the Conversation Name field, click the Edit button, and enter *Positive Health*.
3. In the Name field, type *positiveHealth*.
4. Select and copy all of the example sentences below to your clipboard and paste in the *Advance Input Mode* section under Examples

    ```
    <copy>
    health tips
    mental health treatment
    need positive health tips
    positive outlook
    mental health therapy
    </copy>
    ```
5. Click the +Create button.

### Create the Unresolved intent:
The unresolved intent in a skill handles messages outside of the domain that a skill is designed to process. For this you usually map a dialog flow state to the *unresolvedIntent* action transition to inform the user that the skill could not handle the request.

1. Click the + Intent button.
2. Next to the Conversation Name field, click the Edit button, and enter *Unresolved Intent*.
3. In the Name field, type *unresolvedIntent*.
4. Select and copy all of the example sentences below to your clipboard and paste in the *Advance Input Mode* section under Examples
    ```
    <copy>
    blah blah
    buy me a tv
    play music
    sing a song
    </copy>
    ```
5. Click the +Create button.


### Train and test the intents:

You've now provided the basic ingredients that allow the skill to recognize user input for both the intents. Currently, the skill can't understand any user input.

To enable the skill to interpret user input based on the utterances that you just added, you need to train to build the intent model.

1. On the right side of the page, locate and click the Train. Select *Trainer Ht* and then click *Submit*.

  ![](images/2-train.png " ")

2. Let's perform a quick test in the utterance tester.

  ![](images/2-utttester.png " ")

  Go ahead and test your own utterances and train your bot.

## Task 3: Create Entities

Now it's time to add entities, which detect information in the user input that can help the intent fulfill a user request. We will be creating entities with regular expression, value lists and add them to a composite bag. 



1. In the left navigation for the designer, select the Entities icon.
2. Click + Add Entity to create a new entity.
3. In the Name field, change the value to *FirstName*.
4. Select the Configuration type as *Regular Expression* and value as [a-zA-Z]+
  ![](images/3-fname.png " ")
5. Click the Create button
6. Follow the same steps for entities:  
    - *Last Name* (Name - LastName, type - Regular Expression, Value - [a-zA-Z]+)
    - *PhoneNumber* (Name - PhoneNumber, type - Regular Expression, Value - ^[\+]?[(]?[0-9]{3}[)]?[-\s\.]?[0-9]{3}[-\s\.]?[0-9]{4,6}$)
    - *State* (Name - State, type - Regular Expression, Value - [a-zA-Z]+)
    - *City* (Name - City, type - Regular Expression, Value - [a-zA-Z]+)

Create a Value List Entity

1. Click + Add Entity to create a new entity.
2. In the Name field, change the value to *TimePicker*.
3. In the Configuration section, select *Value list* from the Type menu.
4. Click + Value.
For Value, type *10:00 AM*.
For Synonyms, type *10am*, then click Enter. Type 10:00am, and then click Enter again.<br/> <br/>
Here are the list of values and synonyms:<br/>
8:30 AM	- 8:30, 8:30am, 8:30 am <br/>
10:00 AM - 10am, 10:00am, 10:00 AM, 10 am <br/>
12:30 PM - 12:30pm, 12:30, 12:30 pm <br/>
2:00 PM	- 2:00 pm, 2 pm, 2pm, 2:00pm <br/>
3:30 PM	- 3:30pm, 3:30, 3:30 pm <br/>

Click Create.
  ![](images/3-timepickerval.png " ")

5. Repeat the above steps to create another value list for the *Provider*. <br/>

    Name: Provider <br/>
    Configuration: Value List <br/>
    Values: <br/>
    Dermatology	- Dermatology, derma <br/>
    Family Medicine	- FamilyMed, family medicine, family med <br/>
    Obstetrics and gynecology - ob gyn, ob-gyn, gyn, ob <br/>
    Pediatrics - pediatric, pediatrics <br/>
    Primary care - primarycare, primcare <br/>
    Other - something else, somethingelse, other, others, not here <br/>

  ![](images/3-provider.png " ")

Create a Composite Bag Entity

In this step, you're going to simplify your development efforts using a composite bag entity, which enables you to manage the multiple entities that you just created as a consolidated entity. In addition to unifying your entities, the various composite bag properties enable your skill to match entity values in complex, real-world scenarios that involve erratic user input.

7. Click + Add Entity to create a new entity with the name *RegisterPatientBag* and select the Configuration type as *Composite Bag*.
  ![](images/3-patientbagcreate.png " ")
8. Select the *RegisterPatientBag* and add a *+ Bag Item*.
  ![](images/3-addbag.png " ")
9. Enter the Name as *FirstName*, select the type as *Entity* and Entity name as *FirstName* from the drop down.
  ![](images/3-firstnameentity.png " ")
10. Turn off *Prompt for Disambiguation* and *Out of Order Extraction* toggle button and add the following *prompts*:

    ```
    <copy>
    Enter first name
    </copy>
    ```
    ```
    <copy>
    Invalid name, please re-enter your first name (Ex: John)    
    </copy>
    ```
  ![](images/3-fnprompt.png " ")
11. Click the close button.
12. Add *+ Bag Item* for Last Name.<br/>
    Name: LastName
    Type: Entity
    Entity Name: LastName
    Turn off *Prompt for Disambiguation* and *Out of Order Extraction* toggle button
    Prompts: 

    ```
    <copy>
    Enter your last name
    </copy>
    ```
    ```
    <copy>
    Invalid name, please re-enter your last name (Ex: Smith)  
    </copy>
    ```
13. Add *+ Bag Item* for Phone Number.<br/>
    Name: PhoneNumber
    Type: Entity
    Entity Name: PhoneNumber
    Turn off *Prompt for Disambiguation* and *Out of Order Extraction* toggle button
    Prompts: 

    ```
    <copy>
    Enter your phone number
    </copy>
    ```
    ```
    <copy>
    Enter the phone number in the following format (Ex: 562XXXXXXX/+9198666XXXXX/555-XXX-XXXX)) )
    </copy>
    ```
    ```
    <copy>
    Invalid number, Please try again
    </copy>
    ```

14. Add *+ Bag Item* for Street Address.<br/>
    Name: StreetAddress
    Type: Entity
    Entity Name: Address
    Turn off *Prompt for Disambiguation* and *Out of Order Extraction* toggle button
    Prompts: 

    ```
    <copy>
    Enter your street address
    </copy>
    ```
    ```
    <copy>
    Enter a valid street address (Ex: 2300 Cloud Way)
    </copy>
    ```

      ![](images/3-staddress.png " ")
      ![](images/3-stprompt.png " ")
      
15. Add *+ Bag Item* for City.<br/>
    Name: City
    Type: Entity
    Entity Name: City
    Turn off *Prompt for Disambiguation* and *Out of Order Extraction* toggle button
    Prompts: 

    ```
    <copy>
    Enter your city
    </copy>
    ```
    ```
    <copy>
    Invalid city, please re-enter your city name (Ex: Austin)
    </copy>
    ```
16. Add *+ Bag Item* for State.<br/>
    Name: State
    Type: Entity
    Entity Name: State
    Turn off *Prompt for Disambiguation* and *Out of Order Extraction* toggle button
    Prompts: 

    ```
    <copy>
    Enter your State
    </copy>
    ```
    ```
    <copy>
    Invalid entry, please enter the state you reside in (Ex: Texas)
    </copy>
    ```
17. Add *+ Bag Item* for Zipcode.<br/>
    Name: Zipcode
    Type: Entity
    Entity Name: Number
    Turn off *Prompt for Disambiguation* and *Out of Order Extraction* toggle button
    Prompts: 

    ```
    <copy>
    Enter your zip code
    </copy>
    ```
    ```
    <copy>
    Invalid code, please try again (Ex: 78741)
    </copy>
    ```
18. Add *+ Bag Item* for Location.<br/>
    Name: Location
    Type: Location
    Turn off *Prompt for Disambiguation* and *Out of Order Extraction* toggle button
    Prompts: 

    ```
    <copy>
    Upload your location
    </copy>
    ```



19. Now, Let's create another Composite bag for Date Picker. 

- Click + Add Entity to create a new entity with the name *DatePickerBag* and select the Configuration type as *Composite Bag*.

- Add *+ Bag Item* for *dateEntry*.
<br/>
    Name: dateEntry
    Type: Entity
    Entity Name: DATE

      ![](images/3-dateentry.png " ")

    Ambiguity Resolution Rule: 
<br/>
    Switch on toggle - Consider End User Locale
    Default Date Format - MM/DD/YY
    Resolve Date as *Default* in intents
      ![](images/3-ambrule.png " ")
    Prompts: 

    ```
    <copy>
    Select your preferred date of appointment
    </copy>
    ```
    ```
    <copy>
    Please enter the date in the proper format
    </copy>
    ```

20. We will create another composite bag entity

- Click + Add Entity to create a new entity with the name *TimePickerBag* and select the Configuration type as *Composite Bag*.

- Add *+ Bag Item* for *TimePicker*.
<br/>
    Name: dateEntry
    Type: Entity
    Entity Name: TimePicker

      ![](images/3-dateentry.png " ")

    Prompts: 

    ```
    <copy>
    Select your preferred time slot
    </copy>
    ```

*Note:* Ensure that all the entities are trained.


## Task 4: Create a Dialog Flow

With the NLP model created, you are ready to build a dialog flow for the skill. The dialog flow is a blueprint for the interactions that enable the conversation between the skill and the user. Although you're going to create a single flow in this tutorial, a skill can have multiple flows that support different use cases and functions.

Each flow is made up of one or more states, and each state executes a function: rendering a skill response message, authenticating a user, branching the conversation when certain conditions are met, etc. The Visual Flow Designer provides you with templates for each state.

Let's test the current dialog flow

1. Go ahead and click the preview button to test the current flow.

  ![](images/4-preview.png " ")

2. Start the conversation by typing *Hi* and observe the states and intents in the conversation tester  window.

  ![](images/4-draftconvtest.png " ")

  ![](images/4-draftintents.png " ")


Start building the dialog flow

Each state implemented by a
component
– Executes logic
– Receives user input
– Returns bot responses
– Determines navigation

1. Go ahead and replace *System.intent* component. This will allow you to conditionally direct a conversation to a logical next dialog flow state for each user utterance.  
  ```
  <copy>
  ########### System intent ###############
    intent:
      component: "System.Intent"
      properties:
        variable: "iResult"
      transitions:
        actions:
          unresolvedIntent: "unresolvedIntent"
          greetings: "greetings"
          findDoctor: "findPatientDetails"
          positiveHealth: "startTheraphy"

  </copy>
  ```
2. Add an unresolved state by selecting *+Add Component* to open the component templates. 

  ![](images/4-addcomp.png " ")

- Now, select *Display text message* from the *Hot Picks*, pick *Greetings* from the drop down under *insert after state*, uncheck include template comments and select *Insert Component*.

  ![](images/4-unresolved.png " ")

- Update the component as follows:

```
<copy>
########### Unresolved State ###############
  unresolvedIntent:
    component: "System.Output"
    properties:
      text: "I don't understand. What do you want to do?"
    transitions:
      return: "intent" 

</copy>
```
3. We will add the dialog flow for *Positive Health* intent. Here we are going to display a card carousal with images, text and links to redirect to different videos.

- Select *+ Add component* and pick *Display Action Button Message* (under User messaging -> Display Multimedia Messages).
- Pick "unresolved" from the drop down under *insert after state*, Uncheck include template comments and select *Insert Component*.

  ![](images/4-cardlayout.png " ")

- Update the component as follows:
```
<copy>
######## Begin Theraphy ############ 

  startTheraphy:    
    component: "System.CommonResponse"
    properties:
      processUserMessage: true
      keepTurn: "false"
      metadata:
        responseItems:
        - type: "cards"
          cardLayout: "horizontal"
          name: "Cards"
          actions: []
          cards:
          - title: "${theraphy.name}"
            description: "${theraphy.description}"
            imageUrl: "${theraphy.image}"
            name: "theraphy"
            iteratorVariable: "theraphy"
            actions:
            - label: "Practice Excercise"
              type: "url"
              payload:
                url: "${theraphy.action}"
        globalActions: []
    transitions: 
      return: "done"
</copy>
```

- Also, add transition for *startTheraphy* under the *greetings* component as follows:      
```
<copy>
    transitions:
      actions:
        textReceived: "intent"
        startTheraphy: "startTheraphy"
</copy>
```
- Go ahead and test the flow. 

  ![](images/4-startTheraphy.png " ")

4. Now we will request the user if they already have a provider or if they wish to register. 

- Declare a PatientType variable under context variables.     

```
<copy>
PatientType: "string"
</copy>
```

- Paste the following YAML code in your dialog flow.

```
<copy>
########### Find a doctor and schedule appointment ###############

  findPatientDetails:
    component: "System.CommonResponse"
    properties:
      processUserMessage: true
      variable: "PatientType"
      metadata:
        responseItems:        
        - type: "text" 
          text: "Do you have a provider or are you a new patient?"
          footerText:
          actions:
          - label: "New Patient"
            type: "postback"
            keyword: "New Patient"
            payload:
              action: "registerPatient" 
          - label: "I have a provider"
            type: "postback"
            keyword: "provider"
            payload:
              action: "I have a provider" 
    transitions:
      actions:
        registerPatient: "registerPatient"
        I have a provider: "chooseProvider"
        textReceived: "intent"
</copy>
```

- Also, add transition for *findPatientDetails* under the *greetings* component as follows:      
```
<copy>
    transitions:
      actions:
        startTheraphy: "startTheraphy"
        findPatientDetails: "findPatientDetails"
        textReceived: "intent"
</copy>
```
5. Now, we will go ahead and ask for patient details by leveraging the composite bag entity we created in the previous section.

- Let us declare the variable for *RegisterPatientBag* composite bag entity we created. 

```
<copy>
RegisterPatientBag: "RegisterPatientBag"
</copy>
```
- Add the following YAML code under the *findPatientDetails* component.

```
<copy>
##############Ask for Patient details##################

  registerPatient:
    component: "System.CommonResponse"
    properties:
      processUserMessage: true 
      variable: "RegisterPatientBag"
      nlpResultVariable: "iResult"    
      cancelPolicy: "immediate"
      transitionAfterMatch: "false"    
      metadata:
        responseItems:        
        - type: "text" 
          text: "${system.entityToResolve.value.prompt}"
          actions:
          - label: "${enumValue.value!enumValue.originalString}"
            type: "postback"
            iteratorVariable: "system.entityToResolve.value.enumValues"
            payload:
              variables:
                RegisterPatientBag: "${enumValue.value!enumValue.originalString}" 
        globalActions: 
        - label: "Send Location"
          type: "location"
          visible:
            entitiesToResolve:
              include: "Location"
    transitions:
      actions:
        textReceived: "intent"
      next: "registerUserDB"
</copy>
```
*Note:* You should still be able to test even though you see there are errors in your validation

  ![](images/4-testconv.png)

6. Create a custom component

  Custom components are reusable units of custom code that you can call from your skill's dialog flow. In order to register the patients details in the database, we will call the REST API using the NodeJS. 

  Follow these steps to install the Oracle Node.js Bots SDK to your local machine.
  - Open a terminal window.
  - To install Oracle Bots Node.js SDK for global access on your laptop, enter this command:

```
<copy>
npm install -g @oracle/bots-node-sdk
</copy>
```

On a Mac, you use the sudo command:

```
<copy>
sudo npm install -g @oracle/bots-node-sdk
</copy>
```

To verify the success of your installation, enter this command:

```
<copy>
bots-node-sdk -v
</copy>
```

- Open the directory where you wish to create a custom component and paste the following command in your terminal.
```
<copy>
bots-node-sdk init carecliniccs --component-name registerpatient 
</copy>
```
 ![](images/4-install.png " ")

- Now, open the registerpatient.js file under components and replace the contents with the following code: 


```
<copy>
'use strict';
const fetch = require("node-fetch")

module.exports = {
  metadata: () => ({
    name: 'registerpatient',
    properties: {
      first_name: { required: true, type: 'string' },
      last_name: { required: true, type: 'string' },
      address: { required: true, type: 'string' },
      city: { required: true, type: 'string' },
      state: { required: true, type: 'string' },
      zipcode: { required: true, type: 'string' },
      longitude: { required: true, type: 'int' },
      latitude: { required: true, type: 'string' }, 
      phonenumber: {required: true, type: 'string'}, 
      ordsUrl: {required: true, type: 'string'}, 
      keepTurn: {required: false, type: 'string'}
    },

    supportedActions: ['success', 'failure']
  }),

  invoke: (context, done) => {
    const { first_name } = context.properties()
    const { last_name } = context.properties()
    const { address } = context.properties()
    const { city } = context.properties()
    const { state } = context.properties()
    const { longitude } = context.properties()
    const { latitude } = context.properties()
    const { phonenumber } = context.properties()
    const { zipcode } = context.properties()
    const { ordsUrl } = context.properties()

    var myHeaders = new fetch.Headers();
    myHeaders.append("Content-Type", "application/json");

    var raw = JSON.stringify({
      "patient_id": Math.floor(Math.random() * 100) + 30000,
      "first_name": first_name,
      "last_name": last_name,
      "address": address,
      "city": city,
      "state": state,
      "county": "ALAMEDA",
      "zipcode": zipcode,
      "longitude": longitude,
      "latitude": latitude,
      "practitioner_id": "930",
      "phonenumber": phonenumber
    });

    var requestOptions = {
      method: 'POST',
      headers: myHeaders,
      body: raw,
      redirect: 'follow'
    };

    fetch(ordsUrl, requestOptions)
      .then(response => {
        return response.json();    
      })
      .then((data) => {    
        context.reply("Registered the user successfully!"); 
        context.transition('success');
        context.keepTurn(true);
        done();
        })
      .catch((err) => {
        done(err);
        });  
      }
    };
</copy>
```
- Paste the following commands in your terminal

```
<copy>
cd carecliniccs
npm install
npm pack
</copy>
```
- Go back to the ODA console and create a custom component and add the service as given in the following picture.
  ![](images/4-createservice.png)

- Go to settings icon in the navigation pane on the left and select the configuration tab. 

  ![](images/4-settings.png)

- Go ahead and update the ordsUrl which you saved in your *Notepad*.

  ![](images/4-ordsurl.png)

- Paste the following YAML code in the dialog flow below *registerPatient*.

```
<copy>
  registerUserDB:
    component: "registerpatient"
    properties: 
      ordsUrl: ${system.config.ordsUrl}
      first_name: ${RegisterPatientBag.value.FirstName}
      last_name: ${RegisterPatientBag.value.LastName}
      address: ${RegisterPatientBag.value.StreetAddress.originalString}
      city: ${RegisterPatientBag.value.City}
      state: ${RegisterPatientBag.value.State}
      zipcode:  ${RegisterPatientBag.value.Zipcode.originalString}
      longitude: ${RegisterPatientBag.value.Location.longitude}
      latitude: ${RegisterPatientBag.value.Location.latitude} 
      phonenumber: ${RegisterPatientBag.value.PhoneNumber}
      keepTurn: true
    transitions: 
      actions: 
        success: "chooseProvider"
        textReceived: "intent"
</copy>
```
7. After registration, the next step for the patient is to select the specialization for which we will use the System.ResolveEntities component.

- Select *+ Add component* and pick *Display Action Button Message* (under Hot Picks -> Resolve Entities).
- Pick "registerUserDB" from the drop down under *insert after state*, Uncheck include template comments and select *Insert Component*.

  ![](images/4-resolve.png " ")

- Let us declare the variable for *RegisterPatientBag* composite bag entity we created. 

```
<copy>
    Provider: "Provider"
</copy>
```

- Update the component as follows:

```
<copy>
  chooseProvider:
    component: "System.ResolveEntities"
    properties:
      variable: "Provider"
      nlpResultVariable: "iResult"      
      cancelPolicy: "immediate" 
    transitions:
      next: scheduleDate
      actions: 
        textReceived: intent
</copy>
```
8. After we select the specialization, we should now select a scheduled date. 

*Note:* ODA cannot display the calendar widget, so we will create custom properties specific to the web channel and add the javascript code to display the calendar widget to the bot deployed on a web page.

- Declare the variable for *RegisterPatientBag* composite bag entity we created. 

```
<copy>
    selectedDate: "DatePickerBag"
</copy>
```

- Add the following code below *chooseProvider* component.

```
<copy>
  scheduleDate:
    component: "System.CommonResponse"
    properties:
      processUserMessage: true
      nlpResultVariable: "iResult"
      cancelPolicy: "immediate"
      transitionAfterMatch: "false"
      variable: "selectedDate"
      metadata:
        responseItems:            
        - type: "text" 
          text: "${system.entityToResolve.value.prompt}"
          channelCustomProperties:
          - channel: "websdk"
            properties:
              uiComponent:
                type: calendar
                properties:
                  minDate: "${(.now?long + 1*24*3600*1000)?number_to_date?iso_utc}" #today 
                  maxDate: "${(.now?long + 15*24*3600*1000)?number_to_date?iso_utc}" #next 15 days
                  variable: "selectedDate"
          visible:
            entitiesToResolve:
              include: "dateEntry"     
    transitions:
      actions:
        cancel: "intent"    
      next: "selectTime"
</copy>
```
9. After which Patient needs to select the preferred time slot.

- Declare the variable for *RegisterPatientBag* composite bag entity we created. 

```
<copy>
    TimePickerBag: "TimePickerBag"
</copy>
```
- Add the following code below *scheduleDate* component.

```
<copy>
  selectTime:
    component: "System.ResolveEntities"
    properties:
      variable: "TimePickerBag"
      nlpResultVariable: "iResult"      
      cancelPolicy: "immediate" 
    transitions:
      next: findDoctor
      actions: 
        textReceived: intent
</copy>
```

10. Display the list of Doctors to the patients and show an appointment summary report. Here, we will use free marker expressions to show the summary of the appointment.

```
<copy>
  findDoctor:
    component: "System.CommonResponse"
    properties:
      processUserMessage: true
      keepTurn: false
      metadata:
        responseItems:        
        - type: "text" 
          text: "Here are the best in class doctors for you!"
          footerText:
        - type: "cards"
          cardLayout: "horizontal"
          name: "Doctor"
          actions: []
          cards:
          - title: "${Doctor.name} (ID - ${Doctor.practitionerid})"
            description: "${Doctor.description}"
            imageUrl: "${Doctor.image}"
            name: "Doctor"
            iteratorVariable: "Doctor"             
            actions:
            - label: "Book Appointment"
              type: "postback"
              payload:
                action: "${Doctor.action}" 
                variables: 
                  DoctorName: "${Doctor.name}"
                  practitionerid: "${Doctor.practitionerid}"
        globalActions: []
    transitions: 
      next: "apptSummary"  
      
 
  apptSummary:
    component: "System.CommonResponse"
    properties:
      keepTurn: true
      metadata:
        responseItems:
          - type: "text"
            text: "You have successfully scheduled your appointment with the doctor ${DoctorName.value} (ID - ${practitionerid.value}) for on ${selectedDate.value.dateEntry.date?number_to_date?string['yyyy-MM-dd']} at ${TimePickerBag.value.TimePicker}"
    transitions:
      next: "promptInsurance"
</copy>
```

11. After successfully scheduling the appointment, patient will be given a choice to upload their insurance card from the phone. 

- In this step, we will prompt the Patient to upload the insurance. 
- They will display a QR code to upload your health insurance card from your phone. Here, Patients can use thier camera app on your phone to scan the QR code.
- The bot prompts for a confirmation.

*Note:* Update the QR code with the one generated by your VBCS application. 

```
<copy>

  promptInsurance:
    component: "System.CommonResponse"
    properties:
      processUserMessage: true
      metadata:
        responseItems:        
        - type: "text" 
          text: "Would you like to upload your insurance now or later?"
          footerText:
          actions:
          - label: "Yes! I can upload now"
            type: "postback"
            keyword: "Yes"
            payload:
              action: "Yes" 
          - label: "I will do it later"
            type: "postback"
            keyword: "later"
            payload:
              action: "Later" 
    transitions:
      actions:
        Yes: "uploadHealthInsurance"
        Later: "uploadLater"
        textReceived: "intent"

      
  uploadHealthInsurance:
    component: "System.CommonResponse"
    properties:
      keepTurn: true
      metadata:
        responseItems:        
        - type: "attachment"
          attachmentType: "image"
          attachmentTitle: "Use the following QR code to upload your health insurance card from your phone"
          attachmentUrl: "<<QRcode>>"      
          headerText: "Upload Health Insurance"
          footerText: "Use your camera app on your phone to scan the QR code"
    transitions:
      next: confirmUpload

  confirmUpload:
    component: "System.CommonResponse"
    properties:
      processUserMessage: true
      metadata:
        responseItems:        
        - type: "text" 
          text: "Have you uploaded the insurance card?"
          footerText:
          actions:
          - label: "Yes"
            type: "postback"
            keyword: "Y"
            payload:
              action: "Yes" 
          - label: "No"
            type: "postback"
            keyword: "N"
            payload:
              action: "No" 
    transitions:
      actions:
        Yes: "confirmSuccessUpload"
        No: "uploadLater"
        textReceived: "intent"

  confirmSuccessUpload: 
    component: "System.CommonResponse"
    properties:
      metadata:
        responseItems:
          - type: "text"
            text: "You are all set! Thank you and have a great day!"
    transitions:
      return: "done"
      
      
  uploadLater: 
    component: "System.CommonResponse"
    properties:
      metadata:
        responseItems:
          - type: "text"
            text: "We will send you a link to the email shortly! Please upload the insurance card in 2-3 business days."
    transitions:
      next: "exitFlow"  
</copy>
```


## Task 5: Create a Web Channel

In this task, we will configure and publish the ODA through a web channel. 

- Click on the *Navigation menu* on the top left and select *Channels* under *Development*. 
- Now create a channel with the following properties: 
  Name: CareClinics_WebChannel
  Description: Web channel for Care Clinics
  Channel Type: Oracle Web
  Allowed Domains: *
  Client Authentication Enabled: False

 ![](images/5-webchannel.png)

- After creating the channel, we need to route our channel to the skill we have been working on and enable the channel.

  ![](images/5-channel.png)

- Copy the *Channel Id* in a *Notepad*. 

*Note:* We will use this in our next lab to deploy the chat widget on the Content Management Portal.

*Test your Skill*

Congratulations! You have successfully completed this lab.

## Homework: Create a Custom Component

Go ahead and create a custom component to send out an email with the VBCS url using the Oracle Digital Assistant if the Patient chooses to upload the insurance card later.

Hint: You can go ahead use your gmail smtp server to send out an email 

