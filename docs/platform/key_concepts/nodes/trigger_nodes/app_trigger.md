---
slug: /platform/key-concepts/nodes/trigger/app-trigger
title: App Trigger
position: 2
description: Starts a workflow based on an event occurring within a specified application.
---
# App Trigger

An App Trigger automatically executes a workflow when a specific event happens in a connected app. It continuously monitors the app for the defined action, and when that action occurs on the application, the workflow is automatically triggered.

## Why Use App Trigger?

The App Trigger helps automate workflows that respond instantly to events happening in connected applications. It eliminates the need for manual execution or complex scheduling, allowing real-time automation.

## Select App Trigger

1. ### Select any app

   Select any app from the selection screen  
  
  <img src="\img\platform\key-concepts\nodes\trigger-nodes\select-any-app.png" alt="select any app screen" width="700"/>   

2. ### Credential screen

   After selecting an app, the credential screen will appear, where you can select your credential  
     
<img src="\img\platform\key-concepts\nodes\trigger-nodes\credential-screen.png" alt="credential screen" width="700"/>
   

3. ### Select a trigger action event

   Choose one of the **trigger action events** from the **Action Event** dropdown.  
   **Note:** App triggers are usually listed at the **end of the dropdown** and can be identified by a **trigger icon** displayed beside the action event, as shown in the image below.  
   
<img src="\img\platform\key-concepts\nodes\trigger-nodes\select-a-trigger-action-event.png" alt="select a trigger action event screen" width="700"/>   

4. ### After selection

   After selecting the **trigger action event**, you can continue to configure the App trigger  
   
<img src="\img\platform\key-concepts\nodes\trigger-nodes\after-selection.png" alt="after selection screen" width="700"/>   

5. ### Configure 

   In an App Trigger, you’ll see these two fields. Fill them out based on the requirements of your selected trigger action event.  

   - **Fetch Data Since –** This field lets you set the starting date and time from which data should be fetched. It’s used to pull records that were created or updated after the specified date.  

> Note: You can set this only once; changing it later won’t affect the workflow execution.

   - **Record Limit –** This defines the maximum number of records to be fetched in one execution. You can set a value between 1 and 50, depending on how much data you want to retrieve at once.  
   
<img src="\img\platform\key-concepts\nodes\trigger-nodes\configure-fields.png" alt="configure fields screen" width="700"/>
