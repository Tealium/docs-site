---
title: Marigold Engage by Sailthru Connector Setup Guide
description: This article describes how to set up the Sailthru connector.
url: https://docs.tealium.com/server-side-connectors/marigold-engage-by-sailthru-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add User to List| ✓| ✗|
|Remove User from List| ✓| ✗|
|Add User to List (Batch Job)| ✓| ✗|
|Remove User from List (Batch Job)| ✓| ✗|
|Send Transactional Email| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**
  * API Key to access Sailthru account features.

* **Shared Secret**
  * Sailthru account shared secret.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Add User to List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Sailthru List|  <ul><li>Primary or Secondary List to add User to.</li></ul> |
|User Facebook ID|  <ul><li>Map to User Facebook ID</li></ul> |
|Sailthru Horizon Cookie|  <ul><li>Map to Sailthru Horizon Cookie</li></ul> |
|User SMS|  <ul><li>Map to User SMS</li></ul> |
|User Specified Identifier|  <ul><li>Map to User-Specified Identifier</li></ul> |
|User Email|  <ul><li>Map to User Email</li></ul> |
|User Twitter Name|  <ul><li>Map to User X Name</li></ul> |
|Sailthru Identifier|  <ul><li>Map to Sailthru Identifier</li></ul> |

### Action - Remove User from List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Sailthru List|  <ul><li>Primary or Secondary List to remove User from</li></ul> |
|User Facebook ID|  <ul><li>Map to User Facebook ID</li></ul> |
|Sailthru Horizon Cookie|  <ul><li>Map to Sailthru Horizon Cookie</li></ul> |
|User SMS|  <ul><li>Map to User SMS</li></ul> |
|User Specified Identifier|  <ul><li>Map to User-Specified Identifier</li></ul> |
|User Email|  <ul><li>Map to User Email</li></ul> |
|User Twitter Name|  <ul><li>Map to User X Name</li></ul> |
|Sailthru Identifier|  <ul><li>Map to Sailthru Identifier</li></ul> |

### Action - Add User to List (Batch Job)

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter**             | **Description**                                                                     |
| ------------------------- | ----------------------------------------------------------------------------------- |
| Sailthru List             | <ul><li>Select one or more lists to add user to.</li></ul>                          |
| User Facebook ID          | <ul><li>Map to User Facebook ID</li></ul>                                           |
| Sailthru Horizon Cookie   | <ul><li>Map to Sailthru Horizon Cookie</li></ul>                                    |
| User SMS                  | <ul><li>Map to User SMS</li></ul>                                                   |
| User Specified Identifier | <ul><li>Map to User-Specified Identifier</li></ul>                                  |
| User Email                | <ul><li>Map to User Email</li></ul>                                                 |
| User Twitter Name         | <ul><li>Map to User X Name</li></ul>                                          |
| Sailthru Identifier       | <ul><li>Map to Sailthru Identifier</li></ul>                                        |
| User Custom Variables     | <ul><li>Set custom variables on the user.</li></ul>                                 |
| Opt Out                   | <ul><li>Must be one of the following: `all`, `basic`, `blast` or `none`</li></ul> |
| Signup date               | <ul><li>User signup date.</li></ul>                                                 |

### Action - Remove User from List (Batch Job)

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Sailthru List|  <ul><li>Select one or more lists to remove user from.</li></ul> |
|User Facebook ID|  <ul><li>Map to User Facebook ID</li></ul> |
|Sailthru Horizon Cookie|  <ul><li>Map to Sailthru Horizon Cookie</li></ul> |
|User SMS|  <ul><li>Map to User SMS</li></ul> |
|User Specified Identifier|  <ul><li>Map to User-Specified Identifier</li></ul> |
|User Email|  <ul><li>Map to User Email</li></ul> |
|User Twitter Name|  <ul><li>Map to User X Name</li></ul> |
|Sailthru Identifier|  <ul><li>Map to Sailthru Identifier</li></ul> |
|User Custom Variables|  <ul><li>Set custom variables on the user.</li></ul> |
|Opt Out|  <ul><li>Must be one of the following: `all`, `basic`, `blast` or `none`</li></ul> |
|Signup date|  <ul><li>User signup date.</li></ul> |

### Action - Send Transactional Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|To|  <ul><li>Email address of user to receive this email</li></ul> |
|Email Template|  <ul><li>Email to send to user</li></ul> |
|Email Variable Substitutions|  <ul><li>Replace variables in the provided email template with your Tealium data.</li><li>This will overwrite variables stored on the user.</li><li>Conversely, a variable that is not assigned defaults to what is stored on the user.</li></ul> |
|Email List Substitutions|  <ul><li>Requires array type in data layer.</li><li>The data is formatted correctly to be passed.</li><li>Replace list variables in the provided email template with your Tealium data.</li><li>This will overwrite variables stored on the user.</li><li>Conversely, a variable that is not assigned defaults to what is stored on the user.</li></ul> |
