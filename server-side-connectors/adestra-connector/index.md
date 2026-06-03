---
title: Adestra Connector Setup Guide
description: This article describes how to set up the Adestra connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/adestra-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Create or Update Contact| ✓| ✓|
|Add Contact To List| ✓| ✓|
|Remove Contact From List| ✓| ✓|
|Send Email| ✓| ✓|

## Configure Settings

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**: (Required) Adestra account API key, see: [Create API Token](https://app.adestra.com/doc/page/current/index/integration/zapier/initial-config#Step3:CreateAPITokeninMessageFocus &#34;Create API Token&#34;)

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Create or Update Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Select applicable update strategy.  &lt;ul&gt;&lt;li&gt;**Create Only** Look up an existing contact and if not found, create a new contact.&lt;/li&gt;&lt;li&gt;**Update Only** Look up an existing contact and update it.&lt;/li&gt;&lt;li&gt;**Create or Update** Look up an existing contact and if found, update it, otherwise create a new contact.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Core Table|  &lt;ul&gt;&lt;li&gt;(Required) Select the core table to create or update the contact in.&lt;/li&gt;&lt;/ul&gt; |
|Contact Lookup Email Address|  &lt;ul&gt;&lt;li&gt;(Required) Email address to lookup contact.&lt;/li&gt;&lt;/ul&gt; |

### Action - Add Contact To List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Core Table|  &lt;ul&gt;&lt;li&gt;(Required) Select the core table the contact belongs to.&lt;/li&gt;&lt;/ul&gt; |
|Contact Lookup Email Address|  &lt;ul&gt;&lt;li&gt;(Required) Email address to lookup contact.&lt;/li&gt;&lt;/ul&gt; |
|List|  &lt;ul&gt;&lt;li&gt;(Required) List to add the contact to.&lt;/li&gt;&lt;/ul&gt; |

### Action - Remove Contact From List

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Core Table|  &lt;ul&gt;&lt;li&gt;(Required) Core tables store contacts in Adestra.&lt;/li&gt;&lt;li&gt;Select the core table the contact belongs to.&lt;/li&gt;&lt;/ul&gt; |
|Contact Email Address|  &lt;ul&gt;&lt;li&gt;(Required) Email address to lookup contact.&lt;/li&gt;&lt;/ul&gt; |
|List|  &lt;ul&gt;&lt;li&gt;(Required) List to remove the contact from.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Email

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Email Campaign|  &lt;ul&gt;&lt;li&gt;(Required) Select the campaign to be launched.&lt;/li&gt;&lt;/ul&gt; |
|Contact Email Address|  &lt;ul&gt;&lt;li&gt;(Required) Email address to send email to.&lt;/li&gt;&lt;/ul&gt; |
|Transaction Data|  &lt;ul&gt;&lt;li&gt;(Required) Template data to set within the email campaign.&lt;/li&gt;&lt;/ul&gt; |
