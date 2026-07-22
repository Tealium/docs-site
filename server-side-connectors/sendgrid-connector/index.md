---
title: SendGrid Connector Setup Guide
description: This article describes how to set up the SendGrid connector.
url: https://docs.tealium.com/server-side-connectors/sendgrid-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Upsert Contact| ✓| ✗|
|Remove Contact| ✓| ✗|
|Send Email| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. See the [Connector Overview](https://docs.tealium.com/server-side/connectors/manage/) for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**  
API Key for SendGrid Connector to use. This connector requires the following permissions for the API Key:

  * **Marketing Campaigns:** Full Access
  * **Mail Send:** Full Access
  * **Template Engine:** Read Access

For more information on SendGrid API Keys please view the following documentation: [SendGrid API Keys](https://docs.sendgrid.com/ui/account-and-settings/api-keys).

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Upsert Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Address Line 1|
|Address Line 2|
|Alternate Emails|
|City|
|Country|
|Email| (Required)|
|First Name|
|Last Name|
|Postal Code|
|State Province Region|
|Contact List Ids| (Optional) List IDs. An array of List ID strings that this contact will be added to.|

### Action - Remove Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact Id|
|Email|

### Action - Send Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Name| (Required)|
|Send At|
|Send To All|
|Custom Unsubscribe Url|
|Editor|
|Generate Plain Content|
|HTML Content|
|Ip Pool|
|Plain Content|
|Subject|
|Categories| (Optional) Categories. The categories to associate with this Single Send. Max items 10.|
|Contact List Ids| (Optional) Contact List IDs. The recipient List IDs that will receive the Single Send. Max items 10.|
|Segments| (Optional) Segments. The recipient Segment IDs that will receive the Single Send. Max items 10.|
|Design Id| (Optional) Design ID. A Design Id can be used in place of **Html Content**, **Plain Content**, and/or **subject**.|
|Sender Id| (Optional) Sender ID. The ID of the verified Sender.|
|Suppression Group Id| (Optional) Suppression Group ID. The ID of the Suppression Group to allow recipients to unsubscribe — you must provide this or the **Custom Unsubscribe Url**.|
