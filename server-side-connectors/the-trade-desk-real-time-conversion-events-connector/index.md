---
title: The Trade Desk Real-Time Conversion Events Connector Setup Guide
description: This article describes how to set up The Trade Desk Real-Time Conversion Events connector.
url: https://docs.tealium.com/server-side-connectors/the-trade-desk-real-time-conversion-events-connector/
---
## How it works

The Trade Desk (TTD) Real-Time Conversion Events server-side connector sends conversion event data from Tealium into your TTD instance to track attribution and assist in retargeting.

Enhance this connector with other integrations from the Tealium and The Trade Desk partnership. Use the Unified ID 2.0 (UID2) or European Unified ID (EUID) Function to generate and assign universal user identifiers before sending the event data. Optionally, implement the TTD Universal Pixel in Tealium iQ Tag Management to capture a comprehensive view of the user’s behavior in real time.

 Work with your assigned TTD representative to ensure that all necessary parameters have been generated and are available. 

## API information

This connector uses the following vendor API:

* API Name: The Trade Desk API
* API Version: v3
* API Endpoint: `https://insight.adsrvr.org`
* Documentation: [The Trade Desk API](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

The Trade Desk Real-Time Conversion connector supports Event Mapping and URL Mapping tracking. When configuring the connector, set the following parameters depending on your approach:

* **URL Mapping** - In this approach, the URL of the page visited by the user is assigned within TTD platform as the basis for retargeting and conversion measurement.
    * Recommended for websites where the tracking focus is on the pages that the user views.
    * Uses the same methodology as the [TTD Universal Pixel tag]().
    * Configuration parameters: **Advertiser ID** and **Universal Pixel ID**.
* **Event Mapping** - In this approach, conversions are captured using the event name (for example, `Purchase`, `Addtocart`) with optional relevant commerce product details. The event name and products are assessed within the TTD platform as the basis for the retargeting and conversion measurements.
    * Configuration parameters: **Merchant ID** and **Event Tracker ID**.

After adding the connector, configure the following settings:

* **Advertiser ID**  
Required, if **Merchant ID** is not provided. The `advertiserId` for the advertiser on whose behalf the tracking call was made.
* **Merchant ID**  
Required, if **Advertiser ID** is not provided. Your `merchantId` will be provided by TTD during the onboarding process.
* **Pixel ID**  
Required, if **Event Tracker ID** is not provided. The universal pixel ID for the event.
* **Event Tracker ID**  
Required, if **Pixel ID** is not provided. The platform ID of the event tracker.

 If you provide an **Advertiser ID** and not a **Universal Pixel ID**, the connector request returns an error.
We also recommend that you avoid populating every parameter in the **Configuration Window** and provide only values for the chosen approach. For example, you should not provide both an **Advertiser ID** and a **Merchant ID**. Instead, enter only the configuration setting required by the tracking methodology. 

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion Event | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Conversion Event

Ensure that the event has been appropriately defined within your TTD instance or you may encounter 402 errors from TTD.

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Conversion Event Name | The type of event defined by the partner platform. Available event types:&lt;ul&gt;&lt;li&gt;`addtocart`: The user added an item to the shopping cart.&lt;/li&gt;&lt;li&gt;`purchase`: The user completed a purchase and the **Thank You page** has been displayed.&lt;/li&gt;&lt;li&gt;`viewitem`: The user viewed an item or SKU number.&lt;/li&gt;&lt;li&gt;`searchitem`: The user searched for an item or SKU number.&lt;/li&gt;&lt;li&gt;`searchcategory`: The user searched for a category.&lt;/li&gt;&lt;li&gt;`login`: The user logged in to the site.&lt;/li&gt;&lt;li&gt;`messagebusiness`: The user sent a message to the business or contacted the business with a form or email.&lt;/li&gt;&lt;li&gt;`direction`: The user requested and received directions to the business.&lt;/li&gt;&lt;li&gt;`startcheckout`: The user started the checkout process.&lt;/li&gt;&lt;li&gt;`viewcart`: The user viewed the contents of the shopping cart.&lt;/li&gt;&lt;li&gt;`sitevisit`: The user visited the site.&lt;/li&gt;&lt;li&gt;`wishlistitem`: The user added an item or SKU number to the wish list.&lt;/li&gt;&lt;/ul&gt;|

#### User identifier parameters

| **Parameter** | **Description** |
| --- | --- |
| UID2 | The user&#39;s Unified ID 2.0 as a 44-character base64-encoded SHA-256 string. For more information, see  and [TTD: Unified IDs](https://api.thetradedesk.com/v3/portal/data/doc/UnifiedIDs). |
| UID2 Token (encrypted advertising token)| The encrypted UID2 advertising token. This token is case-sensitive. |
| EUID | The user&#39;s European Unified ID as a 44-character base64-encoded SHA-256 string. For more information, see  and [Unified IDs](https://api.thetradedesk.com/v3/portal/data/doc/UnifiedIDs). |
| TDID | The Trade Desk 36-character GUID (including dashes) for this user. Can be obtained through [The Trade Desk Cookie Matching Service Tag]().|
| IDFA | Ad identifier for iOS devices. |
| AAID | Ad identifier for Android devices. |
| DAID | The raw device ID for this user, sent in 36-character GUID format (including dashes). |
| NAID | Ad identifier for Windows devices. |
| IDL | The 49-character or 70-character RampID (previously known as IdentityLink).&lt;br&gt;Note: This must be a RampID from LiveRamp that is mapped specifically for The Trade Desk. For more information about mapping a RampID, see [LiveRamp documentation](https://sidecar.readme.io/docs/getting-started). |

#### Event parameters

The following parameters are associated with the conversion event and are optional, except for specific events when noted in description.

| **Parameter** | **Description** |
| --- | --- |
| Order ID | The associated order identifier of the event. |
| Referrer URL | The website URL from where the event occurred, if any. Required if using URL mapping. |
| Purchase Value | The revenue-tracking value with a period (not a comma) as a decimal point. |
| Purchase Currency | The ISO 4217 currency code for the revenue value. Required for Purchase events. |
| Client IP Address | The client IPv4 or IPv6 IP address that uniquely identifies a network interface on a machine. |
| Impression ID | A 36-character string (including dashes) that serves as the unique ID for the event impression. |

#### Item parameters

When mapping items, use array of string data attributes to assign multiple items. Ensure that mapped attributes have been populated with the appropriate data from the received conversion event.

| **Parameter** | **Description** |
| --- | --- |
| Item Code | (Required) The item identifier, such as SKU numbers. |
| Name (`name`) | The name associated with the item code. |
| Quantity (`qty`) | The number of items in the order for the item code. |
| Price (`price`) | The unit price of the item. |
| Category (`cat`) | The item category ID. Note: The Real-Time Conversion Events API uses the provided value in all cases except when a merchant has a product catalog with the specified item code in it, but with a different category ID. In this case, the product catalog category ID is used. |

#### Privacy setting properties

All three privacy setting properties are required.

| **Parameter** | **Description** |
| --- | --- |
| `privacy_type` | Only one value per object from the following values: &lt;ul&gt;&lt;li&gt;GDPR (General Data Protection Regulation), applicable to the European Economic Area (EEA).&lt;/li&gt;&lt;li&gt;GPP (Global Privacy Platform), intended for users in US states with applicable privacy regulations.&lt;/li&gt;&lt;/ul&gt; |
| `is_applicable` | Indicates if the value specified in the `privacy_type` parameter is applicable. |
| `consent_string` | The user&#39;s consent when the privacy regulations are in effect. For more information, see the [IAB Tech Lab: GDPR Transparency and Consent Framework](https://iabtechlab.com/standards/gdpr-transparency-and-consent-framework/). |

#### Custom properties

Ten sequentially numbered custom dynamic properties (`td1` through `td10`) that can be used to provide additional conversion metadata, such as a flag for new to brand, product name, and other details useful for reporting.
