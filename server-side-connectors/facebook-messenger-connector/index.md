---
title: Facebook Messenger Connector Setup Guide
description: This article describes how to set up the Facebook Messenger connector.
url: https://docs.tealium.com/server-side-connectors/facebook-messenger-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Facebook Graph API - Messenger Platform
* API Version: v25.0
* API Endpoint: `https://graph.facebook.com`
* Documentation: [Page Access Token for Facebook Pages](https://developers.facebook.com/docs/facebook-login/access-tokens#pagetokens)

## Configuration

Go to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Page Access Token**  
  * This token is used to make Messenger API calls.
  * For more information, see: [Facebook: Page Access Tokens](https://developers.facebook.com/docs/facebook-login/access-tokens#pagetokens).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Text-Only Message | ✓ | ✗ |
| Send Media Message | ✓ | ✗ |
| Send Sender Action | ✓ | ✗ |
| Send Template Message (Advanced) | ✓ | ✗ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Text-Only Message

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Messaging Type | (Required) Specifies the messaging type of the message being sent, and is a more explicit way to ensure bots are complying with policies for specific messaging types and respecting people's preferences. For more information, see: [Facebook: Messaging Types](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`). |
|Recipient Identifiers| (Required) Identifies the recipient to send a message to. The ID, Phone Number, or User Ref must be set. If using a Phone Number to identify a recipient, your bot must be approved for [Customer Matching](https://developers.facebook.com/docs/messenger-platform/customer-matching) and include only digits with country code, area code, and number (for example, `16505551212`). When using a Phone Number, it is also possible to set a First Name and Last Name. |
| Message Text | (Required) The content of the message to send to the user. This field is limited to 2000 characters. This field also supports the Tealium templating engine. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).  |
| Message Text Template Variables | Provide template variables for message data. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). |
| Quick Replies| Quick replies provide a way to present a set of up to 11 buttons in-conversation that contain a title and optional image, and appear prominently above the composer. You can also use quick replies to request a user's location, email address, and phone number. Only array attributes are supported and the arrays specified here must be the same size. For more information, see [Facebook: Quick Reply documentation](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies). |
| Metadata | A custom string that is delivered through [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/reference/webhook-events/) in the `message_echoes` field. 1,000 character limit. Metadata automatically supports templating functionality and template variables. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). |
| Metadata Template Variables | Provide template variables for metadata. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). |
| Notification Type | Type of push notification. <ul><li>**Regular:** Sound/vibration (will be used if not set).</li><li>**Silent Push:** On-screen notification only.</li><li>**No Push:** No notification</li></ul>. |
| Message Tag | Used if **Messaging Type** is set to `Message Tag`. For a complete list of all message tags, refer to the [Facebook: Message Tag documentation](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags) |

### Send Media Message

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Messaging Type | (Required) Specifies the messaging type of the message being sent, and is a more explicit way to ensure bots are complying with policies for specific messaging types and respecting user preferences. For more information, see: [Facebook: Messaging Types](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`). |
|Recipient Identifiers| (Required) Identifies the recipient to send a message to. The ID, Phone Number, or User Ref must be set. If using a Phone Number to identify a recipient, your bot must be approved for [Customer Matching](https://developers.facebook.com/docs/messenger-platform/customer-matching) and include only digits with country code, area code, and number (for example, `16505551212`). When using a Phone Number, it is also possible to set a First Name and Last Name. |
| Media Type | (Required) Type of media to send to recipient.  Supported values are `Image`, `Audio`, `Video`, or `File`. |
| Media URL | (Required) The web `URL` address of the media to be sent. |
| Is Reusable | Select this option to mark content as reusable content that can be sent to other recipients. |
| Quick Replies| Quick replies provide a way to present a set of up to 11 buttons in-conversation that contain a title and optional image, and appear prominently above the composer. You can also use quick replies to request a user's location, email address, and phone number. Only array attributes are supported and the arrays specified here must be the same size. For more information, see [Facebook: Quick Reply documentation](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies). |
| Metadata | A custom string that is delivered through [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/reference/webhook-events/) in the `message_echoes` field. 1,000 character limit. Metadata automatically supports templating functionality and template variables.  For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/). |
| Metadata Template Variables | Provide template variables for metadata. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). |
| Notification Type | Type of push notification. <ul><li>**Regular:** Sound/vibration (will be used if not set).</li><li>**Silent Push:** On-screen notification only.</li><li>**No Push:** No notification</li></ul>. |
| Message Tag | Used if **Messaging Type** is set to `Message Tag`. For a complete list of all message tags, refer to the [Facebook: Message Tag documentation](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags) |

### Send Sender Action

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Messaging Type | (Required) Specifies the messaging type of the message being sent, and is a more explicit way to ensure bots are complying with policies for specific messaging types and respecting user preferences. For more information, see: [Facebook: Messaging Types](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`). |
|Recipient Identifiers| (Required) Identifies the recipient to send a message to. The ID, Phone Number, or User Ref must be set.If using a Phone Number to identify a recipient, your bot must be approved for [Customer Matching](https://developers.facebook.com/docs/messenger-platform/customer-matching) and include only digits with country code, area code, and number (for example, `16505551212`). When using a Phone Number, it is also possible to set a First Name and Last Name. |
| Sender Action | (Required) The sender action to display to the recipient. Supported values are `typing_on`, `typing_off`, or `mark_seen`. |
| Message Tag | Used if **Messaging Type** is set to `Message Tag`. For a complete list of all message tags, refer to the [Facebook: Message Tag documentation](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags) |

### Send Template Message (Advanced)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Messaging Type | (Required) Specifies the messaging type of the message being sent, and is a more explicit way to ensure bots are complying with policies for specific messaging types and respecting user preferences. For more information, see: [Facebook: Messaging Types](https://developers.facebook.com/docs/messenger-platform/send-messages#`messaging_types`). |
|Recipient Identifiers| (Required) Identifies the recipient to send a message to. The ID, Phone Number, or User Ref must be set. If using a Phone Number to identify a recipient, your bot must be approved for [Customer Matching](https://developers.facebook.com/docs/messenger-platform/customer-matching) and include only digits with country code, area code, and number (for example, `16505551212`). When using a Phone Number, it is also possible to set a First Name and Last Name. |
| Template Payload | (Required) The template payload to be sent. Payload supports templating functionality and template variables. Should be formatted as JSON: `{ "template_type": "<TEMPLATE_TYPE>", ... }`. For more information, see [Message Template documentation](https://developers.facebook.com/docs/messenger-platform/send-messages/templates) for specific payload contents. |
| Template Variables | If using the templating engine, template variables will be used. These fields map Attributes to variable names that are used in the Template Payload. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). |
| Quick Replies| Quick replies provide a way to present a set of up to 11 buttons in-conversation that contain a title and optional image, and appear prominently above the composer. You can also use quick replies to request a user's location, email address, and phone number. Only array attributes are supported and the arrays specified here must be the same size. For more information, see [Facebook: Quick Reply documentation](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies). |
| Metadata | A custom string that is delivered through [Facebook Messenger Webhook](https://developers.facebook.com/docs/messenger-platform/reference/webhook-events/) in the `message_echoes` field. 1,000 character limit. Metadata automatically supports templating functionality and template variables. For more information, see [Trimou Templating Engine](https://docs.tealium.com/about-connector-templates/). |
| Metadata Template Variables | If using the templating engine, template variables will be used. These fields map Attributes to variable names that are used in the Metadata. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/). |
| Notification Type | Type of push notification. <ul><li>**Regular:** Sound/vibration (will be used if not set).</li><li>**Silent Push:** On-screen notification only.</li><li>**No Push:** No notification</li></ul>. |
| Message Tag | Used if **Messaging Type** is set to `Message Tag`. For a complete list of all message tags, refer to the [Facebook: Message Tag documentation](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags) |

## Vendor Documentation

* [Page Access Token](https://developers.facebook.com/docs/facebook-login/access-tokens#pagetokens)
* [Messaging Types](https://developers.facebook.com/docs/messenger-platform/send-messages/#messaging_types)
* [Customer Matching](https://developers.facebook.com/docs/messenger-platform/customer-matching)
* [Quick Replies](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies)
* [Message Tags](https://developers.facebook.com/docs/messenger-platform/send-messages/message-tags)
* [Message Templates](https://developers.facebook.com/docs/messenger-platform/send-messages/templates)

##### APIs

* [Facebook Send HTTP API](https://developers.facebook.com/docs/messenger-platform/reference/send-api)