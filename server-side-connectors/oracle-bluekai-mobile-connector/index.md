---
title: Oracle BlueKai Mobile Connector Setup Guide
description: This article describes how to set up the Oracle BlueKai Mobile connector.
url: https://docs.tealium.com/server-side-connectors/oracle-bluekai-mobile-connector/
---
## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| Send Pixel      | ✓                  | ✓               |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Site ID**: Provided by your BlueKai container, associating your desktop and mobile sites in the BlueKai platform.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Pixel

#### Parameters

| **Parameter**   | **Description**                                                                                                                                                                                                                                                                 |
|:----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| User Agent      | <ul><li>If provided, the value will be used in `User-Agent` header</li><li>If not specified, defaults to `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36`</li></ul>                                        |
| User ID Type    | <ul><li>Type of user identifier</li><li>See [ID Swapping](https://docs.oracle.com/en/cloud/saas/data-cloud/dsmkt/integrating-oracle-bluekai-platform.html#GUID-A8856438-EF6A-4BCE-A2E4-B4CE725B0E61) guidelines on BlueKai website</li></ul>                                    |
| User ID Value   | <ul><li>Value of user identifier</li></ul>                                                                                                                                                                                                                                      |
| ID Hashing      | <ul><li>Check to hash the user ID</li><li>Email and phone number must be hashed</li></ul>                                                                                                                                                                                       |
| Hash Type       | <ul><li>Choose hashing algorithm</li><li>Email address and phone number must be hashed with either MD5 or SHA256</li><li>ANDROIDID must be hashed with either with MD5 or SHA1</li><li>ADID and IDFA must be hashed with either with MD5 or SHA1 or not hashed at all</li></ul> |
| Phints          | <ul><li>Provide phints as key-value pairs</li><li>Values on the left will be assigned to the keys on the right</li></ul>                                                                                                                                                        |
| Additional Data | <ul><li>Provide additional data as key-value pairs</li><li>No additional processing will be used for this data</li></ul>                                                                                                                                                        |
