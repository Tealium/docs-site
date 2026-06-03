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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Site ID**: Provided by your BlueKai container, associating your desktop and mobile sites in the BlueKai platform.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Pixel

#### Parameters

| **Parameter**   | **Description**                                                                                                                                                                                                                                                                 |
|:----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| User Agent      | &lt;ul&gt;&lt;li&gt;If provided, the value will be used in `User-Agent` header&lt;/li&gt;&lt;li&gt;If not specified, defaults to `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Safari/537.36`&lt;/li&gt;&lt;/ul&gt;                                        |
| User ID Type    | &lt;ul&gt;&lt;li&gt;Type of user identifier&lt;/li&gt;&lt;li&gt;See [ID Swapping](https://docs.oracle.com/en/cloud/saas/data-cloud/dsmkt/integrating-oracle-bluekai-platform.html#GUID-A8856438-EF6A-4BCE-A2E4-B4CE725B0E61) guidelines on BlueKai website&lt;/li&gt;&lt;/ul&gt;                                    |
| User ID Value   | &lt;ul&gt;&lt;li&gt;Value of user identifier&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                                                                      |
| ID Hashing      | &lt;ul&gt;&lt;li&gt;Check to hash the user ID&lt;/li&gt;&lt;li&gt;Email and phone number must be hashed&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                                                       |
| Hash Type       | &lt;ul&gt;&lt;li&gt;Choose hashing algorithm&lt;/li&gt;&lt;li&gt;Email address and phone number must be hashed with either MD5 or SHA256&lt;/li&gt;&lt;li&gt;ANDROIDID must be hashed with either with MD5 or SHA1&lt;/li&gt;&lt;li&gt;ADID and IDFA must be hashed with either with MD5 or SHA1 or not hashed at all&lt;/li&gt;&lt;/ul&gt; |
| Phints          | &lt;ul&gt;&lt;li&gt;Provide phints as key-value pairs&lt;/li&gt;&lt;li&gt;Values on the left will be assigned to the keys on the right&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                        |
| Additional Data | &lt;ul&gt;&lt;li&gt;Provide additional data as key-value pairs&lt;/li&gt;&lt;li&gt;No additional processing will be used for this data&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                        |
