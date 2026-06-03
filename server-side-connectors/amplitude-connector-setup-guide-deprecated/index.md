---
title: Amplitude Connector Setup Guide (Deprecated)
description: This article describes how to set up the Amplitude connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/amplitude-connector-setup-guide-deprecated/
---
This connector is now deprecated and no longer available in the connector marketplace. For the current connector, see [Amplitude Connector]()

## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| Send Event      | ✓                  | ✓               |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**  
Located under **Settings &amp;gt; Projects**.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Event

#### Parameters

| **Parameter**    | **Description**                                                                                                                                                                                                                                                                                                                       |
|:-----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Event Properties | &lt;ul&gt;&lt;li&gt;(Optional) A dictionary of key-value pairs that represent additional data to be sent along with the event.&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included.&lt;/li&gt;&lt;/ul&gt;                                                                                                                                                |
| User Properties  | &lt;ul&gt;&lt;li&gt;(Optional) A dictionary of key-value pairs that represent additional data tied to the user.&lt;/li&gt;&lt;li&gt;Each distinct value display as a user segment on the Amplitude dashboard.&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included.&lt;/li&gt;&lt;/ul&gt;                                                                             |
| Groups           | &lt;ul&gt;&lt;li&gt;(Optional) Enterprise only.&lt;/li&gt;&lt;li&gt;A dictionary of key-value pairs that represent groups of users.&lt;/li&gt;&lt;li&gt;For more information on groups, see the following[ JavaScript SDK excerpt](https://github.com/amplitude/Amplitude-Javascript#setting-groups).&lt;/li&gt;&lt;li&gt;Empty values are skipped and not included.&lt;/li&gt;&lt;/ul&gt; |
