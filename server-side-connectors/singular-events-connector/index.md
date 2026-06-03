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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**: API Key is required. Clients can retrieve their API key from within their account from the [Singular&#39;s portal](https://app.singular.net/#/sdk).

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Install Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Device ID|  &lt;ul&gt;&lt;li&gt;At least one device identifier is required, for example:  &lt;ul&gt;&lt;li&gt;Advertiser Identifier (`idfa`)&lt;/li&gt;&lt;li&gt;Identifier for Vendor (`idfv`) for iOS apps&lt;/li&gt;&lt;li&gt;Android advertising ID ( `aifa`),&lt;/li&gt;&lt;li&gt;Android ID ( `andi`) for Android.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs) for more information.&lt;/li&gt;&lt;/ul&gt; |
|Platform| `Android` or `iOS`.|
|Application Name|  &lt;ul&gt;&lt;li&gt;Package Name (Android) or Bundle ID (iOS) of your application.&lt;/li&gt;&lt;li&gt;For example: `com.mycompany.app`&lt;/li&gt;&lt;/ul&gt; |
|IP Address|  &lt;ul&gt;&lt;li&gt;IP address of the device session (with decimal points or colons).&lt;/li&gt;&lt;li&gt;Both IPv4 and IPv6 are supported.&lt;/li&gt;&lt;/ul&gt; |
|Device Make|  &lt;ul&gt;&lt;li&gt;Make of the device hardware, which is typically the consumer-facing name.&lt;/li&gt;&lt;li&gt;For example: `Samsung`, `LG`, or `Apple`.&lt;/li&gt;&lt;/ul&gt; |
|Device Model|  &lt;ul&gt;&lt;li&gt;Model of the device hardware.&lt;/li&gt;&lt;li&gt;Examples: `iPhone 8` or `Galaxy S10`&lt;/li&gt;&lt;/ul&gt; |
|Device Build|  &lt;ul&gt;&lt;li&gt;The build of the device, URL-encoded.&lt;/li&gt;&lt;li&gt;For example: `Build%2F13D15`.&lt;/li&gt;&lt;/ul&gt; |
|OS Version|  &lt;ul&gt;&lt;li&gt;Version of the OS on the device.&lt;/li&gt;&lt;li&gt;Example: `9.2`.&lt;/li&gt;&lt;/ul&gt; |
|Language &amp;amp; Country Code|  &lt;ul&gt;&lt;li&gt;The IETF local tag for the device, using two-letter language and country code separated by an underscore.&lt;/li&gt;&lt;li&gt;For example: `en_US`.&lt;/li&gt;&lt;/ul&gt; |
|Optional Parameters|  &lt;ul&gt;&lt;li&gt;Add all other optional parameters here.&lt;/li&gt;&lt;li&gt;For more information on supported parameters, reference the [Singular API documentation](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint).&lt;/li&gt;&lt;/ul&gt; |

### Action - Post Install Events

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event Name|  &lt;ul&gt;&lt;li&gt;Name of the event to report in Singular.&lt;/li&gt;&lt;li&gt;Example: `ViewItem`&lt;/li&gt;&lt;/ul&gt; |
|Application Name|  &lt;ul&gt;&lt;li&gt;Package Name (Android) or Bundle ID (iOS) of the mobile application.&lt;/li&gt;&lt;li&gt;Example: `com.yourcompany.app`&lt;/li&gt;&lt;/ul&gt; |
|Device ID|  &lt;ul&gt;&lt;li&gt;At least one device identifier is required, for example:  &lt;ul&gt;&lt;li&gt;Advertiser Identifier (`idfa`)&lt;/li&gt;&lt;li&gt;Identifier for Vendor (`idfv`) for iOS apps&lt;/li&gt;&lt;li&gt;Android advertising ID ( `aifa`),&lt;/li&gt;&lt;li&gt;Android ID ( `andi`) for Android.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Reference the following [API documentation](https://support.singular.net/hc/en-us/articles/4411780525979-Types-of-Device-IDs) for more information.&lt;/li&gt;&lt;/ul&gt; |
|Platform| Android or iOS.|
|IP Address|  &lt;ul&gt;&lt;li&gt;Raw IP address of the device (with decimal points or colons).&lt;/li&gt;&lt;li&gt;Both IPv4 and IPv6 are supported.&lt;/li&gt;&lt;/ul&gt; |
|Device Make|  &lt;ul&gt;&lt;li&gt;Make of the device hardware, typically the consumer-facing name.&lt;/li&gt;&lt;li&gt;For example: `Samsung`, `LG`, or `Apple`&lt;/li&gt;&lt;/ul&gt; |
|Device Model|  &lt;ul&gt;&lt;li&gt;Model of the device hardware.&lt;/li&gt;&lt;li&gt;Examples: `iPhone XS` or `Galaxy S10`&lt;/li&gt;&lt;/ul&gt; |
|Device Build|  &lt;ul&gt;&lt;li&gt;Build of the device, URL encoded.&lt;/li&gt;&lt;li&gt;Example: `Build%2F13D15`&lt;/li&gt;&lt;/ul&gt; |
|OS Version|  &lt;ul&gt;&lt;li&gt;Version of the OS on the device.&lt;/li&gt;&lt;li&gt;Example: `9.2`&lt;/li&gt;&lt;/ul&gt; |
|Language &amp;amp; Country Code|  &lt;ul&gt;&lt;li&gt;The IETF local tag for the device, using two-letter language and country code separated by an underscore.&lt;/li&gt;&lt;li&gt;For example: `en_US`&lt;/li&gt;&lt;/ul&gt; |
|Optional Parameters|  &lt;ul&gt;&lt;li&gt;Add all other optional parameters here.&lt;/li&gt;&lt;li&gt;For more information, see the [Singular Server-to-Server documentation](https://support.singular.net/hc/en-us/articles/360048588672#Event_Notification_Endpoint).&lt;/li&gt;&lt;/ul&gt; |
