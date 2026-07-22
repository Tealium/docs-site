---
title: Iterable Connector Setup Guide (Deprecated)
description: This article describes how to set up the Iterable connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/iterable-connector-deprecated/
---

<blockquote>
This connector is now deprecated and no longer available in the tag marketplace.
For the current connector, see the [Iterable Connector Setup Guide](https://docs.tealium.com/iterable-connector/).
</blockquote>


## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Track Event| ✗| ✓|
|Add or Update User| ✓| ✗|
|Subscribe User to List| ✓| ✗|
|Unsubscribe User from List| ✓| ✗|
|Send Email to a Specific Email Address| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**  
Go to the left navigation menu in the Iterable interface and click **Integrations &gt; API Keys** to find your API key.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Track Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email|  <ul><li>Either email or userID must be passed in to identify the user</li><li>If both are passed in, email takes precedence</li><li>For additional information, see the following vendor documentation: <ul><li>[Events and Event Properties API documentation](https://support.iterable.com/hc/en-us/articles/206430615-Events-and-Event-Properties)</li></ul> </li></ul> |
|Event Name|  <ul><li>Name of event</li></ul> |
|Created At|  <ul><li>Time event happened</li><li>Set to the time event was received if unspecified</li><li>Expects a Unix timestamp</li></ul> |
|User ID|  <ul><li>User ID that was passed into the `updateUser` call</li></ul> |
|Campaign ID|  <ul><li>Campaign tied to conversion</li></ul> |
|Template ID|  <ul><li>Template ID</li></ul> |
|Data Fields|  <ul><li>Additional data associated with event, for example: item id, item amount, city, state, etc..</li></ul> |

### Action - Add or Update User

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email|  <ul><li>An email must be set unless a profile already exists with a User ID set</li><li>If a profile already exists with a User ID set, a lookup from User ID to email is performed</li><li>For more information, see the following vendor documentation: <ul><li>[Iterable API Documentation](https://api.iterable.com/api/docs#!/users/updateUser)</li></ul> </li></ul> |
|User ID|  <ul><li>Optional User ID</li><li>This is typically your database-generated ID</li></ul> |
|Data Fields|  <ul><li>Data fields to store in the user profile</li></ul> |

### Action - Subscribe User to List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List ID|  <ul><li>ID of the list you to subscribe the user to</li><li>For more information, see the following vendor documentation:  <ul><li>[Iterable API Documentation](https://api.iterable.com/api/docs#!/lists/subscribe)</li><li>[API Overview and Sample Payloads](https://support.iterable.com/hc/en-us/articles/204780579-API-Overview-and-Sample-Payloads#lists).</li></ul> </li></ul> |
|Email|  <ul><li>Email address of the user</li></ul> |
|User ID|  <ul><li>Unique User ID of the user</li></ul> |
|Data Fields|  <ul><li>Data fields to store in the user profile</li></ul> |

### Action - Unsubscribe User from List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|List ID|  <ul><li>The ID of the list you want to unsubscribe the user from</li><li>For additional information, see the following vendor documentation:  <ul><li>[Iterable API Documentation](https://api.iterable.com/api/docs#!/lists/unsubscribe)</li></ul> </li></ul> |
|Email|  <ul><li>The email address of the user</li></ul> |
|Campaign ID|  <ul><li>Attribute unsubscribe to a campaign</li></ul> |
|Channel Unsubscribe|  <ul><li>Unsubscribe email from list's associated channel</li><li>This parameter is essentially a global unsubscribe</li><li>Possible values: `true` or `false`</li><li>The default value is `false`</li></ul> |

### Action - Send Email to a Specific Email Address

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Campaign ID|  <ul><li>The ID of the campaign to trigger</li></ul> |
|Recipient Email|  <ul><li>The recipient's email address</li></ul> |
|Data Fields|  <ul><li>Fields to merge into email template</li></ul> |
|Send At|  <ul><li>Schedule the message for up to 365 days in the future.</li><li>If set in the past or if left blank, email is sent immediately.</li><li>Format is `YYYY-MM-DD HH:MM:SS` in UTC.</li></ul> |
