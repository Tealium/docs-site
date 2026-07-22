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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

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
|Webhook URL|  <ul><li>Required only if not provided in the **Configuration** tab.</li><li>Overwrites the value defined in the **Configuration** tab if a value is provided.</li></ul> |
|Print Attribute Names|  <ul><li>If attribute names get updated, the names in the payload will reflect the update.</li></ul> |

### Action - Send Visitor Data

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Webhook URL|  <ul><li>Required only if not provided in the **Configuration** tab.</li><li>Overwrites the value defined in the **Configuration** tab if a value is provided.</li></ul> |
|Include Current Visit Data|  <ul><li>Check this box if current visit data is to be included.</li></ul> |
| Include Current Visit Data With Visitor Data | <ul><li>Add the current visit data to the payload.</li><li>This includes event visit data if Exclude Current Visit Event Data isn't selected.</li></ul> |
| Exclude Current Visit Event Data | <ul><li>Exclude event data from the current visit data.</li></ul> |
|Print Attribute Names|  <ul><li>If attribute names get updated, the names in the payload will reflect the update</li></ul> |

### Action - Send Customized Data (Advanced)

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Webhook URL|  <ul><li>Required only if not provided in the **Configuration** tab.</li><li>Overwrites the value defined in the **Configuration** tab if a value is provided.</li></ul> |
|Custom Message Definition|  <ul><li>Map values to names for simple one level JSON format, otherwise reference template name, select only the **Custom Message Definition** option, and ensure your template is valid JSON.</li><li>For template support, reference the template name to generate message data from a template.</li></ul> |
|Template Variables|  <ul><li>(Optional) Provide template variables as data input for templates. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>Example: `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
|Templates|  <ul><li>(Optional) Provide templates to be referenced in message data. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul> |