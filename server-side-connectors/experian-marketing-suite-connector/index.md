---
title: Experian Marketing Suite Connector Setup Guide
description: This article describes how to configure Experian Marketing Suite in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/experian-marketing-suite-connector/
---Experian Marketing Suite cross-channel marketing platform empowers brands to manage and execute all customer interactions within a single system, in real-time—removing the need for multiple, disparate platforms and individual channel vendors. 

## Requirements

* Experian Marketing Services Account
* Consumer Key (found on the API ACCESS screen)
* Consumer Secret (found on the API ACCESS screen)

## Supported actions

|**Action Name**| **Trigger on Audience**| **Trigger on Streams**|
|---| ---| ---|
|Insert Data to Table| ✓| ✓|

## Configure settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors]() article.

To configure your vendor, follow these steps:

1. In the **Configure** tab, provide a title for the connector instance.
1. (Optional) Enter the Client ID that you received from Experian.
1. Enter the Consumer Key that you received from Experian&#39;s API ACCESS screen.
1. Enter the Consumer Secret that you received from Experian&#39;s API ACCESS screen.
1. Provide additional notes about your implementation.
1. Click **Test Connection** to verify the keys.

## Action settings - parameters and options

Click **Next** or go to the **Actions** tab. It&#39;s where you&#39;ll set up actions and trigger them.

This section describes how to set up parameters and options for each action.

### Action: Insert Data to Table

#### Parameters

| Parameter | Description |
|---|---|
| Table | (Required) Specify the table to update. |
| Table Entry Data | (Required) Match values to columns in the table. |
| Upward Relations | Link this table entry to other tables. |
| Date Formats | Format incoming data using a specific format. |
| Import Options | Specify additional options for data inserts. |

#### Options: Upward Relations

Upward relations allow for linking table data together. For example, there are 2 tables, `order_item` and `order`:

|**order_item**| **order**|
|---| ---|
|item_id| id|
|quantity| date|
|order|

**Order_item**&#39;s `item_id` and `quantity` will be mapped in the Table Entry Data section. **Order_item**&#39;s `order` and **order**&#39;s `item_id`,`quantity` will need to be mapped in the Upward Relations Section. The resulting mapping will look like:

|**Attribute**| **Path**|
|---| ---|
|event_order_id| `order/id`|
|event_timestamp| `order/date`|

Where &#34;eventorder_id&#34; and &#34;event_timestamp&#34; are single entry event/audience array attributes, allowing for several Upward Relations to be specified.

#### Options: Date Formats

Specify date formats per table field (also applies to Upward Relation paths). The format must follow [Java&#39;s template standard](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html).

Some popular formats include:

|**Format**| **Result**|
|---| ---|
|MM/DD/YYYY| 05/25/1977|
|MM/dd/yyyy hh:mm a| 05/25/1977 07:15 PM|
|yyyy/MM/dd HH:mm:ss| 1977/05/25 19:15:37|
|yyyy/MM/dd HH:mm:ss x| 1977/05/25 19:15:37 &#43;0000|

Custom/incoming dates are assumed to be milliseconds since January 1, 1970 UTC (epoch).

#### Options: Import Options

|**Option**| **Values**| **Description**|
|---| ---| ---|
|Do Not Update Existing| `true` or `false`| `true` to insert a new record instead of updating a matching record|

A CustomValue can be specified for import options not listed above.