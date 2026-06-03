---
title: Google Ads Enhanced Conversions for Leads Connector Setup Guide
description: This article describes how to set up the Google Ads Enhanced Conversions for Leads connector.
url: https://docs.tealium.com/server-side-connectors/google-ads-enhanced-conversions-for-leads-connector/
---
## Connector actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Conversion| ✓| ✓|

## API information

This connector uses the following vendor API:

* API Name: Google Ads API
* API Version: v18
* API Endpoint: `https://googleads.googleapis.com/`
* Documentation: [Google Ads API: Upload Enhanced Conversions For Leads](https://developers.google.com/google-ads/api/docs/conversions/upload-identifiers)

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 2,000
* Max time since oldest request: 10 minutes
* Max size of requests: 2 MB

### Consent

The connector sends the value of `GRANTED` for `adUserData` by default. To override the default, map a relevant EventStream attribute to `Ad User Data Consent` with a value of `DENIED`.

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](/server-side/connectors/manage/) article.

After adding the connector, configure the following settings:

* **Customer ID**  
(Required) Provide Ads account customer ID to manage.
* **Manager Customer ID**  
(Optional) If you are accessing the account on behalf of a client, the Manager Customer ID must be set. You can find your Customer ID by logging into Google Ads and going to **Preferences &gt; Access &amp; Security &gt; Manager**.

Click **Done** when you are finished configuring the connector.

## Action settings — parameters and options

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Send Conversion

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Conversion Action| Select existing conversion action with a type of **UPLOAD_CLICKS** and enhanced conversions enabled.  For more information, see [Google Ads Enhanced Conversion Tracking](https://support.google.com/google-ads/answer/9888656).|

#### User Data

|**Parameter**| **Description**|
|---| ---|
|Email Address (already SHA256 hashed)| Provide an email address that has been already whitespace trimmed, lowercased, and SHA256 hashed. Remove all periods (`.`) that precede the domain name in `gmail.com` and `googlemail.com` email addresses before hashing.|
|Email Address (apply SHA256 hash)| Provide a plain text email address and the connector will remove all periods (`.`) that precede the domain name in `gmail.com` and `googlemail.com` email addresses, whitespace trim, lowercase, and hash this value using SHA256 hash.|
|Phone Number (already SHA256 hashed)| Provide a phone number according to the [E164 standard](https://en.wikipedia.org/wiki/E.164) that has been already whitespace trimmed and SHA256 hashed.|
|Phone Number (apply SHA256 hash)| Provide a plain text phone number and the connector will remove all non-digit symbols, prefix the number with a plus sign (`&#43;`), whitespace trim, and hash this value using SHA256 hash.|
|gclid| Google click ID (gclid) associated with the conversion. Note: If you provide `gclid` and `user_identifiers` (email/phone) for a conversion, Google Ads will ignore the `user_identifiers`.|
| Address Info: First Name (already SHA256 hashed) | Provide a first name which has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: First Name (apply SHA256 hash) | Provide a plain text first name and the connector will lowercase, trim whitespaces, and hash this value using SHA256 hash. |
| Address Info: Last Name (already SHA256 hashed) | Provide a last name which has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Last name (apply SHA256 hash) | Provide a plain text last name and the connector will lowercase, trim whitespaces, and hash this value using SHA256 hash. |
| Address Info: Street Address (already SHA256 hashed) | Provide a street address which has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address Info: Street Address (apply SHA256 hash) | Provide a plain text street address and the connector will lowercase, trim whitespaces, and hash this value using SHA256 hash. |
| Address Info: City | Provide a plain text city. |
| Address Info: State | Provide a plain text state. |
| Address Info: Zip Code | Provide a plain text zip code. |
| Address Info: Country | Provide a plain text country. |

#### Conversion Data

|**Parameter**| **Description**|
|---| ---|
|Conversion Value| Monetary value of the conversion.|
|Conversion Currency| Currency code of the conversion.|
|Conversion Time| The date and time when the original conversion occurred. The time zone must be specified. The format is &lt;code&gt;yyyy-mm-dd hh:mm:ss&#43;&amp;#124;-hh:mm&lt;/code&gt;. For example, `2022-01-01 12:32:45-08:00` or `2022-01-01 12:32:45&#43;08:00`. If no value is mapped, the value is set to the current time.|
|Order ID| The order ID associated with the conversion. An order ID can only be used for one conversion per conversion action.|
|Custom Variables| The custom variables associated with this conversion. Map the value to the custom variable ID. The connector will send `conversion_custom_variable` field in the following format: `customers/{customer_id}/conversionCustomVariables/{custom_variable_id}`.|

#### Cart Data

| **Parameter** | **Description** |
| --- | --- |
|Merchant ID| The Merchant Center ID where the items are uploaded.|
|Feed Country Code| The country code associated with the feed where the items are uploaded.|
|Feed Language Code| The language code associated with the feed where the items are uploaded.|
|Local Transaction Cost| Sum of all transaction level discounts, such as free shipping and coupon discounts for the whole cart.|
|Product ID| The shopping ID of the item. Must be equal to the Merchant Center product identifier. Provide array type attribute to add multiple items. Array type attributes must be of equal length. Single value attributes can be used and will apply to each item.|
|Quantity| Number of items sold. Provide array type attribute to add multiple items. Array type attributes must be of equal length. Single value attributes can be used and will apply to each item.|
|Unit Price| Unit price excluding tax, shipping, and any transaction level discounts. Provide array type attribute to add multiple items. Array type attributes must be of equal length. Single value attributes can be used and will apply to each item.|
| Customer ID Override | (Optional) Provide a Customer ID to override the Customer `ID` in the connector configuration. If using this option you must also use the Conversion Action ID override. |
| Manager Customer ID Override | (Optional) Provide a Manager Customer ID if using the Customer ID Override and accessing a client customer. |
|Conversion Action Override | (Optional) Provide a Conversion Action ID to override the conversion action in the **Required** section. This parameter lets you use EventStream variables to populate the Conversion Action ID. To find the Conversion Action ID, go to your Google Ads dashboard, and click the conversion. The Conversion Action ID is the value of the `ctId` query parameter in the website URL. For example, if the URL is `https://ads.google.com/aw/conversions/detail?ctId=987654321`, the Conversion Action ID is `987654321`. |
| Ad User Data Consent | (Optional) Consent for ad user data. The default value is `GRANTED`. Valid values are `GRANTED` or `DENIED`. |