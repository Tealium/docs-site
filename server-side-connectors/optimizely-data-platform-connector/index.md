---
title: Optimizely Data Platform Connector Setup Guide
description: This article describes how to set up the Optimizely Data Platform connector.
url: https://docs.tealium.com/server-side-connectors/optimizely-data-platform-connector/
---
## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Add User to Audience | ✓ | ✗ |
| Remove User from Audience | ✓ | ✗ |

## Configuration

Navigate to the Connector Marketplace and add a new  connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Username**  
Tealium app username in Optimizely.
* **Password**  
Tealium app password in Optimizely.
* **URL**  
Function URL in Optimizely.

## Actions

The following section lists the supported parameters for each action.

### Add User to Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Tealium User ID | (Required) The Tealium Visitor ID or any unique identifier for the user. For Optimizely web, this should be the ID you are targeting with your web project. |
| Audience Name | (Required) The name for the Audience that the user is being added to. |
| Audience ID | (Required) The unique ID for the audience. |

### Remove User from Audience

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Tealium User ID | (Required) The Tealium Visitor ID or any unique identifier for the user. For Optimizely web, this should be the ID you are targeting with your web project. |
| Audience Name | (Required) The name for the Audience that the user is being added to. |
| Audience ID | (Required) The unique ID for the audience. |
