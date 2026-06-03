---
title: Snapchat Customer Lists (formerly Snapchat Audience Match) Connector Setup Guide
description: This article describes how to set up the Snapchat Customer Lists (formerly Snapchat Audience Match) connector using Tealium-provided credentials.
url: https://docs.tealium.com/server-side-connectors/snapchat-customer-lists-connector/
---
Snap Customer Lists allow an advertiser to use first-party data to create an audience segment. The segment can be used to target or exclude a specific group of users.

## Prerequisites

* After adding the connector, you must invite [asintegrations@tealium.com](mailto:%22asintegrations@tealium.com) to your Snapchat Business manager with the **Member** role and assign to applicable Ad Account with the **Data Manager** role.
This step may take up to 3 working days for approval. You can confirm whether the invitation has been accepted by viewing the users in your Snapchat Ads account.
For additional information, see: [Manage Members and Roles](https://businesshelp.snapchat.com/s/topic/0TO0y000000YVcVGAW/manage-members-and-roles).

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 50000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

## Connector Actions

| **Action Name**          | **AudienceStream** | **EventStream** |
|:-------------------------|:-------------------|:----------------|
| Add User to Segment      | ✓                  | ✓               |
| Remove User from Segment | ✓                  | ✓               |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](/server-side/connectors/manage/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Ad Account ID**
  * (Required) Provide the Ad Account ID found under the Ad Accounts section of your Snapchat Business Settings.
  * Invite [asintegrations@tealium.com](mailto:asintegrations@tealium.com) to your Snapchat Business manager with the **Member** role and assign to applicable Ad Account with **Data Manager** role.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Add User to Segment

#### Parameters

| **Parameter**                  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|:-------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Segment                        | &lt;ul&gt;&lt;li&gt;Target segment to add user to.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| User Identifier Type           | &lt;ul&gt;&lt;li&gt;User Identifiers can be of type **Email**, **Mobile Ad ID**, or **Phone number**.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| User Identifier                | &lt;ul&gt;&lt;li&gt;User Identifiers can be passed as plain text or already normalized and hashed.  &lt;ul&gt;&lt;li&gt;You can normalize email addresses by trimming the leading and trailing whitespace and converting all characters to lowercase before hashing.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Normalize the Mobile Advertiser ID  &lt;ul&gt;&lt;li&gt;Use all lowercase letters.&lt;/li&gt;&lt;li&gt;Do not remove hyphens.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Normalize phone numbers  &lt;ul&gt;&lt;li&gt;Include the country code.&lt;/li&gt;&lt;li&gt;Remove any double zeros (`0`) in front of the country code.&lt;/li&gt;&lt;li&gt;If the number itself begins with a zero (`0`), this should be removed.&lt;/li&gt;&lt;li&gt;Exclude any non-numeric characters such as whitespace, parentheses, plus signs (**&#43;**), or dashes (**-**).&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
| User Identifier Already Hashed | &lt;ul&gt;&lt;li&gt;Only configure one user identifier.&lt;/li&gt;&lt;li&gt;The API supports matching through email or mobile identifier.&lt;/li&gt;&lt;li&gt;Only use one identifier (either email or mobile ad ID) per action.&lt;/li&gt;&lt;li&gt;For more information, see [Snapchat API reference](https://developers.snapchat.com/api/docs/#adding-users).&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                                         |

### Action - Remove User from Segment

#### Parameters

| **Parameter**                  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|:-------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Segment                        | &lt;ul&gt;&lt;li&gt;Target segment to remove user from.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| User Identifier Type           | &lt;ul&gt;&lt;li&gt;User Identifiers can be of type **Email**, **Mobile Ad ID**, or **Phone number**.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| User Identifier                | &lt;ul&gt;&lt;li&gt;User Identifiers can be passed as plain text or already normalized and hashed.  &lt;ul&gt;&lt;li&gt;You can normalize email addresses by trimming the leading and trailing whitespace and converting all characters to lowercase before hashing.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Normalize the Mobile Advertiser ID  &lt;ul&gt;&lt;li&gt;Use all lowercase letters.&lt;/li&gt;&lt;li&gt;Do not remove hyphens.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Normalize phone numbers  &lt;ul&gt;&lt;li&gt;Include the country code.&lt;/li&gt;&lt;li&gt;Remove any double zeros (`0`) in front of the country code.&lt;/li&gt;&lt;li&gt;If the number itself begins with a zero (`0`), this should be removed.&lt;/li&gt;&lt;li&gt;Exclude any non-numeric characters such as whitespace, parentheses, plus signs (**&#43;**), or dashes (**-**).&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
| User Identifier Already Hashed | &lt;ul&gt;&lt;li&gt;Only configure one user identifier.&lt;/li&gt;&lt;li&gt;The API supports matching through email or mobile identifier.&lt;/li&gt;&lt;li&gt;Only use one identifier (either email or mobile ad ID) per action.&lt;/li&gt;&lt;li&gt;For more information, see [Snapchat API reference](https://developers.snapchat.com/api/docs/#adding-users).&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                                                                                                                                                                                                         |
