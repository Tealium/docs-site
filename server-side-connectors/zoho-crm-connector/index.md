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

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview](https://docs.tealium.com/server-side/connectors/manage/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

### Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Create or Update Record

#### Parameters

| **Parameter**          | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                          |
|:-----------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Module                 | <ul><li>Module names.</li><li>For example, `Leads`, `Accounts`</li><li>For all possible module names, see [Insert or Update Records (Upsert)](https://www.zoho.com/crm/developer/docs/api/v2/upsert-records.html).</li></ul>                                                                                                                                                                                                             |
| Template Variables     | <ul><li>Provide template variables as data input.</li><li>For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).</li><li>Name nested template variables with the dot notation.</li><li>For example, `items.name`</li><li>Nested template variables are typically built from data layer list attributes.</li></ul> |
| Templates              | <ul><li>Provide templates to be referenced in body data.</li><li>For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).</li><li>Templates are injected by name with double curly braces into supported fields.</li><li>For example, `{{SomeTemplateName}}`.</li></ul>                                                |
| Duplicate Check Fields | <ul><li>Duplicate check fields dictate whether a new record will be added or updated.</li><li>The system-defined duplicate check fields are used by default.</li><li>For more information about duplicate check fields, see [Insert or Update Records (Upsert)](https://www.zoho.com/crm/developer/docs/api/v2/upsert-records.html).</li></ul>                                                                                           |
| Trigger                | <ul><li>Trigger can be `workflow`, `approval`, or `blueprint`.</li><li>If the trigger is not mentioned, the workflows, approvals, and blueprints related to the API are executed.</li></ul>                                                                                                                                                                                                                                              |