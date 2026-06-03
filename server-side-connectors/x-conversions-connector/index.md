---
title: X Conversions Connector Setup Guide
description: This article describes how to set up the X Conversions connector.
url: https://docs.tealium.com/server-side-connectors/x-conversions-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: X Conversions API
* API Version: v12
* API Endpoint: `https://ads-api.x.com/`
* Rate limit: 60,000 events per account, per 15 minute interval
* Documentation: [X: Web Conversions API](https://developer.x.com/en/docs/x-ads-api/measurement/web-conversions/api-reference/conversions)

## Prerequisites

* [X Ads API](https://developer.x.com/en/docs/x-ads-api/getting-started) access
* [X Developer](http://developer.x.com) account
* X user account with permissions to send events to the ad accounts you want

If you already have an actively used X Ads API application, both the application and existing access tokens can be used for the Conversion API. For more information, see [X: Conversion API Set Up](https://developer.x.com/en/docs/x-ads-api/measurement/web-conversions/conversion-api).

## How it works

Use the X Conversion API to create a separate server-side application that passes conversion events to X for use in optimization, measurement, and attribution across your campaigns. With this API, you can measure the impact of running ads on X by sending conversion events without the need for a X website pixel.

Currently, there are two primary use cases for measuring ad impact using matching identifiers:

* Click-through conversions for website traffic campaigns using the X Click ID
* View-through and click-through conversions for all X campaigns using email

You can measure one or more of the following website actions with conversion tracking depending on your ad campaign:

* **Site visit**: User visits a landing page on an advertiser’s site
* **Purchase**: User completes a purchase of a product or service on the advertiser’s site
* **Download**: User downloads a file, such as a white paper or software package, from the advertiser’s site
* **Sign up**: User signs up for the advertiser’s service, newsletter, or email communication
* **Custom**: This is a catch-all category for a custom action that does not fall into one of the categories above

### Using the X Conversion API

To use the X Conversion API, you need to create a new conversion event in the X Ads Manager or use an existing event already created and used with the X Pixel. To deduplicate conversions between X Pixel and X Conversion API requests, use the existing event you created for the Pixel.

#### Using an Existing Conversion Event in Ads Manager

To use an existing event used with the X Pixel, use the Event ID from that event. If you use both X Pixel and the X Conversion API for the same event, ensure to use the deduplication key in both the X Pixel code snippet and the X Conversion API request (as `conversion_id`). For more information about deduplication, see the Testing Events and Deduplication section in [Conversion API Set Up](https://developer.x.com/en/docs/x-ads-api/measurement/web-conversions/conversion-api) in the X documentation.

#### Identifiers for Conversion Events

For a conversion event to be passed in the X Conversion API, there needs to be at least one X Click ID (`twclid`) or email address set as the as the event identifier.

To successfully setup conversion events to be passed to the X Conversion API, we recommend the following configurations:

* Always parse the `twclid` value when it is present in the URL query parameters to be passed to Tealium EventStream API Hub.
* Store the data alongside relevant form fields or conversion event information.

#### Deduplication

For Page View events, including X-defined **Site Visit** and **Landing Page View** events, X provides a 30 minute window for deduplication. Other event types, such as **Purchase** and **Lead**, are not deduplicated.

Manage event duplication using the `conversion_id` event parameter, which can be included in Pixel or X Conversion API requests.

## Configure Settings

X Conversions requires allowlisting on your X account. For assistance with allowlisting, contact your X representative.

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Event ID**  
The base36 ID of a specific event. It matches a pre-configured event contained within this ad account. This is called **ID** in the corresponding event in Events Manager.
This value can be created in the following ways:
  * Within the Single-Event Website tag configuration. Log in to your ads account at [https://ads.x.com/](https://ads.x.com/) and select **Events Manager** under **Tools**.
  * Use the API. For more information, see [X: Web Event Tags](https://developer.x.com/en/docs/x-ads-api/measurement/api-reference/web-event-tags).
  * Contact your X account manager.

* **Pixel ID**  
The Universal Website Tag (UWT) ID for an ad account. This represents the base36-encoded value for an ad account&#39;s UWT ID.  
  To obtain your Pixel ID:
  1. Log in to your ads account at [https://ads.x.com/](https://ads.x.com).
  1. In the top left corner of the interface, under **Tools**, click **Events Manager**.
  1. If you do not have a X Pixel event source on your left sidebar yet, in the top right corner of the page, select **Add event source**.
  1. The interface displays the Pixel ID and Event ID of this event that is used in the API.

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Conversion Event| ✓| ✓|

Click **Continue** to configure the connector actions. Enter in a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion Event

#### Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions].() Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### User Data

You must provide at least one of the following parameters:

| **Parameter** | **Type** |**Description** |
| --- | --- | -- |
| X Click ID | String | X Click ID as parsed from the click-through URL. Either X Click ID or Email must be specified. Use both to increase match rate. |
| Email Address (already SHA256 hashed) | String | Provide an email address which has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | String | Provide a plain text email address and the connector whitespaces trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | String | Provide a phone number which has been already whitespace trimmed, lowercased, SHA256 hashed, and in E164 format. |
| Phone Number (apply SHA256 hash) | String | Provide a plain text phone number and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
|  `ip_address` |  String |  This value is written in dotted-decimal notation, with four numbers separated by periods. |
| `user_agent` | String | This identifier allows the server to identify the application, operating system, vendor, and/or version of the requesting user agent. |

#### Additional parameters

| **Parameter** | **Description** |
| --- | --- |
| Event ID Override | This is called **Website Tag ID** in the Ads Manager and Ads API and can be found in the **Events Manager** of the X Ads platform. This parameter is a required field, and this setting overrides **Event Source ID** used in the configuration section. |
| Pixel ID Override | The Universal Website Tag (UWT) ID for an ad account. This parameter represents that base36-encoded value for an ad account’s UWT ID. For example: `o5h34`. This setting overrides the **Pixel ID** used in the configuration section. |
| Conversion Time | (Required) The time of a conversion event. Specify date-time of event expressed in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601). If not provided, the value is the time of the event. Example: `2020-11-01T08:00:00.000Z`. |
| Conversion Value | The price value of items being purchased, represented in `price_currency` currency. |
| Number of Items | The number of items being purchased. Must be a positive number greater than zero. If **Number of Items** is not provided, the total number of elements in the **Contents** array is used. |
| Currency | The type of a currency to filter results by, identified using [ISO 4217 format](https://en.wikipedia.org/wiki/ISO_4217). This is a three-letter string, such as `USD`. |
| Conversion ID | For deduplication between pixel and conversion API conversions. An identifier for a conversion event that can be used for de-duplication between Web Pixel and Conversion API conversions in the same event tag. For more information, see [X: Conversion API Set Up](https://developer.x.com/en/docs/x-ads-api/measurement/web-conversions/conversion-api). |
| Description | Description with any additional information on the conversions. |
| Search String | Text that was searched for on the advertiser&#39;s website. |

#### Contents Attributes

Optional parameters: 

| **Parameter** | **Description** |
| --- | --- |
| Content ID | A SKU or GTIN (Global Trade Item Number) identifier that represents the content. |
| Content Group ID | The ID associated with a group of product variants. |
| Content Name | The name of the product or service. |
| Content Price | The price of the product or service. |
| Content Type | The category for the product that was purchased. |
| Number of Items | The number of products purchased. |