---
title: TikTok Offline Events Connector Setup Guide
description: This article describes how to set up the TikTok Offline Events connector.
url: https://docs.tealium.com/server-side-connectors/tiktok-offline-events-connector/
---
## API information

This connector uses the following vendor API:

* API Name: TikTok HTTP API
* API Version: v1.3
* API Endpoint: `https://business-api.tiktok.com/open_api/v1.3`
* Documentation: [TikTok Offline Events API](https://ads.tiktok.com/marketing_api/docs?id=1758427539356673)

## Configure settings

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Access Token**: (Required) The Access Token configured in TikTok.
* **Advertiser ID**: (Required) The ad account ID from your TikTok Ads Manager. For more information, see [TikTok: How to find your ad account ID](https://ads.tiktok.com/help/article/find-your-ad-account-id?lang=en).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Offline Events (Real-Time) | ✗ | ✓ |
| Send Offline Events (Batched) | ✗ | ✓ |

Click **Continue** to configure the connector actions. Enter a name for the action and then select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Send Offline Events (Real-Time)

We recommend that you provide either the email or phone number parameters.

Provide data type attributes for **Content Name**, **Content Type**, **Content Category**, **Content ID**, **Quantity**, and **Price** to add multiple items. Array data type attributes must be of equal length.

Single value attributes can be used and will apply to each item.

If you set **Tealium iQ Tag ID**, the connector uses the **Event ID** value that is sent from Tealium iQ Tag Management.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Name | (Required) Conversion event name. |
| Custom Event Name | Conversion event name. |
| Event Set ID | The event set ID. |
| Event ID | The unique value for each event. This ID can be used to match data with TikTok. |
| Timestamp | Timestamp of the event with ISO 8601 format. For example, `2019-06-12T19:11:01:152Z`. If no timestamp is provided, the current timestamp is used. |
| Email (already SHA256 hashed) | Provide a cleartext email address (must include an `@` symbol) that has been already SHA256 hashed. |
| Email (apply SHA256 hash) | Provide a plain text email address. The connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number that has been SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number. The connector whitespace trims and hashes this value using SHA256 hash. |
| Order ID | Order ID of the transaction. |
| Shop ID | Shop ID of the transaction. |
| Currency | Currency code, ISO 4217. |
| Value | Recommended. Revenue of total contents. |
| Event Channel | Recommended. The event channel. Supports `email`, `website`, `phone_call`, `in_store`, `crm`, `other`. |
| Content Name | Product or content name. Use an array data type attribute to add multiple contents. |
| Content Type | Product or content type. |
| Content Category | Product or content category. |
| Content ID | Product or content identifier. |
| Quantity | Number of items. |
| Price | Price of the product or content. |
| Tealium iQ Tag ID | Uses the event ID from Tealium iQ. |

### Send Offline Events (Batched)

We recommend that you provide either the email or phone number parameters.

Provide data type attributes for **Content Name**, **Content Type**, **Content Category**, **Content ID**, **Quantity**, and **Price** to add multiple items. Array data type attributes must be of equal length.

Single value attributes can be used and will apply to each item.

If you set **Tealium iQ Tag ID**, the connector uses the **Event ID** value that is sent from Tealium iQ Tag Management.

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 10 minutes
* Max size of requests: 10 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Name | (Required) Conversion event name. |
| Custom Event Name | Conversion event name. |
| Event Set ID | The event set ID. |
| Event ID | The unique value for each event. This ID can be used to match data with TikTok. |
| Timestamp | Timestamp of the event with ISO 8601 format. For example, `2019-06-12T19:11:01:152Z`. If no timestamp is provided, the current timestamp is used. |
| Email (already SHA256 hashed) | Provide a cleartext email address (must include an `@` symbol) that has been already SHA256 hashed. |
| Email (apply SHA256 hash) | Provide a plain text email address. The connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number that has been SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number. The connector whitespace trims and hashes this value using SHA256 hash. |
| Order ID | Order ID of the transaction. |
| Shop ID | Shop ID of the transaction. |
| Currency | Currency code, ISO 4217. |
| Value | Recommended. Revenue of total contents. |
| Event Channel | Recommended. The event channel. Supports `email`, `website`, `phone_call`, `in_store`, `crm`, `other`. |
| Content Name | Product or content name. Use an array data type attribute to add multiple contents. |
| Content Type | Product or content type. |
| Content Category | Product or content category. |
| Content ID | Product or content identifier. |
| Quantity | Number of items. |
| Price | Price of the product or content. |
| Tealium iQ Tag ID | Uses the event ID from Tealium iQ. |

    