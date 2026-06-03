---
title: Salesforce Standard Objects Connector Setup Guide
description: This article describes how to set up the Salesforce Standard Objects connector.
url: https://docs.tealium.com/server-side-connectors/salesforce-standard-objects-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Create or Update Standard Object| ✓| ✓|
|Delete Standard Object| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Create or Update Standard Object

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Update Strategy|  &lt;ul&gt;&lt;li&gt;(Required) Select applicable update strategy.&lt;/li&gt;&lt;li&gt;Create Only  &lt;ul&gt;&lt;li&gt;Create new Standard Object without lookup.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Update Only  &lt;ul&gt;&lt;li&gt;Look up an existing Standard Object and update it.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;li&gt;Create or Update  &lt;ul&gt;&lt;li&gt;Look up an existing Standard Object and if found, update it, otherwise create a new item.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
|Standard Object|  &lt;ul&gt;&lt;li&gt;Select the applicable Standard Object to create or update.&lt;/li&gt;&lt;/ul&gt; |

### Action - Delete Standard Object

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Standard Object|  &lt;ul&gt;&lt;li&gt;Type of Standard Object instance to delete.&lt;/li&gt;&lt;/ul&gt; |
