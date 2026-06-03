---
title: Domo JSON Webhook Connector Setup Guide
description: This article describes how to set up the Domo JSON Webhook connector.
url: https://docs.tealium.com/server-side-connectors/domo-json-webhook-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Event Data| ✗| ✓|
|Send Visitor Data| ✓| ✗|
|Send Customized Data (Advanced)| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Webhook URL**
  * Paste the URL provided in the Details section of your Domo connector setup.
  * If you specify a URL endpoint here, it will be applied to all actions in the connector, but may be overridden in the action.

* **Webhook Secret**
  * (Optional) Enter a Webhook Secret.
  * For additional information, see [Domo: JSON Webhook Connector](https://knowledge.domo.com/Connect/Connecting_to_Data_with_Connectors/Configuring_Each_Connector/Miscellaneous_Connectors/JSON_Webhook_Connector)

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Event Data

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Webhook URL|  &lt;ul&gt;&lt;li&gt;Required only if not provided in the **Configuration** tab.&lt;/li&gt;&lt;li&gt;Overwrites the value defined in the **Configuration** tab if a value is provided.&lt;/li&gt;&lt;/ul&gt; |
|Print Attribute Names|  &lt;ul&gt;&lt;li&gt;If attribute names get updated, the names in the payload will reflect the update.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Visitor Data

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Webhook URL|  &lt;ul&gt;&lt;li&gt;Required only if not provided in the **Configuration** tab.&lt;/li&gt;&lt;li&gt;Overwrites the value defined in the **Configuration** tab if a value is provided.&lt;/li&gt;&lt;/ul&gt; |
|Include Current Visit Data|  &lt;ul&gt;&lt;li&gt;Check this box if current visit data is to be included.&lt;/li&gt;&lt;/ul&gt; |
| Include Current Visit Data With Visitor Data | &lt;ul&gt;&lt;li&gt;Add the current visit data to the payload.&lt;/li&gt;&lt;li&gt;This includes event visit data if Exclude Current Visit Event Data isn&#39;t selected.&lt;/li&gt;&lt;/ul&gt; |
| Exclude Current Visit Event Data | &lt;ul&gt;&lt;li&gt;Exclude event data from the current visit data.&lt;/li&gt;&lt;/ul&gt; |
|Print Attribute Names|  &lt;ul&gt;&lt;li&gt;If attribute names get updated, the names in the payload will reflect the update&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Customized Data (Advanced)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Webhook URL|  &lt;ul&gt;&lt;li&gt;Required only if not provided in the **Configuration** tab.&lt;/li&gt;&lt;li&gt;Overwrites the value defined in the **Configuration** tab if a value is provided.&lt;/li&gt;&lt;/ul&gt; |
|Custom Message Definition|  &lt;ul&gt;&lt;li&gt;Map values to names for simple one level JSON format, otherwise reference template name, select only the **Custom Message Definition** option, and ensure your template is valid JSON.&lt;/li&gt;&lt;li&gt;For template support, reference the template name to generate message data from a template.&lt;/li&gt;&lt;/ul&gt; |
|Template Variables|  &lt;ul&gt;&lt;li&gt;(Optional) Provide template variables as data input for templates. For more information, see .&lt;/li&gt;&lt;li&gt;Name nested template variables with the dot notation.&lt;/li&gt;&lt;li&gt;Example: `items.name`&lt;/li&gt;&lt;li&gt;Nested template variables are typically built from data layer list attributes.&lt;/li&gt;&lt;/ul&gt; |
|Templates|  &lt;ul&gt;&lt;li&gt;(Optional) Provide templates to be referenced in message data. For more information, see .&lt;/li&gt;&lt;li&gt;Templates are injected by name with double curly braces into supported fields.&lt;/li&gt;&lt;li&gt;For example, `{{SomeTemplateName}}`.&lt;/li&gt;&lt;/ul&gt; |