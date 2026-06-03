---
title: FullStory Connector Setup Guide
description: This article describes how to set up the FullStory connector.
url: https://docs.tealium.com/server-side-connectors/fullstory-connector/
---
## Connector Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Delete User| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Delete User

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|User ID|  &lt;ul&gt;&lt;li&gt;User ID is your application-specific ID you have given to the user that will have been passed through the FullStory tag.&lt;/li&gt;&lt;li&gt;Use this feature to comply with Right to be Forgotten / Right to Erasure requests from your end users.&lt;/li&gt;&lt;li&gt;For more information on this endpoint, see: [FullStory&#39;s documentation](https://help.fullstory.com/develop-rest/deleteindividual-api).&lt;/li&gt;&lt;li&gt;Recommended best practice:  &lt;ul&gt;&lt;li&gt;Select hashed email as the identifier to be mapped to User ID in the FullStory tag.&lt;/li&gt;&lt;li&gt;For more information on this recommendation or alternate approaches to selecting the User ID, contact your Tealium or FullStory representative.&lt;/li&gt;&lt;/ul&gt; &lt;/li&gt;&lt;/ul&gt; |
