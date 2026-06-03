---
title: Google Ads Customer Match (Tealium-Provided Credentials) Connector Setup Guide
description: This article describes how to set up the Google Ads Customer Match connector, which uses Tealium-Provided Credentials.
url: https://docs.tealium.com/server-side-connectors/google-ads-customer-match-connector/
---
## Migrate to Google Data Manager API actions

The following actions use an older Google Ads API:

* Add User to Remarketing List
* Remove User from Remarketing List

Use the following replacement actions, which are based on the Google Data Manager API:

* Add User to List (Data Manager API)
* Remove User from List (Data Manager API)

For more information, see the [Google Data Manager API migration guide]().

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

When you add this connector, you are prompted to accept the vendor&#39;s data platform policy.

After adding the connector, configure the following settings:

* **Customer ID**: (Required) Provide the Ads account customer ID to manage.
* **Manager Customer ID**: (Optional) If you&#39;re accessing a client customer, the Manager Customer ID must be set and have full access to the Ads account.

### Create user list

To create a user list, click **Create User List** and enter the following information:

| **Parameter** | **Description** |
| --- | --- |
| List Name | (Required) User list name. |
| List Type | (Required) The list type. This affects the type of user identification information to be used with this list:&lt;ul&gt;&lt;li&gt;`CONTACT_INFO`: Users are matched from customer info such as email address, phone number, or physical address.&lt;/li&gt;&lt;li&gt;`CRM_ID`: Users are matched from advertiser generated and assigned user ID.&lt;/li&gt;&lt;li&gt;`MOBILE_ADVERTISING_ID`: Users are matched from mobile device ID (advertising ID/IDFA).&lt;/li&gt;&lt;/ul&gt; |
| App ID | Required for mobile advertising list types. A string that uniquely identifies the mobile application from which data is being sent to Google Ads API. |
| List Membership Lifespan | (Optional) The number of days a user stays on the list since their most recent addition to the list. Number must be between `0` and `540`. The default lifespan is 540 days. |
| List Description | (Optional) List description. |

## Actions

| Action Name | AudienceStream | EventStream |
| ------------| :------------: | :---------: |
| Add User to List (Data Manager API) | ✓ | ✓ |
| Remove User from List (Data Manager API) | ✓ | ✓ |
| Add User to Remarketing List| ✓ | ✓ |
| Remove User from Remarketing List| ✓ | ✓ |

### User Identifiers

Each action requires a user identifier. The vendor requires that these values are normalized and hashed using SHA-256. Each mapped user identifier value is expected to meet the following requirements:

* Lowercase
* Trimmed whitespace from the beginning and end of the text
* Hashed with SHA-256

You can map attributes that are already normalized and hashed or you can allow the connector to normalize and hash them for you. Select the appropriate mapping for your scenario.

The required user identifier is based on the user list type selected. The user list type can be one of the following:

* Google Ads API:
  * `CONTACT_INFO`
  * `CRM_ID`
  * `MOBILE_ADVERTISING_ID`
* Google Data Manager API:
  * `CONTACT_ID`
  * `MOBILE_ID`
  * `USER_ID`

The following user identifier fields are supported:

| User Identifier Field | Description |
|---| ---|
| `CONTACT_INFO` (Google Ads API)|  Provide hashed email, hashed phone number, or address information. All address information fields listed below are required for this user data type.&lt;ul&gt;&lt;li&gt;**Address Info: Country Code**: 2-letter country code, in ISO 3166-1 alpha-2 format, of the user&#39;s address.&lt;/li&gt;&lt;li&gt;**Address Info: First Name (already SHA256 hashed)**: Provide a first name that has been whitespace trimmed, lowercased, and SHA256 hashed.&lt;/li&gt;&lt;li&gt;**Address Info: First Name (apply SHA256 hash)**: Provide a plain text first name and the connector hashes this value using SHA256 hash.&lt;/li&gt;&lt;li&gt;**Address Info: Last Name (already SHA256 hashed)**: Provide a last name that has been whitespace trimmed, lowercased, and SHA256 hashed.&lt;/li&gt;&lt;li&gt;**Address Info: Last Name (apply SHA256 hash)**: Provide a plain text last name and the connector hashes this value using the SHA256 hash.&lt;/li&gt;&lt;li&gt;**Address Info: Postal Code**: Provide a postal code of the user&#39;s address.&lt;/li&gt;&lt;li&gt;**Email Address (already SHA256 hashed)**: Provide an email address or array of email addresses that have been whitespace trimmed, lowercased, and SHA256 hashed.&lt;/li&gt;&lt;li&gt;**Email Address (apply SHA256 hash)**: Provide a plain text email address or array of email addresses and the connector hashes these values using the SHA256 hash.&lt;/li&gt;&lt;li&gt;**Phone Number (already SHA256 hashed)**: Provide a phone number or array of phone numbers that have been whitespace trimmed and SHA256 hashed.&lt;/li&gt;&lt;li&gt;**Phone Number (apply SHA256 hash)**: Provide a plain text phone number or array of phone numbers and the connector hashes the values using the SHA256 hash.&lt;/li&gt;&lt;/ul&gt; |
|`CRM_ID` (Google Ads API)|  &lt;ul&gt;&lt;li&gt;**User ID**: (Required) Advertiser-assigned user ID for customer match upload.&lt;/li&gt;&lt;/ul&gt; |
|`MOBILE_ADVERTISING_ID` (Google Ads API)|  &lt;ul&gt;&lt;li&gt;**Mobile ID**: (Required) Mobile device ID (advertising ID/IDFA).&lt;/li&gt;&lt;/ul&gt; |
|`CONTACT_ID` (Data Manager API)| **Contact info**: Email address, phone number, and address. |
|`MOBILE_ID` (Data Manager API)|  **Mobile ID**: Mobile device ID. |
|`USER_ID` (Data Manager API)|  **User ID**: First-party identifier. |

### Add User to List (Data Manager API)

#### API Information

This connector uses the following vendor API:

* API Name: Google Data Manager API
* API Version: v1
* API Endpoint: `https://datamanager.googleapis.com`
* Documentation: [Google Data Manager API](https://developers.google.com/data-manager/api/reference/rest)

#### Batch limits

This action uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10,000
* Max time since oldest request: 60 minutes
* Max size of requests: 40 MB

#### Parameters

| Parameter | Description |
| --- | --- |
| User List | Select a user list from the Data Manager API. For more information, see: [Data Manager API: Customer match overview](https://developers.google.com/data-manager/api/devguides/audiences/google-ads/customer-match). |

#### User Identifier

| Parameter | Description |
| --- | --- |
| Customer ID Override | (Optional) Provide a Customer ID to override the Customer ID in the connector configuration. If using this option you must also use the User List ID Override. |
| User List ID Override | (Optional) Provide a User List ID to override the user list in the Required Section. This field lets you use event attributes to populate the User List ID. This is required if using Customer ID Override. The value must be the list ID, such as `9310271231`. |

### Remove User from List (Data Manager API)

For mapping options, see [Add User to List (Data Manager API)](#add-user-to-list-data-manager-api).

### Add User to Remarketing List (Deprecated)

#### Batch Limits

This connector action can use batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 33,000
* Max time since oldest request: 60 minutes
* Max size of requests: 40 MB

#### API information

This connector uses the following vendor API:

* API Name: Google Ads API
* API Version: v18
* API Endpoint: `https://googleads.googleapis.com/`
* Documentation: [Google Ads API](https://developers.google.com/google-ads/api/docs/start)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Remarketing List | Select a remarketing user list. For more information, see [Google Ads: Remarketing and Audience Targeting](https://developers.google.com/google-ads/api/docs/remarketing/overview). Available options contain only user lists of first-party CRM data type. To create a user list, see [Create user list](#create-user-list).|
| Customer ID Override | (Optional) Provide a customer ID to override the customer ID in the connector configuration. If using this option, you must also enter a **User List ID Override**. |
| Manager Customer ID Override | (Optional) Provide a Manager Customer ID if using a **Customer ID Override** and accessing a client customer. |
| User List ID Override | (Optional) Provide a user list resource name (list ID and type) to override the user list. This field lets you use EventStream variables to populate the user list ID. This is required if using a **Customer ID Override**. The value should be in the following format `ID:TYPE`, for example `123456:CONTACT_INFO`. |

#### Consent

When using the **Add User to Remarketing List** action, the connector sends values of `GRANTED` for the `adUserData` and `adPersonalization` parameters. To prevent non-consented visitors from being added to lists, create an audience with rules that check visitor profile consent status. Then use the **Remove from Remarketing List** action to remove visitors that have not given consent from lists.

### Remove User from Remarketing List (Deprecated)

For mapping options, see [Add User to Remarketing List](#add-user-to-remarketing-list-deprecated).