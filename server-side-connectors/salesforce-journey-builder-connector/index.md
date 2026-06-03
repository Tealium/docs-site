---
title: Salesforce Journey Builder Connector Setup Guide
description: This article describes how to set up the Salesforce Journey Builder connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/salesforce-journey-builder-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event to Initiate Journey| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Client ID**
  * (Required) Provide your app client ID.
  * For additional information, see: [Get OAuth Client Credentials](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)

* **Client Secret**
  * (Required) Provide your app client secret.

* **Account ID**
  * (Required) Provide the account identifier (MID) of the target business unit.

* **Tenant-specific subdomain**
  * (Required) Provide the tenant-specific subdomain for your application.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure the connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Event to Initiate Journey

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Entry Definition|  &lt;ul&gt;&lt;li&gt;(Required) Select an event entry definition or enter it manually.&lt;/li&gt;&lt;li&gt;The drop-down list is listed from newest to oldest and shows a maximum of 2000 entries.&lt;/li&gt;&lt;li&gt;For more information, see [Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html).&lt;/li&gt;&lt;/ul&gt; |
|Contact Key|  &lt;ul&gt;&lt;li&gt;(Required) Provide contact key.&lt;/li&gt;&lt;/ul&gt; |
|Event Data|  &lt;ul&gt;&lt;li&gt;Required if defined in a custom event or specified by the event.&lt;/li&gt;&lt;li&gt;Map values to contact event attributes.&lt;/li&gt;&lt;li&gt;For more information, see [Salesforce: POST /interaction/v1/events](hhttps://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html).&lt;/li&gt;&lt;/ul&gt; |

## Vendor Documentation

* [Salesforce: Get OAuth Client Credentials](https://developer.salesforce.com/docs/atlas.en-us.mc-getting-started.meta/mc-getting-started/get-api-key.htm)
* [Salesforce: POST /interaction/v1/events](https://developer.salesforce.com/docs/marketing/marketing-cloud/references/mc_rest_interaction/postEvent.html)
* [Salesforce: Entry Events and Data Definitions](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/event-definition-key.html#:~:text=Event%20definitions%20define%20the%20name,the%20journey%20to%20be%20published.)
