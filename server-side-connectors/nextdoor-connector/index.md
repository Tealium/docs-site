---
title: Nextdoor Conversions Connector Setup Guide
description: This article describes how to set up the Nextdoor Conversions connector.
url: https://docs.tealium.com/server-side-connectors/nextdoor-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Nextdoor API
* API Version: v2
* API Endpoint: `https://ads.nextdoor.com/v2/api`
* Documentation: [Nextdoor API](https://developer.nextdoor.com/reference/conversion-api)

## Configuration

Go to the Connector Marketplace and add a new connector. For more information, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Token**: (Required) Obtain an authentication token specific to a logged-in user and their associated account on the Nextdoor Ads Manager account page.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Name | The type of the conversion tracking event. Select a value from the list or enter a custom string value. The following values are available: `Add to Cart`, `Initiate Checkout`, `Search`, `Add to Wishlist`, `Subscribe`, and `View Content`.|
| Action Source | The channel through which conversion occurs. Select a value from the drop-down list. |

#### Conversion Event

| **Parameter** | **Description** |
| --- | --- |
| Client ID | Nextdoor Ads Manager advertiser ID. **Data Source ID** or **Client ID** is required. |
| Data Source ID | Nextdoor Ads Manager data source ID. **Data Source ID** or **Client ID** is required. This allows Nextdoor to deduplicate events for an advertiser that sends events through both the Conversions API and the pixel. |
| Partner ID | The Nextdoor-generated ID associated with a single partner. This value is required in all Conversion API calls. |
| Action Source URL | The browser URL where the event happened. The URL must begin with `http://` or `https://`, and match the verified domain. This value is required for website events. |
| Event ID |  A string or hashed ID that can identify a unique event. This is required to deduplicate events from CAPI and pixel tracking. **Event ID** or **Automatic Deduplication** is required. | 
| Event Time | Timestamp of the event in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format. **Event Time Epoch** or **Event Time** is required. |
| Event Time Epoch | Number of seconds since `1970-01-01`. No milliseconds. **Event Time Epoch** or **Event Time** is required. |
| Test Event | Indicates whether this event is a test event. The default value is `False`. |
| Event Timezone | Time zone indicating where the conversion event took place. |

#### Customer Data

The integration requires at least one or a combination of the following parameters: **Email Address**, **Phone Number**, or **Click ID**.

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address that has already been SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| External ID | Any unique ID from the advertiser, such as loyalty membership IDs, user IDs, and external cookie IDs. You can send one or more external IDs for a given event. If you send an External ID through other channels, use the same format as the Conversions API.| 
| Phone Number (already SHA256 hashed) | Provide a phone number that has already been SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector whitespace trims and hashes this value using SHA256 hash. |
| First Name (already SHA256 hashed) | Provide a first name that has already been SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name that has already been SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Date of Birth (already SHA256 hashed) | Provide a date of birth that has already been SHA256 hashed and in `YYYYMMDD` format. |
| Date of Birth (apply SHA256 hash) | Provide a plain text date of birth and the connector whitespace trims and hashes this value using SHA256 hash in `YYYYMMDD` format. |
| Street Address (already SHA256 hashed) | Provide a street address that has already been SHA256 hashed. |
| Street Address (apply SHA256 hash) | Provide a plain text street address and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| City (already SHA256 hashed) | Provide a city that has already been SHA256 hashed. |
| City (apply SHA256 hash) | Provide a plain text city and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| State (already SHA256 hashed) | Provide a state abbreviation that has already been lowercased in two letter [ANSI abbreviation code](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standard_state_code). |
| State (apply SHA256 hash) | Provide a state abbreviation and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash in two letter [ANSI abbreviation code](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standard_state_code). |
| Zip Code (already SHA256 hashed) | Provide a ZIP code that has already been SHA256 hashed. |
| Zip Code (apply SHA256 hash) | Provide a plain text ZIP code and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Country (already SHA256 hashed) | Provide a 2-letter country code that has already been whitespace trimmed and SHA256 hashed in [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) format. |
| Country (apply SHA256 hash) | Provide a plain text country code and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash using [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) format. |
| Gender (already SHA256 hashed) | Provide a gender that has already been SHA256 hashed. Use the lowercase initial: f for female, m for male, or n for non-binary. Leave empty if you prefer not to say. |
| Gender (apply SHA256 hash) | Provide a plain text gender and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. Use the lowercase initial: f for female, m for male, or n for non-binary. Leave empty if you prefer not to say. |
| Pixel ID | Nextdoor Pixel ID. This allows Nextdoor to deduplicate events for an advertiser that sends events through both the Conversions API and the pixel. |
| Click ID | This is the same as the `ndclid` parameter attached to the clickthrough URL. |
| Client IP Address | <ul><li>The IP address of the browser corresponding to the event must be a valid IPV4 or IPV6 address. IPV6 is preferable over IPV4 for IPV6-enabled users.</li><li> Always provide the real IP address to ensure accurate event reporting.</li><li>Do not hash this value</li><li>Sending both the **Client IP Address** and **User Agent** parameters for all of the events may help improve event matching and ad delivery for campaigns.</li><li>This information is automatically added to events sent through the browser, but it must be manually configured for events sent through the server.</li></ul>|
| Client User Agent | The unhashed browser user agent corresponding to the event. This parameter is required for website events shared using the [Conversions API](https://developers.facebook.com/docs/marketing-api/conversions-api). Sending both the **Client IP Address** and **User Agent** parameters for all of the events may help improve event matching and ad delivery for campaigns. Note that this information is automatically added to events sent through the browser, but must be manually configured for events sent through the server. |
| Data Source ID | Nextdoor Ads Manager data source ID. **Data Source ID** or **Client ID** is required. This allows Nextdoor to deduplicate events for an advertiser that sends events through both the Conversions API and the pixel. |
| Delivery Optimization | <ul><li>`True`: Indicates data can be used for optimization.</li><li>`False`: Indicates the data is only used for attribution.</li></ul> |

#### Custom and App Events

| **Parameter** | **Description** |
| --- | --- |
| Order Value | Required for purchase events. The currency code in [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) format followed by the total numeric value (up to two decimal places) associated with the event. |
| Order ID | The order ID for a transaction. This value is required for offline events. |
| App ID | Corresponds to a unique ID for advertisers. Use the mobile app ID from App Store and Google Play Store. |
| Platform | The user's platform. Values can be `iOS` or `Android`. |
| App Version | Mobile app version. |
| Delivery Category | <ul><li>`In Store`: Customer needs to enter the store to get the purchased product.</li><li>`Curbside`: Customer picks up their order by driving to a store and waiting inside their vehicle.</li><li>`Home Delivery`: Purchase is delivered to the customer's home.</li></ul> |

#### Product Context

| **Parameter** | **Description** |
| --- | --- |
| ID | (Required) Product ID. |
| Content Name | Product name. |
| Quantity | Product quantity. |
| Item Price | Product item price. |
| App Tracking Enabled | User opt-out settings for ATT. Specify whether you want to track app events and send them to Nextdoor through the Conversions API.<ul><li>`False`: Disables app event tracking. No app events are sent to Nextdoor.</li><li>`True`: Enables app event tracking. App events are sent to Nextdoor for attribution and measurement.</li></ul>  |

#### Automatic Deduplication

| **Parameter** | **Description** |
| --- | --- |
| Automatic Deduplication | When you provide the Tealium iQ Tag ID, the connector automatically looks for the **Event ID** value that Tealium iQ sends. |