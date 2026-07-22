---
title: Amazon Ads Data Manager Connector Setup Guide
description: This article describes how to set up the Amazon Ads Data Manager connector.
url: https://docs.tealium.com/server-side-connectors/amazon-ads-data-manager-connector/
---
## Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10,000
* Max time since oldest request: 60 minutes
* Max size of requests: 2 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About: Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:
* **API Base URL**  
  * Select your API Base URL.
* **Amazon Ads Data Manager ID**  
  * Your Ads data manager (ADM) Manager ID. To find it, click Manager Account in the upper-right menu of the ADM UI.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add Visitor to Audience | ✓ | ✓ |
| Remove Visitor from Audience | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Add Visitor to Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience Dataset | Select your ADM audience dataset. Click **Create Audience Dataset** to create an ADM audience dataset. |

#### External User ID

| **Parameter** | **Description** |
| --- | --- |
| External ID | This is an external user identifier defined by data providers. |
| External ID (apply SHA256 hash) | Use this parameter if you’d like the connector to hash the external ID value before sending to Amazon. |


#### User Identifiers

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| First Name (already SHA256 hashed) | Provide a first name, already whitespace trimmed, lowercased, and SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address (already SHA256 hashed) | Provide an address, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address (apply SHA256 hash) | Provide a plain text address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| City (already SHA256 hashed) | Provide a city, already whitespace trimmed, lowercased, and SHA256 hashed. |
| City (apply SHA256 hash) | Provide a plain text city and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| State (already SHA256 hashed) | Provide a state, already whitespace trimmed, lowercased, and SHA256 hashed. |
| State (apply SHA256 hash) | Provide a plain text state and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Postal Code (already SHA256 hashed) | Provide a postal code, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Postal Code (apply SHA256 hash) | Provide a plain text postal code and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| MAID | The mobile advertising ID. |
| LiveRamp ID | The LiveRamp ID. |

#### Country Code

| **Parameter** | **Description** |
| --- | --- |
| Country Code | The country code is 2 character string in the ISO 3166 format that indicates from which country the data was collected. A country code added at the record-level supersedes a country code added at the audience level. |
| IP Address | IP Address is used to determine country for members added to this audience. |

### Remove Visitor from Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience Dataset | Select the ADM Audience Dataset. |

#### External User ID

| **Parameter** | **Description** |
| --- | --- |
| External ID | This is an external user identifier defined by data providers. |
| External ID (apply SHA256 hash) | Use this parameter if you’d like the connector to hash the external ID value before sending to Amazon. |

#### User Identifiers

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| First Name (already SHA256 hashed) | Provide a first name, already whitespace trimmed, lowercased, and SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Address (already SHA256 hashed) | Provide an address, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Address (apply SHA256 hash) | Provide a plain text address and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| City (already SHA256 hashed) | Provide a city, already whitespace trimmed, lowercased, and SHA256 hashed. |
| City (apply SHA256 hash) | Provide a plain text city and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| State (already SHA256 hashed) | Provide a state, already whitespace trimmed, lowercased, and SHA256 hashed. |
| State (apply SHA256 hash) | Provide a plain text state and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| Postal Code (already SHA256 hashed) | Provide a postal code, already whitespace trimmed, lowercased, and SHA256 hashed. |
| Postal Code (apply SHA256 hash) | Provide a plain text postal code and the connector will whitespace trim, lowercase, and hash this value using SHA256 hash. |
| MAID | The mobile advertising ID. |
| LiveRamp ID | The LiveRamp ID. |
