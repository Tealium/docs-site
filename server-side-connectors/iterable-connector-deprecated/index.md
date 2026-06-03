---
title: Iterable Connector Setup Guide (Deprecated)
description: This article describes how to set up the Iterable connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/iterable-connector-deprecated/
---
This connector is now deprecated and no longer available in the tag marketplace.
For the current connector, see the [Iterable Connector Setup Guide]().

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Track Event| ✗| ✓|
|Add or Update User| ✓| ✗|
|Subscribe User to List| ✓| ✗|
|Unsubscribe User from List| ✓| ✗|
|Send Email to a Specific Email Address| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**  
Go to the left navigation menu in the Iterable interface and click **Integrations &amp;gt; API Keys** to find your API key.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Track Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email|  &lt;ul&gt;&lt;li&gt;Either email or userID must be passed in to identify the user&lt;/li&gt;&lt;li&gt;If both are passed in, email takes precedence&lt;/li&gt;&lt;li&gt;For additional information, see the following vendor documentation: &lt;ul&gt;&lt;li&gt;[Events and Event Properties API documentation](https://support.iterable.com/hc/en-us/articles/206430615-Events-and-Event-Properties)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Event Name|  &lt;ul&gt;&lt;li&gt;Name of event&lt;/li&gt;&lt;/ul&gt; |
|Created At|  &lt;ul&gt;&lt;li&gt;Time event happened&lt;/li&gt;&lt;li&gt;Set to the time event was received if unspecified&lt;/li&gt;&lt;li&gt;Expects a Unix timestamp&lt;/li&gt;&lt;/ul&gt; |
|User ID|  &lt;ul&gt;&lt;li&gt;User ID that was passed into the `updateUser` call&lt;/li&gt;&lt;/ul&gt; |
|Campaign ID|  &lt;ul&gt;&lt;li&gt;Campaign tied to conversion&lt;/li&gt;&lt;/ul&gt; |
|Template ID|  &lt;ul&gt;&lt;li&gt;Template ID&lt;/li&gt;&lt;/ul&gt; |
|Data Fields|  &lt;ul&gt;&lt;li&gt;Additional data associated with event, for example: item id, item amount, city, state, etc..&lt;/li&gt;&lt;/ul&gt; |

### Action - Add or Update User

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email|  &lt;ul&gt;&lt;li&gt;An email must be set unless a profile already exists with a User ID set&lt;/li&gt;&lt;li&gt;If a profile already exists with a User ID set, a lookup from User ID to email is performed&lt;/li&gt;&lt;li&gt;For more information, see the following vendor documentation: &lt;ul&gt;&lt;li&gt;[Iterable API Documentation](https://api.iterable.com/api/docs#!/users/updateUser)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|User ID|  &lt;ul&gt;&lt;li&gt;Optional User ID&lt;/li&gt;&lt;li&gt;This is typically your database-generated ID&lt;/li&gt;&lt;/ul&gt; |
|Data Fields|  &lt;ul&gt;&lt;li&gt;Data fields to store in the user profile&lt;/li&gt;&lt;/ul&gt; |

### Action - Subscribe User to List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List ID|  &lt;ul&gt;&lt;li&gt;ID of the list you to subscribe the user to&lt;/li&gt;&lt;li&gt;For more information, see the following vendor documentation:  &lt;ul&gt;&lt;li&gt;[Iterable API Documentation](https://api.iterable.com/api/docs#!/lists/subscribe)&lt;/li&gt;&lt;li&gt;[API Overview and Sample Payloads](https://support.iterable.com/hc/en-us/articles/204780579-API-Overview-and-Sample-Payloads#lists).&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Email|  &lt;ul&gt;&lt;li&gt;Email address of the user&lt;/li&gt;&lt;/ul&gt; |
|User ID|  &lt;ul&gt;&lt;li&gt;Unique User ID of the user&lt;/li&gt;&lt;/ul&gt; |
|Data Fields|  &lt;ul&gt;&lt;li&gt;Data fields to store in the user profile&lt;/li&gt;&lt;/ul&gt; |

### Action - Unsubscribe User from List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List ID|  &lt;ul&gt;&lt;li&gt;The ID of the list you want to unsubscribe the user from&lt;/li&gt;&lt;li&gt;For additional information, see the following vendor documentation:  &lt;ul&gt;&lt;li&gt;[Iterable API Documentation](https://api.iterable.com/api/docs#!/lists/unsubscribe)&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Email|  &lt;ul&gt;&lt;li&gt;The email address of the user&lt;/li&gt;&lt;/ul&gt; |
|Campaign ID|  &lt;ul&gt;&lt;li&gt;Attribute unsubscribe to a campaign&lt;/li&gt;&lt;/ul&gt; |
|Channel Unsubscribe|  &lt;ul&gt;&lt;li&gt;Unsubscribe email from list&#39;s associated channel&lt;/li&gt;&lt;li&gt;This parameter is essentially a global unsubscribe&lt;/li&gt;&lt;li&gt;Possible values: `true` or `false`&lt;/li&gt;&lt;li&gt;The default value is `false`&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Email to a Specific Email Address

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Campaign ID|  &lt;ul&gt;&lt;li&gt;The ID of the campaign to trigger&lt;/li&gt;&lt;/ul&gt; |
|Recipient Email|  &lt;ul&gt;&lt;li&gt;The recipient&#39;s email address&lt;/li&gt;&lt;/ul&gt; |
|Data Fields|  &lt;ul&gt;&lt;li&gt;Fields to merge into email template&lt;/li&gt;&lt;/ul&gt; |
|Send At|  &lt;ul&gt;&lt;li&gt;Schedule the message for up to 365 days in the future.&lt;/li&gt;&lt;li&gt;If set in the past or if left blank, email is sent immediately.&lt;/li&gt;&lt;li&gt;Format is `YYYY-MM-DD HH:MM:SS` in UTC.&lt;/li&gt;&lt;/ul&gt; |
