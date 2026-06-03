---
title: AudienceStore Connector Setup Guide
description: With the AudienceStore Connector, you can send visitor profile data to Tealium's Amazon S3 bucket. A visitor profile contains data pertinent to the visitor and their visit (excluding events), typically captured by the Tealium Collect Tag. Rather than exporting one visitor profile at a time, the AudienceStore connector selects visitor profiles that share common behaviors to send to AudienceStore.
url: https://docs.tealium.com/server-side-connectors/audiencestore-connector/
---

## Requirements

* AudienceStore must be enabled for your account. Contact your Tealium Account Manager for more information.
* Your account must have active audiences. For more information, see [Building an Audience]().
* Audience names must be fewer than 128 characters in length. Otherwise, DataAccess may trim the audience name and errors may occur.

## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Visitor Data to Bucket (All Attributes) | ✓ | ✗ |
| Send Visitor Data to Bucket (Selected Attributes) | ✓ | ✗ |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

The AudienceStore connector has two actions that allow you to specify the data to export and when to trigger the export. Data is compressed in log files and uploaded to the `audiences` folder in the S3 bucket. By default, data is stored as JSON key-value pairs. In S3, you can download the data and analyze it using the business intelligence tool of your choice.

The connector sends data when the batch reaches 100 MB in size or after 1 hour passes, whichever happens first. You can change the default behavior with the **Record Count Maximum**, **Time to Live**, and **Payload Size Maximum** parameters.

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action - Send Visitor Data to Bucket (All Attributes)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Include Current Visit Data | All event data for the most recent visit by the visitor is included. |
| Send By Attribute ID | By default, the Visitor Data JSON property keys are based on AudienceStream attribute names. Select this option to send data keyed by AudienceStream attribute ID. |
| Record Count Maximum | The amount of records for the connector to collect before sending a batch to the `audiences` folder. Enter a value between 1,000 and 100,000 records. |
| Time to Live | The amount of time for the connector to wait before sending a batch to the `audiences` folder. Enter a value between 20 and 180 minutes. |
| Payload Size Maximum | The size of the payload for the connector to collect before sending a batch to the `audiences` folder. Enter a value between 1MB and 100MB. |

### Action - Send Visitor Data to Bucket (Selected Attributes)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Visitor Attributes to Store | Map visitor attributes to column header names. |
| Format Data as CSV (JSON if unchecked) | Store data in CSV format instead of JSON. |
| Record Count Maximum | The amount of records for the connector to collect before sending a batch to the `audiences` folder. Enter a value between 1,000 and 100,000 records. |
| Time to Live | The amount of time for the connector to wait before sending a batch to the `audiences` folder. Enter a value between 20 and 180 minutes. |
| Payload Size Maximum | The size of the payload for the connector to collect before sending a batch to the `audiences` folder. Enter a value between 1MB and 100MB. |

    