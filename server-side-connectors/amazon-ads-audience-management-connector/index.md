---
title: Amazon Ads Audience Management Connector Setup Guide
description: This article describes how to set up the Amazon Ads Audience Management connector.
url: https://docs.tealium.com/server-side-connectors/amazon-ads-audience-management-connector/
---
Amazon Ads Audience Management streamlines the upload, management, and use of audiences within Amazon Marketing Cloud (AMC). Use the Amazon Ads Audience connector to create and upload audiences through the Audience Management Service. These audiences become eligible for follow-on actions through Amazon DSP, AMC user interface workflows, or API actions such as AMC rule-based audiences.

 This connector can add visitors to either AMC or DSP audiences. For AMC audiences, you must create an AMC connection during the [**Configuration**]() process. For DSP audiences, you must select an Advertiser ID when you [create the DSP audience](). 

## API information

This connector uses the following vendor API:

* API Name: Amazon Ads API
* API Version: v1.0
* API Endpoint: `https://advertising-api.amazon.com`

## Batch limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 6,000
* Max time since oldest request: 60 minutes
* Max size of requests: 1 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Amazon Ads Account Region**  
  * (Required) Select the region of your Amazon Ads Account.

### Amazon authentication

To authenticate the connector with Amazon:

1. Select your region from the **Amazon Ads Account Region** list.
1. Click **Establish Connection**.
1. In the Amazon **Sign in** dialog, enter your Amazon credentials.

### AMC audience connection

AMC audiences require a connection object to configure an audience. Amazon stores connections in objects that store the mapping of AMC instances and DSP audiences.

To establish an AMC connection with Amazon:

1. Click **Create AMC Connection**. 
1. In the **Create AMC Connection** dialog, select the AMC instance to use for audience uploads under the **AMC Instance** list.
1. (Optional) Select or enter a DSP Advertiser ID in the **DSP Advertiser ID** list to synchronize the audience to DSP.
1. Click **Done** and then click **Create**.

### Country code

The country code is a two-character string in ISO 3166 format that indicates the country from which the data was collected. **Country code** is an optional parameter, but we strongly recommend that you include it when uploading data. A country code added to records overrides the country code added to an audience.

For more information, see [Amazon Ads: Country Code](https://advertising.amazon.com/API/docs/en-us/guides/amazon-marketing-cloud/audiences/audience-management-service#country-code).

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add Visitor to AMC Audience | ✓ | ✓ |
| Add Visitor to DSP Audience | ✓ | ✓ |
| Remove Visitor from Audience | ✓ | ✓ |

Enter a name for the action and select the action type from the list.

The following section describes how to set up parameters and options for each action.

### Add Visitor to AMC Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience ID | The Audience ID to add a visitor to.&lt;ol&gt;&lt;li&gt; To create a new audience, click **Create Audience**.&lt;/li&gt;&lt;li&gt;In the **Create Audience** screen, select an **AMC Connection** from the list.&lt;/li&gt;&lt;li&gt;Enter an **Audience Name**.&lt;/li&gt;&lt;li&gt;Enter an audience description in the **Description** field.&lt;/li&gt;&lt;li&gt;Enter a **Country Code**. This is a 2-character string in the ISO 3166 format that represents where the user data in an audience is collected from. Default value **UNKNOWN** will be applied if not set.&lt;/li&gt;&lt;li&gt;Click **Done**.&lt;/li&gt;&lt;li&gt;Click **Verify Audience ID** to verify the audience ID.&lt;/li&gt;&lt;/ol&gt;Audiences that you create with this connector prepend the prefix `Tealium:` to the audience name before they are sent to Amazon. |
| AMC Connection | (Required) Select an AMC connection.&lt;ul&gt;&lt;li&gt;If needed, create a new connection in the connector configuration screen.&lt;/li&gt;&lt;li&gt;The connection ID must match the one used when the audience was created.&lt;/li&gt;&lt;/ul&gt; |
| External User ID | Select a non-Amazon user ID, such as a Tealium visitor ID attribute, or another internal customer ID that is known to be unique for each visitor. |
| External ID (apply SHA256 hash) | Select this checkbox to apply a SHA256 hash to the External User ID. |
| Country Code | Provide a two-character string in ISO 3166 format that indicates the country from which the data was collected. A country code added to records overrides the country code added to an audience. |

#### User Identifiers

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number that has been already whitespace trimmed and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector whitespace trims and hashes this value using SHA256 hash. |
| First Name (already SHA256 hashed) | Provide a first name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| City (already SHA256 hashed) | Provide a city that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| City (apply SHA256 hash) | Provide a plain text city and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| State (already SHA256 hashed) | Provide a state that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| State (apply SHA256 hash) | Provide a plain text state and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Postal Code (already SHA256 hashed) | Provide a postal code that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Postal Code (apply SHA256 hash) | Provide a plain text postal code and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |

#### Consent

When using the **Add Visitor to AMC Audience** action, the connector sends the value `GRANTED` for the `amznAdStorage` and `amznUserData` parameters. To prevent non-consented visitors from being added to lists, create an audience with rules that check visitor profile consent status. Then use the **Remove Visitor from Audience** action to remove visitors that have not given consent from lists.

### Add Visitor to DSP Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience ID | The Audience ID to add a visitor to.&lt;ol&gt;&lt;li&gt;To create a new audience, click **Create Audience**. &lt;/li&gt;&lt;li&gt;In the **Create Audience** screen, select or enter a **DSP Advertiser** in the list.&lt;/li&gt;&lt;li&gt;Enter an **Audience Name**.&lt;/li&gt;&lt;li&gt;Enter an audience description in the **Description** field.&lt;/li&gt;&lt;li&gt;Enter a **Country Code**. This is a 2-character string in the ISO 3166 format that represents where the user data in an audience is collected from. Default value **UNKNOWN** will be applied if not set.&lt;/li&gt;&lt;li&gt;Click **Done**.&lt;/li&gt;&lt;li&gt;Click **Verify Audience ID** to verify the audience ID.&lt;/li&gt;&lt;/ol&gt; Audiences that you create with this connector prepend the prefix `Tealium:` to the audience name before they are sent to Amazon. |
| External User ID | Select a non-Amazon user ID, such as a Tealium visitor ID attribute, or another internal customer ID that is known to be unique for each visitor. |
| External ID (apply SHA256 hash) | Select this checkbox to apply a SHA256 hash to the External User ID. |

#### User Identifiers

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number that has been already whitespace trimmed and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector whitespace trims and hashes this value using SHA256 hash. |
| First Name (already SHA256 hashed) | Provide a first name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| City (already SHA256 hashed) | Provide a city that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| City (apply SHA256 hash) | Provide a plain text city and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| State (already SHA256 hashed) | Provide a state that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| State (apply SHA256 hash) | Provide a plain text state and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Postal Code (already SHA256 hashed) | Provide a postal code that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Postal Code (apply SHA256 hash) | Provide a plain text postal code and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Country Code | Provide a two-character string in ISO 3166 format that indicates the country from which the data was collected. A country code added to records overrides the country code added to an audience. |

#### Consent

When using the **Add Visitor to DSP Audience** action, the connector sends the value `GRANTED` for the `amznAdStorage` and `amznUserData` parameters. To prevent non-consented visitors from being added to lists, create an audience with rules that check visitor profile consent status. Then use the **Remove Visitor from Audience** action to remove visitors that have not given consent from lists.

### Remove Visitor from Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Audience ID | To use an existing Tealium-created Amazon audience, enter its ID and click **Verify Audience ID** to verify that the audience is correct. You can copy the audience ID created in the **Add to Audience** action configuration. |
| AMC Connection | (Required) Select an AMC connection.&lt;ul&gt;&lt;li&gt;If needed, create a new connection in the connector configuration screen.&lt;/li&gt;&lt;li&gt;The connection ID must match the one used when the audience was created.&lt;/li&gt;&lt;/ul&gt; |
| External User ID | Select a non-Amazon user ID, such as a Tealium visitor ID attribute, or another internal customer ID, known to be unique for each visitor. |

#### User Identifiers

| **Parameter** | **Description** |
| --- | --- |
| Email Address (already SHA256 hashed) | Provide an email address that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Email Address (apply SHA256 hash) | Provide a plain text email address and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Phone Number (already SHA256 hashed) | Provide a phone number that has been already whitespace trimmed and SHA256 hashed. |
| Phone Number (apply SHA256 hash) | Provide a plain text phone number and the connector whitespace trims and hashes this value using SHA256 hash. |
| First Name (already SHA256 hashed) | Provide a first name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| First Name (apply SHA256 hash) | Provide a plain text first name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Last Name (already SHA256 hashed) | Provide a last name that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Last Name (apply SHA256 hash) | Provide a plain text last name and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| City (already SHA256 hashed) | Provide a city that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| City (apply SHA256 hash) | Provide a plain text city and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| State (already SHA256 hashed) | Provide a state that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| State (apply SHA256 hash) | Provide a plain text state and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |
| Postal Code (already SHA256 hashed) | Provide a postal code that has been already whitespace trimmed, lowercased, and SHA256 hashed. |
| Postal Code (apply SHA256 hash) | Provide a plain text postal code and the connector whitespace trims, lowercases, and hashes this value using SHA256 hash. |