---
title: Insightly Connector Setup Guide (Deprecated)
description: This article describes how to set up the Insightly connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/insightly-connector-deprecated/
---
This connector is now deprecated and no longer available in the tag marketplace. For information about the Insightly CRM connector, see the [Insightly CRM Connector Setup Guide]().

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add a Contact| ✓| ✗|
|Update a Contact| ✓| ✗|
|Add a Lead| ✓| ✗|
|Update a Lead| ✓| ✗|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**
  * For information on where to find your Insightly API Key, see: [Finding or Resetting your API Key](https://support.insight.ly/hc/en-us/articles/204864594-Finding-your-Insightly-API-key)

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Add a Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|First Name|  &lt;ul&gt;&lt;li&gt;First name of the contact.&lt;/li&gt;&lt;li&gt;Either first name or last name is required.&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;Last name of the contact.&lt;/li&gt;&lt;li&gt;Either first name or last name is required.&lt;/li&gt;&lt;/ul&gt; |
|Attributes|  &lt;ul&gt;&lt;li&gt;Additional attributes for the contact.&lt;/li&gt;&lt;li&gt;These parameters must exist within Insightly.&lt;/li&gt;&lt;li&gt;For a list of available attributes, see: [Insightly&#39;s documentation](https://api.insight.ly/v2.3/Help#!/Contacts/AddContact).&lt;/li&gt;&lt;/ul&gt; |
|Tags|  &lt;ul&gt;&lt;li&gt;Tags to assign to the contact.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update a Contact

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Contact ID|  &lt;ul&gt;&lt;li&gt;The ID of the contact to be updated.&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;The first name of the contact.&lt;/li&gt;&lt;li&gt;Either first name or last name is required.&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;The last name of the contact.&lt;/li&gt;&lt;li&gt;Either first name or last name is required.&lt;/li&gt;&lt;/ul&gt; |
|Attributes|  &lt;ul&gt;&lt;li&gt;Additional attributes to be updated.&lt;/li&gt;&lt;li&gt;For a list of available attributes, see: [Insightly&#39;s documentation](https://api.insight.ly/v2.3/Help#!/Contacts/UpdateContact).&lt;/li&gt;&lt;/ul&gt; |
|Tags|  &lt;ul&gt;&lt;li&gt;Tags to be updated.&lt;/li&gt;&lt;/ul&gt; |

### Action - Add a Lead

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Last Name|  &lt;ul&gt;&lt;li&gt;Last name of the lead.&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;First name of the lead.&lt;/li&gt;&lt;/ul&gt; |
|Attributes|  &lt;ul&gt;&lt;li&gt;Additional attributes for the lead.&lt;/li&gt;&lt;li&gt;For a list of available attributes, see: [Insightly&#39;s documentation](https://api.insight.ly/v2.3/Help#!/Leads/AddLead).&lt;/li&gt;&lt;/ul&gt; |
|Tags|  &lt;ul&gt;&lt;li&gt;Tags to assign to the lead.&lt;/li&gt;&lt;/ul&gt; |

### Action - Update a Lead

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Lead ID|  &lt;ul&gt;&lt;li&gt;The ID of the lead to be updated.&lt;/li&gt;&lt;/ul&gt; |
|Last Name|  &lt;ul&gt;&lt;li&gt;Last name of the lead.&lt;/li&gt;&lt;/ul&gt; |
|First Name|  &lt;ul&gt;&lt;li&gt;First name of the lead.&lt;/li&gt;&lt;/ul&gt; |
|Attributes|  &lt;ul&gt;&lt;li&gt;Additional attributes to be updated.&lt;/li&gt;&lt;li&gt;For a list of available attributes, see: [Insightly&#39;s documentation](https://api.insight.ly/v2.3/Help#!/Leads/UpdateLead).&lt;/li&gt;&lt;/ul&gt; |
|Tags|  &lt;ul&gt;&lt;li&gt;Tags to be updated.&lt;/li&gt;&lt;/ul&gt; |
