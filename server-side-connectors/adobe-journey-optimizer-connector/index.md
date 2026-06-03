---
title: Adobe Journey Optimizer Connector Setup Guide
description: This article describes how to set up the Adobe Journey Optimizer connector.
url: https://docs.tealium.com/server-side-connectors/adobe-journey-optimizer-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Adobe Journey Optimizer API
* API Endpoint: `https://platform.adobe.io`
* Documentation: [Adobe Journey Optimizer APIs](https://developer.adobe.com/journey-optimizer-apis/)

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Unitary message execution (Real-time) | ✓ | ✓ |
| Unitary message execution (Batched) | ✓ | ✓ |

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Client ID**  
(Required) The client ID (API key) can be found in the [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) in your Adobe account.
* **Client Secret**  
(Required) The client secret can be found in the Adobe Developer Console in your Adobe account.
* **Organization ID**  
(Required) The organization ID can be found in the Adobe Developer Console in your Adobe account.
* **Sandbox**  
Specify whether you want the API calls to refer to a different environment than the default (prod).

## Actions

The following section lists the supported parameters for each action.

### Unitary message execution (Batched)

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 20
* Max time since oldest request: 5 minutes
* Max size of requests: 1 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Campaign ID | (Required) The campaign identifier. |
| Request ID | The unique request identifier. |
| Namespace | The AEP profile namespace. |

#### Recipient Parameters

| **Parameter** | **Description** |
| --- | --- |
| Type | (Required) The recipient type. For example, `aep`. |
| User ID | (Required) The AEP profile identifier. |
| Context | The context data used for dynamic variable substitution in message content. |
| Email Address | The recipient email address, which is also the external user ID. |
| Mobile Phone Number | The recipient mobile phone number for SMS text messages. |
| Profile | The profile data used for dynamic variable substitution in message content. |
| Template Variables | Provide template variables as data input for **Templates**. For more information and usage examples, see .&lt;br&gt;Name nested template variables with the dot notation. For example: `items.name`.&lt;br&gt;Nested template variables are typically built from data layer list attributes.|
| Templates | Provide templates to be referenced in Body Parameters.For more information, see .&lt;br&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|

### Unitary message execution (Real-time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Campaign ID | (Required) The campaign identifier. |
| Request ID | The unique request identifier. |
| Namespace | The AEP profile namespace. |

#### Recipient Parameters

| **Parameter** | **Description** |
| --- | --- |
| Type | (Required) The recipient type. For example, `aep`. |
| User ID | (Required) The AEP profile identifier. |
| Context | The context data used for dynamic variable substitution in message content. |
| Email Address | The recipient email address, which is also the external user ID. |
| Mobile Phone Number | The recipient mobile phone number for SMS text messages. |
| Profile | The profile data used for dynamic variable substitution in message content. |
| Template Variables | Provide template variables as data input for **Templates**. For more information and usage examples, see .&lt;br&gt;Name nested template variables with the dot notation. For example: `items.name`.&lt;br&gt;Nested template variables are typically built from data layer list attributes.|
| Templates | Provide templates to be referenced in Body Parameters. For more information, see .&lt;br&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`.|