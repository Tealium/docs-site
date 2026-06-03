---
title: Yahoo Pixel API Connector Setup Guide
description: This article describes how to set up the Yahoo Pixel API connector.
url: https://docs.tealium.com/server-side-connectors/yahoo-pixel-api-connector/
---
## API Information

This connector uses the following vendor API:

* API Name: Yahoo API
* API Version: v1
* Documentation: [Yahoo: Ad Tech DataX API Specifications](https://help.yahooinc.com/datax/docs/yahoo-ad-tech-datax-api-specifications)
* API Endpoint: `https://dataxonline.yahoo.com`

## Configuration

Go to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see [About Connectors]().

After adding the connector, configure the following settings:

* **Client ID**  
  * (Required) The Client ID is in the encrypted credentials file provided by Yahoo.
* **Client Secret**  
  * (Required) The Client Secret is in the encrypted credentials file provided by Yahoo.

## Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
| Send Pixel and Event Data | ✓ | ✓ |

Enter a name for the action and select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Send Pixel and Event Data

#### Parameters

| **Parameter** | **Description** |
| --- | --- |
| Action Source | (Required) The source of the event. For example: `Website`, `App`, or `Offline`. |
| Pixel ID | (Required) The integration&#39;s Pixel ID, created in Yahoo DSP. |
| Action Source URL | The website URL. |
| Event Time | The time the event occurred, in epoch milliseconds UTC. If no **Event Time** is mapped, the current timestamp will be sent. |

#### User Data

| **Parameter** | **Description** |
| --- | --- |
| Email (already SHA256 hashed) | Provide an email address that has already been whitespace trimmed, lowercased, and SHA256 hashed. |
| Email (apply SHA256 hash) | (apply SHA256 hash) Provide a plain text email address and the connector will whitespace trim, lowercase, and hash this value using the SHA256 hash. |
| GPSAID | Google Play Store Advertiser ID.  |
| IDFA | Apple Advertiser ID. |
| Yahoo ID | Cookie Sync Identifier. |
| VMCID | Value of the click ID from the URL macro collected from the click or third-party ad server. This will be supported in version 2 of the specification. |

#### Custom Data

| **Parameter** | **Description** |
| --- | --- |
| gv | The monetary value of any given conversion. The default currency for the value is US dollars (USD). This will be reported as a dynamic conversion value in DSP. |
| ec | The content category associated with the event. |
| el | Lower level label under an event category. |
| ea | Action defined by the advertiser, such as `AddToCart`. |
| Product ID | Product ID or multiple IDs, separated by comma delimiters. |
| User Defined | Up to ten custom event labels that the client can set to a custom name instead of the standard events described above. The maximum name length is 32 characters and maximum value length is 255 characters. |