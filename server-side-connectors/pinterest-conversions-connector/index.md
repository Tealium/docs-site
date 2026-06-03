---
title: Pinterest Conversions Connector Setup Guide
description: This article describes how to set up the Pinterest Conversions connector.
url: https://docs.tealium.com/server-side-connectors/pinterest-conversions-connector/
---
## Requirements

* A Pinterest Ad Account with permissions to send conversion events.
* The ability to send one of the following valid user identities in `user_data`:
    * Email (already SHA256 hashed) (`em`).
    * Apple&#39;s Identifier for Advertisers (already SHA256 hashed) or Google Advertising ID (already SHA256 hashed) (`hashed_maids`).
    * Client IP Address and Client User Agent (`client_ip_address` and `client_user_agent`).
    * App ID (if applicable).  Pinterest requires at least one valid user identity for matching. Organizations with PII restrictions should obtain approvals before setting up this integration.
* For all offline events:
    * You must set the **Event Action Source** to `Offline` in the connector configuration.
    * Offline events must include all required event parameters. For more information, see [Pinterest: Format server event parameters](https://developers.pinterest.com/docs/track-conversions/track-conversions-in-the-api/#format-server-event-parameters).

## API information

This connector uses the following vendor API:

* API Name: Pinterest API
* API Version: v5
* API Endpoint: `https://api.pinterest.com/`
* Vendor documentation: [Pinterest: Conversions Guide](https://developers.pinterest.com/docs/conversions/conversion-management/)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 2 MB

## How it works

The Pinterest API for Conversions lets advertisers send conversion events to Pinterest without using the Pinterest tag. Mapping conversions to Pinterest campaigns increases conversion visibility and provides a more accurate view of campaign effectiveness and the actions driving conversions. This approach optimizes targeting, increases transparency, and improves reporting and analysis.

The Pinterest API for Conversions can receive web, in-app, or offline conversions. Events received within an hour of the event occurring are reported as web or app events. Events received outside of that window are categorized as offline events.

We recommend using both the Pinterest Conversions connector and the Pinterest tag together to maximize visibility and track conversions. The Pinterest Conversions connector is available as a standalone solution; however, using both the Pinterest Conversions connector and the Pinterest tag together provides the best results.

Events that can be tracked include:

* **Add to Cart**: Items are added to shopping carts.
* **Checkout**: Completed transactions.
* **Custom**: Track a custom event. Use this event name to track a special event that you want to include in your conversion reporting.
* **Lead**: Interest in product or service.
* **Page Visit**: Views of primary pages, such as product pages and article pages.
* **Search**: Searches on your website.
* **Signup**: Signups for your products or services.
* **View Category**: Views of category pages.
* **Watch Video**: Video views.
* **User-Defined Event**: Add any additional events that you’ve defined for the purpose of audience targeting. Unique events are not available for conversion reporting.

## Deduplication

If redundant implementations exist (for example, the Pinterest API for Conversions and [Pinterest tag]()), deduplication is required to prevent double-counting of a single event when it is sent through both solutions. By using deduplication, advertisers can expect more conversions to be attributed than if the connector or tag solution is used independently.

The [Pinterest tag]() and Pinterest API for Conversions use the Event ID for deduplication. Ensure this value is included when multiple sources are used to track conversion data. To find your Event IDs, complete the following steps:

1. Log in to your [Pinterest business account](http://pinterest.com/business/create/).
1. Navigate to  **Ads &gt; Reporting**.
1. Click the menu icon in the top-right above the table and select **Performance**.

Depending on what event codes you’ve added to your site, they will be listed throughout the table along with the number of times they’ve happened during the selected timeframe.

Look for event attributes using the following naming convention:

```none
pinterest_event_id_{PINTEREST_EVENT}_{TAG_UID}
```

For example: `pinterest_event_id_Checkout_32`

Use a separate action for each type of event ID. Map the event-specific event ID attribute to Event ID with the matching event name mapped to Event Name. For example:

| **Tealium Attribute/Value** | Pinterest Parameter |
|---|---|
| `pinterest_event_id_Checkout_32` | Event ID |
| `Checkout` (dropdown selection) | Event Name |

For more information, see the [Pinterest Tag Setup Guide]().

### Confirm deduplication

Pinterest does not display a deduplicated conversions metric. Instead, you confirm deduplication by validating the following items:

* The `event_id` exists in both web and API payloads.
* The conversion shows only one time in reporting after triggering both versions.

To view `event_id` in Pinterest Ads Manager, use the following steps:

1. Go to **Ads Manager &gt; Conversions &gt; Events**.
1. Select your Ad Account.
1. Select the event (for example, Checkout).
1. Open **Event Diagnostics**.
1. Click an event payload to expand it.
1. Confirm the following:
    * `event_source` = `web` or `api`
    * `event_id` matches
    * **User data status** = `accepted`

## Validation

To validate the connector action, use test event code as follows:

1. In the **Send Conversion Event** action, select **Testing Mode**.
1. Send a test event.
1. In Pinterest, use the following steps:
    * Go to **Conversions &gt; Events &gt; Test Events**.
    * Confirm receipt and payload integrity.

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

When you add this connector, you are prompted to accept the vendor&#39;s data platform policy.

After adding the connector, configure the following settings:

* **EULA Agreement**: (Required) Select the checkbox to accept Pinterest&#39;s data platform policy.
* **Access Token**: (Required) Access token generated through the Pinterest Ads Manager. For more information, see [Pinterest: Conversions Guide](https://developers.pinterest.com/docs/conversions/conversion-management/#Authenticating%20for%20the%20Conversion%20Tracking%20endpoint).
* **Ad Account ID**: (Required) Unique identifier of an ad account. To locate your **Ad Account ID** in Pinterest, log in to the Pinterest account that owns your advertiser account and navigate to **Ads &gt; Overview**. The **Ad Account ID** is visible in the URL path. For example, `ads.pinterest.com/advertiser/{ad_account_id}/...` .

Click **Done** when you finish configuring the connector.

### Offline conversions

Offline events allow you to measure the impact of ads on purchases, interactions, and conversions that happen outside of your website or app, such as in a physical retail location. To process offline events and conversions through the Pinterest Conversions connector, configure the connector to include the required parameters. 

#### Configuration steps

To configure the Pinterest Conversions connector to send offline events:

1. In the **Actions** tab, add a new **Send Conversion Event** action.
1. Map the **Event Action Source** parameter to `Offline`.
1. Map the required parameters, and include optional parameters as needed for your event type.
    * Pinterest recommends mapping a transaction ID, order ID, or Tealium Random to the required Event ID parameter for offline events. 
1. Verify in Pinterest Ads Manager.

## Actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Send Conversion Event | ✓ | ✓ |

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion Event

| **Parameter** | **Description** |
| --- | --- |
| Event Name | (Required) The type of the user event to record. &lt;br&gt;Note: Events with custom event types will not be available to use in reporting.&lt;br&gt;**Add to Cart** - Items are added to shopping carts.&lt;br&gt;**Add to Wishlist** - Items are added to a wishlist.&lt;br&gt;**Checkout** - Completed transactions.&lt;br&gt;**Custom** - Use this event name to track a special event that you want to include in your conversion reporting.&lt;br&gt;**Initiate Checkout** - Checkout process starts. For example, a user clicks a checkout button.&lt;br&gt;**Lead** - Interest in product or service.&lt;br&gt;**Page Visit** - Views of primary pages, such as product pages and article pages.&lt;br&gt;**Search** - Searches on your website.&lt;br&gt;**Signup** - Signups for your products or services.&lt;br&gt;**Subscribe** - User subscribes to a service, such as content streaming or monthly emails, or a product offering, such as monthly deliveries.&lt;br&gt;**View Category** - Views of category pages.&lt;br&gt;**View Content** - User visits a web page related to your business, such as a product or landing page.&lt;br&gt;**Watch Video** - Video views. |
| Event Action Source | (Required) Source indicating where the conversion event occurred. &lt;br&gt;**App Android** - Through mobile in-app events from an Android device.&lt;br&gt;**App iOS** - Through mobile in-app events from an iOS device.&lt;br&gt;**Offline** - Event is from offline.&lt;br&gt;**Web** - Through desktop web browsers as well as mobile web browsers. |

#### Conversion Event Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event ID | (Required) A String value that contains a unique ID for the event. This ID can be used for deduplication of events ingested from the Pinterest API for Conversions and the Pinterest Tag. |
| Ad Account ID Override | This setting overrides the Pinterest **Ad Account ID** used in the connector configuration section. Either **Ad Account ID Override** or **Ad Account ID** in the connector configuration section must be provided. |
| Event Time | Unix timestamp (in UTC) in seconds indicating when the user conversion event occurred. The event time cannot be later than the time Pinterest received the request. If this field is not mapped, it is initialized with the current timestamp. |
| Event Source URL | URL of the web conversion event. |
| Opt Out | When **Event Action Source** is **Web** or **Offline**, this parameter defines whether the user has opted out of tracking for web conversion events. When **Event Action Source** is **App Android** or **App iOS**, it defines whether the user has enabled Limit Ad Tracking on their iOS device, or opted out of Ads Personalization on their Android device. |
| Event Name Override |  When **Event Name** is set to **Custom**, specify the name of the custom event in this field. |

#### User Data

Data mapping must meet the following requirements:

* Map array type attributes to add multiple values.
* Map single value attribute to add a single value. Only single value attributes should be mapped to the **Client IP Address** and **Client User Agent** fields.

The following parameters are required:

| **Parameter** | **Description** |
| --- | --- |
| Email (already SHA256 hashed) | Provide an email address which has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Email (apply SHA256 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Apple&#39;s Identifier for Advertisers (already SHA256 hashed) | Provide an Apple&#39;s Identifier for Advertisers which has already been whitespace trimmed and SHA256 hashed. |
| Apple&#39;s Identifier for Advertisers (apply SHA256 hash) | Provide a plain text Apple&#39;s Identifier for Advertisers and the connector whitespace trims and hashes this value using SHA256 hash. |
| Google Advertising ID (already SHA256 hashed) | Provide a Google Advertising ID which has already been whitespace trimmed and SHA256 hashed. |
| Google Advertising ID (apply SHA256 hash) | Provide a plain text Google Advertising ID and the connector whitespace trims and hashes this value using SHA256 hash. |
| Client IP Address | The user&#39;s IP address, which can be either in IPv4 or IPv6 format. |
| Client User Agent | The user agent string of the user&#39;s web browser. |
| Phone Number (already SHA256 hashed) | Provide a phone number which contains only numeric characters, has already been whitespace trimmed and SHA256 hashed. Remove leading zeros before hashing. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector will remove all non-numeric characters and leading zeroes, whitespace trims, and hash this value using SHA256 hash. |
| Gender (already SHA256 hashed) | Provide a gender which has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Gender (apply SHA256 hash) | Provide a plain text gender and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Birthdate (already SHA256 hashed) | Provide a birthdate which has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Birthdate (apply SHA256 hash) | Provide a plain text birthdate and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| First Name (already SHA256 hashed) | Provide a first name which has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name which has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| City (already SHA256 hashed) | Provide a city which has already been whitespace trimmed, lowercased, and SHA256 hashed. Remove spaces and punctuation before hashing. |
| City (apply SHA256 hash) | Provide a plain text city and the connector removes spaces and punctuation, whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| State (already SHA256 hashed) | Provide a state which has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| State (apply SHA256 hash) | Provide a plain text state and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Zip Code (already SHA256 hashed) | Provide a zip code which contains only numeric characters, has already been whitespace trimmed and SHA256 hashed. |
| Zip Code (apply SHA256 hash) | Provide a plain text zip code and the connector removes all non-numeric characters, whitespace trims, and hashes this value using SHA256 hash. |
| Country Code (already SHA256 hashed) | Provide a country code which has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Country Code (apply SHA256 hash) | Provide a plain text country code and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| External ID (already SHA256 hashed) | Provide one or more external IDs, already whitespace trimmed and SHA256 hashed, and formatted as an array if there are multiple External IDs. For more information, see [Pinterest: What is an External ID?](https://developers.pinterest.com/docs/api-features/conversion-best-practices/#what-is-an-external-id).|
| External ID (apply SHA256 hash) | Provide one or more plain text external IDs and the connector whitespace trims and hashes these values using SHA256 hash. If you provide multiple External IDs, format them as an array. |
| Click ID  | The unique identifier stored in the `_epik` cookie on your domain or the `&amp;epik=` query parameter in the URL. This can improve reporting performance such as ROAS/CPA. |

#### Custom Data

| **Parameter** | **Description** |
| --- | --- |
| Currency | The ISO 4217 currency code. If not provided, Pinterest uses the advertiser&#39;s currency set during account creation. |
| Value | The total value of the event. The connector accepts a string value and then parses it into a [double-precision number](https://en.wikipedia.org/wiki/Double-precision_floating-point_format). For a checkout event with multiple items, use the total price of all items. |
| Content IDs | List of product IDs. |
| Number of Items | Total number of products of the event. For example, the total number of items purchased in a checkout event. |
| Order ID | The order ID. |
| Search String | The search string related to the user conversion event. |
| Opt Out Type | Flags for different privacy rights laws to opt out users of sharing personal information. Values should be comma separated. Array type attributes can be mapped and are converted to a comma separated string. |

#### Contents Data

* Provide array type attributes to add multiple items in the conversion. Array type attributes must be of equal length.
* If you map a single value attribute to a parameter, the value applies to every item in the array for the conversion.

| **Parameter** | **Description** |
| --- | --- |
| Item Price | The price per individual item in the conversion. The connector accepts a string value and then parses it into a [double-precision number](https://en.wikipedia.org/wiki/Double-precision_floating-point_format). For a checkout event with multiple items, provide the price for each item. |
| Quantity | The amount of a product. |
| ID |  The ID of a product. Recommended for **AddToCart** and **Checkout** events. | 
| Item Name | The name of the product. | 
| Item Category |  The category of the product. | 
| Item Brand | The brand of the product. | 

#### App Information

| **Parameter** | **Description** |
| --- | --- |
| App ID | The app store app ID. |
| App Name | Name of the app. |
| App Version | Version of the app. |
| Device Brand | Brand of the user device. |
| Device Carrier | User device&#39;s mobile carrier. |
| Device Model | Model of the user device. |
| Device Type | Type of the user device. |
| OS Version | Version of the device operating system. |
| WiFi | Whether the event occurred when the user device was connected to WiFi. |
| Language | Two-character ISO 639-1 language code indicating the user&#39;s language. |

#### Automatic Deduplication

| **Parameter** | **Description** |
| --- | --- |
| Tealium iQ Tag ID | When the Tealium iQ Tag ID is provided, the event ID value sent from Tealium iQ is automatically identified and sent to Pinterest. The UDO value used to identify the event ID is `pinterest_event_id_EVENTNAME_TAGID`. |

#### Testing Mode

| **Parameter** | **Description** |
| --- | --- |
| Testing Mode | Select the checkbox to mark the request as a test request. The events will not be recorded, but the API  still returns the same response messages. Use this mode to verify your requests are working and your events are constructed correctly. |

#### Disable Automapping

| **Parameter** | **Description** |
| --- | --- |
| Disable Automapping |  Disable automatic mapping for the connector.|

#### Configuration

| **Parameter** | **Description** |
| --- | --- |
| Access Token | Access Token generated through the Pinterest Ads Manager. For more information, see [Pinterest: Conversions Guide](https://developers.pinterest.com/docs/track-conversions/track-conversions-in-the-api/#Authenticating%20for%20the%20Conversion%20Tracking%20endpoint). |