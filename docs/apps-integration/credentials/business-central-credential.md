---
title: "Dynamics 365 Business Central"
slug : /credentials/dynamics-365-business-central-credential
---

Welcome to the Dynamics 365 Business Central credential setup guide!
  
This guide will walk you through connecting your Business Central account to our platform.

By the end of this guide, you'll be able to securely connect your Dynamics 365 BC environment and begin syncing data and automating processes.


---

## Required Fields

You’ll need to provide:

| Field           | Description                                      |
|----------------|--------------------------------------------------|
| Connection Name | A name to identify the connection                |
| Tenant ID       | Your Azure Active Directory tenant ID            |
| Company Name    | The Business Central company you're working with |

---

## Step-by-Step Guide

### 1. Add Connection Name

- Enter a user-friendly name to identify this connection (e.g., `BC Finance`, `D365 Europe Instance`).
- This is only for reference within our platform.

---

### 2. Locate Your Tenant ID

1. Go to the [Azure Portal](https://portal.azure.com).
<img src="/img/credentials/business-central-cred-azure-dashboard.png" alt="APPSeAI Business Central Azure Dashboard" width="700"/>


2. Search for **Azure Active Directory** → **Overview**.
<img src="/img/credentials/business-central-cred-tenant-id.png" alt="APPSeAI Business Central Tenant ID" width="700"/>


3. Copy the **Tenant ID** from the overview page.

> **Example**: `e3f75f41-xxxx-4a70-9b5c-xxxxxxxxxxxx`

---

### 3. Find Your Company Name

1. Log in to your Business Central account.
2. Navigate to **Settings (⚙️)** → **My Settings**.
<img src="/img/credentials/business-central-cred-companyname.png" alt="APPSeAI Business Central Company Name" width="700"/>

3. Locate the value under **Company**.
<img src="/img/credentials/business-central-cred-settings.png" alt="APPSeAI Business Central Settings" width="700"/>


> **Example**: `CRONUS USA, Inc.`

---

### 4. Log in to your Business Central Account

1. You will be showcased a pop-up that prompts you to login to your Business Central account using your Microsoft account credentials.

<img src="/img/credentials/business-central-cred-microsoft-login.png" alt="APPSeAI Business Central Microsoft Login" width="700"/>


2. If you followed all the steps correctly, your Business Central credential should be connected to our platform.

---

## Save Your Credential

Once you've filled in the necessary fields, click **"Save"** to store and verify your setup.

- If successful, your Pipedrive credential will show a "✓" icon. Now you can use this application for your integrations.
- If it fails, you will be displayed a "!" icon. In that case, please recheck your API Key and Domain or contact support.

---

## Need Help?

If you’re unsure about any field or face connection issues, reach out to our support team at support@appseai.com.

---