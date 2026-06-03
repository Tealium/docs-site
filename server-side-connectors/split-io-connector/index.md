---
title: Split.io Connector Setup Guide
description: This article describes how to set up the Split connector.
url: https://docs.tealium.com/server-side-connectors/split-io-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Split API
* API Version: v2
* API Endpoint: `https://api.split.io`
* Documentation: [Split API](https://docs.split.io/reference/introduction)

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Admin API Key**  
  * The admin API key, required for adding and removing users from segments. For more information, visit [Split.io: API keys](https://help.split.io/hc/en-us/articles/360019916211-API-keys).
* **SDK API Key**  
  * The SDK API key, required for the Send Event action. For more information, visit [Split.io: API keys](https://help.split.io/hc/en-us/articles/360019916211-API-keys).
* **Workspace ID**  
  * (Required) The ID (`wsId`) of the project or workspace for your environment.
* **Environment ID**  
  * The environment used for this connection.

### Create Segment

To create a segment, do the following:

1. Click **Create Segment**.
1. Enter a **Name** for the segment.
1. Enter a **Description** for the segment.
1. Select the **Traffic Type ID**.
1. Click **Create**.
1. Click **Done**.

### Create Traffic Type

To create a traffic type, do the following:

1. Click **Create Traffic Type**.
1. Enter a **Name** for the traffic type.
1. Click **Create**.
1. Click **Done**.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add user to segment | ✓ | ✗ |
| Add user to segment (Batch) | ✓ | ✗ |
| Remove user from segment | ✓ | ✗ |
| Remove user from segment (Batch) | ✓ | ✗ |
| Send event | ✗ | ✓ |
| Send event (Batch) | ✗ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Batch Limits

This action uses batched requests to support high-volume data transfers to the vendor. For more information, see [Batched Actions](). Requests are queued until one of the following thresholds is met or the profile is published:

* Max number of requests: 10,000
* Max time since oldest request: 10 minutes
* Max size of requests: 1 MB

### Add user to segment

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Segment | Choose the segment you would like to dynamically add users to. |
| User ID | (Required) The user ID to include in the segment. |
| Comments | A comment for the update. |

### Add user to segment (Batch)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Segment | Choose the segment you would like to dynamically add users to. |
| User ID | (Required) The user ID to include in the segment. |

### Remove user from segment

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Segment | Choose the segment you would like to dynamically remove users from. |
| User ID | (Required) The user ID to remove from the segment. |
| Comments | A comment for the update. |

### Remove user from segment (Batch)

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Segment | Choose the segment you would like to dynamically remove users from. |
| User ID | (Required) The user ID to remove from the segment. |