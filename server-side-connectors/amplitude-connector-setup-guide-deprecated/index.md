---
title: Amplitude Connector Setup Guide (Deprecated)
description: This article describes how to set up the Amplitude connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/amplitude-connector-setup-guide-deprecated/
---

<blockquote>
This connector is now deprecated and no longer available in the connector marketplace. For the current connector, see [Amplitude Connector](https://docs.tealium.com/amplitude-connector/)
</blockquote>


## Connector Actions

| **Action Name** | **AudienceStream** | **EventStream** |
|:----------------|:-------------------|:----------------|
| Send Event      | ✓                  | ✓               |

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview](https://docs.tealium.com/about-connectors/) article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

* **API Key**  
Located under **Settings &gt; Projects**.

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Event

#### Parameters

| **Parameter**    | **Description**                                                                                                                                                                                                                                                                                                                       |
|:-----------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Event Properties | <ul><li>(Optional) A dictionary of key-value pairs that represent additional data to be sent along with the event.</li><li>Empty values are skipped and not included.</li></ul>                                                                                                                                                |
| User Properties  | <ul><li>(Optional) A dictionary of key-value pairs that represent additional data tied to the user.</li><li>Each distinct value display as a user segment on the Amplitude dashboard.</li><li>Empty values are skipped and not included.</li></ul>                                                                             |
| Groups           | <ul><li>(Optional) Enterprise only.</li><li>A dictionary of key-value pairs that represent groups of users.</li><li>For more information on groups, see the following[ JavaScript SDK excerpt](https://github.com/amplitude/Amplitude-Javascript#setting-groups).</li><li>Empty values are skipped and not included.</li></ul> |
