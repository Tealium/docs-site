---
title: Yelp Conversions Connector Setup Guide
description: This article describes how to set up the Yelp Conversions connector.
url: https://docs.tealium.com/server-side-connectors/yelp-conversions-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Yelp API
* API Version: v3
* API Endpoint: `https://api.yelp.com/v3/conversion`
* Documentation: [Yelp API](https://docs.developer.yelp.com/docs/conversions-api)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **API Key** &amp;ndash; (Required) The API key of the application. The API key is attached to requests and can be found in the application settings in Yelp Ads.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Conversion (Real-Time) | ✗ | ✓ |
| Send Conversion (Batched) | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down list.

The following section describes how to set up parameters and options for each action.

### Send Conversion (Real-Time)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Name | The type of the conversion tracking event. Select a value from the drop-down list or enter a custom string value. Used for aggregation during the attribution process. Also used in combination with `event_id` for deduplication process. |

#### Conversion Event Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event ID | A unique identifier for the conversion that is used in the deduplication process. |
| Event Time | The date and time the conversion event occurred in the past. |
| Action Source | Indicates where the conversion took place. Currently limited to `app`, `physical_store` and `website`. |

#### User Data

Contains all user specific data that can be used during the matching process. Providing more data improves the chance and quality of a match.

| **Parameter** | **Description** |
| --- | --- |
| Email Address | (Apply SHA256 hash) Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Email Address | (Already SHA256 hashed) Provide an SHA256 hashed email address. |
| First Name | (Apply SHA256 hash) Provide a plain text first name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| First Name | (Already SHA256 hashed) Provide an SHA256 hashed first name. |
| Last Name | (Apply SHA256 hash) Provide a plain text last name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Last Name | (Already SHA256 hashed) Provide a SHA256 hashed last name. |
| Phone Number | (Apply SHA256 hash) Provide a plain text phone number and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number | (Already SHA256 hashed) Provide an SHA256 hashed phone number. |
| Birth Date | (Apply SHA256 hash) Provide a customer birth date in the format `YYYYMMDD` and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Birth Date | (Already SHA256 hashed) Provide an SHA256 hashed customer birth date in the format of `YYYYMMDD`. |
| Gender | (Apply SHA256 hash) Provide customer’s gender consisting of one character (`f`, `m`, or `n`, representing female, male, non-binary) and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Gender | (Already SHA256 hashed) Provide an SHA256 hashed customer gender, one character consisting of (`f`, `m`, or `n`, representing female, male, or non-binary). |
| Country | (Apply SHA256 hash) Provide a plain text country code and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Country | (Already SHA256 hashed) Provide an SHA256 hashed country code. |
| State | (Apply SHA256 hash) Provide a plain text state and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| State | (Already SHA256 hashed) Provide an SHA256 hashed state. |
| Zip Code | (Apply SHA256 hash) Provide a plain text zip code and the connector will remove all non-numeric characters, whitespace trim, and hash this value using SHA256 hash. |
| Zip Code | (Already SHA256 hashed) Provide an SHA256 hashed zip code. |
| City | (Apply SHA256 hash) Provide a plain text city and the connector will remove spaces and punctuation, whitespace trim, lowercase, and hash this value using SHA256 hash. |
| City | (Already SHA256 hashed) Provide an SHA256 hashed city. |
| External ID | (Apply SHA256 hash) Provide any unique IDs associated with the conversion user, for example, membership ID, loyalty ID etc. The connector will remove spaces and punctuation, whitespace trim, lowercase, and hash this value using SHA256 hash. |
| External ID | (Already SHA256 hashed) Provide SHA256 hashed unique ID associated with the conversion user, for example, membership ID, loyalty ID, etc. |
| IP Address | Provide customer’s IP address in either IPV4 or IPV6 format. This value should be included with `client_user_agent` to maximize match rates. |
| Client User Agent | Provide a customer’s user agent for their browser. This value should be included with `client_ip_address` to maximize match rates. |
| MADID | Customer’s mobile advertiser ID (IDFA/AAID) For mobile events only. |

#### Custom Conversion Data

| **Parameter** | **Description** |
| --- | --- |
| Value | Total monetary value of the conversion. This parameter is a required field to determine ROAS, so must be included if `event_name` value is `purchase`. |
| Currency | Currency must be a valid ISO 4217 three-digit currency code. Currently limited to `USD`. |
| Order ID | Transaction ID or order ID for the conversion event. |
| Content Category | A custom category that the conversion belongs to. |
| Content IDs | Sub-item IDs associated with this conversion. Could be the SKU IDs of all the products included in the same purchase. |
| Custom Conversion Contents | Additional information on the contents of this conversion in the form of a JSON object. |

### Send Conversion (Batched)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following thresholds is met:

* Max number of requests: 1,000
* Max time since oldest request: 10 minutes
* Max size of requests: 2 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event Name | The type of the conversion tracking event. Select a value from the drop-down list or enter a custom string value. Used for aggregation during the attribution process. Also used in combination with `event_id` for deduplication process. |

#### Conversion Event Parameters

| **Parameter** | **Description** |
| --- | --- |
| Event ID | A unique identifier for the conversion that is used in the deduplication process. |
| Event Time | The date and time the conversion event occurred in the past. |
| Action Source | Indicates where the conversion took place. Currently limited to `app`, `physical_store` and `website`. |

#### User Data
Contains all user specific data that can be used during the matching process. The more data that is provided, the higher the chance and quality of a match occurring.

| **Parameter** | **Description** |
| --- | --- |
| Email Address | (Apply SHA256 hash) Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Email Address | (Already SHA256 hashed) Provide an SHA256 hashed email address. |
| First Name | (Apply SHA256 hash) Provide a plain text first name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| First Name | (Already SHA256 hashed) Provide an SHA256 hashed first name. |
| Last Name | (Apply SHA256 hash) Provide a plain text last name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Last Name | (Already SHA256 hashed) Provide a SHA256 hashed last name. |
| Phone Number | (Apply SHA256 hash) Provide a plain text phone number and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number | (Already SHA256 hashed) Provide an SHA256 hashed phone number. |
| Birth Date | (Apply SHA256 hash) Provide a customer birth date in the format `YYYYMMDD` and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Birth Date | (Already SHA256 hashed) Provide an SHA256 hashed customer birth date in the format of `YYYYMMDD`. |
| Gender | (Apply SHA256 hash) Provide customer’s gender consisting of one character (`f`, `m`, or `n`, representing female, male, or non-binary) and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Gender | (Already SHA256 hashed) Provide an SHA256 hashed customer gender, one character consisting of (`f`, `m`, or `n`, representing female, male, or non-binary). |
| Country | (Apply SHA256 hash) Provide a plain text country code and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Country | (Already SHA256 hashed) Provide an SHA256 hashed country code. |
| State | (Apply SHA256 hash) Provide a plain text state and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| State | (Already SHA256 hashed) Provide an SHA256 hashed state. |
| Zip Code | (Apply SHA256 hash) Provide a plain text zip code and the connector will remove all non-numeric characters, whitespace trim, and hash this value using SHA256 hash. |
| Zip Code | (Already SHA256 hashed) Provide an SHA256 hashed zip code. |
| City | (Apply SHA256 hash) Provide a plain text city and the connector will remove spaces and punctuation, whitespace trim, lowercase, and hash this value using SHA256 hash. |
| City | (Already SHA256 hashed) Provide an SHA256 hashed city. |
| External ID | (Apply SHA256 hash) Provide any unique IDs associated with the conversion user, for example, membership ID, loyalty ID etc. The connector will remove spaces and punctuation, whitespace trim, lowercase, and hash this value using SHA256 hash. |
| External ID | (Already SHA256 hashed) Provide SHA256 hashed unique ID associated with the conversion user, for example, membership ID, loyalty ID etc. |
| IP Address | Provide customer’s IP address in either IPV4 or IPV6 format. This should be included with `client_user_agent` to maximize match rates. |
| Client User Agent | Provide a customer’s user agent for their browser. This should be included with `client_ip_address` to maximize match rates. |
| MADID | Customer’s mobile advertiser ID (IDFA/AAID) For mobile events only. |

#### Custom Conversion Data

| **Parameter** | **Description** |
| --- | --- |
| Value | Total monetary value of the conversion. This value is a required field to determine ROAS, so must be included if `event_name` value is `purchase`. |
| Currency | Currency must be a valid ISO 4217 three-digit currency code. Currently limited to `USD`. |
| Order ID | Transaction ID or order ID tied to the conversion event. |
| Content Category | A custom category for the conversion. |
| Content IDs | Sub-item IDs associated with this conversion. Could be the SKU IDs of all the products included in the same purchase. |
| Custom Conversion Contents | Additional information on the contents of this conversion in the form of a JSON object. |