---
title: Gmail
description: Step-by-step guide to set up Gmail credentials for Appse.ai integration
slug: /app-integrations/gmail/
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Introduction

Gmail is Google’s email service that allows users to send, receive, search, and manage emails efficiently. By integrating Gmail with Appse.ai, you can automate email-based workflows such as sending notifications, reading inbox messages, monitoring threads, and triggering actions based on email events. This guide explains how to configure **Gmail OAuth 2.0 credentials** so Appse.ai can securely connect to your Gmail account.

---

## Key Features

- **Send Emails**: Automatically send emails using Gmail.
- **Read Inbox Messages**: Fetch incoming emails and threads.
- **Search Emails**: Query emails using Gmail search operators.
- **Attachment Handling**: Download and upload email attachments.
- **Workflow Automation**: Trigger workflows based on email activity.
- **Secure OAuth Access**: Uses Google OAuth 2.0 for safe authentication.

---

## Setup Credential

Follow the steps below to configure Gmail credentials in Appse.ai.

### Required Fields

The following fields are required to connect Gmail with Appse.ai.

| Field             | Description                                             |
| ----------------- | ------------------------------------------------------- |
| Authorization URL | Google OAuth authorization endpoint                     |
| Token URL         | Google OAuth token endpoint                             |
| Client ID         | OAuth Client ID generated from Google Cloud Console     |
| Client Secret     | OAuth Client Secret generated from Google Cloud Console |
| API Access Scope  | Gmail API scopes required for email access              |
| Base API URL      | Gmail API base endpoint                                 |

:::info
All required fields must be configured correctly to successfully authorize Gmail with Appse.ai.
:::

---

## Step-by-Step Guide

# Gmail Credential Setup Guide

## Step 1: Open the Gmail Credential Form

1. Login to the **appse ai** portal  
2. Click on the **Credentials** option from the Sidebar menu  
3. Click **Add Credentials**  
4. Select **Gmail App** from the App list  
5. Gmail credential form will be displayed  
6. **Note** the `Callback API URL` — you will need this later  

---

## Step 2: Create a Google Cloud Project

1. Go to the [Google Cloud Console](https://console.cloud.google.com/)  
   Accept the Terms and Conditions if prompted
   <img src="/img/credentials/gmail/gm1.png" width="700"/>
2. Click on **Select a project** (top-left) if no project is currently selected  
   <img src="/img/credentials/gmail/gm2.png" width="700"/>
3. Click **New Project**  
   <img src="/img/credentials/gmail/gm3.png" width="700"/>
4. Enter:
   - **Project Name**
   - **Parent resource** (Optional)
   <img src="/img/credentials/gmail/gm4.png" width="700"/>
5. Click on **Create**  
   <img src="/img/credentials/gmail/gm5.png" width="700"/>

---

<a id="navigate-to-apis-services"></a>

## Step 3: Navigate to APIs & Services section in Google Cloud Console

1. In the Google Cloud Console header, click the **Google Cloud** text/logo (top-left).
   <img src="\img\credentials\gmail\gm6.png" width="700"/>
2. From the **Quick access** panel, click **APIs & Services**.
   <img src="\img\credentials\gmail\gm7.png" width="700"/>
3. You will now be on the **APIs & Services** dashboard.

---

## Step 4: Enable Required APIs

### Enable Gmail API

1. Go to **[APIs & Services](#navigate-to-apis-services)** → **Enable APIs and services** 
   <img src="/img/credentials/gmail/gm8.png" width="700"/>
2. Search for **Gmail API**  
3. Select **Gmail API**
   <img src="/img/credentials/gmail/gm9.png" width="700"/>
4. Click **Enable**  
   <img src="/img/credentials/gmail/gm10.png" width="700"/>

---

## Step 5: Configure OAuth Consent Screen

1. Go to **[APIs & Services](#navigate-to-apis-services) → OAuth consent screen**  
   <img src="/img/credentials/gmail/gm11.png" width="700"/>
2. Click **Get started**  
   <img src="/img/credentials/gmail/gm12.png" width="700"/>

---

### Step 5.1: App Information

Fill in:

- **App name**
- **User support email**

- Click **Next**

<img src="/img/credentials/gmail/gm13.png" width="700"/>

---

### Step 5.2: Audience

Select **External** when:

- Your application is intended for **multiple users or customers**
- Users **outside your organization/domain** need access
- You are building a **public integration or SaaS product**
- You want to allow **any Google account** to authorize (with proper permissions)

Select **Internal** when:

- The application is used **only within your organization**
- All users belong to the **same Google Workspace domain**
- You do **not need external users** to access the integration

Click **Next**

<img src="/img/credentials/gmail/gm14.png" width="700"/>

> Selecting External allows any Google account to authorize the Gmail integration.

---

### Step 5.3: Contact Information

- Enter **Contact email**
- Click **Next**

<img src="/img/credentials/gmail/gm15.png" width="700"/>

---

### Step 5.4: Finish Setup

- Accept **Google API Services: User Data Policy**  
- Click **Continue**

<img src="/img/credentials/gmail/gm16.png" width="700"/>

- Click on **Create**
<img src="/img/credentials/gmail/gm17.png" width="700"/>

---

## Step 6: Add Test Users

1. Go to **[APIs & Services](#navigate-to-apis-services) → OAuth consent screen**  
2. Open the **Audience** section  
   <img src="/img/credentials/gmail/gm18.png" width="700"/>
3. Under **Test users**, click **Add users**  
   <img src="/img/credentials/gmail/gm19.png" width="700"/>
4. Add one or more Gmail addresses.
5. Click **Save**

<img src="/img/credentials/gmail/gm20.png" width="700"/>

> Only added users can authorize the credential.

---

## Step 7: Configure OAuth Scopes

1. Go to **[APIs & Services](#navigate-to-apis-services) → OAuth consent screen**  
2. Open **Data Access**  
   <img src="/img/credentials/gmail/gm21.png" width="700"/>
3. Click **Add or remove scopes**  
   <img src="/img/credentials/gmail/gm22.png" width="700"/>

### Search and Add the following scopes:

- https://mail.google.com/ 
   <img src="/img/credentials/gmail/gm23.png" width="700"/>

- https://www.googleapis.com/auth/gmail.modify 
   <img src="/img/credentials/gmail/gm24.png" width="700"/>

- https://www.googleapis.com/auth/gmail.readonly 
   <img src="/img/credentials/gmail/gm25.png" width="700"/>

- https://www.googleapis.com/auth/gmail.send
   <img src="/img/credentials/gmail/gm26.png" width="700"/>

> **Note:** These scopes are required for reading, sending, and modifying emails.

4. Click **Update**  
   <img src="/img/credentials/gmail/gm27.png" width="700"/>

5. Click **Save** after confirming that the selected scopes are correct.
   <img src="/img/credentials/gmail/gm28.png" width="700"/>

---

## Step 8: Create OAuth Client ID & Secret

1. Go to **[APIs & Services](#navigate-to-apis-services) → Credentials**  
   <img src="/img/credentials/gmail/gm29.png" width="700"/>
2. Click **Create Credentials → OAuth client ID**  
   <img src="/img/credentials/gmail/gm30.png" width="700"/>

### Application Type

- Select **Web application**  
- Add **Name**

<img src="/img/credentials/gmail/gm31.png" width="700"/>

### Authorized Redirect URI

- Add the **Callback API URL**  
- The Callback API URL must exactly match the value displayed on the Gmail Credential page in the APPSe AI portal. Refer to the image below for the Callback URL.

<img src="/img/credentials/gmail/gm32.png" width="700"/>

3. Click **Create**
   <img src="/img/credentials/gmail/gm33.png" width="700"/>

---

## Step 9: Credential Generation

After creation, you will get:

- **Client ID**
- **Client Secret**

<img src="/img/credentials/gmail/gm34.png" width="700"/>

- Copy and store them securely  
- You can also download the JSON file  

<img src="/img/credentials/gmail/gm35.png" width="700"/>

---

## Step 10: Add Credential in APPSe ai

1. Go back to the Gmail credential form in APPSe AI platform.
2. Enter:
   - **Connection Name**
   - **Client ID**
   - **Client Secret**
   - Keep the **API Access Scope** unchanged.
3. Click **Save & Authorize**
4. After clicking Save & Authorize, a Gmail popup will open.

<img src="/img/credentials/gmail/gm36.png" width="700"/>

---

## Step 11: Authorize Gmail Access

1. Select your Gmail account  
   <img src="/img/credentials/gmail/gm37.png" width="700"/>
2. Click **Continue**  
   <img src="/img/credentials/gmail/gm38.png" width="700"/>
3. Select all the required checkbox
4. Click **Continue**  
   <img src="/img/credentials/gmail/gm39.png" width="700"/>

---

## Step 12: Verify Credential

- Ensure the credential shows **Successfully Validated**

<img src="/img/credentials/gmail/gm40.png" width="700"/>

---

## ✅ Notes

- Gmail API must be enabled  
- OAuth scopes must be configured correctly  
- Callback URL must match exactly  
- Only test users can authenticate in testing mode  
If the configuration is correct, Appse.ai will complete authorization and securely store the credential.

---

## Common Gmail OAuth URLs

| Type              | URL                                          |
| ----------------- | -------------------------------------------- |
| Authorization URL | https://accounts.google.com/o/oauth2/v2/auth |
| Token URL         | https://oauth2.googleapis.com/token          |
| Base API URL      | https://gmail.googleapis.com                 |

---

## Support

Need help? Contact our support team at hello@appse.ai

---
