---
title: The Trade Desk CRM Data connector setup guide
description: This article describes how to set up the The Trade Desk CRM Data connector.
url: https://docs.tealium.com/server-side-connectors/the-trade-desk-crm-data-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: The Trade Desk CRM API
* API Version: v3
* API Endpoint: `https://api.thetradedesk.com/v3/crmdata/`
* Documentation: [The Trade Desk CRM API](https://partner.thetradedesk.com/v3/portal/data/doc/DataIntegrateCRMData)

## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. Requests are queued until one of the following three thresholds is met:

* Max number of requests: 10,000
* Max time since oldest request: 720 minutes
* Max size of requests: 100 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).


After adding the connector, configure the following settings:
* **Advertiser ID**
  * (Required) Your Trade Desk advertiser ID.
* **API Token**
  * (Required) A long-lived API token.
  * To generate a token, go to the **Manage API Tokens** section in the **User Profile** menu of The Trade Desk Partner Portal.
  * For more information, see [The Trade Desk: API Token Authentication](https://partner.thetradedesk.com/v3/portal/api/doc/Authentication).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Upload Targeting Data | ✓ | ✓ |
| Upload Conversion Data | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Upload Targeting Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Targeting Segment | Select a Trade Desk targeting segment from the list. Click **Create Targeting Segment** to create a targeting segment. |

#### User Identifier

Optional Parameters:

| **Parameter** | **Description** |
| --- | --- |
| Email Address | Provide a plain text email address. |
| Email Address (Already SHA256 hashed) | Provide an email address that has been whitespace trimmed, lowercased, and SHA256 hashed. The connector encodes the raw bytes using Base64 before sending it to The Trade Desk. |
| Phone Number | Provide a plain text phone number. Note that phone numbers cannot be uploaded for EU segments. |
| Phone Number (Already SHA256 hashed) | Provide a phone number that has been whitespace trimmed and SHA256 hashed. The connector encodes the raw bytes using Base64 before sending it to The Trade Desk. Note that phone numbers cannot be uploaded for EU segments. |

### Upload Conversion Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Conversion Segment | Enter the Conversion Segment ID, shown as Tracking Tag ID in The Trade Desk UI.<ul><li>Click **Create Conversion Segment** to create a new conversion segment.</li><li>After creation, the segment ID appears in the **Conversion Segment** field.</li><li>Before uploading, the conversion segment must be attached to a campaign in The Trade Desk UI. You can’t attribute uploaded data to a campaign until this step is complete.</li></ul> |

#### User Identifier

Optional Parameters:

| **Parameter** | **Description** |
| --- | --- |
| Email Address | Provide a plain text email address. |
| Email Address (Already SHA256 hashed) | Provide an email address that has been whitespace trimmed, lowercased, and SHA256 hashed. The connector encodes the raw bytes using Base64 before sending it to The Trade Desk. |
| Phone Number | Provide a plain text phone number. Note that phone numbers cannot be uploaded for EU segments. |
| Phone Number (Already SHA256 hashed) | Provide a phone number that has been whitespace trimmed and SHA256 hashed. The connector encodes the raw bytes using Base64 before sending it to The Trade Desk. Note that phone numbers cannot be uploaded for EU segments. |

#### Conversion Data

Optional Parameters:

| **Parameter** | **Description** |
| --- | --- |
| Timestamp | The timestamp of the conversion. If not populated, the connector sends the current timestamp. |
| Value | The value of the conversion to two decimal places. |
| Currency | The currency of the value amount. For example, `USD`. |
| Country | The full name of the country where the conversion occurred. |
| Region | Required if the **Country** field is set to United States. The full name or code of the region where the conversion occurred. For example, `NY` or `New York`. |
| Metro | The numerical metropolitan area geotargeting code where the conversion occurred. |
| City | The city where the conversion occurred. |
| Order ID | The unique identifier for a transaction or conversion event. The maximum length is 64 characters. |
| Privacy Type | Specifies the applicable privacy regulation based on the user's geographical location (`GDPR`, `GPP`). |
| Is Applicable | Indicates if the value specified in the privacy type property is applicable. |
| Consent String | The user's consent when the privacy regulations are in effect (`TCF` string, `GPP` string). |
