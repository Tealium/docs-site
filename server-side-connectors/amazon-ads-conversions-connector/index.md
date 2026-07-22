---
title: Amazon Ads Conversions Connector Setup Guide
description: This article describes how to set up the Amazon Ads Conversions connector.
url: https://docs.tealium.com/server-side-connectors/amazon-ads-conversions-connector/
---
## API information

This connector uses the following vendor API:

* API Name: Amazon Ads Events API
* API Version: v1
* API Endpoint: `https://advertising-api.amazon.com`
* Documentation: [Amazon Ads Events API](https://advertising.amazon.com/API/docs/en-us/guides/events/events)
* Tag Documentation: [Amazon Advertising Tag](https://docs.tealium.com/amazon-advertising-tag/)

## Connector tips

We recommend a hybrid setup using both a tag and a connector. This configuration ensures maximum data resilience, improves event matching with server-side signals, and maintains data flow continuity while retaining real-time client-side signals.

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **API Base URL**: (Required) Select your API Base URL.
* **Amazon Advertiser ID**: (Required) Enter your Amazon Advertising account ID.

## Deduplication for web events

To configure this connector to deduplicate events from the Amazon Ads Server tag, use the event IDs sent as event attributes with the following naming convention:

```nohl
amazon_event_id_{EVENT_NAME}_{TAG_UID}
```

You can find your tag's UID in the Tealium iQ **Tags** table or the tag details screen:

![](https://docs.tealium.com/images/server-side-connectors/amazon-ad-server-tag-uid.png)

For example, a checkout event from a tag with UID of `170` would send the following attribute value:

```json
{
  "amazon_event_id_checkout_170": "028b2ade7478..."
}
```

A page view event from the same tag would send the following attribute and value:

```json
{
  "amazon_event_id_pageView_170": "028b2ade7478..."
}
```

Use a separate action for each type of event. Map the event-specific event ID attribute to `Event ID` with the matching event name mapped to `Event Name`. For example:

| Tealium attribute  | Amazon Parameter  |
|:-------------------------|:-------------------|
| `amazon_event_id_checkout_170` (attribute)   | Event ID           |
| `"Checkout"` (custom text) | Event Name         |

### Automatic deduplication

When the **Automatic Deduplication** value is populated, the connector looks for the corresponding event ID attribute. You are no longer required to add an `Event ID` if this section is populated and you are using Tealium iQ. However, the following approach may still be needed when using EventStream without Tealium iQ.

The connector follows this order of operations:

* If **Automatic Deduplication** is populated, and the value is found in the data layer (for example: `amazon_event_id_checkout_170`), this value supersedes anything mapped in `Event ID`.
* If **Automatic Deduplication** is populated, but the value isn't found, the mapped `Event ID` is used, if it is populated.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion | ✓ | ✓ |
| Send Conversion (deprecated) | ✓ | ✓ |

Enter a name for the action and select the action type.

The following section describes how to set up parameters and options for each action.

### Send Conversion 

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 500
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Conversion Type | Select the conversion type of the imported event. Possible values are `ADD_TO_SHOPPING_CART`, `APPLICATION`, `CHECKOUT`, `CONTACT`, `LEAD`, `OFF_AMAZON_PURCHASES`, `MOBILE_APP_FIRST_START`, `PAGE_VIEW`, `SEARCH`, `SIGN_UP`, `SUBSCRIBE`, and `OTHER`. |
| Conversion Source | Select the conversion source of the imported event. Possible values are `ANDROID`, `FIRE_TV`, `IOS`, `OFFLINE`, `WEBSITE`, and `MEASUREMENT_PARTNER`. |

#### Conversion Data

| Parameter | Description |
| --- | --- |
| Name | (Required) The name of the imported event. For example, Website Purchase, Newsletter Signup, etc. |
| Country Code | (Required) ISO 3166-1 alpha-2 country code indicating where the user performing the event was located. |
| Dataset Name | Event Dataset Name to which this event should be added. Must be a 1–100 character string beginning with a letter and may then contain only letters, digits, underscores, or hyphens. |
| Event Time | The timestamp of the conversion in ISO format (`YYYY-MM-DDThh:mm:ssTZD`). If not mapped, the connector use the event time. |
| Value | The value of the event. |
| Currency Code | Currency in ISO-4217 format. Only applicable for the `OFF_AMAZON_PURCHASES` conversion type. |
| Units Sold | The number of items purchased. Only applicable for the `OFF_AMAZON_PURCHASES` conversion type. |
| Data Processing Options | A flag for signaling how an event is processed. Events marked for limited data use are not processed. For example, `LIMITED_DATA_USE` |
| Dedupe ID | A unique identifier used to deduplicate conversion events sent from both the tag and the connector. Set the same value in both to prevent duplicate conversion reporting. |

#### User Data

| Parameter | Description |
| --- | --- |
| Email (already SHA256 hashed) | Provide an email address that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email (apply SHA256 hash) | Provide a plain text email and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| Phone (already SHA256 hashed) | Provide a phone number that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Phone (apply SHA256 hash) | Provide a plain text phone number and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| First Name (already SHA256 hashed) |  Provide a first name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| Address (already SHA256 hashed) |  Provide an address that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address (apply SHA256 hash) | Provide a plain text address and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| City (already SHA256 hashed) |  Provide a city that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| City (apply SHA256 hash) | Provide a plain text city and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| State (already SHA256 hashed) | Provide a state that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| State (apply SHA256 hash) | Provide a plain text state and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| Postal Code (already SHA256 hashed) | Provide a postal code that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Postal Code (apply SHA256 hash) | Provide a plain text postal code and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| MAID | Mobile Identifier. Possible values are `MAID`, `ADID`, `IDFA`, and `FIREADID`. |
| Ramp ID | The LiveRamp identifier. |
| Match ID | A generic match identifier type that Amazon supports as a user identity key. | 
| Custom Data | Map custom data associated with the conversion event. |

#### Consent

| Parameter | Description |
| --- | --- |
|  Amazon Ad Storage | Indicates whether the user granted consent to Amazon to store and access advertising identifiers. Possible values are `GRANTED` or `DENIED`. | 
| Amazon User Data | Indicates whether the user granted consent to Amazon to use their user data for ads. Possible values are `GRANTED` or `DENIED`. |
| IP Address | The IP address of the user.|
| GPP String | The GPP consent string. |
| TCF String | The GDPR consent string using IAB (Interactive Advertising Bureau). |

#### Automatic Deduplication

| Parameter | Description |
| --- | --- |
| Automatic Deduplication | Enter the **Tealium iQ Tag ID** and Tealium automatically looks for this Event ID sent from Tealium iQ. |

#### Mapping Overrides

| Parameter | Description |
| --- | --- |
| Advertiser ID | The unique identifier for the advertiser. |
| Base URL | The base URL for the Amazon Ads API. |

For more information about formatting and normalization requirements, see [Format audience file for hashing](https://advertising.amazon.com/help/GCCXMZYCK4RXWS6C).

### Send Conversion (deprecated)


<blockquote>
This action is now deprecated and can no longer be added. For the current action, see [Send Conversion](#send-conversion).
</blockquote>


#### API information

This action uses the following vendor API:

* API Name: Amazon Ads API
* API Version: v1.0
* API Endpoint: `https://advertising-api.amazon.com`
* Documentation: [Amazon API](https://advertising.amazon.com/API/docs/en-us/dsp-conversion-builder)

#### Create a conversion definition

To create a conversion definition, click **Create Conversion Definition** and provide the following information:

* **Advertising Profile**: (Required) Select an advertising profile for this conversion.
* **Conversion Definition Name**: (Required) The name of the conversion definition.
* **Source Type**: (Required) Select the source type of the conversion. The following types are available: `ADD_TO_SHOPPING_CART`, `APPLICATION`, `CHECKOUT`, `CONTACT`, `LEAD`, `OFF_AMAZON_PURCHASES`, `PAGE_VIEW`, `SEARCH`, `SIGN_UP`, `SUBSCRIBE`, and `OTHER`.
* **Conversion Type**: (Required) Select the type of conversion. The following types are available: `ANDROID`, `FIRE_TV`, `IOS`, `OFFLINE`, and `WEBSITE`.
* **Counting Method**: (Required) Select the method used to determine whether to use all or only the first conversion event per user ingested within a 24 hour window for a conversion definition. The following methods are available: `EVERY` and `FIRST`.
* **Conversion Value**: (Optional) The value of the conversion. The default value is `1` and can be overridden through mapping in the **Send Conversion** action.

To save the conversion definition, click **Done**.

Be sure to accept the terms and conditions, either in the Ads data manager console on the conversions page or by using the Terms API (`POST /adm/terms`).

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| Conversion Definition | Select a conversion definition or click **Create Definition** to create a new definition. |

##### Conversion Data

| Parameter | Description |
| --- | --- |
| Country Code | (Required) The country where the user performing the event is located, in ISO 3166-1 alpha-2 format. |
| Conversion Time | The timestamp of the conversion in ISO format (`YYYY-MM-DDThh:mm:ssTZD`). If not mapped, the connector uses the event time. |
| Conversion Value | The value of the conversion. |
| Currency | The currency in ISO 4217 format. Only applicable for the `OFF_AMAZON_PURCHASES` conversion type. |
| Units Sold | The number of items purchased. Only applicable for the `OFF_AMAZON_PURCHASES` conversion type. |
| Dedupe ID | If you are tracking conversions in both the tag and the connector, specify a deduplication ID. The value should match for both events. |

##### User Data

| Parameter | Description |
| --- | --- |
| Email (already SHA256 hashed) | Provide an email address that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email (apply SHA256 hash) | Provide a plain text email and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| Phone (already SHA256 hashed) | Provide a phone number that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Phone (apply SHA256 hash) | Provide a plain text phone number and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| First Name (already SHA256 hashed) |  Provide a first name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| Address (already SHA256 hashed) |  Provide an address that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address (apply SHA256 hash) | Provide a plain text address and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| City (already SHA256 hashed) |  Provide a city that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| City (apply SHA256 hash) | Provide a plain text city and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| State (already SHA256 hashed) | Provide a state that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| State (apply SHA256 hash) | Provide a plain text state and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| Postal Code (already SHA256 hashed) | Provide a postal code that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Postal Code (apply SHA256 hash) | Provide a plain text postal code and the connector trims whitespace, lowercases, and hashes this value using SHA256 hash. |
| MAID | Mobile Identifier. Possible values are `MAID`, `ADID`, `IDFA`, and `FIREADID`. |

#### Automatic Deduplication

| Parameter | Description |
| --- | --- |
| Automatic Deduplication | Enter the **Tealium iQ Tag ID** and Tealium automatically looks for this Event ID sent from Tealium iQ. |
| Tag Conversion Type | When enabling Automatic Deduplication, select one of the following conversion types sent with the tag data: `ADD_TO_SHOPPING_CART`, `APPLICATION`, `CHECKOUT`, `CONTACT`, `LEAD`, `OFF_AMAZON_PURCHASES`, `PAGE_VIEW`, `SEARCH`, `SIGN_UP`, `SUBSCRIBE`, or `OTHER`. |

#### Mapping Overrides

| Parameter | Description |
| --- | --- |
| Advertiser ID | The unique identifier for the advertiser. |
| Base URL | The base URL for the Amazon Ads API. |
| Conversion Definition ID | The ID of the conversion definition to use. |

For more information about formatting and normalization requirements, see [Format audience file for hashing](https://advertising.amazon.com/help/GCCXMZYCK4RXWS6C).