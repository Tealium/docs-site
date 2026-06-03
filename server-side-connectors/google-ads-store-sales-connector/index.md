---
title: Google Ads Store Sales Connector Setup Guide
description: This article describes how to set up the Google Ads Store Sales connector.
url: https://docs.tealium.com/server-side-connectors/google-ads-store-sales-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Google Ads API
* API Version: v18
* API Endpoint: `https://googleads.googleapis.com/`
* Documentation: [Google Ads API](https://developers.google.com/google-ads/api/docs/start)

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Upload Transaction | ✓ | ✓ |
| Upload Transaction (Multiple Identifiers) | ✓ | ✓ |

## Configure Settings

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors]().

When you add this connector you are prompted to accept the vendor&#39;s data platform policy.

After adding the connector, configure the following settings:

* **Customer ID**  
(Required) The Google Ads account customer ID.
* **Manager Customer ID**  
(Optional) If you are accessing the account on behalf of a client, the Manager Customer ID must be set. You can find your Customer ID by logging into Google Ads and going to **Preferences &gt; Access &amp; Security &gt; Manager**.

## Action settings - parameters and options

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action - Upload Transaction

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100000
* Max time since oldest request: 60 minutes
* Max size of requests: 40 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Conversion Action | Resource name of an enabled Google Ads conversion action in the format `customers/{customer_id}/conversionActions/{conversion_action_id}`. The conversion action ID is the `ctId` query parameter in the Google Ads URL. The conversion action must be of the type `STORE_SALES`. For more information, see [Google Ads API: Import store sales conversions](https://developers.google.com/google-ads/api/docs/conversions/upload-store-sales-transactions). |

##### User Identifiers

| **Parameter** | **Description** |
| --- | --- |
| Address Info: Country Code | The country code in the user&#39;s address using the two-letter ISO 3166-1 alpha-2 format. |
| Address Info: First Name (already SHA256 hashed) | Provide the user’s first name that has been already whitespace trimmed, lowercase, and SHA256 hashed. |
| Address Info: First Name (apply SHA256 hash) | Provide a plain text first name for the user and the connector will whitespace trim, lowercase, and hash this value using a SHA256 hash.  |
| Address Info: Last Name (already SHA256 hashed) | Provide the user’s last name that has been already whitespace trimmed, lowercase, and SHA256 hashed. |
| Address Info: Last Name (apply SHA256 hash) | Provide a plain text last name for the user and the connector will whitespace trim, lowercase, and hash this value using a SHA256 hash. |
| Address Info: Postal Code | Postal code of the user&#39;s address. |
| Email Address (already SHA256 hashed) | Provide an email address for the user that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address for the user and the connector will whitespace trim, lowercase, and hash this value using a SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number for the user that has been already whitespace trimmed and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number for the user and the connector will whitespace trim and hash this value using a SHA256 hash. |
| Third Party User ID | A third party-assigned user ID. |

##### Transaction Data

| **Parameter** | **Description** |
| --- | --- |
| Transaction DateTime | (Required) Timestamp when the transaction occurred in the format: `YYYY-MM-DD HH:MM:SS[&#43;/-HH:MM]`, where `[&#43;/-HH:MM]` is an optional timezone offset from UTC. |
| Transaction Amount | (Required) Transaction amount in micros, where one million is equivalent to one currency unit. |
| Currency Code | (Required) The transaction currency code in an ISO 4217 three-letter format. |
| Transaction Upload Fraction | (Required) The ratio of sales uploaded compared to the overall sales associated with a customer. This value must be between 0 and 1 (excluding 0). For example, if you upload half the sales that you are able to associate with a customer, this value would be 0.5. |
| Transaction Order ID | The transaction order ID. |
| Custom Key | Name of the store sales custom variable key. A predefined key that can be applied to the transaction and then later used for custom segmentation in reporting. |
| Custom Value | Value of the custom variable for each transaction. |
| Store Code | Unique store ID previously uploaded to Google. |
| Item ID | A unique identifier of a product. It can be either the Merchant Center Item ID or GTIN (Global Trade Item Number).  |
| Quantity | The number of items sold. If not set, the default is 1. |
| Country Code | Common Locale Data Repository (CLDR) territory code of the country associated with the feed where your items are uploaded.  |
| Language Code | ISO 639-1 code of the language associated with the feed where your items are uploaded |
| Merchant ID | ID of the Merchant Center Account. |

##### Consent

The connector sends the value of `GRANTED` for `adUserData` and `adPersonalization` consent by default. To override the default, map a relevant EventStream attribute to `Ad User Data Consent` and/or `Ad Personalization Consent` with a value of `DENIED`.

| **Parameter** | **Description** |
| --- | --- |
| Ad User Data Consent | Consent for ad user data. The default value is `GRANTED`. Valid values are `GRANTED` and `DENIED`. |
| Ad Personalization Consent | Consent for ad personalization. The default value is `GRANTED`. Valid values are `GRANTED` and `DENIED`. |

### Action - Upload Transaction (Multiple Identifiers)

#### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 33000
* Max time since oldest request: 60 minutes
* Max size of requests: 40 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Conversion Action | Resource name of an enabled Google Ads conversion action in the format `customers/{customer_id}/conversionActions/{conversion_action_id}`. The conversion action ID is the `ctId` query parameter in the Google Ads URL. The conversion action must be of the type `STORE_SALES`. For more information, see [Google Ads API: Import store sales conversions](https://developers.google.com/google-ads/api/docs/conversions/upload-store-sales-transactions). |

##### User Identifiers

| **Parameter** | **Description** |
| --- | --- |
| Address Info: Country Code | The country code in the user&#39;s address using the two-letter ISO 3166-1 alpha-2 format. |
| Address Info: First Name (already SHA256 hashed) | Provide the user’s first name that has been already whitespace trimmed, lowercase, and SHA256 hashed. |
| Address Info: First Name (apply SHA256 hash) | Provide a plain text first name for the user and the connector will whitespace trim, lowercase, and hash this value using a SHA256 hash.  |
| Address Info: Last Name (already SHA256 hashed) | Provide the user’s last name that has been already whitespace trimmed, lowercase, and SHA256 hashed. |
| Address Info: Last Name (apply SHA256 hash) | Provide a plain text last name for the user and the connector will whitespace trim, lowercase, and hash this value using a SHA256 hash. |
| Address Info: Postal Code | Postal code of the user&#39;s address. |
| Email Address (already SHA256 hashed) | Provide an email address for the user that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address for the user and the connector will whitespace trim, lowercase, and hash this value using a SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number for the user that has been already whitespace trimmed and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number for the user and the connector will whitespace trim and hash this value using a SHA256 hash. |
| Third Party User ID | A third party-assigned user ID. |

##### Transaction Data

| **Parameter** | **Description** |
| --- | --- |
| Transaction DateTime | (Required) Timestamp when the transaction occurred in the format: `YYYY-MM-DD HH:MM:SS[&#43;/-HH:MM]`, where `[&#43;/-HH:MM]` is an optional timezone offset from UTC. |
| Transaction Amount | (Required) Transaction amount in micros, where one million is equivalent to one currency unit. |
| Currency Code | (Required) The transaction currency code in an ISO 4217 three-letter format. |
| Transaction Upload Fraction | (Required) The ratio of sales uploaded compared to the overall sales associated with a customer. This value must be between 0 and 1 (excluding 0). For example, if you upload half the sales that you are able to associate with a customer, this value would be 0.5. |
| Transaction Order ID | The transaction order ID. |
| Custom Key | Name of the store sales custom variable key. A predefined key that can be applied to the transaction and then later used for custom segmentation in reporting. |
| Custom Value | Value of the custom variable for each transaction. |
| Store Code | Unique store ID previously uploaded to Google. |
| Item ID | A unique identifier of a product. It can be either the Merchant Center Item ID or GTIN (Global Trade Item Number).  |
| Quantity | The number of items sold. If not set, the default is 1. |
| Country Code | Common Locale Data Repository (CLDR) territory code of the country associated with the feed where your items are uploaded.  |
| Language Code | ISO 639-1 code of the language associated with the feed where your items are uploaded |
| Merchant ID | ID of the Merchant Center Account. |

##### Consent

The connector sends the value of `GRANTED` for `adUserData` and `adPersonalization` consent by default. To override the default, map a relevant EventStream attribute to `Ad User Data Consent`, `Ad Personalization Consent`, or both with a value of `DENIED`.

| **Parameter** | **Description** |
| --- | --- |
| Ad User Data Consent | Consent for ad user data. The default value is `GRANTED`. Valid values are `GRANTED` and `DENIED`. |
| Ad Personalization Consent | Consent for ad personalization. The default value is `GRANTED`. Valid values are `GRANTED` and `DENIED`. |
