---
title: Centro DSP Connector Setup Guide (Deprecated)
description: This article describes how to set up the Centro Demand-Side Platform (DSP) connector in your Customer Data Hub account.
url: https://docs.tealium.com/server-side-connectors/centro-dsp-connector-setup-guide-deprecated/
---
This connector is deprecated and no longer available in the connector marketplace. For the current connector, see the [Basis Technologies DSP Connector]().

Centro DSP is an advertising platform to build and optimize highly targeted advertising campaigns in real-time across multiple channels.

Before data is transmitted, the segment taxonomy must be sent to Centro and confirmed that it has loaded; we will discard data for segment IDs we do not recognize. Send taxonomy to [dsp.newdata@centro.net](http://mailto:dsp.newdata@centro.net).

## Supported Actions

| Action Name | AudienceStream | EventStream |
| --- | :---: | :---: |
|Send Audience Segments| ✓| ✓|

## Configure Settings

Go to the Connector Marketplace and add a new connector. Read the [Connector Overview]() article for general instructions on how to add a connector.

After adding the connector, configure the following settings:

## Action Settings - Parameters and Options

Click **Next** or go to the **Actions** tab. This is where you configure connector actions.

This section describes how to set up parameters and options for each action.

### Action - Send Audience Segments

#### Parameters

|**Parameter**| **Description**|
|---| ---|
|Centro Cookie ID / ssi| Required|
|Segments / Audiences|  &lt;ul&gt;&lt;li&gt;(Required) Provide one or more audience segment IDs as a CSV values. For example: `47598,47600,47601,47603,47604`&lt;/li&gt;&lt;/ul&gt; |
