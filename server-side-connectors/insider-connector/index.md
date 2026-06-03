---
title: Insider Connector Setup Guide
description: This article describes how to set up the Insider connector.
url: https://docs.tealium.com/server-side-connectors/insider-connector/
---
## API Information

This connector uses the following vendor API:

*   API Name: Insider API
*   API Version: v1
*   API Endpoint: `https://unification.useinsider.com/api/user/v1`
*   Documentation: [Insider APIs](https://academy.useinsider.com/docs/api-reference-insider-apis)

## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Upsert and Subscribe (Batched) | ✓ | ✓ |
| Upsert and Subscribe (Real-Time) | ✓ | ✓ |
| Delete Attribution (Batched) | ✓ | ✓ |
| Delete Attribution (Real-Time) | ✓ | ✓ |
| Delete User | ✓ | ✓ |

### Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

*   Max number of requests: 1000
*   Max time since oldest request: 10 minutes
*   Max size of requests: 5 MB

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

*   **Partner Name**&lt;br&gt;Navigate to **Inone &gt; Inone Settings &gt; [Account Preferences](https://academy.useinsider.com/docs/account-preferences)** to copy and paste your partner name.
*   **API Key**&lt;br&gt;An API key is required to authorize your request. For information on generating a token, see [API Authentication Tokens](https://academy.useinsider.com/docs/api-authentication-tokens).

When you are finished configuring the connector, click **Done**.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type.

This section describes how to set up parameters and options for each action.

### Action — Upsert and Subscribe (Batched or Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
|  | **User Identifiers** |
| Email | User&#39;s email address. |
| Phone Number | User&#39;s phone number in E.164 format. For example: &#43;6598765432. |
| UUID | User&#39;s UUID parameter. |
| User Custom Identifiers | User&#39;s custom identifier information. At least one default or custom user identifier must be provided. |
|  | **User Attributes** |
| Email Opt In | User&#39;s permission for marketing emails. When true, emails allowed. When false, email not allowed. |
| GDPR Opt In | User&#39;s permission for Insider campaigns, data collection and processing. When true or empty, Insider may interact with the user through personalization campaigns. When false, user will not see any Insider campaign or receive any message from any channel. |
| SMS Opt In | User&#39;s permission for SMS messages. When true, SMS allowed. When false, SMS not allowed. |
| WhatsApp Opt In | User&#39;s permission for WhatsApp Message. When true, WhatsApp Message allowed. When false, WhatsApp Message not allowed. |
| Name | User&#39;s name. |
| Surname | User&#39;s surname. |
| Birthday | User&#39;s birthday in RFC 3339 format. For example: 1993-03-12T00:00:00Z. |
| Gender | User&#39;s gender. |
| Age | User&#39;s age. |
| Language | Language information for the user. |
| Country | Country information of the user in ISO 3166-1 alpha-2 format. |
| City | User&#39;s city. |
| List ID | Newsletter contact list IDs (users are added directly). |
| User Custom Attributes | Select custom attributes. At least one default or custom user attribute or one event must be provided. |
| | **Events Parameters** |
| Event Name | (Required) Name of the event. |
| Event Time | (Required) The purchase date for the purchase event in RFC 3339 format. For example: 2021-01-10T21:35:20Z. |
| Event Group ID | Event group ID. |
| Product ID | Unique product ID. |
| Name | Name of the product. |
| Currency | Currency used for product pricing, in ISO 4217 format. For example: USD. |
| Unit Price | Price of the product without any discounts. |
| Unit Sale Price | Unit price of the product. |
| Color | Color of the product (selected by user). |
| Size | Size of the product (selected by user). |
| Shipping Cost | Shipping cost of the items in basket. |
| Promotion Name | Name of the promotion. |
| Promotion Discount | Total amount of discount applied by promotions. |
| Events Custom Parameters | Select custom event parameters |
| | To add multiple events, provide array attributes. Array type attributes must be of equal length. Events Parameters arrays and Events Custom Parameters arrays must be of equal length. Single value attributes can be used and apply to each event. |
| | **Templates and Template Variables** |
| Events Template Variables | Provide template variables as data input for **Events Template**. For more information and usage examples, see . Name nested template variables with the dot notation. For example: `items.name`. Nested template variables are typically built from data layer list attributes. |
| Events Template | To support nested objects, define a template, which is a JSON array of variables. Template variables mapped in the **Events Template Variables** section can be used in the template. When a template is defined, configuration in the **Events Parameters** and **Events Custom Parameters** sections is ignored. For more information on templates, see the [Templates Guide]().|

### Action — Delete Attribution (Batched or Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| | **User Identifiers** |
| Email | User&#39;s email address. |
| Phone Number | User&#39;s phone number in E.164 format. For example: &#43;6598765432. |
| UUID | User&#39;s UUID parameter. |
| User Custom Identifiers | Provide user&#39;s custom identifier information. At least one default or custom user identifier must be provided. |
| | **User Attributes** |
| Whole Delete Default User Attributes | Select default user attributes that are going to be deleted fully from the corresponding user.  |
| Whole Delete Custom User Attributes | Select custom user attributes that are going to be deleted fully from the corresponding user. 
| Partial Delete Default User Attributes | Select default user attributes that are going to be deleted partially. For example, removing one of the values from an array attribute. Only array type attributes can be partially deleted. Use array type attributes to delete multiple values. Single value attributes are converted to an array containing a single value.
| Partial Delete Custom User Attributes | Select custom user attributes that are going to be deleted partially. For example, removing one of the values from an array attribute. Only array type attributes can be partially deleted. Map array type attributes to delete multiple values. Single value attributes are converted to an array containing single value. |
| List ID | (Optional) For partial delete only. Newsletter contact list IDs (users are added directly). |

### Action — Delete User

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Email | User&#39;s email address. |
| Phone Number | User&#39;s phone number in E.164 format. For example: &#43;6598765432. |
| UUID | User&#39;s UUID parameter. |
| User Custom Identifiers | Provide user&#39;s custom identifier information. At least one default or custom user identifier must be provided. |