---
title: Criteo Connector Setup Guide
description: This article describes how to set up the Criteo connector.
url: https://docs.tealium.com/server-side-connectors/criteo-connector/
---
## Connector Actions

|**Action Name**| **AudienceStream**| **EventStream**|
| --- | --- | --- |
| Send Event | ✓ | ✓ |
| Send Event (First-party ID) | ✓ | ✓ |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Client Account ID**  
(Required) This is the **Client ID** in Criteo.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Automatic Deduplication

Use the Automatic Deduplication action to send a unique identifier generated from your [Criteo OneTag tag](https://docs.tealium.com/criteo-onetag-tag/) with the event dataset. Ensure that you have enabled **Generate Page View ID** in your Criteo OneTag tag configuration. The event attribute uses the following naming convention:

`criteo_page_view_id_<TAG_UID>`

For example, a page view event from a tag with UID of `171` would send the following attribute value:

```nohl
criteo_page_view_id_171
```

You can find your tag's UID in the Tealium iQ **Tags** table or the tag details screen:

![](https://docs.tealium.com/images/server-side-connectors/criteo-onetag-uid.png)

To configure automatic deduplication, in the **Automatic Deduplication** section, select **Add Mapping**. In the mapping, provide the Criteo OneTag tag ID and map it to the **Tealium iQ Tag ID**. 

After you configure automatic deduplication, Tealium automatically looks for the Criteo page view ID being sent from Tealium iQ and adds it to the event payload for deduplication.

### Action - Send Event

#### Event Type

|**Parameter**| **Description**|
|---| ---|
|Event Type| The standard web, travel, or store event to send. For more information, see [Criteo Server to Server - Event Payloads](https://guides.criteotilt.com/onetag/s2s/#event-payloads).|

#### Standard Parameters

Criteo highly recommends mapping IP Address, Full URL, and User Agent for most accurate data collection.

|**Parameter**| **Description**|
|---| ---|
|Account| The partner ID of the account you are sending the data to. It can be filled on the connector configuration screen or on the action screen. The value on the action screen has higher priority than on the connector configuration screen.|
|Site Type| The device type (or site version) used for browsing. Available values are `d` (for Desktop), `t` (for Tablet), `m` (for Mobile). Default value is `d`.|
|Full URL| The full URL where the event is triggered.|
|Previous URL| The previous URL where the event is triggered.|
|IP| The IP address of the user.|
|User Agent| The user agent string from the users browser.|
|Retailer Visitor ID|  A unique ID that is consistent across multiple sessions for an unauthenticated user. For example, First-party cookie ID.|

#### User Identifiers

Criteo recommends mapping both a Mapped User ID and email where possible. Providing an email address allows for cross-device attribution when available and may enable addressing events without a Mapped User ID.

|**Parameter**| **Description**|
|---| ---|
|GUM ID| The Criteo salted user ID (GUM ID) returned by the GUM call. For more information, see [Criteo Server to Server - Criteo GUM Call](https://guides.criteotilt.com/onetag/s2s/#criteo-gum-call).|
|GAID| Google's advertising identifier.|
|IDFA| Apple's identifier for Advertisers unique identifier.|
|Email Raw| The user's raw email address. The first non-empty email parameter is used. |
|Email MD5 (apply MD5 hash)| The user's unhashed email address.|
|Email MD5 (already MD5 hashed)| The user's email address hashed with MD5.|
|Email SHA256 (apply SHA256 hash)| The user's unhashed email address.|
|Email SHA256 (already SHA256 hashed)| The user's email address hashed with SHA256.|
|Email SHA256 MD5 (apply SHA256 MD5 hash)| The user's unhashed email address.|
|Email SHA256 MD5 (already SHA256 MD5 hashed)| The user's email address hashed with MD5 and SHA256.|

#### Event Parameters

|**Parameter**| **Description**|
|---| ---|
| ID | The order ID used to identify a given order. |
| Item (Top 3 Products) | An array of the top 3 products on the listing page a user visited. |
| Item (Product Id) | The product ID of the product the user looked at. |
| Items Id (String or Array) | The product ID, the unit price, the quantity of the products in the cart. Values could be string with comma (","), separation, or array. |
| Items Price (String or Array) | The unit price of the products in the cart. Values can be comma-separated strings, or an array. |
| Items Quantity (String or Array) | The quantity of the products in the cart. Values can be comma-separated strings, or an array. |
| Items Price (Tail) | Tally or a string attribute containing a valid JSON map of item ID(s) to number values. For example, `{"PID1":1.99,"PID2":3.99}`. For each tally configured, ensure the item ID is used as the tally key and the property value as the tally value. |
| Items Quantity (Tail) | Tally or a string attribute containing a valid JSON map of item ID(s) to number values. For example, `{"PID1":1.99,"PID2":3.99}`. For each tally configured, ensure the item ID is used as the tally key and the property value as the tally value. |
| Currency | The ISO code of the currency being passed to the tags. |
| Timestamp | The timestamp the event happened for the user in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If no timestamp is provided, the current timestamp is used. |
| Checkin Date | The check-in date the user submitted in format `YYYY-MM-DD`. |
| Checkout Date | The check-out date the user submitted in format `YYYY-MM-DD`. |
| NBRA | The number of adults in the search. |
| NBRC | The number of children in the search. |
| NBRI | The number of infants in the search. |
| NBRR | The number of rooms in the search. |
| Store Id | The store ID as passed in the feed. |
| Store Ids | The store ID as passed in the feed. This is an array for stores with the product available. |
| DD | Populate this with a **1** if you want the sale to be attributed to Criteo or a **0** if you do not. The sale will be attributed to Criteo only if the order should have been attributed to Criteo through normal attribution. |
| Category | The category of the listing page. |
| Keyword | The searched keyword of the search listing page. |

#### Automatic Deduplication

When the Tealium iQ tag UID is provided, we will automatically look for the Event ID value that is sent from Tealium iQ.

### Send Event (First-party ID)

#### Event Type

|**Parameter**| **Description**|
|---| ---|
|Event Type| The standard web, travel, or store event to send. For more information, see [Criteo Server to Server - Event Payloads](https://guides.criteotilt.com/onetag/s2s/#event-payloads).|

#### First-party Parameters

| **Parameter** | **Description** |
| --- | --- |
| First-party ID | (Required) A first-party identifier for the visitor. Map the same attribute and value used in the Criteo Server to Server Identification Service tag. |
| First-party Domain |  (Required) The domain of the partner. For example: `yourdomain.com`. This parameter is used by Criteo to avoid ID collisions on two different websites. |
| First-party Name |  (Required) The partner name. |

#### Standard Parameters

Criteo highly recommends mapping IP Address, Full URL, and User Agent for most accurate data collection.

|**Parameter**| **Description**|
|---| ---|
|Account| The partner ID of the account you are sending the data to. It can be filled on the connector configuration screen or on the action screen. The value on the action screen has higher priority than on the connector configuration screen.|
|Site Type| The device type (or site version) used for browsing. Available values are `d` (for Desktop), `t` (for Tablet), `m` (for Mobile). Default value is `d`.|
|Full URL| The full URL where the event is triggered.|
|Previous URL| The previous URL where the event is triggered.|
|IP| The IP address of the user.|
|User Agent| The user agent string from the users browser.|
|Retailer Visitor ID|  A unique ID that is consistent across multiple sessions for an unauthenticated user. For example, First-party cookie ID.|

#### User Identifiers

Criteo recommends mapping both a Mapped User ID and email where possible. Providing an email address allows for cross-device attribution when available and may enable addressing events without a Mapped User ID.

|**Parameter**| **Description**|
|---| ---|
|GUM ID| The Criteo salted user ID (GUM ID) returned by the GUM call. For more information, see [Criteo Server to Server - Criteo GUM Call](https://guides.criteotilt.com/onetag/s2s/#criteo-gum-call).|
|GAID| Google's advertising identifier.|
|IDFA| Apple's identifier for Advertisers unique identifier.|
|Email Raw| The user's raw email address. The first non-empty email parameter is used. |
|Email MD5 (apply MD5 hash)| The user's unhashed email address.|
|Email MD5 (already MD5 hashed)| The user's email address hashed with MD5.|
|Email SHA256 (apply SHA256 hash)| The user's unhashed email address.|
|Email SHA256 (already SHA256 hashed)| The user's email address hashed with SHA256.|
|Email SHA256 MD5 (apply SHA256 MD5 hash)| The user's unhashed email address.|
|Email SHA256 MD5 (already SHA256 MD5 hashed)| The user's email address hashed with MD5 and SHA256.|

#### Event Parameters

|**Parameter**| **Description**|
|---| ---|
| ID | The order ID used to identify a given order. |
| Item (Top 3 Products) | An array of the top 3 products on the listing page a user visited. |
| Item (Product Id) | The product ID of the product the user looked at. |
| Items Id (String or Array) | The product ID, the unit price, the quantity of the products in the cart. Values can be comma-separated strings, or an array. |
| Items Price (String or Array) | The unit price of the products in the cart. Values can be comma-separated strings, or an array. |
| Items Quantity (String or Array) | The quantity of the products in the cart. Values can be comma-separated strings, or an array. |
| Items Price (Tail) | Tally or a string attribute containing a valid JSON map of item ID(s) to number values. For example, `{"PID1":1.99,"PID2":3.99}`. For each tally configured, ensure the item ID is used as the tally key and the property value as the tally value. |
| Items Quantity (Tail) | Tally or a string attribute containing a valid JSON map of item ID(s) to number values. For example, `{"PID1":1.99,"PID2":3.99}`. For each tally configured, ensure the item ID is used as the tally key and the property value as the tally value. |
| Currency | The ISO code of the currency being passed to the tags. |
| Timestamp | The timestamp of the user event in ISO 8601 UTC format `YYYY-MM-DDThh:mm:ssZ`. If no timestamp is provided, the current timestamp is used. |
| Checkin Date | The check-in date the user submitted in format `YYYY-MM-DD`. |
| Checkout Date | The check-out date the user submitted in format `YYYY-MM-DD`. |
| NBRA | The number of adults in the search. |
| NBRC | The number of children in the search. |
| NBRI | The number of infants in the search. |
| NBRR | The number of rooms in the search. |
| Store Id | The store ID as passed in the feed. |
| Store Ids | The store ID as passed in the feed. This is an array for stores with the product available. |
| DD | Populate this with a **1** if you want the sale to be attributed to Criteo or a **0** if you do not. The sale will be attributed to Criteo only if the order should have been attributed to Criteo through normal attribution. |
| Category | The category of the listing page. |
| Keyword | The searched keyword of the search listing page. |