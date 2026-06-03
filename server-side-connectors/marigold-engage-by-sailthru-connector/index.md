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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

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
|Sailthru List|  &lt;ul&gt;&lt;li&gt;Primary or Secondary List to add User to.&lt;/li&gt;&lt;/ul&gt; |
|User Facebook ID|  &lt;ul&gt;&lt;li&gt;Map to User Facebook ID&lt;/li&gt;&lt;/ul&gt; |
|Sailthru Horizon Cookie|  &lt;ul&gt;&lt;li&gt;Map to Sailthru Horizon Cookie&lt;/li&gt;&lt;/ul&gt; |
|User SMS|  &lt;ul&gt;&lt;li&gt;Map to User SMS&lt;/li&gt;&lt;/ul&gt; |
|User Specified Identifier|  &lt;ul&gt;&lt;li&gt;Map to User-Specified Identifier&lt;/li&gt;&lt;/ul&gt; |
|User Email|  &lt;ul&gt;&lt;li&gt;Map to User Email&lt;/li&gt;&lt;/ul&gt; |
|User Twitter Name|  &lt;ul&gt;&lt;li&gt;Map to User X Name&lt;/li&gt;&lt;/ul&gt; |
|Sailthru Identifier|  &lt;ul&gt;&lt;li&gt;Map to Sailthru Identifier&lt;/li&gt;&lt;/ul&gt; |

### Action - Remove User from List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Sailthru List|  &lt;ul&gt;&lt;li&gt;Primary or Secondary List to remove User from&lt;/li&gt;&lt;/ul&gt; |
|User Facebook ID|  &lt;ul&gt;&lt;li&gt;Map to User Facebook ID&lt;/li&gt;&lt;/ul&gt; |
|Sailthru Horizon Cookie|  &lt;ul&gt;&lt;li&gt;Map to Sailthru Horizon Cookie&lt;/li&gt;&lt;/ul&gt; |
|User SMS|  &lt;ul&gt;&lt;li&gt;Map to User SMS&lt;/li&gt;&lt;/ul&gt; |
|User Specified Identifier|  &lt;ul&gt;&lt;li&gt;Map to User-Specified Identifier&lt;/li&gt;&lt;/ul&gt; |
|User Email|  &lt;ul&gt;&lt;li&gt;Map to User Email&lt;/li&gt;&lt;/ul&gt; |
|User Twitter Name|  &lt;ul&gt;&lt;li&gt;Map to User X Name&lt;/li&gt;&lt;/ul&gt; |
|Sailthru Identifier|  &lt;ul&gt;&lt;li&gt;Map to Sailthru Identifier&lt;/li&gt;&lt;/ul&gt; |

### Action - Add User to List (Batch Job)

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter**             | **Description**                                                                     |
| ------------------------- | ----------------------------------------------------------------------------------- |
| Sailthru List             | &lt;ul&gt;&lt;li&gt;Select one or more lists to add user to.&lt;/li&gt;&lt;/ul&gt;                          |
| User Facebook ID          | &lt;ul&gt;&lt;li&gt;Map to User Facebook ID&lt;/li&gt;&lt;/ul&gt;                                           |
| Sailthru Horizon Cookie   | &lt;ul&gt;&lt;li&gt;Map to Sailthru Horizon Cookie&lt;/li&gt;&lt;/ul&gt;                                    |
| User SMS                  | &lt;ul&gt;&lt;li&gt;Map to User SMS&lt;/li&gt;&lt;/ul&gt;                                                   |
| User Specified Identifier | &lt;ul&gt;&lt;li&gt;Map to User-Specified Identifier&lt;/li&gt;&lt;/ul&gt;                                  |
| User Email                | &lt;ul&gt;&lt;li&gt;Map to User Email&lt;/li&gt;&lt;/ul&gt;                                                 |
| User Twitter Name         | &lt;ul&gt;&lt;li&gt;Map to User X Name&lt;/li&gt;&lt;/ul&gt;                                          |
| Sailthru Identifier       | &lt;ul&gt;&lt;li&gt;Map to Sailthru Identifier&lt;/li&gt;&lt;/ul&gt;                                        |
| User Custom Variables     | &lt;ul&gt;&lt;li&gt;Set custom variables on the user.&lt;/li&gt;&lt;/ul&gt;                                 |
| Opt Out                   | &lt;ul&gt;&lt;li&gt;Must be one of the following: `all`, `basic`, `blast` or `none`&lt;/li&gt;&lt;/ul&gt; |
| Signup date               | &lt;ul&gt;&lt;li&gt;User signup date.&lt;/li&gt;&lt;/ul&gt;                                                 |

### Action - Remove User from List (Batch Job)

##### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Sailthru List|  &lt;ul&gt;&lt;li&gt;Select one or more lists to remove user from.&lt;/li&gt;&lt;/ul&gt; |
|User Facebook ID|  &lt;ul&gt;&lt;li&gt;Map to User Facebook ID&lt;/li&gt;&lt;/ul&gt; |
|Sailthru Horizon Cookie|  &lt;ul&gt;&lt;li&gt;Map to Sailthru Horizon Cookie&lt;/li&gt;&lt;/ul&gt; |
|User SMS|  &lt;ul&gt;&lt;li&gt;Map to User SMS&lt;/li&gt;&lt;/ul&gt; |
|User Specified Identifier|  &lt;ul&gt;&lt;li&gt;Map to User-Specified Identifier&lt;/li&gt;&lt;/ul&gt; |
|User Email|  &lt;ul&gt;&lt;li&gt;Map to User Email&lt;/li&gt;&lt;/ul&gt; |
|User Twitter Name|  &lt;ul&gt;&lt;li&gt;Map to User X Name&lt;/li&gt;&lt;/ul&gt; |
|Sailthru Identifier|  &lt;ul&gt;&lt;li&gt;Map to Sailthru Identifier&lt;/li&gt;&lt;/ul&gt; |
|User Custom Variables|  &lt;ul&gt;&lt;li&gt;Set custom variables on the user.&lt;/li&gt;&lt;/ul&gt; |
|Opt Out|  &lt;ul&gt;&lt;li&gt;Must be one of the following: `all`, `basic`, `blast` or `none`&lt;/li&gt;&lt;/ul&gt; |
|Signup date|  &lt;ul&gt;&lt;li&gt;User signup date.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Transactional Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|To|  &lt;ul&gt;&lt;li&gt;Email address of user to receive this email&lt;/li&gt;&lt;/ul&gt; |
|Email Template|  &lt;ul&gt;&lt;li&gt;Email to send to user&lt;/li&gt;&lt;/ul&gt; |
|Email Variable Substitutions|  &lt;ul&gt;&lt;li&gt;Replace variables in the provided email template with your Tealium data.&lt;/li&gt;&lt;li&gt;This will overwrite variables stored on the user.&lt;/li&gt;&lt;li&gt;Conversely, a variable that is not assigned defaults to what is stored on the user.&lt;/li&gt;&lt;/ul&gt; |
|Email List Substitutions|  &lt;ul&gt;&lt;li&gt;Requires array type in data layer.&lt;/li&gt;&lt;li&gt;The data is formatted correctly to be passed.&lt;/li&gt;&lt;li&gt;Replace list variables in the provided email template with your Tealium data.&lt;/li&gt;&lt;li&gt;This will overwrite variables stored on the user.&lt;/li&gt;&lt;li&gt;Conversely, a variable that is not assigned defaults to what is stored on the user.&lt;/li&gt;&lt;/ul&gt; |
