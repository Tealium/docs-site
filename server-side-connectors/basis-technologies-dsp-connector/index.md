---
title: Basis Technologies DSP Connector Setup Guide
description: This article describes how to set up the Basis Technologies DSP connector.
url: https://docs.tealium.com/server-side-connectors/basis-technologies-dsp-connector/
---

## Connector Actions

| **Action Name**              | **AudienceStream** | **EventStream** |
|:-----------------------------|:-------------------|:----------------|
| Add User to Audience Segment | ✓                  | ✓               |

## Configure Settings

Navigate to the Connector Marketplace and add a new connector. For general instructions on how to add a connector, see the [About Connectors](https://docs.tealium.com/about-connectors/) article.

After adding the connector, configure the following settings:

* **Advertiser ID** - (Required) Your Basis Technologies Advertiser ID.

* **Audience Segment** - (Optional) To create a new audience segment in Basis Technologies DSP, click **New Audience Segment**.

Click **Done** when you are finished configuring the connector.

## Action Settings — Parameters and Options

Click **Continue** to configure the connector actions. Enter a name for the action and then select the action type from the drop-down menu.

The following section describes how to set up parameters and options for each action.

### Action — Add User to Audience Segment

#### Parameters

| **Parameter**                   | **Description**                                                                                                                  |
|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------|
| Audience Segment to Add User To | (Required) Select your audience segment or click New Audience Segment to create a new audience segment in Basis Technologies DSP. |
| Basis Technologies Cookie ID    | (Required) Basis Technologies Cookie ID.                                                                                          |
