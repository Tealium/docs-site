---
title: Avo Inspector Connector Setup Guide
description: This article describes how to set up the Avo Inspector connector.
url: https://docs.tealium.com/server-side-connectors/avo-inspector-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Avo Inspector
* API Version: v1.0.2
* API Endpoint: `https://api.avo.app/inspector/tealium/v1/track`
* Documentation: [Avo Inspector API](https://avohq.notion.site/Avo-Tealium-Inspector-API-destination-1-ce5d8dda46fd49bd8cfbaf45a4df3619)

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 30
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Event Data (Real-Time) | ✗ | ✓ |
| Send Event Data (Batched) | ✗ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Key**  
 (Required) This API Key is created when activating an inspector source in Avo. Each inspector source requires a separate Avo destination in Tealium, which allows Avo to determine the source of the events.
* **Environment**  
 (Required) The current environment: **Prod**, **Dev**, or **Staging**.
* **Origin (String)**  
 (Optional) Origin of the call. 

## Actions

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Event Data (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | Type of event. Either `event` or `sessionStarted`. |
| Template Variables | Provide template variables as data input for **Templates**. For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).<br>Name nested template variables with the dot notation. Example: `items.name.`<br>Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in Event Parameters. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).<br>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.|

### Send Event Data (Batched)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type | Type of event. Either `event` or `sessionStarted`. |
| Template Variables | Provide template variables as data input for **Templates**. For more information and usage examples, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).<br>Name nested template variables with the dot notation. Example: `items.name.`<br>Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in Event Parameters. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).<br>Templates are injected by name with double curly braces into supported fields, For example, `{{SomeTemplateName}}`.|