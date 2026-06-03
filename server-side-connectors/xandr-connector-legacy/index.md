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

Go to the Connector Marketplace and add a new Segment Connector. Read the [Connector Overview]() article for general instructions on how to add a Connector.

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
| `uuid2` (Required) | &lt;ul&gt;&lt;li&gt;Use the Xandr Cookie Match tag in Tealium iQ to obtain the Xandr `uuid2` value from the visitor&#39;s browser&lt;/li&gt;&lt;/ul&gt;                              |
| `sess`             | &lt;ul&gt;&lt;li&gt;Automatically sets `sess=1` and sends to Xandr along with `uuid2` value in Cookie Header. Map `sess` to `0` to override the default.&lt;/li&gt;&lt;/ul&gt;   |
| `add`              | &lt;ul&gt;&lt;li&gt;Comma-separated segments to add for the user&lt;/li&gt;&lt;/ul&gt;                                                                                           |
| `add_code`         | &lt;ul&gt;&lt;li&gt;Comma-separated list of segment codes to add for the user.&lt;/li&gt;&lt;li&gt;The the `member` parameter is required when using codes.&lt;/li&gt;&lt;/ul&gt;            |
| `remove`           | &lt;ul&gt;&lt;li&gt;Comma-separated segments to remove for the user&lt;/li&gt;&lt;/ul&gt;                                                                                        |
| `remove_code`      | &lt;ul&gt;&lt;li&gt;Comma-separated list of segment codes to remove for the user.&lt;/li&gt;&lt;li&gt;Use the `member` parameter is required when using codes&lt;/li&gt;&lt;/ul&gt;          |
| `member`           | &lt;ul&gt;&lt;li&gt;ID of the member who owns the segment.&lt;/li&gt;&lt;/ul&gt;                                                                                                 |
| `other`            | &lt;ul&gt;&lt;li&gt;A user-defined field with an integer value that is stored for reporting.&lt;/li&gt;&lt;li&gt;Some members use this as the source of the data used.&lt;/li&gt;&lt;/ul&gt; |
| `redir`            | &lt;ul&gt;&lt;li&gt;A redirect URL used to piggyback another pixel&lt;/li&gt;&lt;/ul&gt;                                                                                         |
| `external_uid`     | &lt;ul&gt;&lt;li&gt;A string that corresponds to an external user ID for this user&lt;/li&gt;&lt;/ul&gt;                                                                         |

## Vendor Documentation

* [Segment Service](https://learn.microsoft.com/en-us/xandr/digital-platform-api/segment-service)
