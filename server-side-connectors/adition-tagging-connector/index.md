---
title: Adition Tagging Connector Setup Guide
description: This article describes how to set up the Adition Tagging connector.
url: https://docs.tealium.com/server-side-connectors/adition-tagging-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Tag visitor| ✓| ✗|

## Configure Settings

Go to the **Connector Marketplace** and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Tag Visitor

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Endpoint URL|  &lt;ul&gt;&lt;li&gt;(Optional) Default endpoint is &lt;https://ad13.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;Provide your assigned endpoint URL.&lt;/li&gt;&lt;li&gt;When provided, it will override the default endpoint&lt;/li&gt;&lt;li&gt;For example: &lt;ul&gt;&lt;li&gt;&lt;https://adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad1.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad2.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad3.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad11.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;li&gt;&lt;https://ad13.adfarm1.adition.com/tagging&gt;&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Client ID|  &lt;ul&gt;&lt;li&gt;Provide your Adition client ID.&lt;/li&gt;&lt;li&gt;Example: `3133`&lt;/li&gt;&lt;/ul&gt; |
|Tag|  &lt;ul&gt;&lt;li&gt;Map custom values to the keys and subkeys as configured in Adition.&lt;/li&gt;&lt;li&gt;Example: Map string `current` to `tag[tealium.abc_de]`.&lt;/li&gt;&lt;li&gt;You can add multiple mappings&lt;/li&gt;&lt;/ul&gt; |
|Adition Cookie|  &lt;ul&gt;&lt;li&gt;Map the string variable which contains the value from the Adition cookie sync to the cookie name: `UserID1` .&lt;/li&gt;&lt;/ul&gt; |
