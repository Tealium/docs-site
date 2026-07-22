---
title: Snapchat Conversions Connector Setup Guide
description: This article describes how to set up the Snapchat Conversions connector.
url: https://docs.tealium.com/server-side-connectors/snapchat-conversions-connector/
---
## How it works

The Snapchat Conversions connector uses the Snap Conversions API. The Snap Conversions API is a structured, privacy-centric interface that lets you directly pass web, app, and offline events to Snap through a Server-to-Server (S2S) integration. This API supports event tracking similar to the tracking provided by the Snap Pixel and uses the device type used to make the conversion. This feature lets you use the Snap App ID for mobile conversions and use the Pixel ID for web and offline conversion events.

Snap Conversions API can be deployed standalone or in-conjunction with the client-side Snap Pixel.

For more information about Snap's Conversions API, see [Snap: Conversion API](https://businesshelp.snapchat.com/s/article/conversions-api?language=en_US).

## API Information

This connector uses the following vendor API:

* API Name: Snapchat Marketing API - Conversion API
* API Version: v3
* API Endpoint: `https://tr.snapchat.com/v3/conversion`

## Considerations

* To unlock campaign optimization, we recommend that you send events as soon as they occur, ideally within an hour of the event occurring.
* We strongly recommend passing data in real-time. By doing so, you will see your campaign-driven results more quickly and ensure your bids are staying competitive with current marketplace demand.
* Conversions API requests are tied to unique identifiers that link server events back to your Snapchat ad account. We use your [Pixel ID](https://businesshelp.snapchat.com/s/article/pixel-website-install?language=en_US) for web and offline events and your [Snapchat App ID](https://businesshelp.snapchat.com/s/article/snap-app-id?language=en_US) for app events.

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2000
* Max time since oldest request: 10 minutes
* Max size of requests: 2 MB

## Deduplication

The Snap Conversions API can be used as a standalone API or alongside other Snapchat solutions. To minimize signal loss and create more efficient results, we recommend passing the same events through the Snap Conversion API that you have configured in your Snap Pixel.

Snap Conversions API shows only Event Deduplication if the following conditions are met:

* Snap App ID, Pixel ID, or both has multiple sources (API, SDK, etc.)
* Events are for the same conversion type (Web, App, or Offline)
* The selected event is added on two or more sources

Tealium has deduplication recommendations based on your integration configuration:

* **Single source redundancy** - The duplication of events sent in the same integration.  
If you send the conversion multiple times through the same integration source, we highly recommend passing consistent information.
* **Cross source redundancy** - The duplication of events sent from multiple integrations.  
When sending data from multiple integrations, we recommend sending redundant data to ensure the best optimization, targeting, and measurement capabilities.

Depending on your deduplication use case, use the following parameters:

* **Event ID** - Deduplicates unique events for web and offline channels. Allows for a 48 hour deduplication window.
* **Transaction ID** - Eligible for deduplicating purchase events for all channels (web, mobile, and offline). Allows for a 30 day deduplication window.
* **Mobile Ad ID** - Use a shared device identifier like AAID or hashed IDFV for unique event deduplication.

For more information, see [Snap: Best Practices - Deduplication](https://developers.snap.com/api/marketing-api/Conversions-API/BestPractices#deduplication).

#### Automatic deduplication


<blockquote>
In version 3, the connector uses **Event ID** for deduplication instead of **Client Dedup ID**.
</blockquote>


When the **Automatic Deduplication** value is populated with a Tealium iQ tag UID, the connector looks for the corresponding event attribute. If this section is populated and you are using Tealium iQ, you are no longer required to add an **Event ID**. However, the following approach may still be needed when using EventStream without Tealium iQ.

The connector order of operations is as follows:

* If **Automatic Deduplication** is populated, and the value is found in the data layer, (for example, `6V5xX1T0n9pC42luElKD`) this value supersedes anything mapped in **Event ID**.
* If **Automatic Deduplication** is populated, but it cannot find the tag ID version, but it can find the legacy version (with no ID attached), that value is used (for example, `6V5xX1T0n9pC42luElKD`).
* If **Automatic Deduplication** is populated, but the value isn't found, the mapped **Event ID** is used, if it is populated.

You can find your tag's UID in the Tealium iQ **Tags** table or the tag details screen:

![](https://docs.tealium.com/images/server-side-connectors/snap-pixel-uid.png)

## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| Send Conversion V3 | ✓                  | ✓               |

## Configure Settings

Go to the Connector Marketplace and add a new connector. See the [Connector Overview](https://docs.tealium.com/about-connectors/) for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Long Lived Token**: This method of authentication does not need the 3-legged OAuth flow and does not expire. For more information, see [Snap: Static Long Lived Tokens](https://marketingapi.snapchat.com/docs/conversion.html#static-long-lived-tokens)

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Conversion V3

### Parameters

| Parameter          | Description               |
|---|---|
| Event Type              | Select the event type from the drop-down list.           |
| Event Conversion Type   | Where the event took place. For example, `OFFLINE`, `WEB`, or `MOBILE_APP`.              |

#### Conversion Data

| Parameter | Description |
| --- | --- |
| Pixel ID | The Pixel ID associated with your Ad Account. |
| App ID | The unique ID assigned for a given application. iOS IDs are numeric, and Android IDs are the Google Advertising ID (`GAID`) |
| Snap App ID | The Snap App ID associated with your app, which is a unique code generated in Ads Manager and included in your MMP dashboard. |
| Event Tag | Custom event set label. For example, in-store, weekend sales, back-to-school campaign. This parameter can be used for future tagging and audience targeting. |
| Event Time | The Epoch timestamp for this conversion. If this field is not mapped, it is initialized with the current timestamp. This parameter is automapped. To override the automapping, map an attribute or disable automapping.|
| Event Source URL | The URL of the Event Source. |
| Event ID | The Event ID. |
| Data Processing Options |  Indicates either opt in or opt out for `WEB` events. For users of iOS 14.5 and above that opt out, set this parameter’s value to a list that has a single element of the value `LMU`. Otherwise, do not set this parameter. Accepted values are: `LMU`, `DELETE`. |
| Advertiser Tracking Enabled |Indicates either opt in or opt out for `MOBILE_APP` events. Accepted values are: `True` for opt in or `False` for opt out. |
| Description | The string description for additional info. |
| Level | Represents a level in the context of a game. |
| Tealium Collect Endpoint | The URL of your Tealium Collect Endpoint. |

#### Content Data

| Parameter | Description |
| --- | --- |
| Content Category | Category of item(s). |
| Content IDs | The Content IDs. |
| Content Name | The name of the page or product associated with the event. |
| Content Type | The `content_type` field indicates what the keys in `content_ids` or `contents` represent. Choose `product` for individual items or `product_group` for items that have multiple options in either size, color, or any other variation. |
| Currency | Standard ISO 4217 code, for example `EUR`, `USD`, `JPY`. |
| Number Items | Number of items (integer, singular value). If this field is mapped to array, it is converted to the sum of array elements. |
| Order ID | ID of the purchased order. |
| Predicted Lifetime Value | The predicted lifetime value of a conversion event. |
| Value | The purchase value associated with the specific event. Required for `PURCHASE` event. |
| Search String | The searched text. |
| Sign Up Method | The string indicating the sign up method, Facebook, Email, X, etc. |
| Brands | Brands associated with the `item_ids` in the conversion event. |

#### Content Info

| Parameter | Description |
| --- | --- |
| ID | The item ID. |
| Quantity | The item quantity. |
| Item Price | The item price. |
| Delivery Category | The delivery method used for the order. |
| Brand | The item brand. |

#### User Info

| Parameter | Description |
| --- | --- |
| Email address (apply SHA256 hash) | Provide a lowercase plain text email address and the connector hashes this value in the format Snapchat expects. Empty or null hashed values are ignored. |
| Email address (already SHA256 hashed) | Provide an email address which has been SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a lowercase plain text phone number and the connector hashes this value in the format Snapchat expects. Empty or null hashed values are ignored. |
| Phone Number (already SHA256 hashed) | Provide a phone number that has been SHA256 hashed. |
| Mobile Ad ID | The mobile advertiser ID. |
| IP Address | The IP Address of the device. |
| Vendor Identifier | Provide a plain text vendor identifier and the connector hashes this value in the format Snapchat expects. |
| First Name (apply SHA256 hash) | Provide a first name in lowercase letters and the connector hashes this value in the format Snapchat expects. |
| First Name (already SHA256 hashed) | Provide a first name value which has been SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a last name in lowercase letters and the connector hashes this value in the format Snapchat expects. |
| Last Name (already SHA256 hashed) | Provide a last name value which has been SHA256 hashed. |
| Gender (apply SHA256 hash) | Provide the gender (`f` for female, `m` for male) and the connector hashes this value in the format Snapchat expects. |
| Gender (already SHA256 hashed) | Provide a gender value which has been SHA256 hashed. |
| City (apply SHA256 hash) | Provide a city associated with the conversion in lowercase letters and the connector hashes this value in the format Snapchat expects. |
| City (already SHA256 hashed) | Provide a city value which has been SHA256 hashed. |
| State (apply SHA256 hash) | Provide a state associated with the conversion and the connector hashes this value in the format Snapchat expects. |
| State (already SHA256 hashed) | Provide a state value which has been SHA256 hashed. |
| Zip (apply SHA256 hash) | Provide a zip or postal code in lowercase and the connector hashes this value in the format Snapchat expects. |
| Zip (already SHA256 hashed) | Provide a zip or postal code which has been SHA256 hashed. |
| Country (apply SHA256 hash) | Provide a country associated with the event and the connector hashes this value in the format Snapchat expects. |
| Country (already SHA256 hashed) | Provide a country value which has been SHA256 hashed. |
| External ID | A unique ID, such as a loyalty card ID or another identifier. |
| Subscription ID | The subscription ID for the user who generated this event. |
| Lead ID | The identifier associated with your Snapchat Lead Ad. |
| Anon ID | This parameter is only for app events. It represents a unique application install ID. |
| Download ID | The ID associated with an app download event |
| Click ID | The value of the `ScCid` query string parameter from the landing page URL. Using this ID improves ad measurement performance. We encourage advertisers using **Click ID** to pass the full destination URL to **Event Source URL**. For more information, see [Snap: Sending a Click ID](https://developers.snap.com/api/marketing-api/Conversions-API/UsingTheAPI#sending-click-id). This parameter is automapped. To override the automapping, map an attribute or disable automapping.  |
| Cookie1 | If you are using the Pixel SDK, you can access a first-party cookie by looking at the `_scid` value under your domain. This parameter is automapped. To override the automapping, map an attribute or disable automapping. |
| Client User Agent | The user agent string of the user's web browser. This parameter is automapped. To override the automapping, map an attribute or disable automapping. |


#### Dynamic Travel Ads

| Parameter | Description |
| --- | --- |
| Checkin Date | The hotel check-in date in the hotel's time-zone. Accepted formats are `YYYYMMDD`, `YYYY-MM-DD`, `YYYY-MM-DDThh:mmTZD` and `YYYY-MM-DDThh:mm:ssTZD`. |
| Travel End | End date of travel. |
| Travel Start | Start date of travel. |
| Suggested Destinations | The suggested destinations. |
| Destination Airport | The IATA code of the destination airport. |
| Country | The country, based on the location the user intends to visit. |
| City | The city, based on the location the user intends to visit. |
| Region | The state, district, or region of interest to the user. |
| Neighborhood | The neighborhood the user is interested in. |
| Departing Departure Date | The starting date and time for travel. |
| Departing Arrival Date | The arrival date and time at the destination for travel. |
| Num Adults | The number of adults staying. |
| Airport Code | The official IATA code of origin airport. |
| Returning Departure Date | The starting date and time of the return journey. |
| Returning Arrival Date | The date and time when the return journey is complete. |
| Number of Children | The number of children staying. |
| Hotel Score | The hotel's score, relative to other hotels to an advertiser. |
| Postal Code | The postal or ZIP code. |
| Number of Infants | The number of infants staying. |
| Preferred Neighborhoods | Any preferred neighborhoods for the stay. |
| Preferred Star Ratings | The minimum and maximum hotel star rating supplied as a tuple. For example, `star1,star2` or `["star1", "star2"]`. |
| Suggested Hotels | The suggested hotels. |
| Destination IDs | The ID representative of the destination in the catalog. |

#### Extended Device Info

| Parameter | Description |
| --- | --- |
| Version | (Required) The version. |
| OS Version | (Required)  The OS version. |
| App Package Name | The app package name. |
| Short Version | The short version of the application. For example, `1`. |
| Long Version | The long version of the application. For example, `1.0.12.1`. |
| Device Model Name | The device model name. |
| Locale | The device locale. The default value is `en-US`. To use a custom locale, enter a value in `xx-YY` format (2-letter language code, dash, 2-letter country code). |
| Timezone Abbreviation | The timezone abbreviation. |
| Carrier | The carrier. |
| Screen Width | The screen width. |
| Screen Height | The screen height. |
| Screen Density | The screen density. |
| CPU Cores | The number of CPU cores. |
| External Storage Size in GB | The external storage size in gigabytes. |
| Free Space on External Storage in GB | The free space on external storage in gigabytes. |
| Device Timezone | The device timezone. |

#### Automatic Deduplication

| Parameter | Description |
| --- | --- |
| Automatic Deduplication | When the Tealium iQ Tag ID is provided, we will automatically look for the Event ID value that is sent from Tealium iQ. |

#### Disable Automapping

| Parameter | Description |
| --- | --- |
| Disable Automapping | If Automapping is disabled, any automapped parameters are not sent to the vendor by default. |

#### Configuration

| Parameter | Description |
| --- | --- |
| Long Lived Token | Mapping a Snap Long Lived Token (`LLT`) will override the `LLT` provided in configuration. |