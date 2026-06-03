---
title: Google Floodlight (CM360/SA360/DV360) Connector Setup Guide
description: This article describes how to configure the Google Floodlight (CM360/SA360/DV360) Connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/google-floodlight-connector/
---
The Google Floodlight connector inserts offline conversions into the Floodlight Conversion Tracking and Attribution system through the Google Campaign Manager 360 API.

Floodlight is the conversion tracking system used across the Google Marketing Platform. All GMP products (Campaign Manager 360*, Search Ads 360, and Display &amp; Video 360) can use Floodlight for measuring conversions.

## Requirements

* You must have a Campaign Manager 360 (CM360) account.
* Your CM360 account must be enabled for API access.
* You must have a CM360 user profile with access to the advertiser account used for Floodlight tracking.
* Enable the following OAuth scope in your CM360 account to grant access to conversion data: `https://www.googleapis.com/auth/ddmconversions`.
* Add the **api@tealium.com** user to your account and grant it access to your CM360 account with the **Insert offline conversions** permission.
* After you add the **api@tealium.com** user to your CM360 account, use the generated profile ID in the connector, either on the configuration page or on an action page. If it is defined in both locations, the profile ID defined on an action page takes precedence.

## API information

This connector uses the following vendor API:

* API Name: Google Campaign Manager 360 API
* API Version: v5
* API Endpoint: `https://www.googleapis.com/dfareporting/`
* Documentation: [Campaign Manager 360 API](https://developers.google.com/doubleclick-advertisers/rest/v5)

### Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

## Delayed actions

Actions are delayed for 30 minutes to accommodate uploading offline conversions, as per Google’s best practices. For more information about delayed actions using the Google Campaign Manager 360 Floodlight connector, see [Google: Best practices for uploading offline conversions](https://support.google.com/campaignmanager/answer/2823388?hl=en).

Actions are not delayed when using [trace]() in EventSream or AudienceStream.

## Configuration

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Floodlight Profile ID**  
  * The Floodlight Profile ID that is given to you by Campaign Manager 360, after adding the `api@tealium.com` user to your Campaign Manager 360 account.

When you add this connector, you are be prompted to accept the vendor&#39;s data platform policy.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Track Floodlight Conversion| ✓| ✓|

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Track Floodlight Conversion

#### Configuration ID parameters

|Parameter| Description|
|---| ---|
|Profile ID|  The Floodlight Profile ID that CM360 gives to you, after adding the **api@tealium.com** user to your CM360 account. If configured here, the value is overwritten with the value defined in the Configuration. |
|Floodlight Configuration ID|  (Required) The Floodlight configuration ID of this conversion. |
|Floodlight Activity ID|  (Required) The Floodlight activity ID of this conversion. |

#### User/Device ID

* If multiple attributes are mapped, the first non-empty value is sent.
* All the conversions are sent after a 30 minute delay.

|Parameter| Description|
|---| ---|
|Encrypted User ID|  If one or more Encrypted User IDs are specified, then Encryption Entity Type, ID, and Source sections are required. |
|Mobile Device ID|  Specify a single device ID, a single click ID, a single user ID, match ID, or multiple user candidate IDs. It is acceptable to use a list with candidate IDs for a single user candidate ID parameter. |
|Google Click ID|  Specify a single device ID, a single click ID, a single user ID, match ID, or multiple user candidate IDs. It is acceptable to use a list with candidate IDs for a single user candidate ID parameter. |
|Display Click ID|  Specify a single device ID, a single click ID, a single user ID, match ID, or multiple user candidate IDs. It is acceptable to use a list with candidate IDs for a single user candidate ID parameter. |
|Match ID|  Specify a single device ID, a single click ID, a single user ID, match ID, or multiple user candidate IDs. It is acceptable to use a list with candidate IDs for a single user candidate ID parameter. |
|Impression ID|  Specify a single device ID, a single click ID, a single user ID, match ID, or multiple user candidate IDs. It is acceptable to use a list with candidate IDs for a single user candidate ID parameter. |

#### Additional parameters

|Parameter| Description|
|---| ---|
|Ordinal|  (Required) The ordinal of the conversion. Used to de-duplicate conversions of the same user and day. |
|Timestamp in micros|  The timestamp of conversion, in Unix epoch microseconds. If not provided, it is auto-generated. |
|Limit Ad Tracking|  Set to `true` to use the conversion for reporting only, not for targeting. |
|Child Directed Treatment|  Set as `true` for conversions directed toward children. |
|Non-Personalized Ad|  Set as `true` if the conversion was for a non-personalized ad. |
|Treatment For Underage|  Set to `true` if the request may come from an underage user (see GDPR). |

#### User identifiers

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address which has been already whitespace trimmed, lowercased, and SHA256 hashed. Remove all periods (`.`) that precede the domain name in `gmail.com` and `googlemail.com` email addresses before hashing. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector removes all periods (`.`) that precede the domain name in `gmail.com` and `googlemail.com` email addresses, whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number which has been already whitespace trimmed and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector removes all non-figit symbols, prefix the number with a plus sign (`&#43;`), whitespace trim and hash this value using SHA256 hash. |
| Address Info: First Name (already SHA256 hashed) | Provide first name which has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: First Name (apply SHA256 hash) |  Provide a plain text first name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Address Info: Last Name (already SHA256 hashed) | Provide last name which has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Last Name (apply SHA256 hash) | Provide a plain text last name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Address Info: Street Address (already SHA256 hashed) | Provide a street address which does not contain special characters, has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Street Address (apply SHA256 hash) | Provide a plain text street address and the connector removes all special characters, whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Address Info: City | City of the user&#39;s address. |
| Address Info: State | State code of the user&#39;s address. |
| Address Info: Postal Code | Postal code of the user&#39;s address. |
| Address Info: Country Code | The 2-letter country code of the user&#39;s address in ISO 3166-1 alpha-2 format. |

#### Encryption

|Parameter| Description|
|---| ---|
|Encryption Entity Type|  Required if Encrypted User ID is specified.. Must match the encryption configuration for ad serving or data transfer. |
|Encryption Entity ID|  Required if Encrypted User ID is specified. Must match the encryption configuration for ad serving or data transfer. |
|Encryption Source|  Required if Encrypted User ID is specified. Describes whether the encrypted cookie was received from ad serving or from data transfer. |

#### Quantity and value

|Parameter| Description|
|---| ---|
|Conversion Quantity|  The quantity of the conversion. |
|Conversion Value|  The value of the conversion. |

#### Custom data

Map attributes to `U` custom variables as needed. Only populated values are sent.
Use of the mapping destinations in this section supersede any mappings in the **Custom Data Arrays - Legacy** section.

|Parameter| Description|
|---| ---|
|Custom Variable Values|  A collection of custom values. Each value must not exceed 50 characters. |
|Custom Variable Types|  A collection of strings, each having a form of `Uxxx` where `xxx` is a number from `1` to `100`. |

#### Cart Data

| **Parameter** | **Description** |
| --- | --- |
| Merchant ID | The Merchant Center ID where the items are uploaded. Providing the Merchant Center ID reduces ambiguity in identifying accurate offer details. |
| Merchant Feed Label | The feed labels associated with the feed where your items are uploaded. |
| Merchant Feed Language | The language associated with the feed where the items are uploaded. Use ISO 639-1 language codes. |
| Item ID | (Required) The shopping ID of the item. Must be equal to the Merchant Center product identifier. |
| Quantity | (Required) Number of items sold. |
| Unit Price | (Required) Unit price excluding tax, shipping, and any transaction level discounts. Interpreted in CM360 Floodlight config parent advertiser currency code.  |
## Vendor documentation

* [Campaign Manager 360 API: Get Started](https://developers.google.com/doubleclick-advertisers/getting_started)
* [Campaign Manager 360 API (Method: conversions.batchinsert)](https://developers.google.com/doubleclick-advertisers/rest/v5/conversions/batchinsert)
* [About Floodlight conversion tracking](https://support.google.com/campaignmanager/answer/2823388?hl=en)