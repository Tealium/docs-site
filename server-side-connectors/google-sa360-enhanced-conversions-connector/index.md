---
title: Google SA360 Enhanced Conversions Connector Setup Guide
description: This article describes how to set up the Google SA360 Enhanced Conversions connector.
url: https://docs.tealium.com/server-side-connectors/google-sa360-enhanced-conversions-connector/
---
The Google SA360 Enhanced Conversions connector can improve the accuracy of your conversion measurement and unlock more powerful bidding. It supplements your existing client-side conversion tags by sending hashed first-party conversion data from your website to Google in a privacy-safe way. 

Conversions are recorded through the client-side [Floodlight (`gtag.js`) tag](https://docs.tealium.com/floodlight-gtagjs-tag/) and are indexed by Google. The Google SA360 Enhanced Conversions connector can be used to enhance these conversions with personally identifiable information (PII) using a server-to-server API call.

## Requirements

This connector requires the following:

* To obtain a profile ID to use in the connector configuration, add the `api@tealium.com` user to your Google Campaign Manager 360 account. This user must have Update Offline Conversions permissions.
* The [Floodlight `gtag.js` tag](https://docs.tealium.com/floodlight-gtagjs-tag/) is required for this connector to update the tag payload with PII data.
* Update the Floodlight `gtag.js` tag to the latest version.
* Map an attribute containing a unique value, such as `tealium_random`, to the tag `match_id` variable. Use the same value in the connector so that Google can identify the conversion to enhance.
* For non-purchase conversions, in the Floodlight `gtag.js` tag, map an attribute containing a unique value to `ordinal`. For example, `tealium_random`.

### Permissions

* To upload conversions from any source (such as bulksheets, the Search Ads 360 API, or the Campaign Manager 360 API), you need edit access to the sub-manager account where you upload conversions. For details, see [Google: About user permissions by assigning roles](https://support.google.com/searchads/answer/1409946).
* In a shared Floodlight setup, you need edit access to each child sub-manager account where you upload conversions. You do not need access to the parent sub-manager or to child sub-managers where you are not uploading conversions. For more information, see [Google: Edit a Floodlight instruction](https://support.google.com/sa360/answer/13400844).
* If you use click IDs to track conversions, you need edit access to the sub-manager that generated the click ID. If you use a click ID from a sub-manager you cannot edit, the upload fails. For more information, see [Google: Edit the downloaded bulksheet](https://support.google.com/sa360/answer/13607450).

## API information

This connector uses the following vendor API:

* API Name: Google Campaign Manager 360 API
* API Version: v5
* API Endpoint: `https://dfareporting.googleapis.com/dfareporting`
* Documentation: [Google: Campaign Manager 360 API - Enhanced Conversions](https://developers.google.com/doubleclick-advertisers/guides/conversions_ec)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

In addition, the connector sends batched conversions after a two-hour delay so that Google can index the client-side conversions.

## Trace

The Tealium [Trace](https://docs.tealium.com/about-trace/) feature bypasses configured batching and delays to permit real-time debugging. The Google indexing of client-side conversions is not immediate, and you will encounter `404 Not Found` errors when using Trace with this connector.

## PII mapping restrictions

Ensure that you adhere to the following restrictions with PII data when using the Floodlight (`gtag.js`) tag with this connector:

* You must send PII data for the connector to work. If the connector data does not include any PII when it connects with Google, the connector generates a missing PII error and it does not send any data to Google. The PII data must include at least one of the following:
    * Email Address
    * Phone Number
    * All address information (First Name, Last Name, Street Address, City, State, Postal Code, Country Code)
* Send PII data either through the Floodlight (`gtag.js`) tag or the Google SA360 Enhanced Conversions connector, but not both. Mapping PII in both results in `conversion already enhanced` errors in the connector. 
* To avoid connector errors, we recommend restricting any conversions without PII by adding conditions to the event feed or event specifications requiring PII.

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.


<blockquote>
When you add this connector, you must accept the vendor's data platform policy.
</blockquote>


After adding the connector, configure the following settings:

* **Floodlight Profile ID**: The Floodlight Profile ID that is provided by Campaign Manager 360, after adding the `api@tealium.com` user to your Campaign Manager 360 account.

Click **Done** when you are finished configuring the connector.

## Actions

| **Action Name** | **AudienceStream** | **EventStream** |
| --- | --- | --- |
| Send Conversion | ✓ | ✓ |

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type.

The following section describes how to set up parameters and options for each action.

### Send Conversion

#### Conversion Data

Required parameters:

| Parameter | Description |
| --- | --- |
| Floodlight Configuration ID | (Required) The Floodlight configuration ID of this conversion. |
| Floodlight Activity ID | (Required) The Floodlight activity ID of this conversion. |
| Match ID | (Required) A unique advertiser-created event identifier that Google uses to match the connector-enhanced conversion calls with a client-side Floodlight event. Use the same attribute value in both this connector and the Floodlight `gtag.js` tag. |
| Ordinal |(Required) The ordinal of the conversion. This parameter can be used to deduplicate conversions of the same user and day by passing the same value (for example, `1`) for each event. Use a unique value to disable deduplication, for example, `order_id` for purchase events or `tealium_random` for non-purchase events. Use the same attribute value in both this connector and the Floodlight `gtag.js` tag. If transaction ID is used in the tag, map the attribute containing that value. |
| Timestamp Micros | The timestamp of conversion, in Unix epoch microseconds. If not provided, the connector generates one automatically. When you map a Tealium date attribute (stored in milliseconds), the connector converts the value to microseconds before sending it to Google. The value should be within one minute of the Google recorded timestamp of the client-side conversion. |
| Quantity | (Required) Quantity of the conversion. If you map an array, the connector sums the values in the array. Use the same attribute value in both this connector and the Floodlight `gtag.js` tag, unless you want to update the value. |
| Value | (Required) Value of the conversion. Use the same attribute value in both this connector and the Floodlight `gtag.js` tag, unless you want to update the value.|
| Profile ID | Overwrites the value defined in the configuration tab of the connector. |

| Parameter | Description |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address which has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number which has been already whitespace trimmed and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector will whitespace trim and hash this value using SHA256 hash. |
| Address Info: First Name (already SHA256 hashed) | Provide first name which has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: First Name (apply SHA256 hash) |  Provide a plain text first name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: Last Name (already SHA256 hashed) | Provide last name which has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Last Name (apply SHA256 hash) | Provide a plain text last name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: Street Address (already SHA256 hashed) | Provide a street address which does not contain special characters, has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Street Address (apply SHA256 hash) | Provide a plain text street address and the connector will remove all special characters, whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address Info: City | City of the user's address. |
| Address Info: State | State code of the user's address. |
| Address Info: Postal Code | Postal code of the user's address. |
| Address Info: Country Code | The 2-letter country code of the user's address in ISO 3166-1 alpha-2 format. |

#### Custom Variables

| Parameter | Description |
|---| ---|
|Custom Variable Values|  <ul><li>An array of custom values.</li><li>Each value must not exceed 50 characters.</li></ul> |
|Custom Variable Types|  <ul><li>An array of strings matching the pattern “U1” through “U100”. Any string that does not match this pattern will be excluded.</li></ul> |

## Troubleshooting

### Identifying Google attributes

Refer to the following image of the Google SA360 **Activities** screen for help in identifying which attributes are needed for this connector:

![](https://docs.tealium.com/images/server-side-connectors/google-sa360-ui.png)

The figure shows the location of the following attributes that are needed for this connector and the Floodlight (gtag.js) tag:

| | Google SA360 Enhanced Conversions Connector | Floodlight (gtag.js) tag |
|---|:---:|:---:|
|Configuration ID | ✓  | ✓ |
|Activity ID |✓ | |
|Activity Tag String | | ✓ | 
|Group Tag String  | | ✓ |
|Counting Method| |✓  |

### Error messages

Potential error messages for this connector are:

|Error Message| Description|
|---| ---|
| `NOT_FOUND` | "MatchId `{matchId}` cannot be found." Google could find no matching conversion from client-side tag pings. This is not an issue with the connector, but may be a cause for investigation into the iQ Tag Management tag setup. This can also be a result of the use of the [Google Consent Mode tag](https://docs.tealium.com/google-consent-mode-tag/), where consent was denied for the tag, but the conversion enhancement was sent through the connector. |
| `NOT_FOUND` | "Specified conversion doesn't exist." The conversion was received from the client-side tag, but has not yet been indexed by Google for enhancing. Tealium will retry these calls up to three times.|