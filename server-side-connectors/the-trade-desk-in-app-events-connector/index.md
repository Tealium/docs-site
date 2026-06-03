---
title: The Trade Desk In-App Events Connector Setup Guide
description: This article describes how to set up the The Trade Desk In-App Events connector.
url: https://docs.tealium.com/server-side-connectors/the-trade-desk-in-app-events-connector/
---## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send In-App Event| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Advertiser ID (adv)**
  * Represents your Advertiser ID on The Trade Desk.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send In-App Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
| TTD Event Tracker ID (`upid`) |  &lt;ul&gt;&lt;li&gt;TTD Event Tracker ID (`upid`)&lt;/li&gt;&lt;/ul&gt; |
| Mobile App Event (`ref`) |  &lt;ul&gt;&lt;li&gt;This should be the same as the name of the event.&lt;/li&gt;&lt;li&gt;Same as the value that you have configured on The Trade Desk configuration page for this specific event (`ref`)&lt;/li&gt;&lt;/ul&gt; |
| Mobile Client IP Address (`client_ip`) |  &lt;ul&gt;&lt;li&gt;Mobile Client IP Address (`client_ip`)&lt;/li&gt;&lt;/ul&gt; |
| Mobile IDFA for iOS (`idfa`) |  &lt;ul&gt;&lt;li&gt;IDFA is the iOS ID for Advertisers (`idfa`)&lt;/li&gt;&lt;/ul&gt; |
| Mobile GPS ADID for Android (`gps_adid`) |  &lt;ul&gt;&lt;li&gt;ADID is the Google Play Advertiser ID (`gps_adid`)&lt;/li&gt;&lt;/ul&gt; |
| Mobile NAID for Windows (`win_naid`) |  &lt;ul&gt;&lt;li&gt;Windows NAID is the Windows Phone Device ID (`win_naid`)&lt;/li&gt;&lt;/ul&gt; |
| Revenue Tracking Value ( `v` ) |  &lt;ul&gt;&lt;li&gt;Revenue tracking parameters `v` and `vf` are only sent if the UI is enabled.&lt;/li&gt;&lt;li&gt;ISO 4217 currency codes are used for `vf` field&lt;/li&gt;&lt;li&gt;Floating point numbers are expected for the `v` field.&lt;/li&gt;&lt;li&gt;Example: `0.99` , `3.99`&lt;/li&gt;&lt;/ul&gt; |
| Revenue Tracking Currency (`vf`) |  &lt;ul&gt;&lt;li&gt;Revenue tracking parameters `v` and `vf` are only sent if the UI is enabled&lt;/li&gt;&lt;li&gt;Note that ISO 4217 currency codes are used for `vf` field&lt;/li&gt;&lt;li&gt;Floating point numbers are expected for the `v` field.&lt;/li&gt;&lt;li&gt;Example: `0.99` , `3.99`&lt;/li&gt;&lt;/ul&gt; |
|Additional Query Data|  &lt;ul&gt;&lt;li&gt;Provide any additional URL query parameter data if needed&lt;/li&gt;&lt;/ul&gt; |
