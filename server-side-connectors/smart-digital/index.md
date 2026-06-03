---
title: Smart Digital Connector Setup Guide
description: This article describes how to set up the Smart Digital connector.
url: https://docs.tealium.com/server-side-connectors/smart-digital/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Track Event | ✗ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors]().


After adding the connector, configure the following settings:

* **Script ID** &amp;ndash; (Required) Identifier of the tracked application.
* **Partner ID**  &amp;ndash; (Required) Identifier of the tracking system.
* **Partner System**  &amp;ndash; (Required) Friendly name of the tracking system.
* **Engine Base URL**  &amp;ndash; (Required) Select engine base URL or provide Tracking API URL as a custom text.

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Track Event

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Name | (Required) Event name. |
| Page Name | (Required) Page name. |
| Visitor ID | Unique identifier of the visitor. If this field is not mapped, it is automatically mapped to the **tealium_visitor_id**. |
| Page URL | The URL of the current page. If this field is not mapped, it is automatically mapped to the **Current URL**. |
| URL Referrer | The previous URL visited by the user. If this field is not mapped, it is automatically mapped to the **Referring URL**. |
| User Agent | User agent of the client. If this field is not mapped, it is automatically mapped to the **User Agent**. |
| Template Variables | Provide template variables as data input for **Templates**. For more information, see . Name nested template variables with the dot notation. For example: **items.name**. Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in Tracking Data Parameters. For more information, see [Trimou Templating Engine Guide](). Templates are injected into supported fields by name, with double curly braces. For example: **&amp;#123;&amp;#123;TemplateName&amp;#125;&amp;#125;**.|