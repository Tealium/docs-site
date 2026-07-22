---
title: The Trade Desk In-App Events Connector Setup Guide
description: This article describes how to set up the The Trade Desk In-App Events connector.
url: https://docs.tealium.com/server-side-connectors/the-trade-desk-in-app-events-connector/
---## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send In-App Event| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

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
| TTD Event Tracker ID (`upid`) |  <ul><li>TTD Event Tracker ID (`upid`)</li></ul> |
| Mobile App Event (`ref`) |  <ul><li>This should be the same as the name of the event.</li><li>Same as the value that you have configured on The Trade Desk configuration page for this specific event (`ref`)</li></ul> |
| Mobile Client IP Address (`client_ip`) |  <ul><li>Mobile Client IP Address (`client_ip`)</li></ul> |
| Mobile IDFA for iOS (`idfa`) |  <ul><li>IDFA is the iOS ID for Advertisers (`idfa`)</li></ul> |
| Mobile GPS ADID for Android (`gps_adid`) |  <ul><li>ADID is the Google Play Advertiser ID (`gps_adid`)</li></ul> |
| Mobile NAID for Windows (`win_naid`) |  <ul><li>Windows NAID is the Windows Phone Device ID (`win_naid`)</li></ul> |
| Revenue Tracking Value ( `v` ) |  <ul><li>Revenue tracking parameters `v` and `vf` are only sent if the UI is enabled.</li><li>ISO 4217 currency codes are used for `vf` field</li><li>Floating point numbers are expected for the `v` field.</li><li>Example: `0.99` , `3.99`</li></ul> |
| Revenue Tracking Currency (`vf`) |  <ul><li>Revenue tracking parameters `v` and `vf` are only sent if the UI is enabled</li><li>Note that ISO 4217 currency codes are used for `vf` field</li><li>Floating point numbers are expected for the `v` field.</li><li>Example: `0.99` , `3.99`</li></ul> |
|Additional Query Data|  <ul><li>Provide any additional URL query parameter data if needed</li></ul> |
