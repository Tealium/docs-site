---
title: Zoho CRM Connector Setup Guide
description: This article describes how to set up the Zoho CRM connector.
url: https://docs.tealium.com/server-side-connectors/zoho-crm-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Zoho CRM API
* API Version: v2
* API Endpoint: `https://www.zohoapis.com/crm/v2/`

## Connector Actions

| **Action Name**         | **AudienceStream** | **EventStream** |
|:------------------------|:-------------------|:----------------|
| Create or Update Record | ✓                  | ✓               |

## Configure Settings

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview](/server-side/connectors/manage/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

### Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Create or Update Record

#### Parameters

| **Parameter**          | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                          |
|:-----------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Module                 | &lt;ul&gt;&lt;li&gt;Module names.&lt;/li&gt;&lt;li&gt;For example, `Leads`, `Accounts`&lt;/li&gt;&lt;li&gt;For all possible module names, see [Insert or Update Records (Upsert)](https://www.zoho.com/crm/developer/docs/api/v2/upsert-records.html).&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                             |
| Template Variables     | &lt;ul&gt;&lt;li&gt;Provide template variables as data input.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;For example, `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
| Templates              | &lt;ul&gt;&lt;li&gt;Provide templates to be referenced in body data.&lt;/li&gt;&lt;li&gt;For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt;                                                |
| Duplicate Check Fields | &lt;ul&gt;&lt;li&gt;Duplicate check fields dictate whether a new record will be added or updated.&lt;/li&gt;&lt;li&gt;The system-defined duplicate check fields are used by default.&lt;/li&gt;&lt;li&gt;For more information about duplicate check fields, see [Insert or Update Records (Upsert)](https://www.zoho.com/crm/developer/docs/api/v2/upsert-records.html).&lt;/li&gt;&lt;/ul&gt;                                                                                           |
| Trigger                | &lt;ul&gt;&lt;li&gt;Trigger can be `workflow`, `approval`, or `blueprint`.&lt;/li&gt;&lt;li&gt;If the trigger is not mentioned, the workflows, approvals, and blueprints related to the API are executed.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                              |