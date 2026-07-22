---
title: Singular Events Connector Setup Guide
description: This article describes how to set up the Singular Events connector.
url: https://docs.tealium.com/server-side-connectors/singular-events-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Install Event| ✗| ✓|
|Post Install Events| ✗| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**: API Key is required. Clients can retrieve their API key from within their account from the [Singular's portal](https://app.singular.net/#/sdk).

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Install Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Device ID|  <ul><li>At least one device identifier is required, for example:  <ul><li>Advertiser Identifier (`idfa`)</li><li>Identifier for Vendor (`idfv`) for iOS apps</li><li>Android advertising ID ( `aifa`),</li><li>Android ID ( `andi`) for Android.</li></ul> </li><li>Reference the following [API documentation](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs) for more information.</li></ul> |
|Platform| `Android` or `iOS`.|
|Application Name|  <ul><li>Package Name (Android) or Bundle ID (iOS) of your application.</li><li>For example: `com.mycompany.app`</li></ul> |
|IP Address|  <ul><li>IP address of the device session (with decimal points or colons).</li><li>Both IPv4 and IPv6 are supported.</li></ul> |
|Device Make|  <ul><li>Make of the device hardware, which is typically the consumer-facing name.</li><li>For example: `Samsung`, `LG`, or `Apple`.</li></ul> |
|Device Model|  <ul><li>Model of the device hardware.</li><li>Examples: `iPhone 8` or `Galaxy S10`</li></ul> |
|Device Build|  <ul><li>The build of the device, URL-encoded.</li><li>For example: `Build%2F13D15`.</li></ul> |
|OS Version|  <ul><li>Version of the OS on the device.</li><li>Example: `9.2`.</li></ul> |
|Language &amp; Country Code|  <ul><li>The IETF local tag for the device, using two-letter language and country code separated by an underscore.</li><li>For example: `en_US`.</li></ul> |
|Optional Parameters|  <ul><li>Add all other optional parameters here.</li><li>For more information on supported parameters, reference the [Singular API documentation](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint).</li></ul> |

### Action - Post Install Events

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Name|  <ul><li>Name of the event to report in Singular.</li><li>Example: `ViewItem`</li></ul> |
|Application Name|  <ul><li>Package Name (Android) or Bundle ID (iOS) of the mobile application.</li><li>Example: `com.yourcompany.app`</li></ul> |
|Device ID|  <ul><li>At least one device identifier is required, for example:  <ul><li>Advertiser Identifier (`idfa`)</li><li>Identifier for Vendor (`idfv`) for iOS apps</li><li>Android advertising ID ( `aifa`),</li><li>Android ID ( `andi`) for Android.</li></ul> </li><li>Reference the following [API documentation](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs) for more information.</li></ul> |
|Platform| Android or iOS.|
|IP Address|  <ul><li>Raw IP address of the device (with decimal points or colons).</li><li>Both IPv4 and IPv6 are supported.</li></ul> |
|Device Make|  <ul><li>Make of the device hardware, typically the consumer-facing name.</li><li>For example: `Samsung`, `LG`, or `Apple`</li></ul> |
|Device Model|  <ul><li>Model of the device hardware.</li><li>Examples: `iPhone XS` or `Galaxy S10`</li></ul> |
|Device Build|  <ul><li>Build of the device, URL encoded.</li><li>Example: `Build%2F13D15`</li></ul> |
|OS Version|  <ul><li>Version of the OS on the device.</li><li>Example: `9.2`</li></ul> |
|Language &amp; Country Code|  <ul><li>The IETF local tag for the device, using two-letter language and country code separated by an underscore.</li><li>For example: `en_US`</li></ul> |
|Optional Parameters|  <ul><li>Add all other optional parameters here.</li><li>For more information, see the [Singular Server-to-Server documentation](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint).</li></ul> |
