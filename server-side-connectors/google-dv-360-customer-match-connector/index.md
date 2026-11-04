---
title: Google Display & Video 360 Customer Match Connector Setup Guide
description: Set up the Google Display & Video 360 Customer Match connector to add and remove users from customer match lists in DV360.
url: https://docs.tealium.com/server-side-connectors/google-dv-360-customer-match-connector/
---
## Requirements

Before configuring this connector, add Tealium as a linked account in your Google Display & Video 360 account.

For more information, see [Google Display & Video 360: Sharing audience lists from external data management platforms or customer match uploader partners](https://support.google.com/displayvideo/answer/9649053?hl=en).

## API information

This connector uses the following vendor API:

* **API Name**: Google Data Manager API
* **API Version**: v1
* **API Endpoint**: `https://datamanager.googleapis.com`
* **Documentation**: [Google Data Manager API](https://developers.google.com/data-manager/api/reference/rest)

The deprecated actions use the Google Ads API. For details, see [Add to Customer Match List (Deprecated)](#add-to-customer-match-list-deprecated).

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/manage-connectors/).


<blockquote>
When you add this connector, you are prompted to accept the vendor's data platform policy.
</blockquote>


After adding the connector, configure the following settings:

* **Customer ID**: (Required) Your Google DV360 Partner ID that is linked to Tealium. To find your Partner ID, go to **Partner Settings > Basic Details** in the Google DV360 dashboard.
* **Target Product**: (Required) The target product of the linked account.

Click **Done**.

### Create customer match list

To create a customer match list, click **Create Customer Match List** and enter the following information:

| **Parameter** | **Description** |
| --- | --- |
| List Name | (Required) Customer match list name. |
| List type | (Required) The list type. This affects the type of user identification information to be used with this list:<ul><li>Contact Info - members are matched from customer info such as email address, phone number, or physical address.</li><li>Mobile Advertising - members are matched from mobile advertising IDs.</li></ul> |
| App ID | Required for Mobile Advertising list types. A string that uniquely identifies the mobile application from which the data was collected. |
|  List Membership Lifespan | (Optional) The number of days a user stays on the list since their most recent addition to the list. Number must be between `0` and `540`. The default lifespan is 540 days. |
| List Description | (Optional) List description. |

## Actions

| Action name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add to Customer Match List (Data Manager API) | ✓ | ✓ |
| Remove from Customer Match List (Data Manager API) | ✓ | ✓ |
| Add to Customer Match List (Deprecated) | ✓ | ✓ |
| Remove from Customer Match List (Deprecated) | ✓ | ✓ |

### User identifiers

Each action requires a user identifier. Normalize and hash these values using SHA-256, or let the connector do it for you. Each value must meet the following requirements:

* Lower-case
* Blank spaces trimmed from the beginning and end of the text
* Hashed with SHA-256

The `User List` type you select determines the type of user identifier. The `User List` type is one of the following:

* `CONTACT_INFO`
* `MOBILE_ADVERTISING_ID`

The following user identifier fields are supported:

|User Identifier Field| Description|
|---| ---|
| `CONTACT_INFO` | <ul><li>Provide a hashed email address, hashed phone number, or address information.</li><li>When providing address information, all four fields are required: country code, first name, last name, and postal code. If any **Address Info** field is missing, the connector removes the entire address object from the request. If no user data remains after removal, the action fails with a validation error and is not retried.</li><li>**Address Info: Country Code**: Provide the two-letter country code for the user's address in ISO 3166-1 alpha-2 format.</li><li>**Address Info: First Name (already SHA256 hashed)**: Provide the first name with leading and trailing whitespace removed, converted to lowercase, and SHA-256 hashed.</li><li>**Address Info: First Name (apply SHA256 hash)**: Provide the first name in plain text. The connector SHA-256 hashes the value.</li><li>**Address Info: Last Name (already SHA256 hashed)**: Provide the last name with leading and trailing whitespace removed, converted to lowercase, and SHA-256 hashed.</li><li>**Address Info: Last Name (apply SHA256 hash)**: Provide the last name in plain text. The connector SHA-256 hashes the value.</li><li>**Address Info: Postal Code**: Provide the postal code for the user's address.</li><li>**Email Address (already SHA256 hashed)**: Provide an email address with leading and trailing whitespace removed, converted to lowercase, and SHA-256 hashed. The value must be a valid SHA-256 hex string containing 64 hexadecimal characters. Invalid values are removed from the request before it is sent.</li><li>**Email Address (apply SHA256 hash)**: Provide an email address in plain text. The connector SHA-256 hashes the value.</li><li>**Phone Number (already SHA256 hashed)**: Provide a phone number with leading and trailing whitespace removed and SHA-256 hashed. The value must be a valid SHA-256 hex string containing 64 hexadecimal characters. Invalid values are removed from the request before it is sent. If no valid user identifiers remain, the action fails with a validation error and is not retried.</li><li>**Phone Number (apply SHA256 hash)**: Provide a phone number in plain text. The connector SHA-256 hashes the value.</li></ul> |

### Add to Customer Match List (Data Manager API)

#### API information

This connector uses the following vendor API:

* API Name: Google Data Manager API
* API Version: v1
* API Endpoint: `https://datamanager.googleapis.com`
* Documentation: [Google Data Manager API](https://developers.google.com/data-manager/api/reference/rest)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 66,000
* Max time since oldest request: 1440 minutes
* Max size of requests: 50 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer Match List | Select a customer match list. Only lists created through the Tealium connector are available. To create a customer match list, see [Create customer match list](#create-customer-match-list). |
| User Identifier | The user identifier to match. For supported fields, see [User identifiers](#user-identifiers). |

##### Consent

By default, the connector sends `GRANTED` for `adUserData` and `adPersonalization` consent. Use audience logic to prevent non-consented visitors from being added to lists. Use the **Remove from Customer Match List** action to remove non-consented visitors from lists.

### Remove from Customer Match List (Data Manager API)

This action uses the same API, batch limits, and parameters as [Add to Customer Match List (Data Manager API)](#add-to-customer-match-list-data-manager-api).

### Add to Customer Match List (Deprecated)


<blockquote>
This action is deprecated. Migrate to [Add to Customer Match List (Data Manager API)](#add-to-customer-match-list-data-manager-api).
</blockquote>


Tealium retrieves list statistics directly from Google DV 360, which may cause a difference between matches and the total volume of connector requests in this connector and the [Google DV 360 Customer Match connector insight](https://docs.tealium.com/connector-insights-google-dv360-customer-match/).

#### API information

This connector uses the following vendor API:

* API Name: Google Ads API
* API Version: v18
* API Endpoint: `https://googleads.googleapis.com/`
* Documentation: [Google Ads API](https://developers.google.com/google-ads/api/docs/start)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 1440 minutes
* Max size of requests: 50 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer Match List | Select a customer match list. Only lists created through the Tealium connector are available. To create a customer match list, see [Create customer match list](#create-customer-match-list). |

##### Consent

For consent behavior, see [Add to Customer Match List (Data Manager API)](#add-to-customer-match-list-data-manager-api).

### Remove from Customer Match List (Deprecated)


<blockquote>
This action is deprecated. Migrate to [Remove from Customer Match List (Data Manager API)](#remove-from-customer-match-list-data-manager-api).
</blockquote>


#### API information

This connector uses the following vendor API:

* API Name: Google Ads API
* API Version: v18
* API Endpoint: `https://googleads.googleapis.com/`
* Documentation: [Google Ads API](https://developers.google.com/google-ads/api/docs/start)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 100,000
* Max time since oldest request: 1440 minutes
* Max size of requests: 50 MB

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Customer Match List | Select a customer match list. Only lists created through the Tealium connector are available. |
