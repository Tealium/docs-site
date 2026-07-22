---
title: The Trade Desk Offline Conversion Connector Setup Guide
description: This article describes how to set up The Trade Desk (TheTradeDesk) Offline Conversion connector.
url: https://docs.tealium.com/server-side-connectors/the-trade-desk-offline-conversion-connector/
---
## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).

After adding the connector, configure the following settings:

* **Agency Secret Key**: The secret key provided to you by The Trade Desk.
* **Merchant ID**: (Optional) The ID associated with the merchant account in The Trade Desk. The Trade Desk provides this ID.

## Actions

| **Action Name** | **AudienceStream**| **EventStream**|
|---| ---| ---|
| Send Offline Conversion | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Offline Conversion

#### Batch Limits

This connector uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](https://docs.tealium.com/batched-actions/). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 1000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

#### Data Provider ID

|**Parameter**| **Description**|
|---| ---|
| Data Provider ID | The ID for the data provider in the TTD system. Your Technical Account Manager from The Trade Desk can provide this value. |

#### Data ID

* Map a Trade Desk ID, a device advertising ID, a Unified ID, or an IdentityLink.
* If more than one is mapped, then the first non-empty ID is chosen in the priority of: Trade Desk ID, Device Advertising ID, Unified ID, IdentityLink.
* A Device Advertising ID is represented with either iOS IDFA or Android Advertising ID (AAID).
* Only raw (not hashed) IDFA and raw AAID IDs with a GUID that is 36 characters (including dashes) are accepted.

|**Parameter**| **Description**|
|---| ---|
| The Trade Desk ID (TDID) (`TDID`) | The Trade Desk 36-character GUID (including dashes) for this user. |
| Device Advertising ID (`DAID`) | The raw device ID for this user, sent in 36-character GUID format (including dashes). Use iOS IDFA or Android's AAID. |
| Unified ID (`UID2`) | The raw UID2 value, also known as UID2. This value is case-sensitive. Raw UID2s are generated and managed using UID2 APIs. |
| UID2 Token (encrypted advertising token) | The encrypted UID2 advertising token. This token is case-sensitive. |
| IdentityLink (`IDL`) | The 49-character or 70-character RampID (previously known as IdentityLink). This must be a RampID from LiveRamp that is mapped specifically for The Trade Desk. |

#### Item Data

|**Parameter**| **Description**|
|---| ---|
| Tracking Tag ID | (Required) The Tracking tag ID created using the Tracking tag APIs. Example: `abc1234` |
| Conversion Timestamp | (Required) Conversion date and time in UTC. The time the offline conversion happened. Example: `2019-02-07T13:25:00Z` |
| Impression ID | The raw (not hashed) GUID that is 36 characters long, including dashes. |
| Monetary value |  Monetary value. Example: `0.02` |
| Monetary currency |  Monetary value currency. Example: `USD` |
| Country |  Country. Example: `United States`. |
| Region |  Region. Example: `New York`. |
| Metro Area |  Metro area. Example: `501` |
| City |  City. Example: `Brooklyn`.|
| Postal Code | The postal code. Example: `'11223'`. |
| Event Name | The type of event is defined by the partner platform. For more information, see [The Trade Desk: Event Mapping](https://partner.thetradedesk.com/v3/portal/data/doc/post-providerapi-offlineconversion#event-mapping).  |
| Order ID | The unique identifier for a transaction or conversion event, with a maximum length of 64 characters. |

#### Additional Data

|**Parameter**| **Description**|
|---| ---|
| `TD1 - TD10` |  Optional reporting fields used for category or other organization, with a maximum length of 64 characters.|

#### Line items

The properties that contain merchant product catalog line item information. These mappings accept array attributes.

|**Parameter**| **Description**|
|---| ---|
| Item Code | The item identifier (such as SKU). |
| Item Name | The name associated with the item code, with a maximum length of 150 characters. |
| Item Quantity |  The number of items in the order for the item code. |
| Item Price | The unit price of the item. |
| Item Category | The item category ID. |
