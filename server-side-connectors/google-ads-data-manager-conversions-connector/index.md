---
title: Google Ads Data Manager Conversions Connector Setup Guide
description: Send offline and online conversion events to Google Ads using the Google Data Manager API.
url: https://docs.tealium.com/server-side-connectors/google-ads-data-manager-conversions-connector/
---
## Requirements

This connector requires the following:

* A Google Ads conversion action configured for the action type you plan to use:
  * **Send Offline Conversion**: The conversion action type must be `UPLOAD_CLICKS`.
  * **Send Online Conversion**: The conversion action type must be `WEBPAGE`.
* Tealium linked as a connected product in your Google Ads account. For instructions, see [Link Tealium to Google Ads](#link-tealium-to-google-ads).

## How it works

The Google Ads Data Manager Conversions connector sends offline and online conversion events to Google Ads through the Google Data Manager API. The connector supports a broader event schema than the [Google Ads Conversions connector](https://docs.tealium.com/google-ads-conversions-connector/), including user identifiers, ad identifiers, device information, conversion data, cart data, user properties, custom variables, and consent.

Tealium authenticates using its own approved Google Data Partner credentials. You do not enter Google OAuth credentials in the connector configuration.

## Link Tealium to Google Ads

Link Tealium to the Google Ads account that receives conversion events before configuring the connector.

1. Sign in to Google Ads.
1. Go to **Tools > Data Manager > Connected Products**.
1. Click **+ Connect product** and select Tealium.
1. Complete the product link.
1. Return to Tealium and click **Check Product Link Status** in the connector configuration to verify the connection.

The account where you create the link determines which account IDs to enter in the connector:

* **Customer account**: If you link Tealium directly to the customer account that owns the conversion action, enter that account ID in **Customer ID**.
* **Manager account**: If you link Tealium through a manager account, enter the customer account ID in **Customer ID** and the manager account ID in **Customer Manager ID**.

## API information

This connector uses the following vendor API:

* **API Name**: Google Data Manager API.
* **API Version**: v1.
* **API Endpoint**: `POST https://datamanager.googleapis.com/v1/events:ingest`.
* **Documentation**: [Google: Data Manager API Ingest Events](https://developers.google.com/data-manager/api/reference/rest/v1/events/ingest).

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2,000
* Max time since oldest request: 60 minutes
* Max size of requests: 2 MB

## Configuration

Go to the connector marketplace and add a new connector. For more information, see [about-connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Customer ID**: The Google Ads customer ID that owns the conversion action. When provided, this value is used as the fallback for events that do not include a Customer ID Override. Leave this field blank only when every event supplies a Customer ID Override.
* **Customer Manager ID**: The Google Ads manager customer ID, if you linked Tealium to Google Ads through a manager account. Leave this field blank when Tealium is linked directly to the customer account.
* **Check Product Link Status**: Click to verify that Tealium is linked to the configured Google Ads account as a connected product. The check uses **Customer Manager ID** when provided, and **Customer ID** otherwise. This button is disabled when neither field is configured.

After you configure the connector, click **Done**.

## Actions

| Action name | Customer Data Platform (CDP) | Event Streaming |
| --- | :---: | :---: |
| Send Offline Conversion | ✓ | ✓ |
| Send Online Conversion | ✓ | ✓ |

Click **Continue** to configure the connector actions. Enter a name for the action and select the action type from the list.

### Send Offline Conversion

#### Conversion action

| **Parameter** | **Description** |
| --- | --- |
| Conversion Action ID | (Required) Select or enter the Google Ads conversion action ID that receives this event. The conversion action must be of type `UPLOAD_CLICKS`. To find the conversion action ID, open the conversion action in Google Ads and view the number next to **Conversion type ID**. |

#### User identifiers

Map user identifiers associated with the conversion. Email addresses, phone numbers, and address name fields are normalized and SHA-256 hashed before being sent to Google. The connector sends hashed values as lowercase hex-encoded strings.

If you provide address information, you must provide all four address fields: first name, last name, country code, and postal code. Partial address data is not sent.

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | A SHA-256 hashed email address. Before hashing, trim all whitespace and convert to lowercase. For `gmail.com` and `googlemail.com` addresses, also remove periods before the `@` symbol and remove the plus sign and all following characters in the local part. Provide the hash as a 64-character lowercase hexadecimal string. |
| Email Address (apply SHA256 hash) | A plain-text email address. The connector normalizes and hashes the value before sending it to Google. |
| Phone Number (already SHA256 hashed) | A SHA-256 hashed phone number. Before hashing, normalize the number to E.164 format with a leading plus sign and country code, containing only digits after the plus sign. Provide the hash as a 64-character lowercase hexadecimal string. |
| Phone Number (apply SHA256 hash) | A plain-text phone number that includes the country code. The connector formats the value in E.164 format and hashes it before sending it to Google. |
| Address Info: First Name (already SHA256 hashed) | A SHA-256 hashed first name. Before hashing, convert to lowercase, trim whitespace, and remove punctuation and prefixes such as "Mrs.". Provide the hash as a 64-character lowercase hexadecimal string. |
| Address Info: First Name (apply SHA256 hash) | A plain-text first name without a title or prefix. The connector normalizes and hashes the value before sending it to Google. |
| Address Info: Last Name (already SHA256 hashed) | A SHA-256 hashed last name. Before hashing, convert to lowercase, trim whitespace, and remove punctuation and suffixes such as "Jr.". Provide the hash as a 64-character lowercase hexadecimal string. |
| Address Info: Last Name (apply SHA256 hash) | A plain-text last name without a suffix. The connector normalizes and hashes the value before sending it to Google. |
| Address Info: Country Code | The two-letter ISO 3166-1 alpha-2 country or region code associated with the address. Do not hash this value. |
| Address Info: Postal Code | The postal or ZIP code associated with the address. Trim leading and trailing whitespace. For US addresses, provide five digits or five digits followed by a four-digit extension. Do not hash this value. |

#### Ad identifiers

Provide these values in their original format. Do not hash ad identifiers.

| **Parameter** | **Description** |
| --- | --- |
| Google Click ID (GCLID) | The Google Click ID associated with the conversion event. |
| GBRAID | The click identifier for app conversions from iOS devices, beginning with iOS 14. |
| WBRAID | The click identifier for web conversions from iOS devices, beginning with iOS 14. |
| DCLID | The Display click ID associated with the conversion event. |
| Impression ID | The impression ID associated with the conversion event. |
| Match ID | The match ID used to associate this event with a previous event. |
| Mobile Device ID | The mobile advertising identifier associated with the event, such as IDFA on iOS or the Android Advertising ID. Do not hash this value. |
| Session Attributes | The Base64-encoded Google session attributes string. Session attributes provide additional attribution signals when click identifiers are not available. |

#### Conversion data

| **Parameter** | **Description** |
| --- | --- |
| Transaction ID | A unique identifier for the conversion event. Recommended when available. |
| Conversion Time | The date and time when the conversion occurred. Use RFC 3339 format, such as `2026-08-21T18:30:00Z` or `2026-08-21T18:30:00-08:00`. If no value is provided, the connector uses the event time. |
| Event Source | (Required) The source of the conversion event. Valid values are `WEB`, `APP`, `PHONE`, `IN_STORE`, `MESSAGE`, and `OTHER`. |
| Last Updated Time | The date and time when the conversion record was last updated. Use RFC 3339 format. Provide this value only when it differs from Conversion Time. |
| Conversion Value | The monetary value associated with the conversion. Do not include currency symbols. |
| Conversion Currency | The three-letter ISO 4217 currency code associated with the conversion value, such as `USD` or `EUR`. |
| Conversion Count | The number of conversions represented by this event. |

#### Cart data

| **Parameter** | **Description** |
| --- | --- |
| Merchant ID | The Merchant Center account ID where the items are uploaded. |
| Merchant Feed Label | The feed label associated with the Merchant Center feed. |
| Merchant Feed Language Code | The language code associated with the Merchant Center feed. |
| Transaction Discount | The total of all transaction-level discounts applied to the entire cart, such as free shipping and coupon discounts. |
| Coupon Codes | Coupon codes applied to the cart. |

#### Cart items

To send multiple items, use array-type attributes for item fields. Arrays must contain the same number of values, with corresponding positions representing the same item.

To send complex or nested item data, map a template reference such as `{{my_template}}` to **Cart Items**. The template must construct the complete cart items array, including Product ID, Quantity, and Unit Price for each item. When a template is mapped, individual item field mappings are ignored.

| **Parameter** | **Description** |
| --- | --- |
| Product ID | (Required) The identifier of the item in the cart. This value must match the product identifier used in Merchant Center. |
| Merchant Product ID | The product identifier associated with the item in the Merchant Center feed. |
| Quantity | (Required) The number of units sold. |
| Unit Price | (Required) The price of one unit, excluding tax, shipping, and transaction-level discounts. |
| Item Conversion Value | The conversion value associated with the item. |

#### Device info

| **Parameter** | **Description** |
| --- | --- |
| User Agent | The user-agent string of the device used when the conversion occurred. |
| IP Address | The IP address of the device used when the conversion occurred. Google Ads does not support IP address matching for users in the EEA, United Kingdom, or Switzerland. |
| Device Category | The category of device used, such as desktop, tablet, or mobile. |
| Language Code | The language of the device in ISO 639-1 format. |
| Screen Height | The height of the device screen in pixels. |
| Screen Width | The width of the device screen in pixels. |
| Operating System | The operating system or platform of the device. |
| Operating System Version | The version of the operating system or platform. |
| Device Model | The model of the device. |
| Device Brand | The brand or manufacturer of the device. |
| Browser | The browser used when the conversion occurred. |
| Browser Version | The version of the browser used when the conversion occurred. |

#### Consent

Map consent values at the event level. The connector passes these values to Google without modification. When consent is denied, all mapped event fields are still included in the request. Google applies restrictions on its side.

| **Parameter** | **Description** |
| --- | --- |
| Ad User Data Consent | The consent status for ad user data. Valid values are `CONSENT_GRANTED`, `CONSENT_DENIED`, and `CONSENT_STATUS_UNSPECIFIED`. The shorthand values `GRANTED` and `DENIED` are also accepted. If this field is not mapped, the consent field is omitted from the event. |
| Ad Personalization Consent | The consent status for ad personalization. Valid values are `CONSENT_GRANTED`, `CONSENT_DENIED`, and `CONSENT_STATUS_UNSPECIFIED`. The shorthand values `GRANTED` and `DENIED` are also accepted. If this field is not mapped, the consent field is omitted from the event. |

#### User properties

| **Parameter** | **Description** |
| --- | --- |
| Customer Type | The type of customer associated with the conversion. Valid values are `NEW`, `RETURNING`, and `REENGAGED`. |
| Customer Value Bucket | The value bucket for the customer. Valid values are `LOW`, `MEDIUM`, and `HIGH`. |
| Additional User Property | An additional user property as a name-and-value pair. Both the property name and value are required. |

#### Custom variables

Map additional conversion data as custom key-value pairs.


<blockquote>
Map custom variable **IDs**, not variable names. Mapping variable names or free-form text causes a request error.
</blockquote>


| **Parameter** | **Description** |
| --- | --- |
| Variable | The custom variable ID. |
| Value | The value associated with the custom variable. |

#### Experimental fields

Map additional experimental fields as custom key-value pairs.

| **Parameter** | **Description** |
| --- | --- |
| Field | The experimental field name. |
| Value | The value associated with the experimental field. |

#### Optional overrides

| **Parameter** | **Description** |
| --- | --- |
| Conversion Action ID Override | (Optional) Select or map a conversion action ID to override the action-level **Conversion Action ID**. The override value takes precedence when resolved. |
| Customer ID Override | (Optional) Select or map a customer ID to override the connector-level **Customer ID** for this event. |
| Validate Only | Select this checkbox to validate the request without ingesting the events. Use this option for testing. |

### Send Online Conversion

#### Conversion action

| **Parameter** | **Description** |
| --- | --- |
| Conversion Action ID | (Required) Select or enter the Google Ads conversion action ID that receives this event. The conversion action must be of type `WEBPAGE`. To find the conversion action ID, open the conversion action in Google Ads and view the number next to **Conversion type ID**. |

#### User identifiers

Map user identifiers associated with the conversion. Email addresses, phone numbers, and address name fields are normalized and SHA-256 hashed before being sent to Google. The connector sends hashed values as lowercase hex-encoded strings.

If you provide address information, you must provide all four address fields: first name, last name, country code, and postal code. Partial address data is not sent.

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | A SHA-256 hashed email address. Before hashing, trim all whitespace and convert to lowercase. For `gmail.com` and `googlemail.com` addresses, also remove periods before the `@` symbol and remove the plus sign and all following characters in the local part. Provide the hash as a 64-character lowercase hexadecimal string. |
| Email Address (apply SHA256 hash) | A plain-text email address. The connector normalizes and hashes the value before sending it to Google. |
| Phone Number (already SHA256 hashed) | A SHA-256 hashed phone number. Before hashing, normalize the number to E.164 format with a leading plus sign and country code, containing only digits after the plus sign. Provide the hash as a 64-character lowercase hexadecimal string. |
| Phone Number (apply SHA256 hash) | A plain-text phone number that includes the country code. The connector formats the value in E.164 format and hashes it before sending it to Google. |
| Address Info: First Name (already SHA256 hashed) | A SHA-256 hashed first name. Before hashing, convert to lowercase, trim whitespace, and remove punctuation and prefixes such as "Mrs.". Provide the hash as a 64-character lowercase hexadecimal string. |
| Address Info: First Name (apply SHA256 hash) | A plain-text first name without a title or prefix. The connector normalizes and hashes the value before sending it to Google. |
| Address Info: Last Name (already SHA256 hashed) | A SHA-256 hashed last name. Before hashing, convert to lowercase, trim whitespace, and remove punctuation and suffixes such as "Jr.". Provide the hash as a 64-character lowercase hexadecimal string. |
| Address Info: Last Name (apply SHA256 hash) | A plain-text last name without a suffix. The connector normalizes and hashes the value before sending it to Google. |
| Address Info: Country Code | The two-letter ISO 3166-1 alpha-2 country or region code associated with the address. Do not hash this value. |
| Address Info: Postal Code | The postal or ZIP code associated with the address. Trim leading and trailing whitespace. For US addresses, provide five digits or five digits followed by a four-digit extension. Do not hash this value. |

#### Ad identifiers

Provide these values in their original format. Do not hash ad identifiers.

| **Parameter** | **Description** |
| --- | --- |
| Google Click ID (GCLID) | The Google Click ID associated with the conversion event. |
| GBRAID | The click identifier for app conversions from iOS devices, beginning with iOS 14. |
| WBRAID | The click identifier for web conversions from iOS devices, beginning with iOS 14. |
| DCLID | The Display click ID associated with the conversion event. |
| Impression ID | The impression ID associated with the conversion event. |
| Match ID | The match ID used to associate this event with a previous event. |
| Mobile Device ID | The mobile advertising identifier associated with the event, such as IDFA on iOS or the Android Advertising ID. Do not hash this value. |
| Session Attributes | The Base64-encoded Google session attributes string. Session attributes provide additional attribution signals when click identifiers are not available. |

#### Conversion data

| **Parameter** | **Description** |
| --- | --- |
| Transaction ID | (Required) A unique identifier for the conversion event. Google uses this value to deduplicate Data Manager API events with conversions received from the Google tag. |
| Conversion Time | The date and time when the conversion occurred. Use RFC 3339 format, such as `2026-08-21T18:30:00Z` or `2026-08-21T18:30:00-08:00`. If no value is provided, the connector uses the event time. |
| Event Source | The source of the conversion event. If provided, the value must be `WEB`. |
| Last Updated Time | The date and time when the conversion record was last updated. Use RFC 3339 format. Provide this value only when it differs from Conversion Time. |
| Conversion Value | The monetary value associated with the conversion. Do not include currency symbols. |
| Conversion Currency | The three-letter ISO 4217 currency code associated with the conversion value, such as `USD` or `EUR`. |
| Conversion Count | The number of conversions represented by this event. |

#### Cart data

| **Parameter** | **Description** |
| --- | --- |
| Merchant ID | The Merchant Center account ID where the items are uploaded. |
| Merchant Feed Label | The feed label associated with the Merchant Center feed. |
| Merchant Feed Language Code | The language code associated with the Merchant Center feed. |
| Transaction Discount | The total of all transaction-level discounts applied to the entire cart, such as free shipping and coupon discounts. |
| Coupon Codes | Coupon codes applied to the cart. |

#### Cart items

To send multiple items, use array-type attributes for item fields. Arrays must contain the same number of values, with corresponding positions representing the same item.

To send complex or nested item data, map a template reference such as `{{my_template}}` to **Cart Items**. The template must construct the complete cart items array, including Product ID, Quantity, and Unit Price for each item. When a template is mapped, individual item field mappings are ignored.

| **Parameter** | **Description** |
| --- | --- |
| Product ID | (Required) The identifier of the item in the cart. This value must match the product identifier used in Merchant Center. |
| Merchant Product ID | The product identifier associated with the item in the Merchant Center feed. |
| Quantity | (Required) The number of units sold. |
| Unit Price | (Required) The price of one unit, excluding tax, shipping, and transaction-level discounts. |
| Item Conversion Value | The conversion value associated with the item. |

#### Device info

| **Parameter** | **Description** |
| --- | --- |
| User Agent | The user-agent string of the device used when the conversion occurred. |
| IP Address | The IP address of the device used when the conversion occurred. Google Ads does not support IP address matching for users in the EEA, United Kingdom, or Switzerland. |
| Device Category | The category of device used, such as desktop, tablet, or mobile. |
| Language Code | The language of the device in ISO 639-1 format. |
| Screen Height | The height of the device screen in pixels. |
| Screen Width | The width of the device screen in pixels. |
| Operating System | The operating system or platform of the device. |
| Operating System Version | The version of the operating system or platform. |
| Device Model | The model of the device. |
| Device Brand | The brand or manufacturer of the device. |
| Browser | The browser used when the conversion occurred. |
| Browser Version | The version of the browser used when the conversion occurred. |

#### Consent

Map consent values at the event level. The connector passes these values to Google without modification. When consent is denied, all mapped event fields are still included in the request. Google applies restrictions on its side.

| **Parameter** | **Description** |
| --- | --- |
| Ad User Data Consent | The consent status for ad user data. Valid values are `CONSENT_GRANTED`, `CONSENT_DENIED`, and `CONSENT_STATUS_UNSPECIFIED`. The shorthand values `GRANTED` and `DENIED` are also accepted. If this field is not mapped, the consent field is omitted from the event. |
| Ad Personalization Consent | The consent status for ad personalization. Valid values are `CONSENT_GRANTED`, `CONSENT_DENIED`, and `CONSENT_STATUS_UNSPECIFIED`. The shorthand values `GRANTED` and `DENIED` are also accepted. If this field is not mapped, the consent field is omitted from the event. |

#### User properties

| **Parameter** | **Description** |
| --- | --- |
| Customer Type | The type of customer associated with the conversion. Valid values are `NEW`, `RETURNING`, and `REENGAGED`. |
| Customer Value Bucket | The value bucket for the customer. Valid values are `LOW`, `MEDIUM`, and `HIGH`. |
| Additional User Property | An additional user property as a name-and-value pair. Both the property name and value are required. |

#### Custom variables

Map additional conversion data as custom key-value pairs.


<blockquote>
Map custom variable **IDs**, not variable names. Mapping variable names or free-form text causes a request error.
</blockquote>


| **Parameter** | **Description** |
| --- | --- |
| Variable | The custom variable ID. |
| Value | The value associated with the custom variable. |

#### Experimental fields

Map additional experimental fields as custom key-value pairs.

| **Parameter** | **Description** |
| --- | --- |
| Field | The experimental field name. |
| Value | The value associated with the experimental field. |

#### Optional overrides

| **Parameter** | **Description** |
| --- | --- |
| Conversion Action ID Override | (Optional) Select or map a conversion action ID to override the action-level **Conversion Action ID**. The override value takes precedence when resolved. |
| Customer ID Override | (Optional) Select or map a customer ID to override the connector-level **Customer ID** for this event. |
| Validate Only | Select this checkbox to validate the request without ingesting the events. Use this option for testing. |
