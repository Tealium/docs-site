---
title: Appcues Connector Setup Guide
description: This article describes how to set up the Appcues connector.
url: https://docs.tealium.com/server-side-connectors/appcues-connector/
---## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Update User Profile| ✓| ✗|
|Record User Event| ✗| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **Account ID**
  * Your Appcues Account ID.
  * Found on the account settings page.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Update User Profile

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|User ID|  &lt;ul&gt;&lt;li&gt;The end user ID of the profile to update.&lt;/li&gt;&lt;/ul&gt; |
|Properties|  &lt;ul&gt;&lt;li&gt;Object containing arbitrary key-value data to update in the user&#39;s stored profile.&lt;/li&gt;&lt;li&gt;For more information, see: [Appcues HTTP API (Developer)](http://docs.appcues.com/article/254-http-api).&lt;/li&gt;&lt;/ul&gt; |

### Action - Record User Event

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|User ID|  &lt;ul&gt;&lt;li&gt;The end user ID of the profile to update.&lt;/li&gt;&lt;/ul&gt; |
|Event Name|  &lt;ul&gt;&lt;li&gt;Event name.&lt;/li&gt;&lt;li&gt;Maximum of 127 characters.&lt;/li&gt;&lt;li&gt;This is the main mechanism for grouping and targeting on specific events.&lt;/li&gt;&lt;li&gt;For more information, see: [Appcues HTTP API (Developer)](http://docs.appcues.com/article/254-http-api).&lt;/li&gt;&lt;/ul&gt; |
|Timestamp|  &lt;ul&gt;&lt;li&gt;Time at which the event occurred.&lt;/li&gt;&lt;li&gt;Either integer format (as Unix time) or string format (as ISO 8601 compliant date, for example **2016-01-13T13:05:22.000Z**).&lt;/li&gt;&lt;/ul&gt; |
|Event Attributes|  &lt;ul&gt;&lt;li&gt;Event attributes&lt;/li&gt;&lt;/ul&gt; |
