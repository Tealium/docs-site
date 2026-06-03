---
title: The Trade Desk Third-Party Data Connector Setup Guide
description: This article describes how to set up The Trade Desk Third Party Data connector.
url: https://docs.tealium.com/server-side-connectors/the-trade-desk-third-party-data-connector/
---
This connector is not currently available in the Connector Marketplace. Using The Trade Desk Third-Party Data connector requires support from both Tealium and The Trade Desk account managers. To use this connector, contact your Tealium account manager.

## API information

This connector uses the following vendor API:

* API Name: The Trade Desk API
* API Version: v3.0
* API Endpoint: `https://bulk-data.adsrvr.org`
  * Data Rate Endpoint: `POST /datarate/batch`
  * Third-Party Endpoint: `POST /data/thirdparty`
* Documentation: [The Trade Desk API](https://partner.thetradedesk.com/v3/portal/data/doc/post-data-thirdparty)

## Batch limits
  
This connector uses batched requests to support high-volume data transfers to the vendor. Parallel processing may result in events reaching the vendor out of sequence. Add a sequence value to events if ordering is important. For more information, see [Batched actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10000
* Max time since oldest request: 30 minutes
* Max size of requests: 2 MB

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Secret Key**: (Required) The secret key.
* **API Base URL**: (Required) Select your API base URL.

## Admin configuration

### Generate authentication token

You must generate an authentication token with a valid username and password before the admin tasks can be performed. Authentication only applies to the admin tasks and is not required for the connector to work.

* **Login**: (Required) Enter your login.
* **Password**: (Required) Enter your password.

### Create taxonomy segment

For more information, see [The Trade Desk Partner Portal: Third-Party Data Taxonomy Design](https://partner.thetradedesk.com/v3/portal/data/doc/DataTaxonomyDesign#top).

| Parameter                | Description|
|--------------------------|----------------------------|
| Provider ID          | (Required) The unique ID for your provider account, which your Account Manager provided to you.|
| Provider Element ID  | (Required) The unique ID assigned to the segment when the taxonomy was designed. The ID must be 512 characters long or less. This value cannot be changed after you create it.|
| Parent Element ID    | (Required) The provider element ID value from the parent segment in the taxonomy. This parameter establishes the hierarchical structure of your taxonomy. This value cannot be changed after you create it. All data providers use the `ROOT` base element of the taxonomy.|
| Display Name         | (Required) The name for the segment that buyers see in the DMP user interface. The display name must be 256 characters long or less, but we recommend 50 characters or less for readability, especially for lower-level child elements with longer full paths. Do not include tabs or special characters such as `&#39;`, `&#34;`, or `^`.|
| Buyable              | (Required) Set to `true` to make the segment visible and available for buyers in the DMP. For container elements, set this property value to `false`, since they are used only for organizing child elements and assigning rates. If you change the property value to `false` for a buyable segment, any customers that currently have the segment in their audience can use it until their campaign ends.|
| Description          | (Optional) A description of the data segment, displayed to customers in the DMP. The description must be 4,000 characters long or less, but we recommend 256 characters or less for readability.|
| Is Direct IP Targeting | (Optional) If `true`, the `TargetingData` used or created is type `16` (`DirectIpTargeting`) instead of the default `7` (`ThirdPartyData`).|

### Assign rate to segment  

| Parameter                     | Description |
|-------------------------------|-------------|
| Provider ID               | (Required) The unique ID for your provider account, which your Account Manager provided to you. |
| Provider Element ID        | (Required) A unique ID that identifies this data element in the system. |
| Brand ID                  | (Required) The unique ID that identifies a provider-managed brand. |
| Rate Level                | (Required) The rate level for the third-party data. To request access, contact your Technical Account Manager.&lt;br&gt;`Partner`: For specific partners and their advertisers.&lt;br&gt;`Advertiser`: For specific advertisers. Note that this rate level requires additional permissions. |
| Partner ID                | (Required) The platform ID of the partner eligible to access data segments at this rate in a custom taxonomy. |
| Advertiser ID             | (Required) The platform ID of the advertiser eligible to access data segments at this rate in a custom taxonomy. |
| Rate Type                 | (Required) The data rate type for the segment. All system-level data rates for syndicated taxonomies must be assigned as hybrid rates, which use a percentage of media cost with a maximum CPM (cost per thousand) cap. This means that you must set this property to `Hybrid` and provide values for both `CPMRate` and `PercentOfMediaCostRate` properties. While custom taxonomies can use any data rate type, hybrid rates are strongly recommended. |
| CPM Rate Amount           | (Required) The CPM rate amount. |
| CPM Rate Currency Code    | (Required) The CPM rate currency code. |
| Percent of Media Cost Rate| (Optional) A percentage of media cost to be used in conjunction with the `CPMRate` cap for the hybrid data rate (selected in **Rate Type**). Enter the percentage as a decimal. |

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Upload 3rd Party Data | ✓ | ✗ |
| Delete Third Party Data | ✓ | ✗ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Upload 3rd Party Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Data Provider ID | (Required) The provider ID supplied by your Technical Account Manager. |

#### IDs

At least one ID parameter is required. Multiple IDs may be included in the same request. The Trade Desk supports the following IDs:

| Parameter | Description |
| --- | --- |
| TDID | The Trade Desk 36-character GUID (including dashes) for this user. |
| DAID | The raw device ID for this user sent in 36-character GUID format (including dashes). Use iOS IDFA or Android&#39;s AAID. |
| UID2Token (already SHA256 hashed) | The user&#39;s Unified ID 2.0, already SHA256 hashed. |
| UID2Token (apply SHA256 hash) | The user&#39;s Unified ID 2.0, to which a SHA256 hash is applied. |
| UID2 | The user&#39;s Unified ID 2.0 as a 44-character base64-encoded SHA-256 string. For more information, see [The Trade Desk Partner Portal: PII Normalization and Hash Encoding](https://partner.thetradedesk.com/v3/portal/data/doc/DataPiiNormalization) and [Unified IDs](https://partner.thetradedesk.com/v3/portal/data/doc/UnifiedIDs). |
| EUIDToken (already SHA256 hashed) | The user&#39;s European Unified ID, already SHA256 hashed. |
| EUIDToken (apply SHA256 hash) | The user&#39;s European Unified ID, to which a SHA256 hash is applied |
| EUID | The user&#39;s European Unified ID as a 44-character base64-encoded SHA-256 string. For more information, see [The Trade Desk Partner Portal: PII Normalization and Hash Encoding](https://partner.thetradedesk.com/v3/portal/data/doc/DataPiiNormalization). EUID offers user transparency and privacy controls designed to meet market requirements in Europe and the UK, and it requires the same normalization and encoding of email addresses as UID2. For more information, see [The Trade Desk Partner Portal: Unified IDs](https://partner.thetradedesk.com/v3/portal/data/doc/UnifiedIDs). |
| IDL | The 49-character or 70-character RampID (previously known as IdentityLink). This value must be a RampID from LiveRamp that is mapped specifically for The Trade Desk. For more information about mapping a RampID, see [LiveRamp: LiveRamp&#39;s Sidecar](https://sidecar.readme.io/docs/getting-started). |

#### Data

| Parameter | Description |
| --- | --- |
| Name | (Required) The segment name. Maximum 128 characters. |
| TTL in Minutes | (Required) Time to live (TTL) is the amount of time (in minutes) during which this user is to remain active relative to the `TimeStampUtc` value. When the TTL has expired, the user is no longer used for targeting. The maximum TTL is 259200 minutes (180 days). |
| Timestamp | The timestamp of when a user is eligible for a segment. If not specified, the timestamp is assigned based on the time when the data is processed. This timestamp is used to determine a user&#39;s recency for targeting and bid adjustments. |

### Delete Third Party Data

#### Parameters

| Parameter | Description |
| --- | --- |
| Data Provider ID | Required. The provider ID supplied to you by your Technical Account Manager. |
| Request Type | &lt;ul&gt;&lt;li&gt;**Opt-out**: The Trade Desk will opt out the ID from your data segments by setting its TTL value to `0`, thereby limiting its targeting in your campaigns.&lt;/li&gt;&lt;li&gt;**Delete**: The Trade Desk deletes the ID from your datasets, including data segments and `REDS` feeds. |

#### IDs

At least one ID parameter is required. Multiple IDs may be included in the same request. The Trade Desk supports the following IDs:

| Parameter | Description |
| --- | --- |
| TDID | The Trade Desk 36-character GUID (including dashes) for this user. |
| DAID | The raw device ID for this user sent in 36-character GUID format (including dashes). Use iOS IDFA or Android AAID. |
| UID2Token (already SHA256 hashed) | The user&#39;s Unified ID 2.0, already SHA256 hashed. |
| UID2Token (apply SHA256 hash) | The user&#39;s Unified ID 2.0, to which a SHA256 hash is applied. |
| UID2 | The user&#39;s Unified ID 2.0 as a 44-character base64-encoded SHA-256 string. For more information, see [The Trade Desk Partner Portal: PII Normalization and Hash Encoding](https://partner.thetradedesk.com/v3/portal/data/doc/DataPiiNormalization) and [Unified IDs](https://partner.thetradedesk.com/v3/portal/data/doc/UnifiedIDs). |
| EUIDToken (already SHA256 hashed) | The user&#39;s European Unified ID, already SHA256 hashed. |
| EUIDToken (apply SHA256 hash) | The user&#39;s European Unified ID, to which a SHA256 hash is applied |
| EUID | The user&#39;s European Unified ID as a 44-character base64-encoded SHA-256 string. For more information, see [The Trade Desk Partner Portal: PII Normalization and Hash Encoding](https://partner.thetradedesk.com/v3/portal/data/doc/DataPiiNormalization). EUID offers user transparency and privacy controls designed to meet market requirements in Europe and the UK, and it requires the same normalization and encoding of email addresses as UID2. For more information, see [The Trade Desk Partner Portal: Unified IDs](https://partner.thetradedesk.com/v3/portal/data/doc/UnifiedIDs). |
| RampID | The 49-character or 70-character RampID (previously known as IdentityLink). This must be a RampID from LiveRamp that is mapped specifically for The Trade Desk. For more information, see [LiveRamp: LiveRamp&#39;s Sidecar](https://sidecar.readme.io/docs/getting-started). |