---
title: Apollo
description: Step-by-step guide to set up Apollo credentials for Appse.ai integration
slug: /app-integrations/apollo/
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

## Introduction

Apollo is a sales intelligence platform used to find prospects, enrich contact data, and support outreach workflows. This guide explains how to configure Apollo credentials in Appse.ai so the platform can securely communicate with the Apollo API.

## Required Fields

You’ll be asked to fill in the following required fields when setting up Apollo credentials in Appse.ai:

| Field           | Description |
|-----------------|-------------|
| Connection Name | A name to help you identify this Apollo connection in Appse.ai |
| API Key         | Your Apollo API key used to authenticate API requests |

## Authentication Methods

<Tabs>

<TabItem value="apollo-apikey" label="API Key">

#### Step 1: Add Connection Name

- Click on **Select a credential**.
- Choose **Create new credential**.
- Enter a **Connection Name** that helps you recognize this Apollo connection later.

<img src="/img/credentials/apollo/connection-name.png" alt="Enter connection name for Apollo credential" width="600"/>

#### Step 2: Enter API Key

- In the **API Key** field, paste your Apollo API key.
- This key will be used to authenticate all requests sent from Appse.ai to Apollo.

<img src="/img/credentials/apollo/api-key.png" alt="Enter Apollo API key in credential form" width="600"/>

#### Step 3: Review Base Configuration

- The **Base Url**, **API Key Name**, and **Key Addto** fields are preconfigured.
- These fields are automatically managed by Appse.ai and cannot be edited.

<img src="/img/credentials/apollo/base-configuration.png" alt="Preconfigured and hidden Apollo credential fields" width="600"/>

### Save Your Credential

- Click **Save** to store the credential.
- Appse.ai will validate the API key using the configured validation endpoint.
- If validation succeeds, the credential will be saved and available for use in workflows.
- If validation fails, recheck the API key and try again.

</TabItem>

</Tabs>

## Support

Need help? Contact our support team at hello@appse.ai
 