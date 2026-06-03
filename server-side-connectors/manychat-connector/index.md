---
title: Manychat Connector Setup Guide
description: This article describes how to set up the Manychat connector.
url: https://docs.tealium.com/server-side-connectors/manychat-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Manychat API
* API Endpoint: `https://api.manychat.com`
* Documentation: [Manychat API](https://api.manychat.com/swagger#/)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **API Key**  
  *   Manychat provides an API Key to use with the Account Public API.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add Tag by Name | ✓ | ✗ |
| Remove Tag by Name | ✓ | ✗ |
| Set Custom Field by Name | ✓ | ✗ |
| Upsert Subscriber | ✓ | ✗ |
| Send Message | ✓ | ✗ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Add Tag by Name

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Subscriber ID | The unique identifier for the subscriber. |
| Tag Name | The label to tag the subscriber. |

### Remove Tag by Name

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Subscriber ID | The unique identifier for the subscriber. |
| Tag Name | The tag to remove from subscriber. |

### Set Custom Field by Name

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Subscriber ID | The unique identifier for the subscriber. |
| Field Name | The field name to set a value for. |
| Field Value | The field value. |
| Datetime field | (Optional) If the custom field expects a datetime format (`YYY-MM-DDTHH:MM:SS&#43;00:00`), select the checkbox. Otherwise, the `YYYY-MM-DD` date format will be used. |

### Upsert Subscriber

#### Subscriber Parameters

| **Parameter** | **Description** |
| --- | --- |
| Subscriber ID | The unique identifier for the subscriber. |
| First Name | Subscriber&#39;s first name. |
| Last Name | Subscriber&#39;s last name. |
| Phone | Subscriber&#39;s phone number. |
| Email | Subscriber&#39;s email address. |
| Whatsapp Phone | Subscriber&#39;s WhatsApp phone number. |
| Gender | Subscriber&#39;s gender. |
| Has opt-in SMS | Boolean. Required if property Phone Number is not empty. |
| Has opt-in Email | Boolean. Required if property Email is not empty. |
| Consent Phrase | Required if property Has opt-in SMS is `true`. |

### Send Message

#### Message Parameters

| **Parameter** | **Description** |
| --- | --- |
| Subscriber ID | The unique identifier for the subscriber. |
| Data | Message data. Template variables must be used to build this object. [More info](https://manychat.github.io/dynamic_block_docs/). |
| Message Tag | The tag describing the message. For example: `ACCOUNT_UPDATE`. |
| OTN Topic Name | One-Time Notification topic name. For example: Сhannel news. |
| Template Variables | Provide template variables as data input for **Templates**.&lt;br&gt;For more information and usage examples, see .&lt;br&gt;Name nested template variables with the dot notation. Example: items.name.&lt;br&gt;Nested template variables are typically built from data layer list attributes. |
| Templates | Provide templates to be referenced in Data fieldF. or more information, see .&lt;br&gt;Templates are injected by name with double curly braces into supported fields. For example, `{{SomeTemplateName}}`. |