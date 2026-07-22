---
title: The Trade Desk First Party Data connector setup guide
description: This article describes how to set up The Trade Desk First Party Data connector.
url: https://docs.tealium.com/server-side-connectors/the-trade-desk-first-party-data-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Agency Secret Key**: The secret key provided to you by The Trade Desk.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send First Party Advertiser Data | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send First Party Advertiser Data


<blockquote>
Use either the `TDID` parameter or the `UID2` parameter, not both. Setting a value for both `TDID` and `UID2` can cause connector errors.
</blockquote>


#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Data Center Region | (Required) Select the data center geographically closest to where user data comes from. |

#### Advertiser Columns

|**Parameter**| **Description**|
|---| ---|
| Advertiser ID | (Required) Advertiser ID. Available types are `DAID`, `TDID`, `UID2`, `EUID`, `IDL` (`RampID`), `ID5`, and `netID`. Only one ID is required. |
| Device Advertising ID (DAID) | Device Advertising ID (`DAID`) |
| Trade Desk ID (TDID) | Trade Desk ID (`TDID`) |
| Unified ID (UID2 already hashed) | Unified ID (`UID2`). If already hashed, use the **Already SHA256 Hashed** option and provide a value that has been whitespace trimmed, lowercased, and hashed using SHA256. For more information, see [Use a function to generate a UID2](https://docs.tealium.com/use-visitor-function-uid20/). |
| UID2 Token (encrypted advertising token) | The encrypted UID2 advertising token. This token is case-sensitive. |
| Identity Link (IDL) | Identity Link (`IDL`) |

#### Data Columns

|**Parameter**| **Description**|
|---| ---|
| Override TTL in Minutes | Override time to live (`ttl`), in minutes. The maximum `ttl` is 259200 minutes (180 days). |
| Override Timestamp | Override timestamp |
| Data Name | (Required) Data Name |