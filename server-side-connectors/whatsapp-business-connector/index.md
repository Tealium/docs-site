---
title: WhatsApp Business Connector Setup Guide
description: This article describes how to set up the WhatsApp Business connector.
url: https://docs.tealium.com/server-side-connectors/whatsapp-business-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Facebook Graph API - WhatsApp Business API
* API Version: v25.0
* API Endpoint: `https://graph.facebook.com`
* Documentation: [WhatsApp Business Platform Cloud API](https://developers.facebook.com/docs/whatsapp/cloud-api)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Access Token**: (Required) Access Token of the Facebook System User. 
<blockquote>
When authenticating the connector using an Access Token, we recommend that you use a Business System User access token. Unlike User access tokens, which expire frequently and require regeneration every few hours, Business System User tokens offer extended validity (typically up to 60 days) providing a more stable and reliable authentication method. To obtain a Business System User access token, you must create a System User in your Facebook Business Manager, assign the necessary assets and permissions, and then generate a token in the Facebook App dashboard. For detailed instructions, see [WhatsApp: Get System User Access Tokens for the WhatsApp Business Platform](https://developers.facebook.com/docs/whatsapp/business-management-api/get-started#system-user-access-token).
</blockquote>


Click **Done** when you are finished configuring the connector.

## Message types

For WhatsApp Business API, there are two primary message types:

* **Template Messages** are pre-approved by WhatsApp and are designed for business-initiated conversations, such as sending alerts, updates, or re-engagement messages. These messages can include variables and are required when messaging users who haven’t contacted your business in the past 24 hours. 

* **Text-Based Messages** are session-based and can only be used in response to a user-initiated message within a 24-hour window. They offer greater flexibility for dynamic, conversational content, but are not allowed for unsolicited outreach. 

Use Template Messages when initiating a conversation or sending notifications outside of the 24-hour window, and use Text-Based Messages to maintain real-time interactions during an active session with the user.

Before sending a template message, you need to create a template. For more information, see [WhatsApp: Create Message Templates for Your WhatsApp Business Account](https://www.facebook.com/business/help/2055875911147364).

|Action Name| AudienceStream| EventStream|
|---| ---| ---|
|Send Text Message| ✓| ✓|
|Send Message Template| ✓| ✓|

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type.

The following section describes how to set up parameters and options for each action.

### Send Text Message

#### Parameters

|Parameter| Description|
|---| ---|
|Send From| Phone Number ID you want to send a message from.|
|Send To| WhatsApp ID or phone number you want to send a message to. For more information, see [WhatsApp: Phone Numbers, Formatting](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/phone-numbers#formatting).|
|Message| The text of the message, which can contain URLs and formatting. For usage examples, see [WhatsApp: Send Text Messages](https://developers.facebook.com/docs/whatsapp/cloud-api/guides/send-messages#text-messages).|
|Preview URL| Boolean value (`true` or `false`) to allow or disable URL previews in text messages. For more information, see [WhatsApp: Sending URLs in Text Messages](https://developers.facebook.com/docs/whatsapp/api/messages/text#urls).|

### Send Message Template

#### Parameters

|Parameter| Description|
|---| ---|
|Send From| Phone Number ID you want to send a message from.|
|Send To| WhatsApp ID or phone number you want to send a message to. For more information, see [WhatsApp: Phone Numbers, Formatting](https://developers.facebook.com/docs/whatsapp/cloud-api/reference/phone-numbers#formatting).|
|Message Template| Provide the message template. For usage examples, see [WhatsApp: Send Message Templates](https://developers.facebook.com/docs/whatsapp/cloud-api/guides/send-message-templates).<br> The template expects a valid JSON object format.<br> You can use template variables specified in the **Message Template Variables** section. For more information, see [about-connector-templates](https://docs.tealium.com/about-connector-templates/).|
|Message Template Variables| Provide template variables as data input for the **Message Template**. For more information, see [connector-template-variables](https://docs.tealium.com/connector-template-variables/).<br> Name nested template variables with the dot notation (Example: `items.name`).<br> Nested template variables are typically built from data layer list attributes.|