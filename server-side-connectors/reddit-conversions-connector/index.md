---
title: Reddit Conversions Connector Setup Guide
description: This article describes how to set up the Reddit Conversions connector.
url: https://docs.tealium.com/server-side-connectors/reddit-conversions-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Reddit API
* API Version: v3
* API Endpoint: `https://ads-api.reddit.com/api/v3`
* Documentation: [Reddit Advertising API](https://ads-api.reddit.com/docs/v3/)

## Batch limits
  
This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

## Configuration

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Account ID**  
  * (Required) The ID of the Reddit Ad account that the conversion event belongs to.
  * To find the Reddit Ad account ID, go to **Conversions Events &gt; Pixel ID** in the Reddit Ads UI.
  * The Reddit Ad account must have the following permissions: `adsread`, `history`, `adsconversions`, and `adsleadgendownloader`.
  * For more information, see [Reddit: Authentication](https://ads-api.reddit.com/docs/v2/#section/Authentication).
* **Conversion Access Token**  
  * A conversion access token is a non-expiring secure key that lets you send conversion event data to the Reddit Conversions API.
  * Any administrator for any ad account within your business can use this easily generated, shareable, long-lived access token.
  * Reddit recommends using a conversion access token over a developer access token / OAuth for Conversions API.
  * For more information, see [Reddit: Conversion Access Token](https://business.reddithelp.com/s/article/conversion-access-token).
  * If you aren&#39;t using a conversion access token, use the **Establish Connection** button to initiate the OAuth authentication workflow.
  * To migrate from OAuth to conversion access token, enter the token in the conversion access token field and the connector uses that token instead of the OAuth token.
  * To override this token per event, map the **Conversion Access Token Override** field in the Send Conversion V3 action.

## Deduplication for web events

To configure this connector to deduplicate events from the [Reddit Pixel tag](), use the event IDs sent as event attributes with the following naming convention:

```nohl
reddit_pixel_event_id_{REDDIT_EVENT}_{TAG_UID}
```

You can find your tag&#39;s UID in the Tealium iQ **Tags** table or the tag details screen:

![](/images/server-side-connectors/facebook-pixel-tag-uid.png)

For example, a Purchase event from a tag with a UID of `168` would send the following attribute value:

```json
{
  &#34;reddit_pixel_event_id_Purchase_168&#34;: &#34;028b2ade7478...&#34;
}
```

An Add To Cart event from the same tag would send the following attribute value:

```json
{
  &#34;reddit_pixel_event_id_AddToCart_168&#34;: &#34;084b1cda7461...&#34;
}
```

Use a separate action for each type of event. Map the event-specific event ID attribute to `Event ID` with the matching event name mapped to `Event Name`. For example:

| Tealium attribute  | Reddit parameter |
|:-------------------------|:-------------------|
| `reddit_pixel_event_id_Purchase_168` (attribute)   | Event ID           |
| `&#34;Purchase&#34;` (custom text) | Event Name         |

If you&#39;re only receiving event ID attributes using the naming format `reddit_pixel_event_id_{REDDIT_EVENT}` (without the tag UID), we recommend updating your tag. For more information, see .

### Automatic deduplication

When the **Automatic Deduplication** value is populated, the connector looks for the corresponding event ID attribute. You are no longer required to map `Event ID` if this section is populated and you are using Tealium iQ. However, the following approach may still be needed when using EventStream without Tealium iQ.

The connector follows this order of operations:

* If **Automatic Deduplication** is populated and the value is found in the data layer, this value supersedes anything mapped in `Event ID`. For example, `reddit_pixel_event_id_Purchase_30`.
* If **Automatic Deduplication** is populated, but it cannot find the tag ID version, but it can find the legacy version (with no ID attached), that value is used. For example, `reddit_pixel_event_id_Purchase`.
* If **Automatic Deduplication** is populated, but the value isn&#39;t found, the mapped `Event ID` is used, if it is populated.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion V3 | ✗ | ✓ |
| Send Conversion (deprecated) | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion V3

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Type Data | The type of tracking for standard events: Add to Cart, Add to Wishlist, Lead, Page Visit, Purchase, Search, Sign Up, View Content, Custom. |
| Custom Event Type | A custom event name when tracking type is set to `CUSTOM`. Free-form, case-sensitive, up to 64 characters including spaces. For example, `Promotion Event` and `PromotionEvent` are considered two distinct events. Reddit recommends setting this to a value that doesn&#39;t match pre-existing events. |
| Event Testing | Enable testing by providing the Reddit Test ID. |

#### Conversion Event Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event At | The Unix epoch timestamp in milliseconds when the conversion event occurred. By default, the connector automatically maps `tealium_timestamp_epoch`. |
| Conversion ID | The unique conversion ID that corresponds to a distinct conversion event. Conversion ID is used for deduplication and prevents the same conversion event from being processed more than once if it is sent multiple times. |
| Value | The value of the transaction in the base unit of the currency. |
| Currency | The three-character ISO 4217 currency code for the value provided. |
| Item Count | The number of items in the event. |

#### User Data

At least one attribution signal is required with each conversion event. Reddit recommends sending as many signals as possible to improve attribution accuracy and performance. One of these must be populated: Click ID, Email address, IP address &#43; user agent &#43; screen dimensions, IDFA, AAID.

| **Parameter** | **Description** |
| --- | --- |
| Reddit Click ID | The Reddit-generated ID associated with a single ad click. The connector automatically maps this value from the `rdt_cid` query parameter unless you configure a mapping for this field. |
| Email Address | (apply SHA256 hash) Provide a plain text email address. The connector whitespace trims, lowercases, and hashes this value using SHA256. |
| Phone Number | (apply SHA256 hash) Provide a plain text phone number. The connector whitespace trims, normalizes, and hashes this value using SHA256. |
| IP Address | The connector SHA256-hashes the mapped IP address. |
| User Agent | The user agent of the user&#39;s browser. |
| External ID | (apply SHA256 hash) An advertiser-assigned persistent identifier for the user (must accompany the Reddit Click ID or an additional attribution signal). The connector whitespace trims, lowercases, and hashes this value using SHA256. |
| IDFA | (apply SHA256 hash) The IDFA of the user&#39;s device. The connector whitespace trims, lowercases, and hashes this value using SHA256. |
| AAID | (apply SHA256 hash) The AAID of the user&#39;s device. The connector whitespace trims, lowercases, and hashes this value using SHA256. |
| Screen Height | The height of the user&#39;s screen in pixels. |
| Screen Width | The width of the user&#39;s screen in pixels. |
| UUID | The value from the first-party pixel `_rdt_uuid` cookie on your domain. Use the full value or just the UUID portion. This value is not hashed. The connector automatically maps this value from the `_rdt_uuid` cookie unless you configure a mapping for this field. |

#### Products Data

| **Parameter** | **Description** |
| --- | --- |
| Product ID | An array of product IDs. |
| Product Name | An array of product names. |
| Product Category | An array of product categories. |

#### Data Processing Options

| **Parameter** | **Description** |
| --- | --- |
| Modes | An array of data processing modes for this conversion event. Reddit only supports `LDU` (Limited Data Use). |
| Country | The country code of the user in ISO 3166-1 alpha-2 standard. |
| Region | The region code of the user in ISO 3166-2 standard or the region code without country prefix. |
| Account ID Override | The ID of the Reddit Ad account that the conversion event belongs to. |
| Conversion Access Token Override | Overrides the conversion access token set in the connector configuration for this event. Use this to route events to multiple Reddit Ad accounts or to assign tokens from a secure attribute. If this field is empty or not mapped, the connector uses the configured value. If neither is set, the event is skipped. Events with different override tokens are split into separate requests. |

#### Disable Automapping

| **Parameter** | **Description** |
| --- | --- |
| Disable Automapping | When enabled, the connector does not send automapped values to the vendor by default. Explicit mappings are still applied. |

### Send Conversion (deprecated)

Reddit launched Conversions API v3, so this action is deprecated. We recommend using **Copy Mappings to an Action** to migrate your existing action mappings to the **Send Conversion V3** action.

#### API information

This connector uses the following vendor API:

* API Name: Reddit API
* API Version: v2.0
* API Endpoint: `https://ads-api.reddit.com/api/v2.0`
* Documentation: [Reddit API](https://ads-api.reddit.com/docs/v2)

#### Parameters

| Parameter | Description |
| --- | --- |
| Event Name | The type of the conversion tracking event. The event name can be one of the listed values, or it can be a custom string value. |
| Event Time | The RFC3339 timestamp when the conversion event occurred. By default, the connector sends the current time.|
|Conversion ID | The unique conversion ID that corresponds to a distinct conversion event. Conversion ID is used for deduplication and prevents the same conversion event from being processed more than once if it is sent multiple times. |
| Transaction Value (Decimal) | The value of the transaction in the base unit of the currency. |
| Currency | The three-character ISO 4217 currency code for the value provided. |
| Item Count | The number of items in the event. |
| Test Mode | Set to `true` to test the API integration. No data is posted to the account. |
| Reddit Click ID | The Reddit-generated ID associated with a single ad click. |
| Phone Number (already SHA256 hashed) | Provide a phone number, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector whitespace trims, lowercases, and hashes this value using SHA256. |
| Email Address (already SHA256 hashed) | Provide an email address, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using SHA256. |
| IP Address | The connector SHA256-hashes the mapped IP address. |
| User Agent | The user agent of the user&#39;s browser. |
| External ID (already SHA256 hashed) | An advertiser-assigned persistent identifier for the user (must accompany the Reddit Click ID or an additional attribution signal). Provide a value that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| External ID (apply SHA256 hash) | An advertiser-assigned persistent identifier for the user (must accompany the Reddit Click ID or an additional attribution signal). The connector whitespace trims, lowercases, and hashes this value using SHA256. |
| IDFA (already SHA256 hashed) | The IDFA of the user&#39;s device. Provide a value that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| IDFA (apply SHA256 hash) | The IDFA of the user&#39;s device. The connector whitespace trims, lowercases, and hashes this value using SHA256. |
| AAID (already SHA256 hashed) | The AAID of the user&#39;s device. Provide a value that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| AAID (apply SHA256 hash) | The AAID of the user&#39;s device. The connector whitespace trims, lowercases, and hashes this value using SHA256. |
| Opt Out | A flag indicating whether the user has opted out of tracking. |
| Screen Height | The height of the user&#39;s screen in pixels. If you do not set **Screen Height**, `events.user.screen_dimensions` is populated from the Tealium Collect event data. For example, from `data.com.viewport_height`. |
| Screen Width | The width of the user&#39;s screen in pixels. If you do not set **Screen Width**, `events.user.screen_dimensions` is populated from the Tealium Collect event data. For example, from `data.com.viewport_width`. |
| Account ID Override | The ID of the Reddit ad account associated with the conversion event. Use this mapping to dynamically override the account ID and, if needed, use multiple Reddit accounts with one instance of the connector. |

#### Products Data

| Parameter | Description |
| --- | --- |
| Product ID | An array of product IDs. |
| Product Name | An array of product names. |
| Product Category | An array of product categories. |

#### Processing Data

| Parameter | Description |
| --- | --- |
| Modes | Data Processing Mode for this conversion event. |
| Country | ISO 3166-1 alpha-2 country code. |
| Region | ISO 3166-2 region code. Also accepts just the region code without country prefix. |

#### Automatic Deduplication

| Parameter | Description |
| --- | --- |
| Tealium iQ Tag ID |  When the Tealium iQ Tag UID is provided, Tealium automatically looks for your event ID value sent from Tealium iQ. |