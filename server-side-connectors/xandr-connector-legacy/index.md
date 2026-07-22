---
title: Xandr (formerly AppNexus) Connector Setup Guide for AudienceStream
description: This article describes how to set up the Xandr (formerly AppNexus) connector.
url: https://docs.tealium.com/server-side-connectors/xandr-connector-legacy/
---
## Requirements

* Xandr Account

## Supported Actions

| **Action Name**                    | **Trigger on Audience** | **Trigger on Streams** |
|:-----------------------------------|:------------------------|:-----------------------|
| Add User to or Remove from Segment | ✓                       | ✓                      |

## Configure Settings

Go to the Connector Marketplace and add a new Segment Connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a Connector.

To configure your vendor, follow these steps:

1. In the **Configure** tab, enter a title for the Connector instance.
1. Provide additional notes about your implementation.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you will set up actions and trigger them.

This section describes how to set up parameters and options for each action.

### Action - Add User to or Remove from Segment

#### Parameters

* **General Mappings**
  * (Required) Map your Attribute(s) to the required event fields.
  * Select the field of choice from the **To** drop-down list or enter a custom value.

#### Options - General Mappings

| **Option**         | **Description**                                                                                                                                          |
|:-------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------|
| `uuid2` (Required) | <ul><li>Use the Xandr Cookie Match tag in Tealium iQ to obtain the Xandr `uuid2` value from the visitor's browser</li></ul>                              |
| `sess`             | <ul><li>Automatically sets `sess=1` and sends to Xandr along with `uuid2` value in Cookie Header. Map `sess` to `0` to override the default.</li></ul>   |
| `add`              | <ul><li>Comma-separated segments to add for the user</li></ul>                                                                                           |
| `add_code`         | <ul><li>Comma-separated list of segment codes to add for the user.</li><li>The the `member` parameter is required when using codes.</li></ul>            |
| `remove`           | <ul><li>Comma-separated segments to remove for the user</li></ul>                                                                                        |
| `remove_code`      | <ul><li>Comma-separated list of segment codes to remove for the user.</li><li>Use the `member` parameter is required when using codes</li></ul>          |
| `member`           | <ul><li>ID of the member who owns the segment.</li></ul>                                                                                                 |
| `other`            | <ul><li>A user-defined field with an integer value that is stored for reporting.</li><li>Some members use this as the source of the data used.</li></ul> |
| `redir`            | <ul><li>A redirect URL used to piggyback another pixel</li></ul>                                                                                         |
| `external_uid`     | <ul><li>A string that corresponds to an external user ID for this user</li></ul>                                                                         |

## Vendor Documentation

* [Segment Service](https://learn.microsoft.com/en-us/xandr/digital-platform-api/segment-service)
