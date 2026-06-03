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

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Pixel

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Domain|  &lt;ul&gt;&lt;li&gt;(Required) Contact your Salesforce Audience Studio Representative to get this value.&lt;/li&gt;&lt;/ul&gt; |
|Publisher UUID|  &lt;ul&gt;&lt;li&gt;(Required) Contact your Salesforce Audience Studio Representative to get this value.&lt;/li&gt;&lt;/ul&gt; |
|Site|  &lt;ul&gt;&lt;li&gt;(Required) Contact your Salesforce Audience Studio Representative to get this value.&lt;/li&gt;&lt;/ul&gt; |
|Unique User ID|  &lt;ul&gt;&lt;li&gt;(Required) For iOS, this should be the unique Advertiser ID (not the Device ID).&lt;/li&gt;&lt;/ul&gt; |
|Section|  &lt;ul&gt;&lt;li&gt;This is the section of the application that you want to send data for.&lt;/li&gt;&lt;li&gt;For example, `open_app` or `home_page`&lt;/li&gt;&lt;/ul&gt; |
|Browser Attributes|  &lt;ul&gt;&lt;li&gt;All browser attribute data that needs to be sent to supplement the user-agent data.&lt;/li&gt;&lt;/ul&gt; |
|Additional Information|  &lt;ul&gt;&lt;li&gt;For additional information, see the [Salesforce Audience Studio](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API#trackingviews) documentation.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Event URL Endpoint|  &lt;ul&gt;&lt;li&gt;Event URL is created in the [Salesforce Audience Studio UI](https://console.krux.com/events/list).&lt;/li&gt;&lt;/ul&gt; |
|Unique User ID|  &lt;ul&gt;&lt;li&gt;(Required) For iOS, this should be the unique Advertiser ID, not the Device ID.&lt;/li&gt;&lt;/ul&gt; |

### Action - Send Transaction

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Unique User ID|  &lt;ul&gt;&lt;li&gt;(Required) For iOS, this should be the unique Advertiser ID, not the Device ID.&lt;/li&gt;&lt;/ul&gt; |
|Transaction URL Endpoint|  &lt;ul&gt;&lt;li&gt;URL provided by Salesforce Audience Studio representative to send transactional data.&lt;/li&gt;&lt;/ul&gt; |
|Publisher UUID|  &lt;ul&gt;&lt;li&gt;(Required) Contact your Salesforce Audience Studio representative to get this value.&lt;/li&gt;&lt;/ul&gt; |
|Order Total|  &lt;ul&gt;&lt;li&gt;(Required) The order total.&lt;/li&gt;&lt;/ul&gt; |
|Quantity|  &lt;ul&gt;&lt;li&gt;(Required) The quantity of items purchased.&lt;/ul&gt; |
|Transaction Date|  &lt;ul&gt;&lt;li&gt;(Required)&lt;/li&gt;&lt;/ul&gt; |
|Additional Information|  &lt;ul&gt;&lt;li&gt;For additional information, see the [Salesforce Audience Studio](https://konsole.zendesk.com/hc/en-us/articles/219493027-Mobile-HTTP-API#trackingviews) documentation.&lt;/li&gt;&lt;/ul&gt; |
