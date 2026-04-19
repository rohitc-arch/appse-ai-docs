---
title: "SAP Business One"
slug : /app-integrations/sap-b1
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

SAP Business One (SAP B1) is an integrated enterprise resource planning (ERP) solution designed for small and medium-sized businesses. With appse ai, you can seamlessly connect SAP B1 to your workflows, automating processes like inventory management, financial reporting, and customer relationship management to improve business performance and agility.

---

## Setup Credential

Follow the steps below to quickly set up your credential.

### Required Fields

You will be asked to fill in the following details:

| Field       | Description                                  |
|-------------|----------------------------------------------|
| Host URL    | The server URL where your SAP B1 is hosted   |
| Port        | The port number for the SAP B1 service layer |
| Username    | Your SAP B1 username                         |
| Password    | Your SAP B1 password                         |
| Company DB  | The company database name used in SAP B1     |

### Step-by-Step Guide

#### 1. Add Connection Name

Provide a name for your credential in the `Connection Name` field. This will be showcased in the credential listing page.

#### 2. Find Your Host URL and Port

- Open the SAP Business One **Service Layer** configuration or ask your SAP B1 administrator.
   - It will look something like: `https://{localip}:50000/ControlCenter/`
   - You should see page titled - `System Landscape Directory`

- Login to the platform using your **System Landscape Directory Credentials**.
<img src="/img/credentials/sap-b1/sap-b1-cred-sld-login.png" alt="APPSeAI SAP Business One Credentials System Landscape Directory Login" />

- Locate the base URL used to access the Service Layer API. Go to _Services_ â†’ _Service Layer_
<img src="/img/credentials/sap-b1/sap-b1-cred-host-url.png" alt="APPSeAI SAP Business One Credentials Url and Port" />

- Add your Host URL and Port. With respect to the image you will be adding:
> - **Host URL**: `https://10.0.2.68`
> - **Port**: `50000`

#### 3. Find Your Company DB Name

- In the same **System Landscape Directory**
- Go to _DB Instances and Companies_ â†’ Click on Your Server Name
<img src="/img/credentials/sap-b1/sap-b1-cred-db-name.png" alt="APPSeAI SAP Business One Credentials DB Instances and Companies" />

Copy the **Schema Name**, this is your `Database Name`

<img src="/img/credentials/sap-b1/sap-b1-cred-db-name2.png" alt="APPSeAI SAP Business One Credentials Database Name" />

> **Note**: Depending on your setup, you might see `https://insync.pro` instead of `https://10.0.2.68`. Either can be used as your Host URL input.

#### 4. Get Your Username and Password
<img src="/img/credentials/sap-b1/sap-b1-credentials.png" alt="APPSeAI SAP Business One Credentials" width="602" height="306" />

- Use your **SAP B1 client login credentials**.
- Make sure the user has sufficient API permissions for integration.

### Save Your Credential

Once you've filled in the necessary fields, click **"Save"** to store and verify your setup.

- If successful, your SAP B1 credential will show a "✓" icon. Now you can use this application for your integrations.
- If it fails, you will be displayed a "!" icon. In that case, please recheck your API Key and Domain or contact support.

---

## Triggers and Actions

Every application has a pre-defined set of triggers and actions that allow users to perform application specific activities within the platform. Here is a list of all the actions and triggers available:

<Tabs>
<TabItem value="triggers" label="Trigger">

### Triggers

### New Items Created

The **New Item Created** trigger starts the workflow automatically when a new item is created in SAP Business One.  
It captures the item details and passes them to the next step for further processing.

> **Note:** This is a trigger node, so it does not take any input data.

-----

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

-------

#### Example Configuration
   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

----------------

#### Result
```json
[
  {
    "ItemCode": "ITM-1001",
    "ItemName": "Sample Item",
    "CreateDate": "2026-03-27",
    "UpdateDate": "2026-03-27",
    "InventoryItem": "tYES",
    "Valid": "tYES"
  }
]
```
   


-------

### Items updated

The **Items Updated Trigger** initiates a workflow whenever existing item details are modified in the SAP Business One. It captures the updated item information and passes it as structured data.

This trigger is commonly used to **sync inventory changes**, **update product catalogs**.

> **Note:** The trigger executes only after the item update is successfully saved. All relevant details (such as item ID, updated fields, and timestamps) are included in the output payload.

------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

-------

#### Example Configuration
   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

--------------

#### Result
```json
[
  {
    "ItemCode": "ITM-1001",
    "ItemName": "Sample Item - Updated",
    "UpdateDate": "2026-03-27",
    "UpdatedFields": [
      "ItemName",
      "Price",
      "WarehouseCode"
    ]
  }
]
```

------

### New Order Created

The **New Order Created Trigger** initiates a workflow whenever a new order is successfully created in the SAP Business One. It automatically captures order details and passes them as structured data to subsequent steps in the workflow.

This trigger is commonly used to **automate order processing**, **send notifications**, **update records**, or **initiate downstream actions** based on new order events.

> **Note:** The trigger executes only after the order is fully created and confirmed in the system. All relevant order fields (such as order ID, customer details, and items) are included in the output payload.

--------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

--------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

------------

#### Result
```json
[
  {
    "DocEntry": 11464,
    "DocNum": 503,
    "CardCode": "BC6129916",
    "DocDate": "2026-03-27",
    "DocumentLines": [
      {
        "ItemCode": "BCB2B0001",
        "Quantity": 5
      }
    ]
  }
]
```

-------

### New Quotation Created

The **New Quotation Created Trigger** initiates a workflow whenever a new quotation is generated in the SAP Business One. It captures quotation details and passes them as structured data to subsequent steps in the workflow.

This trigger is commonly used to **automate quotation processing**, **track sales opportunities**, or **trigger approval workflows**.

> **Note:** The trigger executes only after the quotation is successfully created. All relevant quotation details (such as quotation ID, customer information, pricing, and items) are included in the output payload.

------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuration
   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

--------------

#### Result
```json
[
  {
    "DocEntry": 503,
    "DocNum": 221,
    "CardCode": "BC6129916",
    "DocDate": "2026-03-27",
    "NumAtCard": "REF-145",
    "DocumentLines": [
      {
        "ItemCode": "BCB2B0001",
        "Quantity": 3,
        "UnitPrice": 100
      }
    ]
  }
]
```

-------

### New Business Partner Created

The **New Business Partner Created Trigger** initiates a workflow whenever a new business partner is added to the SAP Business One. It captures partner details and passes them as structured data to subsequent workflow steps.

This trigger is commonly used to **automate onboarding processes**.

> **Note:** The trigger executes only after the business partner is successfully created. All relevant details (such as partner ID, name, contact information, and address) are included in the output payload.

-------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

--------------

#### Result
```json
[
  {
    "CardCode": "BP-001",
    "CardName": "Joe Mark",
    "Phone1": "9XXXXXXXXX",
    "EmailAddress": "example@domain.com",
    "CardType": "cCustomer"
  }
]
```

### Business partners updated

The **Business Partners Updated Trigger** initiates a workflow whenever existing business partner details are modified in the SAP Business One. It captures the updated information and passes it as structured data to subsequent workflow steps.

This trigger is commonly used to **sync partner data across systems**, or **trigger validation processes**.

> **Note:** The trigger executes only after the business partner update is successfully saved. All relevant details (such as partner ID, modified fields, contact information, and timestamps) are included in the output payload.

-----

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg " width="700" />

Click on **Continue** , then **Run** the node.

------------------

#### Result

```json
[
  {
    "CardCode": "BP-001",
    "CardName": "Joe Mark Updated",
    "Phone1": "9XXXXXXXXX",
    "EmailAddress": "example@domain.com",
    "UpdateDate": "2026-03-27"
  }
]
```

--------

### New AR Invoices created

The **New AR Invoices Created Trigger** initiates a workflow whenever a new Accounts Receivable (AR) invoice is created in the SAP Business One. It captures invoice details and passes them as structured data to subsequent workflow steps.

This trigger is commonly used to **automate invoice processing**, **send payment notifications**, **update financial records**, or **trigger accounting workflows**.

> **Note:** The trigger executes only after the AR invoice is successfully created. All relevant invoice details (such as invoice ID, customer information, amount, due date, and line items) are included in the output payload.

--------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

------------

#### Result
```json
[
  {
    "DocEntry": 11462,
    "DocNum": 715,
    "CardCode": "BC6129916",
    "DocTotal": 3500,
    "DocDueDate": "2026-03-27"
  }
]
```

-------

### New Credit Note Created

The **New Credit Note Created Trigger** initiates a workflow whenever a new credit note is generated in the SAP Business One. It captures credit note details and passes them as structured data to subsequent workflow steps.

This trigger is commonly used to **automate refund processing**, **adjust customer balances**, **notify stakeholders**, or **update financial records**.

> **Note:** The trigger executes only after the credit note is successfully created. All relevant details (such as credit note ID, customer information, amount, and related invoice details) are included in the output payload.

-------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

------------

#### Result
```json
[
  {
    "DocEntry": 188,
    "DocNum": 91,
    "CardCode": "BC6129916",
    "DocTotal": 500,
    "BaseType": 13
  }
]
```

---------

### New deliverynotes Created

The **New Delivery Notes Created Trigger** initiates a workflow whenever a new delivery note is created in the SAP Business One. It captures delivery details and passes them as structured data to subsequent workflow steps.

This trigger is commonly used to **track shipments**, **update order status**, **notify customers**, or **trigger logistics and fulfillment processes**.

> **Note:** The trigger executes only after the delivery note is successfully created. All relevant details (such as delivery note ID, customer information, shipment details, and items) are included in the output payload.

-------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuation

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

-------------

#### Result
```json
[
  {
    "DocEntry": 151,
    "DocNum": 65,
    "CardCode": "ZC0001",
    "DocDate": "2026-03-27",
    "DocumentLines": [
      {
        "ItemCode": "DIET002",
        "Quantity": 10
      }
    ]
  }
]
```

--------

### New incoming payments created

The **New Incoming Payments Created Trigger** initiates a workflow whenever a new incoming payment is recorded in the SAP Business One. It captures payment details and passes them as structured data to subsequent workflow steps.

This trigger is commonly used to **update payment status**, **reconcile invoices**, **notify stakeholders**, or **trigger accounting and financial workflows**.

> **Note:** The trigger executes only after the incoming payment is successfully created. All relevant details (such as payment ID, customer information, amount, payment method, and associated invoices) are included in the output payload.

-------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

------------

#### Result
```json
[
  {
    "DocEntry": 522,
    "DocNum": 301,
    "CardCode": "ZC0001",
    "PaymentMeans": "IncomingPayment",
    "DocTotal": 500
  }
]
```

---------

### New service calls created

The **New Service Calls Created Trigger** initiates a workflow whenever a new service call is logged in the SAP Business One. It captures service request details and passes them as structured data to subsequent workflow steps.

This trigger is commonly used to **automate support workflows**, **assign tickets to agents**, **notify teams**, or **track service requests and resolutions**.

> **Note:** The trigger executes only after the service call is successfully created. All relevant details (such as service call ID, customer information, issue description, and priority) are included in the output payload.

-------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

---------

#### Result
```json
[
  {
    "ServiceCallID": 1024,
    "CustomerCode": "CUST-001",
    "Subject": "System Installation Issue",
    "Status": "Open",
    "Priority": "High"
  }
]
```

--------------

### New returs created

The **New Returns Created Trigger** initiates a workflow whenever a new return request is created in the SAP Business One. It captures return details and passes them as structured data to subsequent workflow steps.

This trigger is commonly used to **manage return processes**, **update inventory**, **initiate refunds or replacements**, or **notify relevant teams**.

> **Note:** The trigger executes only after the return is successfully created. All relevant details (such as return ID, customer information, returned items, and reason for return) are included in the output payload.

-------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

------------

#### Result
```json
[
  {
    "DocEntry": 205,
    "DocNum": 88,
    "CardCode": "ZC0001",
    "Comments": "Damaged item returned",
    "DocumentLines": [
      {
        "ItemCode": "DIET001",
        "Quantity": 1
      }
    ]
  }
]
```

---------------

### New activities created

The **New Activities Created Trigger** initiates a workflow whenever a new activity is logged in the SAP Business One. It captures activity details and passes them as structured data to subsequent workflow steps.

This trigger is commonly used to **track user actions**, **log interactions**, **notify stakeholders**, or **trigger follow-up tasks and workflows**.

> **Note:** The trigger executes only after the activity is successfully created. All relevant details (such as activity ID, type, associated entity, and timestamps) are included in the output payload.

--------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Fetch data since | Select the date and time to fetch newly created items from that point onward . (e.g., 27/03/2026 06:51) |
| Limit | Set the maximum number of items to retrieve per run. (e.g., 10) |

---------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP_Trigger Configure.jpg" width="700" />

Click on **Continue** , then **Run** the node.

--------------

#### Result
```json
[
  {
    "ActivityCode": 9001,
    "ActivityType": "Task",
    "Subject": "Follow-up call",
    "CreateDate": "2026-03-27",
    "AssignedTo": "Sales Team"
  }
]
```

</TabItem>
<TabItem value="actions" label="Action" default>

## Actions

The **Actions** component represents a set of operations that are executed within a workflow after a trigger or condition is met. Actions perform specific tasks by processing input data and producing outputs that can be used in subsequent steps.

Actions are commonly used to **create, update, retrieve, or delete records**, **send notifications**, **integrate with external systems**, or **transform data** within workflows.

> **Note:** Each action requires proper configuration of inputs and may produce output data that can be referenced in later steps of the workflow.

----
## BusinessPartners Actions

### Get a BusinessPartner by EmailAddress

The **Get a Business Partner by Email Address** action retrieves the details of a business partner using their email address as the search criteria. It returns the matching record as a structured object.

This action is commonly used to **lookup partner information**, **validate existing records**, **avoid duplicates**, or **fetch customer/vendor details** in workflows.

> **Note:** If multiple records match the provided email address, the system may return the first matching result or a list of records based on configuration. If no match is found, the output will be empty or null.

-------

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GBPbyEM44.jpg" width="700" />

Click on **Continue** button.

------------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Email Address | Enter the email address of the business partner to search for. This field is used as the primary identifier to fetch the corresponding record. |

Click on **Continue**, then **Run** the node.

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP-AC-GETBPbyEmail14.jpg" width="700" />

-------------

#### Result
```json
[
  {
    "CardCode": "BC6129916",
    "CardName": "MAX6",
    "EmailAddress": "example@domain.com",
    "Phone1": "9XXXXXXXXX"
  }
]
```

----------------

### Get CardCode by ContactEmployee email

The **Get a Business Partner by Email Address** action retrieves the details of a business partner using their email address as the search criteria. It returns the matching record as a structured object.

This action is commonly used to **lookup partner information**, **validate existing records**, **avoid duplicates**, or **fetch customer/vendor details** in workflows.

> **Note:** If multiple records match the provided email address, the system may return the first matching result or a list of records based on configuration. If no match is found, the output will be empty or null.

------

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GCCbyCEmp45.jpg" width="700" />

Click on **Continue** button.

----------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Email | Enter the email address of the business partner to search for. This field is used as the primary identifier to fetch the corresponding record (e.g., "example@domain.com"). |

Click on **Continue**, then **Run** the node.

-------

#### Example Configuration
   <img src="/img/credentials/sap-b1/SAP-AC-GET CC by CE email16.jpg" width="700" />

-----------------

#### Result
```json
[
  {
    "CardCode": "BC6129916",
    "ContactEmployee": {
      "Name": "CTP-002",
      "EmailAddress": "example@domain.com"
    }
  }
]
```

-----------

### Create New BusinessPartner

The **Create New Business Partner with CardCode** action creates a new business partner in the system using a unique CardCode. It allows you to configure mandatory and optional details, which are then stored and passed as structured data for further workflow steps.
This action is commonly used to **onboard new customers or vendors**, **store contact and address information**, and **enable downstream business processes**.

> **Note:** CardCode must be unique. Optional fields can be configured based on business requirements, and missing optional values will not block the creation process.

------

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-CNBP46.jpg" width="700" />

Click on **Continue** button.

-------------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| CardCode | Enter a unique identifier for the business partner (e.g., "BP-001"). |

#### Optional Fields

#### 1. Customer Details

| Field          | Description |
|---------------|------------|
| Customer Name | Enter Required Customer Name (e.g., "Joe Mark") |
| Phone1 | Enter Required Phone Number (e.g., "9XXXXXXXXX") |
| Email Address | Enter Required Mobile Number (e.g., "example@domain.com")|

#### 2. BP Addresses

| Field          | Description |
|---------------|------------|
| Address Name | Enter Address Name (e.g., "ADD 001" )|
| Address Type | Select either **Ship To** or **Bill To** |
| Optional Address Fields  
Street  
Block or Sector  
Zip Code  
City  
Country  
State | Enter Required Address details |

#### 3. Contact Employees

| Field          | Description |
|---------------|------------|
| Name | (e.g., "CTP-002")|
| Optional Contact Fields  
First Name  
Last Name  
Phone1  
Email Address  
Job Title  
Position | Enter Required Contact details |

Click on **Continue**, then **Run** the node.

-----------------

#### Configuration

   <img src="/img/credentials/sap-b1/SAP-AC-CNBPD19.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-NBPD20.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-NBPD21.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-NBPD22.jpg" width="700" />

-----------

#### Result
```json
[
  {
    "CardCode": "BP-001",
    "CardName": "Joe Mark",
    "Phone1": "9XXXXXXXXX",
    "EmailAddress": "example@domain.com",
    "BPAddresses": [
      {
        "AddressName": "ADD 001",
        "AddressType": "bo_ShipTo"
      }
    ],
    "ContactEmployees": [
      {
        "Name": "CTP-002",
        "Position": "Manager"
      }
    ]
  }
]
```

-----------------

### Create a new businesspartner witout CardCode

The **Create New Business Partner (Without CardCode)** action creates a new business partner in the system without requiring a CardCode. The system automatically generates a unique CardCode upon successful creation.

This action is commonly used to **quickly create business partners**, **reduce manual effort in assigning IDs**, and **support automated onboarding workflows**.

> **Note:** The CardCode is auto-generated by the system. Optional fields can be configured as needed, and leaving them empty will not prevent the creation of the business partner.

#### Select the Credential and Action Event

   <img src="/img/credentials/sap-b1/SAP-C-CNBWOUTCC24.jpg" width="700" />

Click on **Continue** button.

#### Configuration Fields

#### 1. Customer Name

| Field          | Description |
|---------------|------------|
| Customer Name | Enter Required Customer Name (e.g., "Joe Mark") |

#### Optional Field
| Field          | Description |
|---------------|------------|
| Phone1 | Enter Required Phone Number (e.g., "9XXXXXXXXX") |
| Email Address | Enter Required Mobile Number (e.g., "example@domain.com")|

#### 2. BP Addresses

| Field          | Description |
|---------------|------------|
| Address Name | Enter Address Name (e.g., "ADD 001" )|
| Address Type | Select either **Ship To** or **Bill To** |
| Optional Address Fields  
Street  
Block or Sector  
Zip Code  
City  
Country  
State | Enter Required Address details |

#### 3. Contact Employees

| Field          | Description |
|---------------|------------|
| Name | (e.g., "CTP-002")|
| Optional Contact Fields  
First Name  
Last Name  
Phone1  
Email Address  
Job Title  
Position | Enter Required Contact details |

Click on **Continue**, then **Run** the node.

---------------

#### Configuration

   <img src="/img/credentials/sap-b1/SAP-AC-CNBPWOUTCC25.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-CNBPWOUTCC26.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-CNBPWOUTCC27.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-NBPWOUTCC28.jpg" width="700" />

--------------

#### Result
```json
[
  {
    "CardCode": "V10025",
    "CardName": "Joe Mark",
    "Phone1": "9XXXXXXXXX",
    "EmailAddress": "example@domain.com"
  }
]
```

-----------------

### Update a businesspartner

The **Update Business Partner** action modifies the details of an existing business partner in the system. It allows updating specific fields while retaining unchanged information.

This action is commonly used to **maintain accurate partner records**, **update contact and address information**, and **sync changes across systems**.

> **Note:** Only the fields provided in the configuration will be updated. Fields left empty will remain unchanged in the existing business partner record.

#### Select the Credential and Action Event

   <img src="/img/credentials/sap-b1/SAP-C-UBP29.jpg" width="700" />

Click on **Continue** button.

-----------------

#### Configuration Fields

#### 1. Customer Details

| Field          | Description |
|---------------|------------|
| Customer Name | Enter Required Customer Name (e.g., "Joe Mark") |
| Phone1 | Enter Required Phone Number (e.g., "9XXXXXXXXX") |
| Email Address | Enter Required Mobile Number (e.g., "example@domain.com")|

#### 2. BP Addresses

| Field          | Description |
|---------------|------------|
| Address Name | Enter Address Name (e.g., "ADD 001" )|
| Address Type | Select either **Ship To** or **Bill To** |
| Optional Address Fields  
Street  
Block or Sector  
Zip Code  
City  
Country  
State | Enter Required Address details |

#### 3. Contact Employees

| Field          | Description |
|---------------|------------|
| Name | (e.g., "CTP-002")|
| Optional Contact Fields <br/> First Name  <br/> Last Name  <br/> Phone1  <br/> Email Address  <br/> Job Title  <br/> Position  | Enter Required Contact details |

Click on **Continue**, then **Run** the node.

-----------------

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP-AC-UBP30.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-UBP31.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-UBP32.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-UBP33.jpg" width="700" />

-----------------

#### Result
```json
[
  {
    "CardCode": "BP-001",
    "CardName": "Joe Mark Updated",
    "Phone1": "9XXXXXXXXX",
    "EmailAddress": "example@domain.com",
    "ContactEmployees": [
      {
        "Name": "CTP-002",
        "JobTitle": "Sales Lead"
      }
    ]
  }
]
```

<img src="/img/credentials/sap-b1/SAP-AR-UBP34.jpg" width="700" />

---------


## Items Actions

### Get a Item by ItemCode

The **Get an Item by ItemCode** action retrieves the details of an item using its unique ItemCode. It returns the matching item record as a structured object.

This action is commonly used to **lookup item information**, **validate product records**, **fetch inventory details**, or **use item data in workflows**.

> **Note:** If the provided ItemCode does not exist, the output will be empty or null.

#### Select the Credential and Action Event

   <img src="/img/credentials/sap-b1/SAP-C-GIC35.jpg" width="700" />

Click on **Continue** button.

--------------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| ItemCode | Enter the unique identifier of the item to fetch its details. (e.g,. "AN005")|

Click on **Continue**, then **Run** the node.

#### Example Configuration

   <img src="/img/credentials/sap-b1/SAP-AC-GIC36.jpg" width="700" />

----------

#### Result
```json
[
  {
    "ItemCode": "AN005",
    "ItemName": "Demo Item",
    "InventoryItem": "tYES",
    "SalesItem": "tYES",
    "PurchaseItem": "tYES"
  }
]
```

-------------

### Create a New Item {#create-a-new-item}

The **Create New Item** action creates a new item in the system with the specified details. It captures item information and stores it as a structured record for use in workflows and inventory processes.

This action is commonly used to **add new products**, **manage inventory**, **update product catalogs**, and **support sales and procurement workflows**.

> **Note:** If ItemCode is not provided, the system may automatically generate one. Optional fields can be configured as needed without blocking item creation.

#### Select the Credential and Action Event

   <img src="/img/credentials/sap-b1/SAP-C-CNI38.jpg" width="700" />

Click on **Continue** button.

----------------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| Item Code | Unique identifier for the item. |
| Item Name | Enter the name of the item. |

#### Optional Fields â€“ Item Configuration

Below are the optional fields available while creating an item, along with short descriptions:

| Field          | Description |
|---------------|------------|
| Remarks | Additional notes or comments related to the item. (e.g., "High demand electronic accessory")|
| Item Prices | Defines pricing details for the item across different price lists. (e.g., "PriceList: 1 â†’ 500 INR, PriceList: 2 â†’ 550 INR")|
| Inventory Item | Indicates whether the item is managed in inventory. (e.g., "Yes or No")|
| InventoryUOM | itemâ€™s stock is tracked and managed in the inventory system (e.g., Nos, Kg, Liters).| 
| Location | Specifies the storage location of the item.(e.g., "Warehouse-1")|
|Item Group Code | Categorizes the item into a specific group. (e.g., "100")|
| Additional Identifier | Any extra reference ID for the item.|
| Purchase Item | Marks the item as available for purchasing. (e.g., "Yes or No")|
| Sales Item | Marks the item as available for sales. (e.g., "Yes or No")|
| Ship Type | Defines the shipping method applicable to the item. (e.g., "5, 6")|
| Tax Type | Specifies the tax category applicable to the item. (e.g., "tt_Yes")|
| Manage Stock by Warehouse | Enables stock tracking per warehouse. (e.g., "Yes or No")|
| WT Liable | Indicates if withholding tax is applicable. (e.g., "Yes or No")|
| BaseUnitName | Defines the base unit of measurement for the item. (e.g., "Nos")|
| ItemType | Specifies the type of item (e.g., product or service).(e.g., "Items, Labour, travel")|
| ServiceGroup | Groups service-type items under a category. (e.g., "-1")|
| ProductSource | Defines the origin/source of the product.(e.g., "Local")|
| BarCode | Unique barcode identifier for the item.(e.g., "null")|
| VatLiable | Indicates if VAT is applicable to the item.(e.g., "Yes or No")|

> **Note:** These fields are optional and can be configured based on business requirements.

Click on **Continue**, then **Run** the node.

#### Example configuration Fields

   <img src="/img/credentials/sap-b1/SAP-AC-NIC39.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-NIC40.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-NIC41.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-ACNIC42.jpg" width="700" />
   <img src="/img/credentials/sap-b1/SAP-AC-NIC43.jpg" width="700" />

#### Result
```json
[
  {
    "ItemCode": "ITM-1001",
    "ItemName": "Laptop Pro 15",
    "InventoryUOM": "Nos",
    "ItemGroupCode": 100,
    "SalesItem": "tYES",
    "PurchaseItem": "tYES",
    "VatLiable": "tYES"
  }
]
```

-----------------

### Update an Item {#update-a-item}

The **Update Item** action modifies the details of an existing item in the system using its ItemCode. It allows updating specific fields while keeping other data unchanged.

This action is commonly used to **maintain accurate product data**, **update pricing and availability**, and **sync item details across systems**.

> **Note:** Only the fields provided will be updated. Fields left empty will remain unchanged.

#### Select the Credential and Action Event

   <img src="/img/credentials/sap-b1/SAP-AC-CNBPD19.jpg" width="700" />

Click on **Continue** button.

------------

#### Configuration Fields

Below are the optional fields available while Updating an item, along with short descriptions:

| Field          | Description |
|---------------|------------|
| Item Code | Unique identifier of the item to be updated.(e.g.,"ITM-1001")

Below are the optional fields available while updating an item, along with short descriptions and examples:

| Field          | Description |
|---------------|------------|
| Item Name | Name of the item. (e.g., "Laptop Pro 15") |
| Remarks | Additional notes or comments related to the item. (e.g.,"Updated model with enhanced features") |
| Additional Identifier | Any extra reference ID for the item.(e.g., "ALT-56789") |
| Item Group Code | Categorizes the item into a specific group.  (e.g.,"Electronics") |
| Purchase Item | Marks the item as available for purchasing (True/False).  (e.g., "True") |
| Sales Item | Marks the item as available for sales (e.g., "True/False"). |
| Inventory Item | Indicates whether the item is managed in inventory (e.g., "True/False"). |
| Manufacturer | Specifies the manufacturer of the item. (e.g.,"HP") |
| Default Warehouse | Defines the default warehouse for the item. (e.g., "WH-01") |
| Item Price | Defines the price of the item. (e.g., "65000") |

> **Note:** Only the fields provided will be updated. Fields left empty will remain unchanged.

Click on **Continue**, then **Run** the node.

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-UI48.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-UI49.jpg" width="700" />

#### Result
```json
[
  {
    "ItemCode": "ITM-1001",
    "ItemName": "Laptop Pro 15",
    "Remarks": "Updated model with enhanced features",
    "ItemGroupCode": "Electronics",
    "DefaultWarehouse": "WH-01",
    "Price": 65000
  }
]
```

<img src="/img/credentials/sap-b1/SAP-AC-UI50.jpg" width="700" />

---------------


## Quotations Actions

### Get a quotation by customer reference no

The **Get a Quotation by Customer Reference Number** action retrieves quotation details using the customer reference number (`NumAtCard`). It returns the matching quotation record as a structured object.

This action is commonly used to **lookup quotation details**, **track customer-specific references**, **validate records**, or **fetch quotation data for further processing**.

> **Note:** If multiple quotations match the provided reference number, the system may return the first matching result or a list based on configuration. If no match is found, the output will be empty or null.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GETQTbyNumAtCard51.jpg" width="700" />

-------

#### Configuration Fields

| Field          | Description |
|---------------|------------|
| NumAtCard | Enter the customer reference number associated with the quotation. (e.g., "664111000000373064") |

Click on **Continue**, then **Run** the node.

----------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-GETQbyNumAtCard52.jpg" width="700" />

----------

#### Result
```json
[
  {
    "DocEntry": 503,
    "DocNum": 221,
    "NumAtCard": "664111000000373064",
    "CardCode": "BC6129916",
    "DocTotal": 300
  }
]
```

--------------


### Create a new quotation

The **Create New Quotation** action creates a new sales quotation in the system using customer and item details. It captures all configured data and stores it as a structured document for further processing.

This action is commonly used to **generate sales quotations**, **share pricing details with customers**, and **initiate sales processes**.

> **Note:** Mandatory fields must be provided to create a quotation. Optional fields can be configured as needed without blocking the process.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-NQTC54.jpg" wdith="700" />

Click on **Continue** button.

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| DocDueDate | Specify the due date of the quotation. (e.g., "2026-08-04") |
| CardCode | Enter the customer code. (e.g., "BC6129916") |
| DocumentLines
ItemCode | Unique identifier of the item. (e.g., "BCB2B0001")
| Quantity | Quantity of the item. (e.g., "3") |
| Optional Fields (Document Lines)
UnitPrice | Price per unit of the item. (e.g., "100") |
| TaxCode | Tax code applicable to the item. (e.g., "NT") |
| Vat Group | VAT group classification. (e.g., "VAT1") |
| Discount Percentage | Discount applied to the item. (e.g., "10%, 10.5%") |
| Optional Fields
DocDate | Date of the quotation. (e.g., "2026-03-13") |
| NumAtCard | Customer reference number. (e.g., "null, Ref-145 etc..,") |
| Address Extension 
ShipToStreet
ShipToBlock
ShipToCity
ShipToCountry
ShipToZipCode
ShipToState | Enter ShipTo details as per the requirement |
| Address Extension 
BillToStreet
BillToBlock
BillToCity
BillToCountry
BillToZipCode
BillToState | Enter BillTo details as per the requirement |
| Document Additional Expenses (Optional) 
Freight or Expenses Code | Additional costs applied to the quotation such as freight, handling, or service charges. (e.g., "300") |

Click on **Continue**, then **Run** the node.

--------------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-NQTC55.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-NQTC56.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-NQTC57.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-NQTC58.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-NQTC59.jpg" width="700" />

#### Result
```json
[
  {
    "DocEntry": 503,
    "DocNum": 221,
    "DocDate": "2026-03-13",
    "DocDueDate": "2026-08-04",
    "CardCode": "BC6129916",
    "NumAtCard": "REF-145",
    "DocumentLines": [
      {
        "ItemCode": "BCB2B0001",
        "Quantity": 3,
        "UnitPrice": 100,
        "TaxCode": "NT"
      }
    ]
  }
]
```

-----------------

### Update quotation

The **Update Quotation** action modifies an existing quotation in the system using the document number (DocNum). It allows updating header details, address information, document lines, and additional expenses.

This action is commonly used to **modify quotation details**, **update pricing or items**, and **maintain accurate sales records**.

> **Note:** Only the fields provided will be updated. Fields left empty will remain unchanged in the quotation.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-UQT61.jpg" width="700" />

Click on **Continue** button.

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| DocNum | Enter the quotation document number to be updated. (e.g., "503") |
| Optional Document Fields  
| DocDueDate | pdate the due date of the quotation. (e.g., "2026-08-09") | 
| CardCode |  CardCode will unique. (e.g., "BC6129916") |
| NumAtCard | Update the customer reference number. (e.g., "null, Ref-1122")|
| Address Extension 
ShipToStreet
ShipToBlock
ShipToCity
ShipToCountry
ShipToZipCode
ShipToState | Enter ShipTo details as per the requirement |
| Address Extension 
BillToStreet
BillToBlock
BillToCity
BillToCountry
BillToZipCode
BillToState | Enter BillTo details as per the requirement |
| DocumentLines
ItemCode | Unique identifier of the item. (e.g., "BCB2B0001")
| Quantity | Quantity of the item. (e.g., "5") |
| Optional Fields (Document Lines)
UnitPrice | Price per unit of the item. (e.g., "123") |
| TaxCode | Tax code applicable to the item. (e.g., "IGST, CGST, NT, Exempt ect..,") |
| Vat Group | VAT group classification. (e.g., "VAT1") |
| Discount Percentage | Discount applied to the item. (e.g., "10%") |
| Document Additional Expenses (Optional) 
Freight or Expenses Code | Additional costs applied to the quotation such as freight, handling, or service charges. (e.g., "300") |

Click on **Continue**, then **Run** the node.

#### Example Configuration 

<img src="/img/credentials/sap-b1/SAP-AC-UQT62.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-UQT63.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-UQT64.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-UQT65.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-UQT66.jpg" width="700" />

#### Result
```json
[
  {
    "value": "Quotation updated successfully"
  }
]
```

<img src="/img/credentials/sap-b1/SAP-AR-UQT67.jpg" width="700" />

-----------

### Update quotation customer reference no

The **Update Quotation Customer Reference Number** action updates the customer reference number (`NumAtCard`) for an existing quotation in the system.

This action is commonly used to **update customer-specific references**, **align documents with external systems**, or **correct quotation details**.

> **Note:** Only the `NumAtCard` field will be updated for the specified quotation. Ensure the correct DocEntry is provided to avoid updating the wrong record.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-UQTbyNumAtCard68.jpg" width="700" />

Click on **Continue** button.

---------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| DocEntry | Enter the internal document entry number of the quotation. (e.g., "503") |
| NumAtCard | Enter the updated customer reference number. (e.g., "Old data - Ref-100 and updated data Ref-104") |

Click on **Continue**, then **Run** the node.

---------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-UQTbyNumAtCard69.jpg" width="700" />

------------------

#### Result
```json
[
  {
    "value": "Quotation customer reference updated successfully"
  }
]
```

<img src="/img/credentials/sap-b1/SAP-AR-UQTbyNumAtCard70.jpg" width="700" />

------------------

## Orders Actions

### Get an sales order by customer reference no

The **Get a Sales Order by Customer Reference Number** action retrieves sales order details using the customer reference number (`NumAtCard`). It returns the matching sales order record as a structured object.

This action is commonly used to **lookup sales order details**, **track customer-specific references**, **validate records**, or **fetch order data for further processing**.

> **Note:** If multiple sales orders match the provided reference number, the system may return the first matching result or a list based on configuration. If no match is found, the output will be empty or null.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GETSObyCRno71.jpg" width="700" />

Click on **Continue** button.

-------------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| NumAtCard | Enter the customer reference number associated with the sales order. (e.g"Ref-104, 222, 664111000000375101 etc..,") |

Click on **Continue**, then **Run** the node.

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-GETSObyNumAtCard72.jpg" width="700" />

------------

#### Result
```json
[
  {
    "DocEntry": 11464,
    "DocNum": 503,
    "NumAtCard": "Ref-104",
    "CardCode": "BC6129916",
    "DocTotal": 1280
  }
]
```

### Get order list by item code

The **Get Order List by Item Code** action retrieves a list of sales orders that contain a specific item. It returns the matching orders as a structured collection of records.

This action is commonly used to **track item demand**, **analyze order history**, **monitor sales activity**, or **fetch related orders for processing**.

> **Note:** The result will include only up to the specified size limit. If no matching records are found, the output will be empty.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GETSOLbyIC74.jpg" width="700" />

Click on **Continue** button.

----------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| Size Limit | Specify the maximum number of records to retrieve. (e.g., "100") |
| Item Code | Enter the unique identifier of the item to search for in orders. (e.g., "") |

Click on **Continue**, then **Run** the node.

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-GETSOLbyIC75.jpg" width="700" />

----------

#### Result
```json
[
  {
    "DocEntry": 11464,
    "DocNum": 503,
    "ItemCode": "BCB2B0001",
    "Quantity": 5,
    "CardCode": "BC6129916"
  }
]
```

---------

### Create a new sales order

The **Create New Sales Order** action creates a new sales order in the system using customer, item, and delivery details. It captures all configured data and stores it as a structured document for further processing.

This action is commonly used to **create customer orders**, **manage sales transactions**, and **initiate delivery and billing processes**.

> **Note:** Mandatory fields must be provided to create a sales order. Optional fields can be configured as needed without blocking the process.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-CNO77.jpg" width="700" />

Click on **Continue** button.

#### Example Configuration

| Field          | Description |
|---------------|---------------|
| Document Date | Specify the date of the sales order. (e.g., "") |
| Document Due Date | Specify the due/delivery date. (e.g., "") |
| Card Code | Enter the customer code. (e.g., "") |
| DocumentLines
ItemCode | Unique identifier of the item. (e.g., "BCB2B0001")
| Quantity | Quantity of the item. (e.g., "5") |
| Optional Fields (Document Lines)
UnitPrice | Price per unit of the item. (e.g., "123") |
| TaxCode | Tax code applicable to the item. (e.g., "IGST, CGST, NT, Exempt ect..,") |
| Vat Group | VAT group classification. (e.g., "VAT1") |
| Discount Percentage | Discount applied to the item. (e.g., "10%") |
| Additional Fields 
Contact Person Code | Identifier for the contact person. (e.g., "") |
| NumAtCard | Customer reference number. (e.g., "") |
| Address Extension 
ShipToStreet
ShipToBlock
ShipToCity
ShipToCountry
ShipToZipCode
ShipToState | Enter ShipTo details as per the requirement |
| Address Extension 
BillToStreet
BillToBlock
BillToCity
BillToCountry
BillToZipCode
BillToState | Enter BillTo details as per the requirement |
| Document Additional Expenses (Optional) 
Freight or Expenses Code | Additional costs applied to the quotation such as freight, handling, or service charges. (e.g., "300") |

-------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-CNO78.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CNO79.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CNO80.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CNO81.jpg" width="700" />

------------

#### Result
```json
[
  {
    "DocEntry": 11464,
    "DocNum": 503,
    "DocDate": "2026-04-01",
    "DocDueDate": "2026-04-05",
    "CardCode": "BC6129916",
    "DocumentLines": [
      {
        "ItemCode": "BCB2B0001",
        "Quantity": 5,
        "UnitPrice": 123
      }
    ]
  }
]
```

------------------

### Create a Service

The **Create Service** action creates a service-type document (Order or Quotation) in the system using customer and service details. It captures all configured data and stores it as a structured document for further processing.

This action is commonly used to **create service orders or quotations**, **manage service-based transactions**, and **track customer service activities**.

> **Note:** Mandatory fields must be provided to create the service document. Optional fields can be configured as needed.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-CS83.jpg" width="700" />

Click on **Continue** button.

------------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| Object Type | Select the document type (**Orders** or **Quotation**). (e.g., "orders") |
| Card Code | Enter the customer code. (e.g., "BC6129916") |
| Document Date | Specify the document date. (e.g., "2026-04-01") |
| Document Due Date | Specify the due date. (e.g., "2026-05-09") |
| Item Descritpion | Description of the service provided. (e.g., "Installation service") |
| Unit Price | Price per unit of service. (e.g., "200") |
| Quantity | Number of service units. (e.g., "3") |
| Optionals 
TaxCode | Tax code applicable to the item. (e.g., "IGST, CGST, NT, Exempt ect..,") |
| Discount Percentage | Discount applied to the item. (e.g., "10%") |
| Additional Field
Comments | Add any remarks or notes related to the service document. (e.g., "Urgent service request") |

Click on **Continue**, then **Run** the node.

----------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-CS84.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CS85.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CS86.jpg" width="700" />

---------

#### Result
```json
[
  {
    "ObjectType": "orders",
    "CardCode": "BC6129916",
    "DocDate": "2026-04-01",
    "DocDueDate": "2026-05-09",
    "ServiceDescription": "Installation service",
    "Quantity": 3,
    "UnitPrice": 200
  }
]
```

---------------------

### Update Order

The **Update Order** action modifies an existing sales order in the system using the document entry (DocEntry). It allows updating header details, document lines, address information, and additional expenses.

This action is commonly used to **update order details**, **modify pricing or items**, and **maintain accurate sales records**.

> **Note:** Only the fields provided will be updated. Fields left empty will remain unchanged in the existing order.

------

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-UO88.jpg" width="700" />

Click on **Continue** button.

------------

#### Configuration Fields

| Field         | Description |
|---------------|---------------|
| DocEntry | Enter the internal document entry number of the order. (e.g., "11464") |
| Doc Due Date | Update the due/delivery date. (e.g., "2026-08-11") |
| NumAtCard | Update the customer reference number. (e.g., "Ref-111") |
| Rounding | Enable or disable rounding (**tYes** or **tNo**). (e.g., "tYes") |
| Rounding Difference Amount | Specify the rounding adjustment value. (e.g., "2.50") |
| DocumentLines
ItemCode | Unique identifier of the item. (e.g., "BCB2B0001")
| Quantity | Quantity of the item. (e.g., "8") |
| Optional Fields (Document Lines)
UnitPrice | Price per unit of the item. (e.g., "160") |
| TaxCode | Tax code applicable to the item. (e.g., "IGST, CGST, NT, Exempt ect..,") |
| Vat Group | VAT group classification. (e.g., "VAT1") |
| Discount Percentage | Discount applied to the item. (e.g., "13%") |
| Address Extension 
ShipToStreet
ShipToBlock
ShipToCity
ShipToCountry
ShipToZipCode
ShipToState | Enter ShipTo details as per the requirement |
| Address Extension 
BillToStreet
BillToBlock
BillToCity
BillToCountry
BillToZipCode
BillToState | Enter BillTo details as per the requirement |
| Document Additional Expenses (Optional) 
Freight or Expenses Code | Additional costs applied to the quotation such as freight, handling, or service charges. (e.g., "300") |

Click on **Continue**, then **Run** the node.

--------------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-UO89.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-UO90.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-UO91.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-UO92.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-UO93.jpg" width="700" />

------------

### Result
```json
[
  {
    "value": "Sales order updated successfully"
  }
]
```

<img src="/img/credentials/sap-b1/SAP-AR-UO94.jpg" width="700" />

------------------

### Update salesorder customer reference no

The **Update Sales Order Customer Reference Number** action updates the customer reference number (`NumAtCard`) for an existing sales order in the system.

This action is commonly used to **update customer-specific references**, **align orders with external systems**, or **correct sales order details**.

> **Note:** Only the `NumAtCard` field will be updated for the specified sales order. Ensure the correct DocEntry is provided to avoid updating the wrong record.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-USOCRno95.jpg" width="700" />

Click on **Continue** button.

----------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| DocEntry | Enter the internal document entry number of the sales order. (e.g., ("11464")) |
| NumAtCard | Enter the updated customer reference number. . (e.g., "Ref-1AAA") |

Click on **Continue**, then **Run** the node.

-------------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-USOCRno96.jpg" width="700" />

### Result
```json
[
  {
    "value": "Sales order customer reference updated successfully"
  }
]
```

<img src="/img/credentials/sap-b1/SAP-AR-USOCRno97.jpg" width="700" />

---------------

### Cancel a Sales Order

The **Cancel Sales Order** action cancels an existing sales order in the system using the document entry (DocEntry). Once cancelled, the order is marked as inactive and cannot be processed further.

This action is commonly used to **void incorrect orders**, **handle order cancellations**, or **stop further processing of an order**.

> **Note:** Once a sales order is cancelled, it cannot be reactivated. Ensure the correct DocEntry is provided before performing this action.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-CSO98.jpg" width="700" />

Click on **Continue** button.

---------------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| DocEntry | Enter the internal document entry number of the sales order to be cancelled. (e.g., "11464") |

Click on **Continue**, then **Run** the node.

----------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-CSO99.jpg" width="700" />

#### Result
```json
[
  {
    "DocEntry": 11464,
    "Cancelled": "tYES",
    "DocumentStatus": "bost_Close",
    "Message": "Sales order cancelled successfully"
  }
]
```

--------------

## Invoices Actions

### Get invoice by DocEntry 

The **Get Invoice by DocEntry** action retrieves invoice details using the internal document entry number (`DocEntry`). It returns the matching invoice record as a structured object.

This action is commonly used to **lookup invoice details**, **validate financial records**, **track billing information**, or **fetch invoice data for further processing**.

> **Note:** If the provided DocEntry does not exist, the output will be empty or null.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GETbyDocEntry113.jpg" width="700" />

Click on **Continue** button.

-------------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| DocEntry | Enter the internal document entry number of the invoice. (e.g., "11462") |

Click on **Continue**, then **Run** the node.


-----------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-GETbyDocEntry114.jpg" width="700" />

-------------

#### Result
```json
[
  {
    "DocEntry": 11462,
    "DocNum": 715,
    "CardCode": "BC6129916",
    "DocDate": "2026-04-01",
    "DocTotal": 3955
  }
]
```

--------------

### Get invoice by order DocEntry

The **Get Invoice by Order DocEntry** action retrieves invoice details associated with a specific sales order using the order's document entry number. It returns the related invoice record(s) as structured data.

This action is commonly used to **track invoices generated from orders**, **validate billing against sales orders**, or **fetch related financial documents for processing**.

> **Note:** If no invoices are linked to the provided order DocEntry, the output will be empty or null. In case of multiple invoices, the system may return one or a list based on configuration.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GETbyODRDocEntry110.jpg" width="700" />

Click on **Continue** button.

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| DocEntry | Enter the internal document entry number of the sales order. (e.g., "") |

Click on **Continue**, then **Run** the node.

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-GETbyODRDocEntry111.jpg" width="700" />

-----------

#### Result
```json
[
  {
    "Invoice": {
      "DocEntry": 11462,
      "DocNum": 715,
      "BaseEntry": 11464
    },
    "DocumentLines": [
      {
        "ItemCode": "BCB2B0001",
        "Quantity": 7,
        "BaseType": 17
      }
    ]
  }
]
```

-------------

### Get invoice by NumAtCard

The **Get Invoice by Customer Reference Number** action retrieves invoice details using the customer reference number (`NumAtCard`). It returns the matching invoice record(s) as structured data.

This action is commonly used to **lookup invoice details**, **track customer-specific references**, **validate billing records**, or **fetch invoice data for further processing**.

> **Note:** If multiple invoices match the provided reference number, the system may return a single record or a list based on configuration. If no match is found, the output will be empty or null.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GETINVbyNumAtCard107.jpg" width="700" />

Click on **Continue** button.

------------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| NumAtCard | Enter the customer reference number associated with the invoice. (e.g., "REF-INV01") |

Click on **Continue**, then **Run** the node.

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-GETINVbyNumAtCard108.jpg" width="700" />

#### Result
```json
[
  {
    "DocEntry": 11462,
    "DocNum": 715,
    "NumAtCard": "REF-INV01",
    "CardCode": "BC6129916",
    "DocTotal": 3955
  }
]
```

-------------

### Create a new AR invoice

The **Create New AR Invoice** action creates a new Accounts Receivable invoice in the system using customer and item details. It supports both standard AR invoices and reserve invoices.

This action is commonly used to **generate invoices**, **bill customers**, and **manage financial transactions**.

> **Note:** Mandatory fields must be provided to create an invoice. Optional fields can be configured as needed without blocking the process.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-CNINV102.jpg" width="700" />

Click on **Continue** button.

-------------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| DocDate | Specify the invoice date. (e.g., "2026-04-01") |
| DocDueDate | Specify the due date of the invoice. (e.g., "2026-05-19") |
| CardCode | Enter the customer code. (e.g., "BC6129916") |
| Reserve Invoice | Select the invoice type (**AR Invoice** or **Reserve Invoice**). (e.g., "AR Invoice") |
| DocumentLines
ItemCode | Unique identifier of the item. (e.g., "BCB2B0001 or WOOCOM101")
| Quantity | Quantity of the item. (e.g., "7") |
| TaxCode | Tax code applicable to the item. (e.g., "IGST, CGST, NT, Exempt ect..,") |
| Optional Fields (Document Lines)
UnitPrice | Price per unit of the item. (e.g., "500") |
| Vat Group | VAT group classification. (e.g., "VAT1") |
| Discount Percentage | Discount applied to the item. (e.g., "13%") |
| BaseLine | Base document line reference. (e.g., "0") |
| BaseType | Base document type. (e.g., "-1") |
| BaseEntry | Base document entry reference. (e.g., "null or 1455") |
| NumAtCard | Enter the customer reference number. (e.g., "REF-INV01") |
| ContactPerson | Identifier of the contact person. (e.g., "134") |
| Document Additional Expenses (Optional) 
Freight or Expenses Code | Additional costs applied to the quotation such as freight, handling, or service charges. (e.g., "300") |

Click on **Continue**, then **Run** the node.

------------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-CNINV103.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CNINV104.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CNINV105.jpg" width="700" />

------------

#### Result
```json
[
  {
    "DocEntry": 11462,
    "DocNum": 715,
    "DocDate": "2026-04-01",
    "DocDueDate": "2026-05-19",
    "CardCode": "BC6129916",
    "ReserveInvoice": "AR Invoice",
    "DocumentLines": [
      {
        "ItemCode": "BCB2B0001",
        "Quantity": 7,
        "UnitPrice": 500,
        "TaxCode": "NT"
      }
    ]
  }
]
```

----------------


## Returns Actions

### Create Returns

The **Create Returns** action creates a return document in the system for items returned by a customer. It captures return details and stores them as a structured document for further processing.

This action is commonly used to **process product returns**, **adjust inventory**, and **manage refund or replacement workflows**.

> **Note:** Mandatory fields must be provided to create a return document. Optional fields can be configured as needed.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-CRETURN107.jpg" width="700" />

Click on **Continue** button.

----------

#### Configuration Fields

| Field          | Description |
|---------------|---------------|
| DocDate | Specify the invoice date. (e.g., "2026-04-01") |
| DocDueDate | Specify the due date of the invoice. (e.g., "2026-05-19") |
| CardCode | Enter the customer code. (e.g., "ZC0001") |
| DocumentLines
ItemCode | Unique identifier of the item. (e.g., "DIET001")
| Quantity | Quantity of the item. (e.g., "1") |
| TaxCode | Tax code applicable to the item. (e.g., "IGST, CGST, NT, DEFAULT, Exempt ect..,") |
| Optional Fields (Document Lines)
UnitPrice | Price per unit of the item. (e.g., "20") |
| Vat Group | VAT group classification. (e.g., "tNO") |
| Discount Percentage | Discount applied to the item. (e.g., "0") |
| Warehouse | Warehouse where the return is processed. (e.g., "01") |
| BaseLine | Base document line reference. (e.g., "0") |
| BaseType | Base document type. (e.g., "-1") |
| BaseEntry | Base document entry reference. (e.g., "null or 1455") |
| NumAtCard | Enter the customer reference number. (e.g., "REF-INV01") |
| ContactPerson | Identifier of the contact person. (e.g., "134") |
| Document Additional Expenses (Optional) 
Freight or Expenses Code | Additional costs such as handling or return charges. (e.g., "300") |
| Comments | Add remarks related to the return. (e.g., "Damaged item returned") |

Click on **Continue**, then **Run** the node.

--------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-CRETURN108.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CRETURN109.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CRETURN110.jpg" width="700" />

-------------

#### Result
```json
[
  {
    "DocEntry": 205,
    "DocNum": 88,
    "CardCode": "ZC0001",
    "Comments": "Damaged item returned",
    "DocumentLines": [
      {
        "ItemCode": "DIET001",
        "Quantity": 1,
        "UnitPrice": 20,
        "WarehouseCode": "01"
      }
    ]
  }
]
```

--------------------

## ServiceCall Actions

### Create Service Call

The **Create Service Call** action creates a new service request in the system with customer, item, and issue details. It helps in tracking service activities and managing support processes.

**Note:** Mandatory fields must be provided to create a service call. Optional fields can be configured based on business requirements.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-CSRVCCL121.jpg" width="700" />

Click on **Continue** button.

-----------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Customer Code | Enter the customer code. (e.g., "CUST-001") |
| Subject | Provide the subject of the service call. (e.g., "System Installation Issue") |
| Status | Define the current status of the service call. (e.g., "Open") |
| Customer Name | Enter the name of the customer. (e.g., "ABC Pvt Ltd") |
| Contact Person Code | Identifier of the contact person. (e.g., "101") |
| Description | Detailed description of the issue/request. (e.g., "Installation not completed successfully") |
| Priority | Set the priority level. (e.g., "High") |
| Start Date | Specify the start date of the service. (e.g., "2026-04-01") |
| Start Time | Specify the start time. (e.g., "10:00") |
| End Due Date | Specify the expected completion date. (e.g., "2026-04-02") |
| End Time | Specify the expected completion time. (e.g., "18:00") |
| Assigned Date | Date when the service is assigned. (e.g., "2026-04-01") |
| Item Code | Unique identifier of the item. (e.g., "ITEM-001") |
| Item Description | Description of the item. (e.g., "Laptop Installation") |
| Item Group Code | Categorizes the item. (e.g., "Electronics") |
| Optionals
| Ship To Address Type | Type of shipping address. (e.g., "Customer") |
| ShipToStreet | Shipping street address. (e.g., "Street 1") |
| Ship To Address 2 | Additional shipping address line. (e.g., "Area 51") |
| Ship To Address 3 | Additional shipping address line. (e.g., "Near Park") |
| ShipToBlock | Shipping block/area. (e.g., "Block A") |
| ShipToCity | Shipping city. (e.g., "Hyderabad") |
| ShipToCountry | Shipping country. (e.g., "India") |
| ShipToZipCode | Shipping postal code. (e.g., "500001") |
| ShipToState | Shipping state. (e.g., "Telangana") |
| Bill To Address Type | Type of billing address. (e.g., "Customer") |
| BillToStreet | Billing street address. (e.g., "Street 2") |
| Bill To Address 2 | Additional billing address line. (e.g., "Area 52") |
| Bill To Address 3 | Additional billing address line. (e.g., "Near Mall") |
| BillToBlock | Billing block/area. (e.g., "Block B") |
| BillToCity | Billing city. (e.g., "Hyderabad") |
| BillToCountry | Billing country. (e.g., "India") |
| BillToZipCode | Billing postal code. (e.g., "500002") |
| BillToState | Billing state. (e.g., "Telangana") |

Click on **Continue**, then **Run** the node.

-----------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-CSRVCCL122.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CSRVCCL123.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CSRVCCL124.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CSRVCCL125.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CSRVCCL126.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CSRVCCL127.jpg" width="700" />

---------------

#### Result
```json
[
  {
    "ServiceCallID": 1024,
    "CustomerCode": "CUST-001",
    "CustomerName": "ABC Pvt Ltd",
    "Subject": "System Installation Issue",
    "Status": "Open",
    "Priority": "High",
    "ItemCode": "ITEM-001"
  }
]
```

--------------


### Update Service Call

The **Update Service Call** action is used to modify an existing service request with updated customer, item, status, and resolution details. It helps in tracking progress, updating issue status, and maintaining service history.

**Note:** Ensure valid status and priority values are selected based on business rules. Optional address fields can be updated if required.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-USVCL130.jpg" width="700" />

Click on **Continue** button.

------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Customer Code | Enter the customer code. (e.g., "BC6129916") |
| Customer Name | Enter the name of the customer. (e.g., "MAX WELL") |
| Contact Person Code | Identifier of the contact person. (e.g., "134") |
| Subject | Provide the subject of the service call. (e.g., "DemoCall - updated") |
| Description | Updated description of the issue. (e.g., "This call is regarding testing purposes.") |
| Priority | Select priority based on requirement. (e.g., "Low", "Medium", "High") |
| Status | Select current status. (e.g., "Open", "On_Hold", "Pending", "Escalated", "Closed") |
| Start Date | Specify the start date. (e.g., "2026-04-06") |
| Start Time | Specify the start time. (e.g., "17:32:00") |
| End Due Date | Specify the expected completion date. (e.g., "2026-04-20") |
| End Time | Specify the expected completion time. (e.g., "23:32:00") |
| Assigned Date | Date when the service is assigned. (e.g., "2026-04-01") |
| Item Code | Unique identifier of the item. (e.g., "BCB2B0001") |
| Item Description | Description of the item. (e.g., "Hyderated Water Bottle1") |
| Item Group Code | Categorizes the item. (e.g., "100") |
| Resolution | Final resolution or action taken. (e.g., "Test") |
| Optional Fields
Ship To Address Type | Type of shipping address. (e.g., "null") |
| ShipToStreet | Shipping street address. (e.g., "Domin Street") |
| Ship To Address 2 | Additional shipping address line. (e.g., "District Complex") |
| Ship To Address 3 | Additional shipping address line. (e.g., "Old Star Build") |
| Ship To Number | Shipping Number. (e.g., "1/33 Valley")
| ShipToBlock | Shipping block/area. (e.g., "Omega Block") |
| ShipToCity | Shipping city. (e.g., "Hyderabad") |
| ShipToCountry | Shipping country. (e.g., "India or IN") |
| ShipToZipCode | Shipping postal code. (e.g., "500033") |
| ShipToState | Shipping state. (e.g., "Telangana or TS") |
| Bill To Address Type | Type of billing address. (e.g., "TEST CHECk123") |
| BillToStreet | Billing street address. (e.g., "Zing Street") |
| Billing to Street Number | Billing Street Number (e.g., "1-987") |
| Bill To Address 2 | Additional billing address line. (e.g., "Domestic Resort") |
| Bill To Address 3 | Additional billing address line. (e.g., "Merchant street") |
| BillToBlock | Billing block/area. (e.g., "d block valley") |
| BillToCity | Billing city. (e.g., "Hyderabad") |
| BillToCountry | Billing country. (e.g., "India or IN") |
| BillToZipCode | Billing postal code. (e.g., "500002") |
| BillToState | Billing state. (e.g., "Telangana or TS") |

Click on **Continue**, then **Run** the node.

-------------

#### Example Configuration
<img src="/img/credentials/sap-b1/SAP-AC-USRVCCL131.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-USRVCCL132.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-USRVCCL133.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-USRVCCL134.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-USRVCCL135.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-USRVCCL136.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-USRVCCL137.jpg" width="700" />

-----------

#### Result
```json
[
  {
    "ServiceCallID": 1024,
    "CustomerCode": "BC6129916",
    "CustomerName": "MAX WELL",
    "Status": "Closed",
    "Priority": "Medium",
    "Resolution": "Test"
  }
]
```

<img src="/img/credentials/sap-b1/SAP-AR-USRVCCL138.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AR-USRVCCL139.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AR-USRVCCL140.jpg" width="700" />

--------------------


## SalesOpportunities Actions

### Create a new Sales Opportunity

The **Create a New Sales Opportunity** action is used to record potential sales deals in the system. It helps track leads, monitor progress through different stages, and estimate revenue.

**Note:** Sales Opportunity Lines are mandatory to track stages and progress of the opportunity. Optional fields can be configured based on business requirements.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-CNSOPPR141.jpg" width="700" />

Click on **Continue** button.

----------

#### Configuration Fields

| Field | Description |
|------|-------------|
| BusinessPartner Code | Enter the customer/business partner code. (e.g., "CUST-001") |
| Opportunity Name | Provide the name of the opportunity. (e.g., "New ERP Implementation") |
| Start Date | Specify the opportunity start date. (e.g., "2026-04-01") |
|Sales Opportunity Lines
Start Date | Specify the start date of the stage. (e.g., "2026-04-01") |
| Closing Date | Expected closing date of the opportunity. (e.g., "2026-04-30") |
| Maximum Local Total | Estimated maximum value of the opportunity. (e.g., "50000") |
| Stage Key | Define the stage of the opportunity. (e.g., "1 - Qualification") |
|Optional Fields
Contact Person Code | Identifier of the contact person. (e.g., "101") |
| Total Amount | Total estimated value of the opportunity. (e.g., "45000") |
| Remarks | Additional notes or comments. (e.g., "High priority client") |

Click on **Continue**, then **Run** the node.

----------------------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-CNSOPP142.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CNSOPP143.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CNSOPP144.jpg" width="700" />

------------

#### Result
```json
[
  {
    "OpportunityName": "Demo Opportunity",
    "CardCode": "BC6129916",
    "CustomerName": "MAX6",
    "StartDate": "2026-04-06",
    "PredictedClosingDate": "2026-04-06",
    "Status": "sos_Open",
    "Remarks": "Test Demo",
    "TotalAmountLocal": 80000,
    "TotalAmounSystem": 80000,
    "ClosingPercentage": 100,
    "CurrentStageNo": 3,
    "SalesPerson": -1,

    "SalesOpportunitiesLines": [
      {
        "StageKey": 3,
        "StartDate": "2026-04-06",
        "ClosingDate": "2026-04-06",
        "MaxLocalTotal": 80000,
        "MaxSystemTotal": 80000,
        "PercentageRate": 100,
        "WeightedAmountLocal": 80000,
        "WeightedAmountSystem": 80000
      }
    ]
  }
]
```

-------------


## Exchange Rate Actions

### Get Currency Exchange Rate

The **Get Currency Exchange Rate** action retrieves the exchange rate between two currencies for a specific date. It helps in financial calculations, reporting, and currency conversions.

This action is commonly used to **convert currencies**, **calculate financial values**, or **fetch historical exchange rates**.

> **Note:** If no date is provided, the system may return the latest available exchange rate.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GCRNCYRATE147.jpg" width="700" />

Click on **Continue** button.

-------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Currency Code | Enter the currency code for which the exchange rate is required. (e.g., "USD", "INR", "EUR") |
| Date | Specify the date to fetch the exchange rate. (e.g., "2026-04-06") |

Click on **Continue**, then **Run** the node.

------------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-GCRNCYRATE148.jpg" width="700" />

----------

#### Result
```json
[
  {
    "value": "5.60"
  }
]
```

------------


### Set Currency Rate

The **Set Currency Rate** action is used to define or update the exchange rate for a specific currency on a given date. This is useful for maintaining accurate financial records and currency conversions.

> **Note:** Ensure the exchange rate is accurate, as it impacts financial transactions and reporting.

--------------

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-STCRNCYRATE150.jpg" width="700" />

Click on **Continue** button.

------------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Currency Code | Enter the currency code for which the rate is being set. (e.g., "USD", "INR", "EUR") |
| Rate Date | Specify the date for the exchange rate. (e.g., "2026-04-061") |
| Exchange Rate | Enter the exchange rate value. (e.g., "3.9") |

Click on **Continue**, then **Run** the node.

-------------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-SCRNCYRATE151.jpg" width="700" />

-----------

#### Result
```json
[
  {
    "Currency": "USD",
    "RateDate": "2026-04-06",
    "ExchangeRate": 3.9,
    "Status": "success",
    "Message": "Currency rate updated successfully"
  }
]
```

--------------------


## Sales Tax Codes Actions

### Create Sales Tax Code

The **Create Sales Tax Code** action is used to define a new tax code in the system. It helps manage taxation rules for sales and purchasing transactions.

> **Note:** Tax configurations should be set carefully as they directly impact financial calculations and compliance.

#### Select the Credential and Action Event

<img src="\img\credentials\sap-b1\SAP-C-CSLSTAXCODE234.jpg" width="700" />

Click on **Continue** button.

------------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Tax Code | Unique identifier for the tax. (e.g., "IMST") |
| Tax Name | Name of the tax. (e.g., "IMST") |
| Tax Rate (%) | Percentage of the tax rate. (e.g., "5") |
|Sales Tax Code Lines
Tax Authority Code (STACode) | Code representing the tax authority. (e.g., "CA") |
| Tax Authority Type (STAType) | Type of tax authority. (e.g., "Country") |
|Optional Fields
Sales Tax Code | Additional tax code reference if applicable. (e.g., "GST_SALES") |
| Effective Rate | Effective tax rate after adjustments. (e.g., "18") |
| Tax on Tax Code | Specifies dependent tax code. (e.g., "CESS") |
| Tax on Tax Type | Type of tax applied on another tax. (e.g., "Inclusive") |
|Additional Optional Settings
Valid for AR (Accounts Receivable) | Indicates if applicable for sales transactions. (e.g., "Yes") |
| Valid for AP (Accounts Payable) | Indicates if applicable for purchase transactions. (e.g., "Yes") |
| Freight | Specifies if tax applies to freight charges. (e.g., "Yes") |
| Is Item Level | Determines if tax is applied at item level. (e.g., "Yes") |
| FA Debit | Indicates if applicable for fixed asset debit. (e.g., "No") |
| Inactive | Marks the tax code as inactive if not in use. (e.g., "No") |

Click on **Continue**, then **Run** the node.

-------------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CSLSTAXCODE235.jpg" width="700" />

-------------

#### Result
```json
[
  {
    "odata.metadata": "https://insync.pro/b1s/v1/$metadata#SalesTaxCodes/@Element",
    "ValidForAR": "tYES",
    "ValidForAP": "tYES",
    "UserSignature": 7,
    "Rate": 6,
    "Name": "IMST",
    "Freight": "tNO",
    "Code": "IMST",
    "IsItemLevel": "tNO",
    "Inactive": "tNO",
    "FADebit": "tNO",
    "SalesTaxCodes_Lines": [
      {
        "STATaxOnTaxType": null,
        "STATaxonTaxCode": null,
        "STCCode": "IMST",
        "STAType": -3,
        "STACode": "CA",
        "RowNumber": 0,
        "EffectiveRate": 6
      }
    ]
  }
]
```
--------------------

### Update Sales Tax Code

The **Update Sales Tax Code** action is used to modify an existing tax code in the system. It allows updating tax details and configurations based on business or compliance requirements.

#### Select Credentials and Action Event

Click on **Continue** button

-------

### Configuration Fields

| Field | Description |
|------|-------------|
| Tax Code (Identifier) | Enter the unique tax code to be updated. (e.g., "GST18") |
| Tax Name | Name of the tax. (e.g., "IMST") |
| Tax Rate (%) | Percentage of the tax rate. (e.g., "6") |
|Sales Tax Code Lines
Tax Authority Code (STACode) | Code representing the tax authority. (e.g., "CA") |
| Tax Authority Type (STAType) | Type of tax authority. (e.g., "Country") |
|Optional Fields
Sales Tax Code | Additional tax code reference if applicable. (e.g., "GST_SALES") |
| Effective Rate | Effective tax rate after adjustments. (e.g., "18") |
| Tax on Tax Code | Specifies dependent tax code. (e.g., "CESS") |
| Tax on Tax Type | Type of tax applied on another tax. (e.g., "Inclusive") |
|Additional Optional Settings
Valid for AR (Accounts Receivable) | Indicates if applicable for sales transactions. (e.g., "Yes") |
| Valid for AP (Accounts Payable) | Indicates if applicable for purchase transactions. (e.g., "Yes") |
| Freight | Specifies if tax applies to freight charges. (e.g., "Yes") |
| Is Item Level | Determines if tax is applied at item level. (e.g., "Yes") |
| FA Debit | Indicates if applicable for fixed asset debit. (e.g., "No") |

> **Note:** Only the provided fields will be updated. Ensure the correct Tax Code is used, as it directly impacts financial calculations and reporting.

Click on **Continue**, Then **Run** node

-----------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-USLSTAXCODE236.jpg" width="700" />

----------

#### Result

```json
[
  {
    "Code": "GST18",
    "Name": "IMST",
    "Rate": 6,
    "ValidForAR": "tYES",
    "ValidForAP": "tYES",
    "Freight": "tNO",
    "IsItemLevel": "tNO",
    "FADebit": "tNO",
    "SalesTaxCodes_Lines": [
      {
        "STCCode": "GST18",
        "STACode": "CA",
        "STAType": -3,
        "EffectiveRate": 18
      }
    ]
  }
]
```

<img src="\img\credentials\sap-b1\SAP-AR-USLSTAXCODE237.jpg" width="700" />

-------------------

## Special Prices Action

### Get Special Prices by Card Code

The **Get Special Prices by Card Code** action retrieves all special pricing details configured for a specific business partner. It helps in identifying customer-specific pricing agreements and discounts.

> **Note:** This action returns all special prices associated with the given Card Code, including item-level pricing and discounts if configured.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-GSPRCbyCRDCDE153.jpg" width="700" />

Click on **Continue** button.

----------

#### Configuration Fields

| Field | Description |
|------|--------------|
| Card Code | Enter the business partner (customer/vendor) code. (e.g., "BC6129916") |

Click on **Continue**, then **Run** the node.

------------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-GETSPRCbyCRDCODE154.jpg" width="700" />

--------------

#### Result
```json
[
  {
    "CardCode": "BC6129916",
    "ItemCode": "BCB2B0001",
    "PriceListNum": 1,
    "SpecialPrice": 450,
    "Currency": "$",
    "DiscountPercent": 10,
    "AutoUpdate": "tNO"
  },
  {
    "CardCode": "BC6129916",
    "ItemCode": "WOOCOM101",
    "PriceListNum": 1,
    "SpecialPrice": 500,
    "Currency": "$",
    "DiscountPercent": 5,
    "AutoUpdate": "tNO"
  }
]
```

--------------

## Return Request Actions

### Create Return Request

The **Create Return Request** action creates a new return request document in the system for items that need to be returned. It captures customer, item, and pricing details for further processing.

#### Select the Credential and Action Event

<img src="/img/credentials/sap-b1/SAP-C-CRTNRQST161.jpg" width="700" />

Click on **Continue** button.

-------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| DocDate | Specify the return request date. (e.g., "2026-04-30") |
| CardCode | Enter the customer code. (e.g., "BC6129916") |
| Document Lines
ItemCode | Unique identifier of the item. (e.g., "BCB2B0001") |
| Quantity | Quantity of the item to be returned. (e.g., "2") |
| Unit Price | Price per unit. (e.g., "100") |
| Optional Fields (Document Lines)
Tax Code | Applicable tax code. (e.g., "NT") |
| VatGroup | VAT classification. (e.g., "null") |
| DiscountPercentage | Discount applied to the item. (e.g., "0") |
| WarehouseCode | Warehouse for processing return. (e.g., "01") |
| BaseType | Base document type. (e.g., "-1") |
| BaseEntry | Base document entry reference. (e.g., "null") |
| BaseLine | Base document line reference. (e.g., "null") |
| Optional Fields (Header)
DocDate | Specify document date if different. (e.g., "2026-04-10") |
| NumAtCard | Customer reference number. (e.g., "null") |
| ContactPersonCode | Identifier of the contact person. (e.g., "134") |
| Comment | Additional remarks. (e.g., "Return due to defect") |
| Additional Expenses (Optional)
 Additional Expenses | Extra charges such as handling or logistics. (e.g., "200") |

> **Note:** Mandatory fields must be provided to create a return request. Optional fields can be configured based on business requirements.

Click on **Continue**, then **Run** the node.

-------

#### Example Configuration

<img src="/img/credentials/sap-b1/SAP-AC-CRTNRQST162.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CRTNRQST163.jpg" width="700" />
<img src="/img/credentials/sap-b1/SAP-AC-CRTNRQST164.jpg" width="700" />

---------

#### Result
```json
[
  {
    "DocEntry": 162,
    "DocNum": 78,
    "DocDate": "2026-04-30",
    "CardCode": "BC6129916",
    "CardName": "MAX6",
    "Comments": "Return due to defect",
    "DocTotal": 200,
    "DocCurrency": "$",
    "ContactPersonCode": 134,
    "DocumentStatus": "bost_Open",
    "DocumentLines": [
      {
        "LineNum": 0,
        "ItemCode": "BCB2B0001",
        "Quantity": 2,
        "UnitPrice": 100,
        "TaxCode": "NT",
        "VatGroup": null,
        "DiscountPercent": 0,
        "WarehouseCode": "01",
        "BaseType": -1,
        "BaseEntry": null,
        "BaseLine": null,
        "LineTotal": 200
      }
    ],
    "DocumentAdditionalExpenses": [
      {
        "LineNum": 0,
        "ExpenseCode": 1,
        "LineTotal": 200
      }
    ]
  }
]
```

---------------------


## Sales Opportunities Action

### Create a new sales opportunity

The **Create a New Sales Opportunity** action is used to record and track potential sales deals in the system, including stages, expected value, and customer details.

#### Select the Credential and Action Event

<img src="\img\credentials\sap-b1\SAP-C-CSOPP191.jpg" width="700" />

Click on **Continue** button.

----------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Business Partner Code | Enter the customer/business partner code. (e.g., "BC6129916") |
| Opportunity Name | Provide the name of the opportunity. (e.g., "OPPO TEST 22") |
| Start Date | Specify the opportunity start date and time. (e.g., "14/04/2026 13:18") |
| Sales Opportunity Lines
Start Date | Specify the stage start date and time. (e.g., "14/04/2026 13:20") |
| Closing Date | Expected closing date and time. (e.g., "14/04/2026 13:20") |
| Maximum Local Total | Estimated maximum value of the opportunity. (e.g., "550") |
| Stage Key | Define the stage of the opportunity. (e.g., "1") |
| Optional Fields
Contact Person Code | Identifier of the contact person. (e.g., "134") |
| Total Amount | Total estimated value of the opportunity. (e.g., "550") |
| Remarks | Additional notes or comments. (e.g., "Demo Purpose") |

> **Note:** Sales Opportunity Lines are required to track the progress and lifecycle of the opportunity. Optional fields can be configured as needed.

Click on **Continue**, then **Run** the node.

------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CNSOPP192.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CNSOPP193.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CNSOPP194.jpg" width="700" />

--------------

#### Result

```json
[
  {
    "odata.metadata": "https://insync.pro/b1s/v1/$metadata#SalesOpportunities/@Element",
    "SequentialNo": 90,
    "CardCode": "BC6129916",
    "SalesPerson": -1,
    "ContactPerson": 134,
    "Source": null,
    "InterestField1": null,
    "InterestField2": null,
    "InterestField3": null,
    "InterestLevel": null,
    "StartDate": "2026-04-14",
    "PredictedClosingDate": "2026-04-14",
    "MaxLocalTotal": 550,
    "MaxSystemTotal": 550,
    "WeightedSumLC": 55,
    "WeightedSumSC": 55,
    "GrossProfit": 0,
    "GrossProfitTotalLocal": 0,
    "GrossProfitTotalSystem": 0,
    "Remarks": "Demo Purpose",
    "Status": "sos_Open",
    "ReasonForClosing": null,
    "TotalAmountLocal": 550,
    "TotalAmounSystem": 550,
    "ClosingGrossProfitLocal": 0,
    "ClosingGrossProfitSystem": 0,
    "ClosingPercentage": 10,
    "CurrentStageNo": 1,
    "CurrentStageNumber": 1,
    "OpportunityName": "OPPO TEST 22",
    "Industry": null,
    "LinkedDocumentType": null,
    "DataOwnershipfield": null,
    "StatusRemarks": null,
    "ProjectCode": null,
    "BPChanelName": null,
    "UserSignature": 7,
    "CustomerName": "MAX6",
    "DocumentCheckbox": null,
    "LinkedDocumentNumber": null,
    "Territory": null,
    "ClosingDate": null,
    "BPChannelContact": null,
    "BPChanelCode": null,
    "ClosingType": "sos_Days",
    "AttachmentEntry": null,
    "OpportunityType": "boOpSales",
    "UpdateDate": "2026-04-14",
    "UpdateTime": "18:51:44",
    "U_WebId": null,
    "SalesOpportunitiesLines": [
      {
        "LineNum": 0,
        "SalesPerson": -1,
        "StartDate": "2026-04-14",
        "ClosingDate": "2026-04-14",
        "StageKey": 1,
        "PercentageRate": 10,
        "MaxLocalTotal": 550,
        "MaxSystemTotal": 550,
        "Remarks": null,
        "Contact": "tNO",
        "Status": "so_Open",
        "WeightedAmountLocal": 55,
        "WeightedAmountSystem": 55,
        "DocumentNumber": null,
        "DocumentType": "bodt_MinusOne",
        "DocumentCheckbox": null,
        "ContactPerson": null,
        "BPChanelName": null,
        "BPChanelCode": null,
        "SequenceNo": 90,
        "DataOwnershipfield": null,
        "BPChannelContact": null
      }
    ],
    "SalesOpportunitiesCompetition": [],
    "SalesOpportunitiesPartners": [],
    "SalesOpportunitiesInterests": [],
    "SalesOpportunitiesReasons": []
  }
]
```

--------------------

## Purchase Order Action

### Create Purchase Order

The **Create Purchase Order** action creates a new purchase order in the system for procuring goods or services from a vendor. It captures vendor, item, pricing, and delivery details.

#### Select Credentials and action Event

<img src="\img\credentials\sap-b1\SAP-C-CPRORD205.jpg" width="700" />

Click on **Continue** button.

-------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Vendor Code | Enter the vendor code. (e.g., "SRITEST") |
| Document Date | Specify the purchase order date. (e.g., "2026-04-17") |
| Delivery Date | Specify the expected delivery date. (e.g., "2026-04-24") |
| Document Lines
Item Code | Unique identifier of the item. (e.g., "DIET002") |
| Quantity | Quantity of the item. (e.g., "10") |
| Unit Price | Price per unit. (e.g., "20") |
| Optional Fields (Document Lines)
Item Description | Description of the item. (e.g., "TEST") |
| Discount Percentage | Discount applied to the item. (e.g., "2") |
| Tax Code | Applicable tax code. (e.g., "NT") |
| Warehouse Code | Warehouse for receiving goods. (e.g., "01") |
| Required Date | Required delivery date for the item. (e.g., "2026-04-17") |
| VAT Group | VAT classification. (e.g., "VAT18") |
| Optional Fields (Header)
Vendor Reference No | Vendor-provided reference number. (e.g., "728902") |
| Ship To Address Code | Code for shipping address. (e.g., "SHIP 001") |
| Bill To Address Code | Code for billing address. (e.g., "BILL 001") |
| Remarks | Additional notes. (e.g., "Urgent order or Demo purpose") |
| Contact Person Code | Identifier of the contact person. (e.g., "134") |
| Document Currency | Currency of the document. (e.g., "INR") |
| Discount Percentage | Overall document discount. (e.g., "5") |
| Additional Expenses | Extra charges such as freight. (e.g., "300") |
| Address Extension (Optional)
Ship To Address |
| ShipToStreet | Shipping street address (e.g., "Lake Street")|
| ShipToStreetNo | Street number (e.g., "1/33") |
| ShipToCity | City (e.g., "Hyderabad") |
| ShipToZipCode | Postal code (e.g., "500039") |
| ShipToCountry | Country (e.g., "IN") |
| ShipToState | State (e.g., "TS") |
| BillToStreet | Billing street address (e.g., "Mark street") | 
| BillToStreetNo | Street number (e.g., "RD 200") | 
| BillToBuilding | Building name (e.g., "Lake Apartment") |
| BillToCity | City (e.g., "Hyderabad") |
| BillToZipCode | Postal code (e.g., "500038") |
| BillToCountry | Country (e.g., "IN") |
| BillToState | State (e.g., "TS") |
| BillToAddressType | Address type |

> **Note:** Mandatory fields must be provided to create a purchase order. Optional fields can be configured based on business requirements.

Click on **Continue**, then **Run** the node.

--------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CPRORD200.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CPRORD201.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CPRORD202.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CPRORD203.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CPRORD204.jpg" width="700" />

#### Result

```json
[
  {
    "DocEntry": 39,
    "DocNum": 19,
    "DocDate": "2026-04-17",
    "DocDueDate": "2026-04-24",
    "CardCode": "SRITEST",
    "CardName": "SRI EXPORTS",
    "DocTotal": 196,
    "DocCurrency": "$",
    "Comments": "",
    "ShipToCode": "SHIP 001",
    "DocumentStatus": "bost_Open",

    "DocumentLines": [
      {
        "LineNum": 0,
        "ItemCode": "DIET002",
        "ItemDescription": "TEST",
        "Quantity": 10,
        "Price": 19.6,
        "DiscountPercent": 2,
        "WarehouseCode": "01",
        "TaxCode": "NT",
        "LineTotal": 196,
        "UnitPrice": 20,
        "Currency": "$",
        "RequiredDate": "2026-04-17"
      }
    ],

    "AddressExtension": {
      "ShipToStreet": "Lake Street",
      "ShipToStreetNo": "1/33",
      "ShipToCity": "Hyderabad",
      "ShipToZipCode": "500039",
      "ShipToState": "TS",
      "ShipToCountry": "IN",

      "BillToStreet": "Mark street",
      "BillToStreetNo": "RD 200",
      "BillToCity": "Hyderabad",
      "BillToZipCode": "500038",
      "BillToState": "TS",
      "BillToCountry": "IN"
    }
  }
]
```
--------------

### Update Purchase Order

The **Update Purchase Order** action modifies an existing purchase order using the document entry (DocEntry). It allows updating vendor reference details, item lines, and address information.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-UPRORD201.jpg" width="700" />

Click on **Continue** button

-----------

#### Configuration Fields

| Field | Description |
|------|-------------|
| DocEntry | Enter the internal document entry number of the purchase order. (e.g., "39") |
| NumAtCard (Vendor Ref No) | Enter the vendor reference number. (e.g., "728902") |

### Document Lines

| Field | Description |
|------|-------------|
| Line Number | Enter Item Line Number e.g., ("01")|
| Item Code | Unique identifier of the item. (e.g., "DIET002") |
| Quantity | Quantity of the item. (e.g., "20") |
| Unit Price | Price per unit. (e.g., "20") |
| Discount Percentage | Discount applied to the item. (e.g., "3") |
| Tax Code | Applicable tax code. (e.g., "NT") |

### Address Extension (Optional)

#### Ship To Address
| ShipToStreet | Shipping street address e.g., ("Lake Street2")|
| ShipToStreetNo | Street number e.g., ("1/43")|
| ShipToBlock | Block/area e.g., ("")|
| ShipToCity | City e.g., ("Hyderabad")|
| ShipToZipCode | Postal code e.g., ("500037")|
| ShipToCountry | Country e.g., ("IN")|
| ShipToState | State e.g., ("TS")|
| Bill To Address
BillToStreet | Billing street address e.g., ("Mark Spencer street")|
| BillToStreetNo | Street number e.g., ("RDL 233")|
| BillToCity | City e.g., ("Hyderabad")|
| BillToZipCode | Postal code e.g., ("500036")|
| BillToCountry | Country e.g., ("IN")|
| BillToState | State e.g., ("TS")|


> **Note:** Only the fields provided will be updated. Ensure the correct DocEntry is used to avoid modifying the wrong purchase order.

Click on **Continue**, then **Run** the node

-----------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-UPRORD211.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-UPRORD212.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-UPRORD213.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-UPRORD214.jpg" width="700" />

#### Result

```json
[
  {
    "DocEntry": 39,
    "NumAtCard": "728902",
    "DocumentLines": [
      {
        "LineNum": 1,
        "ItemCode": "DIET002",
        "Quantity": 20,
        "UnitPrice": 20,
        "DiscountPercent": 3,
        "TaxCode": "NT"
      }
    ],
    "AddressExtension": {
      "ShipToStreet": "Lake Street2",
      "ShipToStreetNo": "1/43",
      "ShipToBlock": "",
      "ShipToCity": "Hyderabad",
      "ShipToZipCode": "500037",
      "ShipToCountry": "IN",
      "ShipToState": "TS",
      "BillToStreet": "Mark Spencer street",
      "BillToStreetNo": "RDL 233",
      "BillToCity": "Hyderabad",
      "BillToZipCode": "500036",
      "BillToCountry": "IN",
      "BillToState": "TS"
    }
  }
]
```

<img src="\img\credentials\sap-b1\SAP-AR-UPRORD216.jpg" width="700" />

----------------------


## Incoming Payments Action

### Create CreditCard Incoming Payments

The **Create Credit Card Incoming Payments** action records an incoming payment made via credit card for a customer. It captures card details, payment amount, and related information.

#### Select the Credetials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-CCRDPMNT217.jpg" width="700" />

Click on **Continue** button

------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Card Code | Enter the customer code. (e.g., "CUST-001") |
| Credit Card Details
Credit Card | Specify the credit card type. (e.g., "Visa", "MasterCard") |
| Credit Card Number | Enter the credit card number. (e.g., "4111111111111111") |
| Card Valid Until | Enter the card expiry date. (e.g., "12/2028") |
| Voucher | Enter the payment voucher/reference number. (e.g., "VCH-12345") |
| Credit Amount | Enter the payment amount. (e.g., "5000") |
| Optional Fields
Remarks | Add any additional notes related to the payment. (e.g., "Payment received via credit card") |

> **Note:** Ensure credit card details are accurate and valid before processing the payment.


Click on **Continue**, then **Run** node

------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CCRDPMNT216.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CCRDPMNT217.jpg" width="700" />

----------

#### Result

```json
[
  {
    "DocEntry": 517,
    "DocNum": 299,
    "DocType": "rCustomer",
    "DocDate": "2026-04-17",
    "CardCode": "BC6129916",
    "CardName": "MAX6",
    "DocCurrency": "$",
    "Remarks": "Demo Purpose",
    "JournalRemarks": "Incoming Payments - BC6129916",
    "DueDate": "2026-04-17",

    "PaymentCreditCards": [
      {
        "LineNum": 0,
        "CreditCard": 1,
        "CreditCardNumber": "4242",
        "CardValidUntil": "2028-04-19",
        "VoucherNum": "1",
        "PaymentMethodCode": 1,
        "NumOfPayments": 1,
        "FirstPaymentDue": "2026-04-17",
        "CreditSum": 500,
        "CreditCur": "$"
      }
    ],

    "CashFlowAssignments": [
      {
        "PaymentMeans": "pmtCreditCard",
        "CheckNumber": "1",
        "AmountLC": 500
      }
    ]
  }
]
```
---------------

### Create Check Incoming Payments

The **Create Check Incoming Payments** action records an incoming payment made via cheque for a customer. It captures bank details, cheque amount, and related payment information.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-CCKINMGPMNT218.jpg" width="700" />

Click on **Continue** button

-------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Card Code | Enter the customer code. (e.g., "CUST-001") |
| Payment Checks
Cheque Bank Account | Enter the bank account linked to the cheque. (e.g., "HDFC-001") |
| Cheque Amount | Enter the cheque amount. (e.g., "7500") |
| Optional Fields
Cheque Due Date | Specify the cheque clearance date. (e.g., "2026-04-10") |
| Transferable | Indicate if the cheque is transferable (**Yes** or **No**). (e.g., "Yes") |
| Document Due Date | Specify the due date for the payment document. (e.g., "2026-04-15") |
| Remarks | Add any additional notes. (e.g., "Cheque received from customer") |

> **Note:** Ensure cheque details are accurate before processing to avoid payment discrepancies.

Click on **Continue**, then **Run** node

-----------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CCKINCMGPMNT218.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CCKINMGPMNTS219.jpg" width="700" />

---------

#### Result

```json
[
  {
    "DocEntry": 522,
    "DocNum": 301,
    "DocType": "rCustomer",
    "DocDate": "2026-04-17",
    "CardCode": "ZC0001",
    "CardName": "GivaJewellers",
    "DocCurrency": "$",
    "JournalRemarks": "Incoming Payments - ZC0001",
    "DueDate": "2026-04-17",

    "PaymentChecks": [
      {
        "LineNum": 0,
        "DueDate": "2026-04-17",
        "CheckNumber": 1,
        "CheckSum": 500,
        "Currency": "$",
        "CheckAccount": "_SYS00000000006"
      }
    ]
  }
]
```

### Create Cash Incoming Payments

The **Create Cash Incoming Payments** action records an incoming payment made via cash for a customer. It captures customer details, cash account, and payment amount.

#### Select Credentials and Action Events

<img src="\img\credentials\sap-b1\SAP-C-CCASHINCMGPMNTS212.jpg" width="700" />

Click on **Continue** button

--------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| CardCode | Enter the customer code. (e.g., "NR") |
| Cash Account | Specify the cash account to which payment is received. (e.g., "_SYS00000000002") |
| Cash Amount | Enter the amount received in cash. (e.g., "600") |
| Optional Fields
Posting Date | Specify the posting date of the transaction. (e.g., "2026-04-18") |
| Remarks | Add any notes related to the payment. (e.g., "Demo Purpose") |
| Journal Remarks | Enter journal-related remarks for accounting reference. (e.g., "Incoming Payments - ZC0001") |

> **Note:** Ensure the correct cash account and amount are provided to maintain accurate financial records.

Click on **Continue**, then **Run** node

----------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CCASHINCMGPMNTS221.jpg" width="700" />

---------

#### Result

```json
[
  {
    "DocEntry": 522,
    "DocNum": 301,
    "DocType": "rCustomer",
    "DocDate": "2026-04-17",
    "CardCode": "ZC0001",
    "CardName": "GivaJewellers",
    "DocCurrency": "$",
    "JournalRemarks": "Incoming Payments - ZC0001",
    "DueDate": "2026-04-17",

    "PaymentChecks": [
      {
        "LineNum": 0,
        "CheckNumber": 1,
        "DueDate": "2026-04-17",
        "CheckSum": 500,
        "Currency": "$",
        "CheckAccount": "_SYS00000000006"
      }
    ]
  }
]
```

## Delivery Note Actions

### Create a Delivery Note

The **Create Delivery Note** action creates a delivery document in the system for goods being shipped to a customer. It captures delivery, item, and logistics details for order fulfillment.

#### Select Credentials and Action Event

<img src="img\credentials\sap-b1\SAP-C-CDLVRYNT222.jpg" width="700" />

Click on **Continue** button

-------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Document Date | Specify the delivery document date. (e.g., "2026-04-01") |
| Delivery Date | Specify the expected delivery date. (e.g., "2026-04-03") |
| Customer Code | Enter the customer code. (e.g., "CUST-001") |
| Document Lines
Item Code | Unique identifier of the item. (e.g., "ITEM-001") |
| Quantity | Quantity to be delivered. (e.g., "3") |
| Unit Price | Price per unit. (e.g., "1200") |
| Optional Fields (Document Lines)
Warehouse Code | Warehouse from which goods are delivered. (e.g., "WH-01") |
| Tax Code | Applicable tax code. (e.g., "GST18") |
| Discount Percentage | Discount applied to the item. (e.g., "5") |
| VAT Group | VAT classification. (e.g., "VAT18") |
| Base Document Line | Reference to base document line. (e.g., "0") |
| Base Document Type | Base document type reference. (e.g., "17") |
| Base Document Entry | Base document entry reference. (e.g., "14012") |
| Optional Fields (Header)
Contact Person Code | Identifier of the contact person. (e.g., "101") |
| Sales Person Code | Identifier of the sales employee. (e.g., "5") |
| Remarks | Additional notes. (e.g., "Deliver urgently") |
| Customer Reference No | Customer reference number. (e.g., "REF-DEL-001") |
| Ship To Code | Shipping address code. (e.g., "SHIP-01") |
| Bill To Code | Billing address code. (e.g., "BILL-01") |
| Address Extension (Optional)
ShipToStreet | Shipping street address (e.g., "Street 1") |
| ShipToCity | Shipping city (e.g., "Hyderabad") |
| ShipToCountry | Shipping country (e.g., "India") |
| ShipToZipCode | Postal code (e.g., "500001") |
| BillToStreet | Billing street address (e.g., "Street 2") |
| BillToCity | Billing city (e.g., "Hyderabad") |
| BillToCountry | Billing country (e.g., "India") |
| BillToZipCode | Postal code (e.g., "500002") |
| Additional Expenses (Optional)
Additional Expenses | Extra charges such as freight or handling. (e.g., "250") |

> **Note:** Mandatory fields must be provided to create a delivery note. Optional fields can be configured based on business requirements.

Click on **Continue**, then **Run** node

------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CDLVRYNT223.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CDLVRYNT224.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CDLVRYNT225.jpg" width="700" />

----------

#### Result

```json
[
  {
    "DocEntry": 151,
    "DocNum": 65,
    "DocDate": "2026-04-18",
    "DocDueDate": "2026-04-18",
    "CardCode": "ZC0001",
    "CardName": "GivaJewellers",
    "DocTotal": 900,
    "DocCurrency": "$",
    "Comments": "Demo Purpose",
    "JournalMemo": "Deliveries - ZC0001",
    "ShipToCode": "GivaJewellers",
    "DocumentStatus": "bost_Open",

    "DocumentLines": [
      {
        "LineNum": 0,
        "ItemCode": "DIET002",
        "ItemDescription": "PINK-ROSE-Update-Checking data",
        "Quantity": 10,
        "UnitPrice": 100,
        "DiscountPercent": 10,
        "Price": 90,
        "WarehouseCode": "01",
        "TaxCode": "NT",
        "LineTotal": 900,
        "Currency": "$"
      }
    ],

    "AddressExtension": {
      "ShipToStreet": "Adffhgjh",
      "ShipToCity": "Miami",
      "ShipToZipCode": "33144",
      "ShipToState": "FL",
      "ShipToCountry": "US",

      "BillToStreet": "streetNo",
      "BillToCity": "NewYork",
      "BillToZipCode": "10001",
      "BillToState": "NY",
      "BillToCountry": "US"
    }
  }
]
```

### Update a Delivery Note

The **Update Delivery Note** action modifies an existing delivery document using the document entry (DocEntry). It allows updating item details, quantities, pricing, and header information.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-UDLVRYNT226.jpg" width="700" />

Click on **Continue** button

#### Configuration Fields

| Field | Description |
|------|-------------|
| DocEntry | Enter the internal document entry number of the delivery note. (e.g., "151") |
| Customer Code | Enter the Customer Code. (e.g., "ZC0001") |
| Document Lines (Optional)
Line Number | Specify the line number to update. (e.g., "1") |
| Item Code | Update the item code. (e.g., "DIET002") |
| Quantity | Update the quantity. (e.g., "10") |
| Unit Price | Update the unit price. (e.g., "100") |
| Additional Optional Fields (Document Lines)
Warehouse Code | Warehouse from which goods are delivered. (e.g., "01") |
| Tax Code | Applicable tax code. (e.g., "NT") |
| Optional Fields (Header)
Contact Person Code | Identifier of the contact person. (e.g., "102") |
| Sales Person Code | Identifier of the sales employee. (e.g., "6") |
| Remarks | Additional notes. (e.g., "Demo Purpose Update") |
| Customer Reference No | Customer reference number. (e.g., "REF-DEL-002") |
| Ship To Code | Shipping address code. (e.g., "SHIP-02") |
| Bill To Code | Billing address code. (e.g., "BILL-02") |
| Address Extension (Optional)
ShipToStreet | Shipping street address (e.g., "Street A") |
| ShipToCity | Shipping city (e.g., "Chennai") |
| ShipToCountry | Shipping country (e.g., "India") |
| ShipToZipCode | Postal code (e.g., "600001") |
| BillToStreet | Billing street address (e.g., "Street B") |
| BillToCity | Billing city (e.g., "Chennai") |
| BillToCountry | Billing country (e.g., "India") |
| BillToZipCode | Postal code (e.g., "600002") |
| Additional Expenses (Optional)
Additional Expenses | Extra charges such as freight or handling. (e.g., "200") |

> **Note:** Only the fields provided will be updated. Ensure the correct DocEntry is used to avoid modifying the wrong delivery note.

Click on **Continue**, then **Run** node

---------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-UDLVRYNT227.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-UDLVRYNT228.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-UDLVRYNT229.jpg" width="700" />

---------------

#### Result

```json
[
  {
    "DocEntry": 151,
    "CardCode": "ZC0001",
    "Comments": "Demo Purpose Update",
    "NumAtCard": "REF-DEL-002",
    "DocumentLines": [
      {
        "LineNum": 1,
        "ItemCode": "DIET002",
        "Quantity": 10,
        "UnitPrice": 100,
        "WarehouseCode": "01",
        "TaxCode": "NT"
      }
    ],
    "AddressExtension": {
      "ShipToStreet": "Street A",
      "ShipToCity": "Chennai",
      "ShipToCountry": "India",
      "ShipToZipCode": "600001",
      "BillToStreet": "Street B",
      "BillToCity": "Chennai",
      "BillToCountry": "India",
      "BillToZipCode": "600002"
    }
  }
]
```

<img src="\img\credentials\sap-b1\SAP-AR-UDLVRYNT229.jpg" width="700" />


### Get Delivery by Order DocEntry

The **Get Delivery by Order DocEntry** action retrieves delivery note details associated with a specific sales order using the order's document entry number. It returns the related delivery document(s) as structured data.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-GDLVRYNTbyDOCENTRYNO229.jpg" width="700" />

Click on **Continue** button

------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Order DocEntry | Enter the internal document entry number of the sales order. (e.g., "1876") |

> **Note:** If no delivery notes are linked to the provided Order DocEntry, the output will be empty or null. If multiple deliveries exist, the system may return one or a list based on configuration.

Click on **Continue**, then **Run** node

---------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-GDLVRYNTbyDOCENTRYNO230.jpg" width="700" />

------------

#### Result

```json
[
  {
    "DeliveryNotes": {
      "DocEntry": 134,
      "DocNum": 59,
      "NumAtCard": null
    },
    "DeliveryNotes/DocumentLines": {
      "ItemCode": "TV654",
      "ItemDescription": "LG OLED55C2PUA 55-inch OLED TV",
      "Quantity": 100,
      "ShipDate": "2025-11-29",
      "BaseType": 17,
      "BaseEntry": 1876
    }
  }
]
```
--------------

### Get Delivery by NumAtCard

The **Get Delivery by Customer Reference Number** action retrieves delivery note details using the customer reference number (`NumAtCard`). It returns the matching delivery document(s) as structured data.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-GDLVRYNTbyNumAtCard231.jpg" width="700" />

Click on **Continue** button

#### Configuration Fields

| Field | Description |
|------|-------------|
| NumAtCard | Enter the customer reference number associated with the delivery. (e.g., "1564") |

> **Note:** If multiple delivery notes match the provided reference number, the system may return a single record or a list based on configuration. If no match is found, the output will be empty or null.

Click on **Continue**, then **Run** node

--------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-GDLVRYNTbyNumAtCard232.jpg" width="700" />

-----------

#### Result

```json
[
  {
    "DocEntry": 108,
    "DocNum": 45,
    "DocDate": "2025-03-11",
    "DocDueDate": "2025-03-11",
    "CardCode": "DEMOBP111",
    "CardName": "SuccessVector Customer1",
    "DocTotal": 7650,
    "DocCurrency": "$",
    "Comments": "Based On Sales Orders 426.",
    "JournalMemo": "Deliveries - DEMOBP111",
    "DocumentStatus": "bost_Open",

    "DocumentLines": [
      {
        "LineNum": 0,
        "ItemCode": "DEMO808",
        "ItemDescription": "WATERMELON-01",
        "Quantity": 5,
        "UnitPrice": 720,
        "WarehouseCode": "01",
        "TaxCode": "EXEMPT",
        "LineTotal": 3600,
        "BaseType": 17,
        "BaseEntry": 913,
        "BaseLine": 0
      },
      {
        "LineNum": 1,
        "ItemCode": "DEMO909",
        "ItemDescription": "Rooseberry-BLUE",
        "Quantity": 5,
        "UnitPrice": 810,
        "WarehouseCode": "01",
        "TaxCode": "EXEMPT",
        "LineTotal": 4050,
        "BaseType": 17,
        "BaseEntry": 913,
        "BaseLine": 1
      }
    ],

    "AddressExtension": {
      "ShipToCity": "Hyderabad",
      "ShipToZipCode": "500002",
      "ShipToState": "TS",
      "ShipToCountry": "IN",

      "BillToCity": "Hyderabad",
      "BillToZipCode": "500038",
      "BillToState": "AP",
      "BillToCountry": "IN"
    }
  }
]
```
----------

## DownPayment Actions

The **Create Down Payment** action creates a down payment document for a customer. It is used to record advance payments before the final invoice is generated.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-CDNPMNTINVC231.jpg" width="700" />

Click on **Continue** button

----------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Doc Date | Specify the document date. (e.g., "2026-04-18") |
| DocDueDate | Specify the due date. (e.g., "2026-04-18") |
| Card Code | Enter the customer code. (e.g., "POST321") |
| Document Lines
Item Code | Unique identifier of the item. (e.g., "LT001") |
| Quantity | Quantity of the item. (e.g., "10") |
| Optional Fields (Document Lines)
Unit Price | Price per unit. (e.g., "100") |
| Tax Code | Applicable tax code. (e.g., "NT") |
| Discount Percentage | Discount applied. (e.g., "5") |

> **Note:** Down payments are typically used for advance billing. Ensure correct customer and pricing details before creating the document.

Click on **Continue**, then **Run** node

--------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CDNPAMNTINV232.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CDNPAMNTINV233.jpg" width="700" />

-------------

#### Result

```json
{
  "DocDate": "2026-04-18",
  "CardCode": "POST321",
  "DownPaymentType": "dptInvoice",
  "DownPaymentPercentage": 100,
  "DocumentLines": [
    {
      "ItemCode": "LT001",
      "Quantity": 10,
      "UnitPrice": 100,
      "DiscountPercent": 5,
      "WarehouseCode": "01"
    }
  ]
}
```
----------------

## SalesForecast Action

### Create a SalesForecast

The **Create Sales Forecast** action is used to define future sales expectations for items over a specified period. It helps in planning inventory, production, and business strategies.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-CSLSFRCST239.jpg" width="700" />

Click on **Continue** button

--------------------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Forecast Code | Unique identifier for the forecast. (e.g., "FC-001") |
| Forecast Name | Name of the forecast. (e.g., "Q2 Sales Forecast") |
| Optional Fields
Forecast Start Date | Start date of the forecast period. (e.g., "2026-04-01") |
| Forecast End Date | End date of the forecast period. (e.g., "2026-06-30") |
| Sales Forecast Lines
Item Code | Unique identifier of the item. (e.g., "ITEM-001") |
| Quantity | Forecasted quantity. (e.g., "100") |
| Sales Forecasted Day | Date for the forecast entry. (e.g., "2026-04-15") |
| Optional Fields (Forecast Lines)
Warehouse | Warehouse related to the forecast. (e.g., "WH-01") |
| Forecast View | Defines how forecast is viewed (e.g., "Monthly", "Daily") |

> **Note:** Forecast lines are essential for defining item-level predictions. Optional fields can be configured based on planning requirements.

Click on **Continue**, then **Run** node

-------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CSLSFRCST240.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CSLSFRCST241.png" width="700" />

----------------

#### Result

```json
[
  {
    "odata.metadata": "https://insync.pro/b1s/v1/$metadata#SalesForecast/@Element",
    "ForecastStartDate": "2026-04-19",
    "ForecastEndDate": "2026-04-28",
    "ForecastCode": "D022",
    "ForecastName": "For Daily forecast3",
    "Numerator": 42,
    "View": "fvtDaily",
    "SalesForecastLines": []
  }
]
```

### Update SalesForecast

The **Update Sales Forecast** action is used to modify an existing sales forecast using its unique identifier. It allows updating forecast details and item-level forecast data.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-USLSFRCS242.jpg" width="700" />

Click on **Continue** button

--------------------

#### Configuration

| Field | Description |
|------|-------------|
| Id (Numerator) | Enter the unique identifier of the forecast. (e.g., "1001") |
| Optional Fields
Forecast Name | Update the name of the forecast. (e.g., "Updated Q2 Forecast") |
| Forecast Start Date | Update the start date of the forecast period. (e.g., "2026-04-01") |
| Forecast End Date | Update the end date of the forecast period. (e.g., "2026-06-30") |
| Sales Forecast Lines (Optional)
Item Code | Unique identifier of the item. (e.g., "ITEM-002") |
| Quantity | Updated forecasted quantity. (e.g., "150") |
| Sales Forecasted Day | Date for the forecast entry. (e.g., "2026-05-01") |
| Additional Optional Fields
Warehouse | Warehouse related to the forecast. (e.g., "WH-02") |

> **Note:** Only the provided fields will be updated. Ensure the correct forecast Id is used to avoid modifying the wrong forecast data.

Click on **Continue**, then **Run** node

------------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-USLSFRCST243.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-USLSFRCST244.jpg" width="700" />

-----------------

#### Result

```json
[
  {
    "value": ""
  }
]
```

<img src="" width="700" />

---------------

### Get Sales Forecast by Id

The **Get Sales Forecast by Id** action retrieves details of a specific sales forecast using its unique identifier (Numerator). It returns forecast header and line-level data.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-GSLSFRCSTbyId245.jpg" width="700" />

Click on **Continue** button

---------------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Id (Numerator) | Enter the unique identifier of the sales forecast. (e.g., "42") |

> **Note:** If no forecast exists for the provided Id, the response will be empty or null.

Click on **Continue**, then **Run** node

--------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-GSLSFRCSTbyId246.jpg" width="700" />

---------------

#### Result

```json
[
  {
    "odata.metadata": "https://insync.pro/b1s/v1/$metadata#SalesForecast/@Element",
    "ForecastStartDate": "2026-04-19",
    "ForecastEndDate": "2026-04-28",
    "ForecastCode": "D022",
    "ForecastName": "For Daily forecast333-Latest",
    "Numerator": 42,
    "View": "fvtDaily",
    "SalesForecastLines": [
      {
        "Quantity": 11,
        "ForecastedDay": "2026-04-19",
        "ItemNo": "DIET002",
        "Warehouse": "01"
      }
    ]
  }
]
```

## PaymentDraft Actions

### Create Payment Draft

The **Create Payment Draft** action is used to create a draft payment document (incoming or outgoing). It allows users to save payment details for review before final posting.

#### Select Credentials and Payments

<img src="\img\credentials\sap-b1\SAP-C-CDRFTPAMNT247.jpg" width="700" />

Click on **Continue** button

--------------------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Payment Type | Select the type of payment. (e.g., "Incoming Payment" or "Outgoing Payment") |
| Card Code | Enter the customer/vendor code. (e.g., "CUST-001") |
| Optional Fields
Document Date | Specify the document date. (e.g., "2026-04-01") |
| Tax Date | Specify the tax date. (e.g., "2026-04-01") |
| Due Date | Specify the due date. (e.g., "2026-04-05") |
| Remarks | Add any notes related to the payment. (e.g., "Draft payment created") |
| Journal Remarks | Enter accounting-related remarks. (e.g., "Payment Draft Entry") |
| Cash Amount | Enter the cash amount for the payment. (e.g., "1000") |

> **Note:** Draft payments can be reviewed and finalized later. Mandatory fields must be provided to create the draft successfully.

Click on **Continue**, then **Run** node

----------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CDRFTPAMNTS248.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CDRFTPAMNTS249.jpg" width="700" />

-------------

#### Result

```json
[
  {
    "DocEntry": 30,
    "DocNum": 308,
    "DocType": "rCustomer",
    "DocDate": "2026-04-19",
    "DueDate": "2026-04-19",

    "CardCode": "ZC0001",
    "CardName": "GivaJewellers",

    "DocCurrency": "$",
    "CashAccount": "_SYS00000000002",
    "CashSum": 600,

    "Remarks": "Demo Purpose",
    "JournalRemarks": "Incoming Payment",

    "PaymentType": "bopt_None",

    "CashFlowAssignments": [
      {
        "PaymentMeans": "pmtCash",
        "AmountLC": 600,
        "AmountFC": 0
      }
    ]
  }
]
```

### Get Payment Draft by DocEntry

The **Get Payment Draft by DocEntry** action retrieves details of a specific payment draft using its internal document entry number. It returns the draft payment information as structured data.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-GDRFTPAMNTbyDOCENTRY249.jpg" width="700" />

Click on **Continue** button

----------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| DocEntry | Enter the internal document entry number of the payment draft. (e.g., "30012") |

> **Note:** If no draft exists for the provided DocEntry, the response will be empty or null.

Click on **Continue**, then **Run** node

-----------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CDRFTPAMNTbyDOCENTRY250.jpg" width="700" />

---------------

#### Result

```json
{
  "DocType": "rCustomer",
  "DocDate": "2026-04-19",
  "TaxDate": "2026-04-19",
  "DueDate": "2026-04-19",
  "CardCode": "ZC0001",
  "Remarks": "Demo Purpose",
  "JournalRemarks": "Incoming Payment",

  "CashAccount": "_SYS00000000002",
  "CashSum": 600,

  "DocCurrency": "$",

  "CashFlowAssignments": [
    {
      "PaymentMeans": "pmtCash",
      "AmountLC": 600
    }
  ]
}
```

### Convert Payment Draft to Incoming Payment

The **Convert Payment Draft to Incoming Payment** action converts an existing payment draft into a finalized incoming payment. This is typically done after reviewing and confirming the draft details.

#### Select Crdentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-ConvertdrafttoIncomingPayments251.jpg" width="700" />

Click on **Continue** button

----------------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| DocEntry | Enter the internal document entry number of the payment draft. (e.g., "30012") |

> **Note:** Once converted, the draft becomes a posted incoming payment and may no longer be editable as a draft. Ensure all details are verified before conversion.

Click on **Continue**, then **Run** node

---------------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-ConvertdrafttoIncomingPayment251.jpg" width="700" />

-------

#### Result

```json
[
  {
    "value": ""
  }
]
```

<img src="\img\credentials\sap-b1\SAP-AR-ConvertdrafttoIncomingPayment252.jpg" width="700" />

------------

## Blanket Agreements Actions

### Create Sales Blanket Agreement

The **Create Sales Blanket Agreement** action is used to define long-term agreements with customers for supplying goods or services under predefined terms. It helps in managing recurring sales with agreed pricing and quantities.

#### Select Credentials and Action Event

<img src="\img\credentials\sap-b1\SAP-C-BLNKARGEMNT253.jpg" width="700" />

Click on **Continue** button

--------------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Agreement Type | Specify the type of agreement. (e.g., "atGeneral") |
| BP Code | Enter the business partner (customer) code. (e.g., "ZC0001") |
| Agreement Method | Define how the agreement is managed. (e.g., "amItem") |
| End Date | Specify the agreement end date. (e.g., "2026-04-20") |
| Agreement Item Lines
Item No | Unique identifier of the item. (e.g., "DIET002") |
| Optional Fields (Item Lines)
Planned Quantity | Planned quantity for the agreement. (e.g., "4") |
| Unit Price | Agreed price per unit. (e.g., "100") |
| Line Discount | Discount applied on the item. (e.g., "2") |
| Optional Fields (Header)
BP Name | Name of the business partner. (e.g., "GivaJewellers") |
| NumAtCard | Customer reference number. (e.g., "664111000000360085") |
| Contact Person Code | Identifier of the contact person. (e.g., "4") |
| Remarks | Additional notes. (e.g., "Demo Purpose") |

> **Note:** Blanket agreements are used for long-term contracts. Ensure correct pricing and quantities are defined before creating the agreement.

Click on **Continue**, then **Run** node

--------------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-CBLNKTAGREMENT255.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CBLNKTAGREMENT256.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-CBLNKTAGREMENT257.jpg" width="700" />

-----------------------

#### Result

```json
{
  "BPCode": "ZC0001",
  "StartDate": "2026-04-19",
  "EndDate": "2026-04-20",
  "AgreementType": "atGeneral",
  "AgreementMethod": "amItem",
  "PriceMode": "pmNet",
  "BPCurrency": "$",
  "Remarks": "Demo Purpose",

  "BlanketAgreements_ItemsLines": [
    {
      "ItemNo": "DIET002",
      "PlannedQuantity": 4,
      "UnitPrice": 100,
      "PriceCurrency": "$"
    }
  ]
}
```

### Update Sales Blanket Agreement

The **Update Sales Blanket Agreement** action is used to modify an existing blanket agreement using its agreement number. It allows updating business partner details, agreement validity, and item-level terms.

#### Select Credentials and Action Events

<img src="\img\credentials\sap-b1\SAP-C-USLSBLANKTAGREMENT258.jpg" width="700" />

Click on **Continue** button

------------------------

#### Configuration Fields

| Field | Description |
|------|-------------|
| Agreement No | Enter the unique agreement number. (e.g., "5001") |
| Optional Fields (Header)
BP Code | Update the business partner code. (e.g., "CUST-002") |
| BP Name | Update the business partner name. (e.g., "XYZ Pvt Ltd") |
| NumAtCard | Customer reference number. (e.g., "REF-BA-002") |
| Remarks | Additional notes. (e.g., "Updated agreement terms") |
| End Date | Update the agreement end date. (e.g., "2027-12-31") |
| Agreement Item Lines
Agreement Row Number | Specify the line number to update. (e.g., "1") |
| Optional Fields (Item Lines)
Item No | Update the item code. (e.g., "ITEM-002") |
| Planned Quantity | Update the planned quantity. (e.g., "1500") |
| Unit Price | Update the unit price. (e.g., "550") |
| Line Discount | Update the discount percentage. (e.g., "10") |

> **Note:** Only the provided fields will be updated. Ensure the correct Agreement No and row number are used to avoid unintended changes.

Click on **Continue**, then **Run** node

-----------------

#### Example Configuration

<img src="\img\credentials\sap-b1\SAP-AC-USLABLANKTAGREMENT258.jpg" width="700" />
<img src="\img\credentials\sap-b1\SAP-AC-USLSBLNKTAGREMENT259.jpg" width="700" />

-------------

#### Result

```json
[
  {
    "value": ""
  }
]
```

<img src="\img\credentials\sap-b1\SAP-AR-USLSBLNKTAGREMENT260.jpg" width="700" />




































































### Actions

> Quotations Actions

- Get list of Quotations with filtering and sorting options

> Invoices Actions

- Create AR Invoice
- Create AR Reserve Invoice

> Drafts Actions

- Create Drafts
- Update an existing Draft
- Get list of Drafts with filtering and sorting options
- Delete Draft

> Orders Actions

- Get list of Orders with filtering and sorting options
- Update an existing Sales Order
- Create a Sales Order

> Down Payments Actions

- Update an existing Down Payment
- Create a new Down Payment Invoice
- Get list of Down Payments with filtering and sorting options

> Invoice Actions

- Create an Invoice
- Update an existing Invoice

> Business Partners Actions

- Get list of BusinessPartners with filtering and sorting options
- Create a new BusinessPartner
- Update an existing BusinessPartner

> Items Actions

- Delete Item
- Update Item
- Create a new Item
- Get list of Items

> Credit Notes Actions

- Create AR Credit Memo

</TabItem>
</Tabs>

---

## Need Help?

If youâ€™re unsure about any field or face connection issues, reach out to our support team at hello@appse.ai


