---
title: Heap Connector Setup Guide
description: This article describes how to set up the Heap connector.
url: https://docs.tealium.com/server-side-connectors/heap-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Add User Properties| ✓| ✗|
|Track| ✗| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Add User Properties

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|App ID|  &lt;ul&gt;&lt;li&gt;The `app_id` corresponding to one of your projects.&lt;/li&gt;&lt;/ul&gt; |
|Identity|  &lt;ul&gt;&lt;li&gt;An identity, typically corresponding to an existing user.&lt;/li&gt;&lt;li&gt;If no such identity exists, a new user is created with that identity.&lt;/li&gt;&lt;li&gt;Limited to 255 characters.&lt;/li&gt;&lt;li&gt;For more information, see: [Heap: Add User Properties](https://developers.heap.io/docs/using-identify)&lt;/li&gt;&lt;/ul&gt; |
|User Properties|  &lt;ul&gt;&lt;li&gt;An object with key-value properties you want associated with the user.&lt;/li&gt;&lt;li&gt;Each key and property must either be a number or string with fewer than 1024 characters.&lt;/li&gt;&lt;li&gt;For more information, see: [Heap: Add User Properties](https://developers.heap.io/docs/using-identify)&lt;/li&gt;&lt;/ul&gt; |

### Action - Track

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|App ID|  &lt;ul&gt;&lt;li&gt;The `app_id` corresponding to one of your projects.&lt;/li&gt;&lt;/ul&gt; |
|Identity|  &lt;ul&gt;&lt;li&gt;An identity, typically corresponding to an existing user.&lt;/li&gt;&lt;li&gt;If no such identity exists, then a new user will be created with that identity.&lt;/li&gt;&lt;li&gt;Limited to 255 characters.&lt;/li&gt;&lt;li&gt;For more information, see the [Heap documentation](https://developers.heap.io/reference#track).&lt;/li&gt;&lt;/ul&gt; |
|Event|  &lt;ul&gt;&lt;li&gt;The name of the server-side event.&lt;/li&gt;&lt;li&gt;Limited to 1024 characters.&lt;/li&gt;&lt;li&gt;For more information, see the [Heap documentation](https://developers.heap.io/reference#track).&lt;/li&gt;&lt;/ul&gt; |
|Properties|  &lt;ul&gt;&lt;li&gt;An object with key-value properties you want associated with the user.&lt;/li&gt;&lt;li&gt;Each key and property must either be a number or string with fewer than 1024 characters.&lt;/li&gt;&lt;li&gt;For more information, see the [Heap documentation](https://developers.heap.io/reference#track).&lt;/li&gt;&lt;/ul&gt; |
|Timestamp|  &lt;ul&gt;&lt;li&gt;ISO 8601 or Unix epoch milliseconds.&lt;/li&gt;&lt;li&gt;Example: `2017-03-10T22:21:56&#43;00:00`&lt;/li&gt;&lt;li&gt;For more information, see the [Heap documentation](https://developers.heap.io/reference#track).&lt;/li&gt;&lt;/ul&gt; |
