---
title: Microsoft UET Conversion API Connector Setup Guide
description: This article describes how to set up the Microsoft UET Conversion API connector.
url: https://docs.tealium.com/server-side-connectors/microsoft-uet-conversion-api-connector/
---

<blockquote>
This connector is not currently available in the connector marketplace. Using the Microsoft UET Conversions connector requires support from both Tealium and the Microsoft account managers. To use this connector, contact your Tealium account manager.
</blockquote>


## Overview

Advertisers use the Microsoft UET Conversion API to send web and offline conversion events directly to Microsoft Advertising. This connector enables enhanced attribution, signal resiliency, and privacy-focused measurement.

You can use the Microsoft UET Conversion API as a standalone integration or together with the Microsoft UET tag. In a dual-delivery setup, the UET tag sends real-time, client-side events, while the conversion API delivers events reliably in cases of cookie loss, JavaScript restrictions, or offline conversions. Using both methods provides redundancy and improves coverage throughout the customer journey.

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see Batched Actions. Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1,000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

## Prerequisites

* **Microsoft Ads Account**: Active Microsoft Advertising account with UET tag and CAPI access.
* **UET Tag ID**: Microsoft requires a UET tag ID for attribution and audience association, even if using only server-side tracking through Tealium for online or offline conversions. Find the UET tag ID in your Microsoft Ads platform. Use an existing tag or provision a new UET tag ID as needed.
* **Access Token**: The Microsoft Developer token for CAPI. For more information, see [Generate access token](#generate-access-token).
* **Conversion Goal**: To ensure Microsoft can attribute CAPI events correctly, create at least one conversion goal tied to your UET tag.
    1. Go to **Tools > Conversion Goals**.
    1. Click **+ New Conversion Goal**.
    1. Choose a goal type (for example, purchase, lead, booking).
    1. Associate it with your UET tag ID.

## Configuration

To add the connector, go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **UET tagID**: You can use your existing tag or provision a new UET tag ID in your Microsoft Advertising account.
* **Access Token**: The access token for your Microsoft Advertising account.

### Generate access token

To generate an access token for the Microsoft UET Conversion API, follow these steps:

1. In your Microsoft Ads account, go to **Conversions > UET tag**.
1. Hover over the tag name and then click the pencil icon.
    * You may need to select a value for **Industry**.
1. Click **Save and next**.
1. Click **Use Conversions API**.
1. Click **Save and next**.
1. Save your token in a secure location for reference later. It is required to establish the connection.
1. Save the tag.

## Deduplication

To configure this connector to deduplicate events from the Microsoft UET Advertising tag, use the event IDs sent as event attributes with the following naming convention:

```
microsoft_event_id_{EVENT_NAME}}_{TAG_ID}}
```

You can find your tag’s UID in the Tealium iQ Tags table or the tag details screen.

For example, a purchase event from a tag with a UID of 88 would send the following attribute value:

```
microsoft_event_id_purchase_88: “084b1cda7461…”
```

A page load event from the same tag would send the following attribute value:

```
microsoft_event_id_pageload_88: “028b2ade7478…”
```

### Automatic deduplication

When the Automatic Deduplication value is populated, the connector looks for the corresponding event ID attribute. You are no longer required to add an Event ID if this section is populated and you are using Tealium iQ. However, the following approach may still be needed when using EventStream without Tealium iQ.

The connector follows this order of operations:

* If Automatic Deduplication is populated, and the value is found in the data layer, (for example, `microsoft_purchase_id_88`) this value supersedes anything mapped in Event ID.
* If Automatic Deduplication is populated, but it cannot find the tag ID version, but it can find the legacy version (with no ID attached), that value is used (for example, `microsoft_purchase_id`).
* If Automatic Deduplication is populated, but the value isn’t found, the mapped Event ID is used, if it is populated.

## Offline conversions

To process offline and store events through the Microsoft UET Conversions connector, configure the connector to include the required parameters.

For online conversions, attribution typically occurs in real time. For offline conversions, Microsoft supports backdated events up to 90 days old. Attribution accuracy improves when events are sent closer to real time.

### Prerequisites

* **Enable Offline Conversion Import**: This must be enabled in Microsoft Ads to allow it to ingest CAPI events sent from Tealium.
    1. Go to **Tools > Offline Conversions**.
    1. Select **Import Conversions**.
    1. Select **Microsoft (Offline conversions via API)**.
* **Associate the conversion goal with the UET tag**: This must be enabled to ensure Microsoft can attribute conversions to ad interactions.
    1. Go to **Tools > Conversion Goals**.
    1. Click **+ New Conversion Goal**.
    1. Select a goal type relevant to offline events (for example, **In-Store Purchase**, **Phone Booking**, **Loan Application**).
    1. Under **Goal Source**, select **Offline Conversions (Import via file or API)**.
    1. Associate the goal with your existing UET tag ID.
* **Ensure that the UET tag ID exists**: Ensure that the UET tag ID referenced in your goal exists in Microsoft Ads, even if the tag itself is not deployed.
* **Pass click IDs or hashed PII with the event**: This lets Microsoft perform matching.

## Best practices

* **Persist the click ID**: The Microsoft Click ID (`msclkid`) is critical to conversion tracking. When auto-tagging is enabled in Microsoft Ads, this identifier is appended as a query parameter on the landing page URL after a user clicks an ad. Persisting the click ID with a [Persist Data Values extension](https://docs.tealium.com/persist-data-value-extension/) ensures that it is available for server-side use. Map the cookie attribute server-side. Without the click ID, Microsoft may not be able to link the conversion back to the originating ad click, resulting in lost attribution and under-optimized bidding.
* **Every click fires a page load event**: Every page view or single-page application (SPA) navigation must fire one page load event. You may also fire one or more custom events. Each custom event links to a page load event through the `pageLoadId` parameter.
* **Enable Microsoft ID Beacon Sync**: Enable Microsoft ID Beacon Sync in the Microsoft UET tag to improve identity resolution and remarketing performance. This feature supports identity stitching across devices and improves the ability to match online behavior to offline conversions.
* **Consent granted by default**: By default, Microsoft processes all events as consent state being granted. If you need to use explicit consent signals, you can use the parameter `adStorageConsent` with the following options:
    * `G` = granted.
    * `D` = denied. Denied events will not be used for any ad purposes (including conversion attribution and retargeting).
* **Strict phone and email formats**: When using SHA256 hashed PII, follow these formatting rules:
    * Format phone numbers according to the E.164 standard.
    * For email addresses:
        * Remove whitespaces from the beginning and end of the email address.
        * Ensure the text is in lower case.
        * Remove everything between `+` and `@` (for example, `user+withplus@example.com` becomes `user@example.com`).
        * Remove periods before `@` (for example, `us.er@example.com` becomes `user@example.com`).
        * Ensure email addresses contain the `@` sign.
        * Remove any spaces.
        * Ensure there is a period after `@`, such as `.com`.
        * Ensure it doesn't start or end with a period.
        * Remove any accents (for example, `à`).
* Enable automatic deduplication by turning on **Event ID Generation** in the UET Tag. Enter the **Tag ID** in the **Automatic Deduplication** mapping section. Microsoft detects matching IDs across delivery methods and prevents double-counting. This step is important in dual-delivery setups to maintain data integrity. 

## Frequently asked questions

* **Can I use the UET Conversion API without the UET tag?**  
Yes. However, it is not recommended. While the UET Conversion API can work independently, Microsoft strongly recommends implementing both the UET tag and UET CAPI. Using both methods improves attribution accuracy by recovering from signal loss.
* **Can I send the same conversion in the tag and connector?**  
Yes. It is not required but highly recommended. Microsoft supports deduplication to prevent over-counting. Sending conversions through both channels ensures resiliency; if one fails, the other still attributes the event correctly.
* **Can I send a conversion without a click ID?**  
Only when necessary or unavailable. The click ID is the most accurate way to attribute a conversion to a Microsoft/Bing Ad click. While sending hashed PII as a fallback is possible, the conversion match quality may be reduced, especially for Smart Bidding and reporting.
* **Can I use this connector for lead forms or phone calls?**  
Yes. Send lead form completions, pre-qualification submissions, and call center events using this connector. This is ideal for finance, auto, and travel verticals with high offline conversion volume.

## Troubleshooting

Use the [Trace tool](https://docs.tealium.com/about-trace/) to monitor event flow in EventStream and AudienceStream. You can also enable the "Test Mode" toggle or send events to a staging instance if configured in your Microsoft Ads account.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion Event | ✓ | ✓ |
| Send Conversion Event (Batched) | ✓ | ✓ |

Enter a name for the action and select the **Action Type**.

The following section describes how to set up parameters and options for each action.

### Send Conversion Event

#### Parameters

##### Event Type

| **Parameter** | **Description** |
| --- | --- |
| Event type | The event type. Available options are `Page Load` or `Custom`. |

##### Conversion Data

| **Parameter** | **Description** |
| --- | --- |
| Event ID | Unique ID of the event. Event ID is required for deduplication. |
| Event Name | Event action for custom conversion goals, if used. |
| Event Time | Timestamp of the event (UNIX epoch time UTC) in seconds. The connector automatically maps this parameter when it appears in the event. If no value is set, the connector uses the current time.|
| Event Source URL | URL of the page, used for external destination URL goals. The connector automatically maps this parameter when it appears in the event. If you map an attribute, it overrides this value. |
| Ad Storage Consent | For consent signals, use `G` for granted and `D` for denied. |
| Page Load ID | Page load ID that links to one or more custom events from the same page. This parameter must be formatted as a v4 UUID. |
| Referrer URL | Referrer of the page, used for external "referral" remarketing lists. |
| Page Title | Page title (for example, `document.title`). |
| Keywords | Page keywords (SEO meta keywords). |

##### User Data

| **Parameter** | **Description** |
| --- | --- |
| Client User Agent | User agent header from the browser of the end user. |
| Anonymous ID | Guest user anonymous ID, also used for ID sync. Prefer (not required) a v1 UUID. |
| External ID | Authenticated user ID (anonymized) if user is logged in. Also used for ID sync. |
| Email Address (already SHA256 hashed) | Provide an email address which has been already whitespace trimmed, lowercased and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number which has been already whitespace trimmed, lowercased and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Client IP Address | The IPv4 or IPv6 address of the user. |
| Microsoft Click ID | The click ID is used to assist the connector in attributing conversions accurately to clicks. |
| GAID | For Android devices, the Google advertising ID. |
| IDFA | For iOS devices ID, the Apple device ID. |

##### Custom Data

| **Parameter** | **Description** |
| --- | --- |
| Event Category | Event category for custom conversion goals, if used. The connector automatically maps this parameter when it appears in the event. |
| Event Label | Event label for custom conversion goals, if used. |
| Event Value | Event value (float) for custom conversion goals, if used. The connector automatically maps this parameter when it appears in the event. |
| Search Term | Search query used by the user for a search results page, optional. |
| Transaction ID | Unique ID associated with this, optional but recommended for singular events like a purchase. The connector automatically maps this parameter when it appears in the event. |
| Value | Revenue value (float) to report variable revenue for goals, if used. The connector automatically maps this parameter when it appears in the event. |
| Currency | The revenue currency in 3-digit ISO 4217 format, if used. The connector automatically maps this parameter when it appears in the event. |


##### Item Data

| **Parameter** | **Description** |
| --- | --- |
| ID | Item ID. The connector automatically maps this parameter when it appears in the event. |
| Quantity | Item quantity. The connector automatically maps this parameter when it appears in the event.|
| Price | Item price after discounts. The connector automatically maps this parameter when it appears in the event.|
| Name | Item name. The connector automatically maps this parameter when it appears in the event.|

##### Vertical Specific Type

| **Parameter** | **Description** |
| --- | --- |
| Select Vertical Specific Type | The vertical type for the event. Accepted values are `Retail` and `Hotel`. |

##### Vertical Specific Parameters if Vertical Specific Type is empty

If no **Select Vertical Specific Type** is selected, manually map attributes to vendor parameters.

##### Vertical Specific Parameters if Vertical Specific Type is Hotel

| **Parameter** | **Description** |
| --- | --- |
| Total Price | Total price of the booking, including taxes and fees. |
| Base Price | Price of the booking, not including taxes and fees. |
| Checkin Date | Check-in date in `YYYY-MM-DD` format. |
| Checkout Date | Check-out date in `YYYY-MM-DD` format. This value is not required if **Length of Stay** is specified. |
| Length of Stay | Number of nights the booking is for. This value is not required if **Checkout Date** is specified. |
| Partner Hotel ID | The ID that you used to identify the hotel in your property feed. |
| Booking Href | Encrypted or obfuscated booking reference number. |

##### Vertical Specific Parameters if Vertical Specific Type is Retail

| **Parameter** | **Description** |
| --- | --- |
| Item Ids | Comma-separated list of product IDs. |
| Page Type | The page type. This value can be one of the following: `cart`, `category`, `home`, `other`, `product`, `purchase`, or `searchresults`. |
| Ecomm Total Value | Total value of the cart or purchase. |
| Ecomm Category | The category ID. |

##### Automatic Deduplication

| **Parameter** | **Description** |
| --- | --- |
| Tealium iQ Tag ID | When the Tealium iQ tag ID is provided, the connector automatically looks for your event ID value that is sent from Tealium iQ. |

##### Disable Automapping

| **Parameter** | **Description** |
| --- | --- |
| Disable Automapping | If automapping is disabled, automatically mapped parameters are not sent to the vendor by default. |

### Send Conversion Event (Batched)

This action uses the same parameters and mapping options as the **Send Conversion Event** action. For more information, see [Send Conversion Event](#send-conversion-event).