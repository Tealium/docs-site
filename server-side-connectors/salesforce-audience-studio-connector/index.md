---
title: Salesforce Audience Studio Connector Setup Guide
description: This article describes how to set up the Salesforce Audience Studio connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-audience-studio-connector/
---
## Supported Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Pixel| ✓| ✓|
|Send Event| ✓| ✓|
|Send Transaction| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Pixel

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Domain|  <ul><li>(Required) Contact your Salesforce Audience Studio Representative to get this value.</li></ul> |
|Publisher UUID|  <ul><li>(Required) Contact your Salesforce Audience Studio Representative to get this value.</li></ul> |
|Site|  <ul><li>(Required) Contact your Salesforce Audience Studio Representative to get this value.</li></ul> |
|Unique User ID|  <ul><li>(Required) For iOS, this should be the unique Advertiser ID (not the Device ID).</li></ul> |
|Section|  <ul><li>This is the section of the application that you want to send data for.</li><li>For example, `open_app` or `home_page`</li></ul> |
|Browser Attributes|  <ul><li>All browser attribute data that needs to be sent to supplement the user-agent data.</li></ul> |
|Additional Information|  <ul><li>For additional information, see the [Salesforce Audience Studio](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API#trackingviews) documentation.</li></ul> |

### Action - Send Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event URL Endpoint|  <ul><li>Event URL is created in the [Salesforce Audience Studio UI](https://console.krux.com/events/list).</li></ul> |
|Unique User ID|  <ul><li>(Required) For iOS, this should be the unique Advertiser ID, not the Device ID.</li></ul> |

### Action - Send Transaction

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Unique User ID|  <ul><li>(Required) For iOS, this should be the unique Advertiser ID, not the Device ID.</li></ul> |
|Transaction URL Endpoint|  <ul><li>URL provided by Salesforce Audience Studio representative to send transactional data.</li></ul> |
|Publisher UUID|  <ul><li>(Required) Contact your Salesforce Audience Studio representative to get this value.</li></ul> |
|Order Total|  <ul><li>(Required) The order total.</li></ul> |
|Quantity|  <ul><li>(Required) The quantity of items purchased.</ul> |
|Transaction Date|  <ul><li>(Required)</li></ul> |
|Additional Information|  <ul><li>For additional information, see the [Salesforce Audience Studio](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API#trackingviews) documentation.</li></ul> |
