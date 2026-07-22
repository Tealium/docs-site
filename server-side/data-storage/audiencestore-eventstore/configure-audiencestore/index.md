---
title: Configure AudienceStore
description: This article provides information about configuring an AudienceStore connector.
url: https://docs.tealium.com/server-side/data-storage/audiencestore-eventstore/configure-audiencestore/
---

<blockquote>
To have AudienceStore enabled for your account and profile, contact your account manager.
</blockquote>


## Configure an AudienceStore connector

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors](https://docs.tealium.com/about-connectors/).


<blockquote>
Audience names must be fewer than 128 characters in length. Otherwise, DataAccess may trim the audience name and errors may occur.
</blockquote>


## Actions

| Action Name | AudienceStream | EventStream |
| --- | --- | --- |
| Send Visitor Data to Bucket (All Attributes) | ✓ | ✗ |
| Send Visitor Data to Bucket (Selected Attributes) | ✓ | ✗ |

### Send Visitor Data to Bucket (All Attributes)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Include Current Visit Data | Select this checkbox to include all event data for the current visit. |
| Send By Attribute ID | By default, the visitor data JSON property keys are based on AudienceStream attribute names. Select this checkbox to send data keyed by AudienceStream attribute ID. |

#### Batching Options

| **Parameter** | **Description** |
| --- | --- |
| Record Count Maximum | The amount of records for the connector to collect before sending a batch to the audiences folder. Enter a value between 1,000 and 100,000 records. |
| Time To Live | The amount of time for the connector to wait before sending a batch to the audiences folder. Enter a value between 20 and 180 minutes. |
| Payload Size Maximum | The size of the payload for the connector to collect before sending a batch to the audiences folder. Enter a value between 1MB and 100MB. |

### Send Visitor Data to Bucket (Selected Attributes)

#### Parameters

| Parameter | Description |
| --- | --- |
| Visitor Attributes to Store | Map visitor attributes to column header names. |
| Format Data as CSV (JSON if unchecked) |  Select this checkbox to store the data as a CSV file instead of the default JSON file.|

#### Batching Options

| **Parameter** | **Description** |
| --- | --- |
| Record Count Maximum | The amount of records for the connector to collect before sending a batch to the audiences folder. Enter a value between 1,000 and 100,000 records. |
| Time To Live | 	The amount of time for the connector to wait before sending a batch to the audiences folder. Enter a value between 20 and 180 minutes. |
| Payload Size Maximum | The size of the payload for the connector to collect before sending a batch to the audiences folder. Enter a value between 1MB and 100MB. |

For more information, see the [AudienceStore Connector Setup Guide]().

After the AudienceStore connector is configured, the details page for the connector lists the actions, how many times they have been triggered, and their status.


<blockquote>
If AudienceStore is later disabled, the AudienceStore connector will also be disabled. If AudienceStore is enabled again, the AudienceStore connector must be manually enabled.
</blockquote>


After configuring an Audience connector, go to **Store > AudienceStore** to view and download the JSON or CSV files. Each file contains visitor profile data (visitor and visit attributes). You can also use third-party tools to view the files. For more information, see [View files]().